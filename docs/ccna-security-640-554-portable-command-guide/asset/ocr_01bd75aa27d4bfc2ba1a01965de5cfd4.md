Like the IPv4 Protocol field, the IPv6 Next Header identifies the extension header and is not of fixed length. It can contain additional information such as a hop-by-hop list of destinations, routing header (RH), IPsec information, and more. All extension headers are daisy-chained, each header pointing to the next header until they reach the transport layer data. This arrangement allows an IPv6 packet to be customized with features and functionality (for example, TCP, UDP, ICMPv6).

> **NOTE** Attackers can use these extension headers for malicious purposes.

# ICMPv6

Internet Control Message Protocol (ICMP) has a greater role in IPv6.

| ICMP Message Type | ICMPv4 | ICMPv6 |
|---|---|---|
| Connectivity checks | ✓ | ✓ |
| Information/error messaging | ✓ | ✓ |
| Fragmentation needed notification | ✓ | ✓ |
| Address assignment |  | ✓ |
| Address resolution |  | ✓ |
| Router discovery |  | ✓ |
| Multicast group management |  | ✓ |
| Mobile IPv6 support |  | ✓ |

ICMPv6 is used for neighbor and router discovery.

| ICMPv6 Message | Type | Description |
|---|---:|---|
| Neighbor solicitation (NS) | 135 | Similar to the IPv4 Address Resolution Protocol (ARP), it is sent by a host to determine the link-layer address of a neighbor.<br><br>Used to verify that a neighbor is still reachable.<br><br>An NS is also used for duplicate address detection (DAD). |
| Neighbor advertisement (NA) | 136 | A response to an NS message.<br><br>A node may also send unsolicited an NA to announce a link-layer address change. |
| Router advertisement (RA) | 134 | RAs contain prefixes that are used for address configuration including a hop limit value, maximum transmission unit (MTU) value, and so on.<br><br>RAs are sent either periodically or in response to an RS message. |
| Router solicitation (RS) | 133 | When a host is booting, it sends out an RS requesting routers to immediately generate an RA rather than wait for their next scheduled time. |