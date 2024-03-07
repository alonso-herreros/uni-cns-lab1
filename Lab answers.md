# IP and ICMP traffic analysis practice

---

## 1. ICMP and ping

### (1) d) Analyze the output of `ping`

#### d.1) Number of packets sent

> I sent 5 packets. The ping command outputs a summary (host ping statistics) at the end of execution, with
> the number of packets sent, received, lost percentage, execution time and RTT min/avg/max/mdev.

#### d.2) IP addr of host

> I pinged `doc010.lab.it.uc3m.es`, which resolved to `163.117.144.109`.

#### d.3) Time and TTL

> The *time* is the Round Trip Time, meaning the time between sending a ping request and receiving the
> response. This is the total time it took the packet to leave the machine, reach the destination, and return,
> including all intermediate hops, processing times, delays, etc.
>
> This could be measured by taking a timestamp just before sending the ping, and another one just after
> receiving the response, and then taking the difference. The units and accuracy depend on the timestamping
> method used. In the case of this ping command, the time is given in milliseconds, but the measurement could
> be taken using a finer resolution and then converting the units.
>
> The *TTL* (Time To Live) is the TTL field in the IP header of the packet received. This field is calculated
> by the routers that handle the packet between the source and the destination, and it is decremented by 1 at
> each hop. It is set to 64 by default. Both the ping request and the ping response have a TTL field. The TTL
> is set to 64 when sending the request. The response TTL is also set to 64 when it's sent. When it reaches
> the pinging machine, the output is the TTL field **of the response packet** (not round-trip). In this case,
> it was 63, suggesting there was only one router between the pinged machine and the pinging machine
> (however, the initial value may have been different, so this is not a definitive conclusion).
>
> The TTL does not require any calculations, just looking at the response packet. When the machine receives
> the ping response, it just prints the TTL field of the response.

#### d.4) Ping to Valladolid

> The ping to the machine in Valladolid was not successful. The traceroute command showed no further
> information than hop 11: `157.88.29.201`. The ping did reach the University of Valladolid, as suggested by
> hop 8: `redcayle-uva-router.red.rediris.es`.

## (2) a) Filter ICMP packets

> I used the simple shortcut filter `icmp` to filter ICMP packets.

## (2) c) Draw the packet

> ```mermaid
> block-beta
> columns 4
>     block:vihl:1
>         V  ["V = 4\n(Ver.)"]
>         IHL["IHL = 5"]
>         end
>     TOS  ["TOS=0x00\n(Type of Service)"]
>     LEN  ["Length=84"]                :2
>     ID   ["Identification=0x3c8d"]    :2
>     block:offset:2
>         FLAGS["R=0 | DF=1 | MF=0"]
>         OFF  ["Fragment Offset=0"]
>         end
>     TTL  ["TTL=64"]
>     PROTO["Proto=0x01 (ICMP)\n(Protocol)"]
>     HCS  ["H. Checksum = 0x7a03"] :2
>     SRC  ["Src=163.117.172.192"]:4
>     DST  ["Dest=163.117.144.109"]:4
> ```

## (2) e) Duplicate ID and sequence

> There are no duplicate ID and sequence numbers in the ping packets, but wireshark shows two interpretations
> of the same data: the ID and sequence tagged with "BE" correspond to the big-endian interpretation, and the
> ones tagged with "LE" correspond to the little-endian interpretation.

## (2) f) ID and sequence

> The ID and sequence numbers are used to match the request and response packets. The ID is unique for the
> same ping command, while the sequence number is incremented by 1 for each packet sent. This way, the
> response packet can be matched with the request packet. A machine may send multiple different pings to a
> destination, and the ID helps to match the response packets with the corresponding request, and direct them
> appropriately (easily grouping them in the same output, for example). The sequence number helps may help to
> detect packet loss and measure the correct RTT for each packet (in case a previous packet arrives after
> sending a second one, for example)

## (2) g) ICMP type and code

> The type and code for echo reply are, respectively, `0x0` and `0x0`. Checksum, identifier and sequence
> number are 2 bytes each.
