The generic permit and deny command shows the syntax for an extended IPv6 ACL. With IPv6, the difference between standard and extended ACLs is subtle. There is no keyword that distinguishes an IPv6 ACL as either standard or extended. Instead, an extended IPv6 ACL simply uses more than the source and destination IPv6 address fields when matching.

IPv6 extended ACLs can match on many of the values within the IPv6 header. IPv6 ACLs can match on the DSCP value for QoS marking, the flow label, and the source and destination IPv6 address. IPv6 extended ACLs have the ability to match not only on the source and destination IP addresses, but also an upper-layer protocol information. The next-header value in the IPv6 header indicates the number of the type of header that immediately follows the IPv6 header. In many cases, this would be either a TCP or UDP header where the protocol value would be tcp or udp, respectively. However, it could also be an ICMPv6 packet or it could be an extension header that has been added between the IPv6 header and the upper-layer header. IPv6 extended ACLs can match on destination option headers, fragmentation headers, routing headers, and Mobile IPv6 (MIPv6) headers. (To extend your learning about additional IPv6 extension header types, search for and read a copy of IETF RFC 2460.)

Besides matching IPv6 packets, IPv6 ACLs can also match ICMPv6 packets. ICMPv6 packets are IPv6 packets that also include an ICMPv6 header. By specifying icmp as the protocol keyword in the IPv6 ACL entry, the command matches the subset of IPv6 packets that also have an ICMPv6 header. Using the icmp keyword also enables many filtering options for ICMPv6 packets. For IPv6 ACL entries that match on ICMPv6 message headers, the following syntax defines how these ACL entries are configured:

```
```text
[permit | deny] icmp { source-ipv6-prefix/prefix-length | any | host source-ipv6-address } auth { operator [port-number] } { destination-ipv6-prefix/prefix-length | any | host destination-ipv6-address | auth } [ operator [port-number] ] [ icmp-type [icmp-code] | icmp-message ] [ dest-option-type | doh-number | doh-type ] [ dscp value ] [ flow-label value ] [ fragments ] [ hbh ] [ log ] [ log-input ] [ mobility ] [ mobility-type ] [ mh-number | mh-type ] [ routing ] [ routing-type | routing-number ] [ sequence value ] [ time-range name ]
```
```

ICMPv6 ACLs can match on the source and destination IPv6 addresses, but also the ICMPv6 type and code values. ICMPv6 ACLs can also match on many other IPv6 extension headers like IPv6 extended ACLs.

It is possible to create an IPv6 ACL that matches TCP header values including source and destination port numbers. It is possible, although uncommon, for an ACL to match on TCP flags such as ACK, FIN, PSH, RST, SYN, and URG. TCP IPv6 ACLs can also match the other IPv6 extension header values. Following is the syntax for an IPv6 ACL that uses the tcp value for the protocol along this ACL to permit or deny a TCP packet:

```
```text
[permit | deny] tcp { source-ipv6-prefix/prefix-length | any | host source-ipv6-address } { operator [port-number] } { destination-ipv6-prefix/prefix-length | any | host destination-ipv6-address } { operator [port-number] } [ ack ] [ dest-option-type | doh-number | doh-type ] [ dscp value ] [ fragments ] [ hbh ] [ log ] [ log-input ] [ mobility ] [ mobility-type ] [ mh-number | mh-type ] [ neq { port | protocol } ] [ psh ] [ range { port | protocol } ] [ reflect name ] [ router-alert ] [ routing ] [ routing-type | routing-number ] [ rst ] [ sequence value ] [ syn ] [ time-range name ] [ urg ]
```
```

IPv6 ACLs also have the ability to match UDP packets. UDP packets do not have any of the flow-control flags used in TCP packets, and as a result, the ACL syntax is simpler. However, UDP IPv6 ACLs can still match on IPv6 extension header values. When the udp protocol