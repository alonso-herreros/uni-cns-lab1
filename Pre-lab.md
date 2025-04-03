## Communication Networks and Services

# Lab 1 preparation (answers)

*Academic year 2023-2024*  
*Telematics Engineering Department - Universidad Carlos III de Madrid*

---

## CE1. Ping command

### a) Parameters

The `-c 1` parameter indicates how many packets will be sent to the destination. In this case, only 1 packet
will be sent.

### b) Sequence of packets

The sequence of packets is as follows:

* `Eth_1: IP(53.4.1.1, 53.4.3.1, 64, ICMP(type 8, code 0: Echo Request))`
* `Eth_2: IP(53.4.1.1, 53.4.3.1, 63, ICMP(type 8, code 0: Echo Request))`
* `Eth_3: IP(53.4.1.1, 53.4.3.1, 62, ICMP(type 8, code 0: Echo Request))`
* `Eth_3: IP(53.4.3.1, 53.4.1.1, 64, ICMP(type 0, code 0: Echo Reply))`
* `Eth_2: IP(53.4.3.1, 53.4.1.1, 63, ICMP(type 0, code 0: Echo Reply))`
* `Eth_1: IP(53.4.3.1, 53.4.1.1, 62, ICMP(type 0, code 0: Echo Reply))`

## CE2. Traceroute command

### a) Parameters

The `-I` parameter is used to force the use of ICMP requests instead of the default (UDP). The `-q 1`
parameter is used to specify the number packets to be sent. In this case, only 1 packet will be sent,
instead of the default 3.

### b) Sequence of packets

The sequence of packets is as follows:

* `Eth_3: IP(53.4.3.1, 53.4.1.1, 1, ICMP(type 8, code 0: Echo Request))`
* `Eth_3: IP(53.4.3.3, 53.4.3.1, 64, ICMP(type 11, code 0: TTL Expired))`
* `Eth_3: IP(53.4.3.1, 53.4.1.1, 2, ICMP(type 8, code 0: Echo Request))`
* `Eth_2: IP(53.4.3.1, 53.4.1.1, 1, ICMP(type 8, code 0: Echo Request))`
* `Eth_2: IP(53.4.2.2, 53.4.3.1, 64, ICMP(type 11, code 0: TTL Expired))`
* `Eth_3: IP(53.4.2.2, 53.4.3.1, 63, ICMP(type 11, code 0: TTL Expired))`
* `Eth_3: IP(53.4.3.1, 53.4.1.1, 3, ICMP(type 8, code 0: Echo Request))`
* `Eth_2: IP(53.4.3.1, 53.4.1.1, 2, ICMP(type 8, code 0: Echo Request))`
* `Eth_1: IP(53.4.3.1, 53.4.1.1, 1, ICMP(type 8, code 0: Echo Request))`
* `Eth_1: IP(53.4.1.1, 53.4.3.1, 64, ICMP(type 0, code 0: Echo Reply))`
* `Eth_2: IP(53.4.1.1, 53.4.3.1, 63, ICMP(type 0, code 0: Echo Reply))`
* `Eth_3: IP(53.4.1.1, 53.4.3.1, 62, ICMP(type 0, code 0: Echo Reply))`
