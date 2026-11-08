
So many similarities exist between EIGRP for IPv6 and EIGRP for IPv4 that you should just assume that they work the same, except for a few differences, as noted in the following list:

- EIGRP for IPv6 advertises IPv6 prefixes, whereas EIGRP for IPv4 advertises IPv4 subnets.
- EIGRP for IPv6 show commands use a keyword of `ipv6`, in the same position where EIGRP show commands use a keyword of `ip`.
- EIGRP for IPv6 uses the same checklist for choosing whether to become neighbors, except EIGRP for IPv6 routers may become neighbors if they have IPv6 addresses in different subnets. (EIGRP for IPv4 neighbors must be in the same IPv4 subnet.)
- EIGRP for IPv6 does not have an autonomous system concept (while EIGRP for IPv4 does).

Next, focus for a moment on troubleshooting related to EIGRP for IPv6 interfaces. As with OSPF, most troubleshooting revolves around the neighbor relationships. However, this short list describes two problems that can happen related to the interfaces:

- The omission of an `ipv6 eigrp asn` interface subcommand on an interface that has no possible neighbors may go overlooked. This omission does not impact EIGRP for IPv6 neighbors. However, this omission means that EIGRP for IPv6 is not enabled on that interface, and therefore the router will not advertise about that connected subnet. This problem shows up as a missing route.
- Making an interface passive to the EIGRP for IPv6 process, when a potential EIGRP for IPv6 neighbor is connected to that link, prevents the two routers from becoming neighbors. Note that the neighbor relationship fails with just one of the two routers having a passive interface.

Table 24-3 lists the items to consider when troubleshooting EIGRP neighbor relationships.

**Table 24-3** Neighbor Requirements for EIGRP for IPv4 and EIGRP for IPv6

| Requirement | EIGRP for IPv4 | EIGRP for IPv6 |
|---|---|---|
| Interfaces must be in an up/up state. | Yes | Yes |
| Interfaces must be in the same subnet. | Yes | No |
| Access control lists (ACLs) must not filter routing protocol messages. | Yes | Yes |
| Must pass routing protocol neighbor authentication (if configured). | Yes | Yes |
| Must use the same ASN on the router configuration command. | Yes | Yes |
| K values must match. | Yes¹ | Yes¹ |
| Hello and hold timers must match. | No | No |
| Router IDs must be unique. | No² | No² |

¹ K values define the EIGRP metric calculation algorithm. Cisco recommends that the settings be left as is; the metric weights command in router mode reconfigures the settings.

² Having duplicate EIGRP RIDs does not prevent routers from becoming neighbors, but it can cause problems when external EIGRP routes are added to the routing table.

As for troubleshooting IPv6 routes, again, most of the troubleshooting for routes begins with questions about neighbors. Thinking through a potential EIGRP for IPv6 problem actually follows the same logic as working through an OSPFv3 problem. Repeating some of the logic from the preceding chapter, when a router simply has no route to a given subnet—for instance, if R1 had no route at all for subnet 33—then do the following:

- **Step 1.** Check the routers with interfaces directly connected to that IPv6 prefix. A router must have EIGRP for IPv6 enabled on that interface before EIGRP for IPv6 will advertise that subnet.
- **Step 2.** Check EIGRP for IPv6 neighbor relationships for all routers between the local router and the routers with an interface connected to IPv6 prefix X.

For instance, in Figure 24-2, if Router R4 did not have an `ipv6 eigrp 1` command under its G0/0 interface, all the routers would have their correct EIGRP for IPv6 neighbor relationships, but R4 would not advertise about subnet 33.

If a router has a route but it appears to be the wrong (suboptimal) route, take these steps:

- **Step 1.** Check for broken neighbor relationships over what should be the optimal path from the local router and prefix Y.
- **Step 2.** Check the interface bandwidth and delay settings. Pay particular attention to the lowest bandwidth in the end-to-end route, because EIGRP ignores the faster bandwidths, using only the lowest (slowest) bandwidth in its metric calculation.

## Chapter 25

At this point you should be familiar with IPv4 ACLs but just starting to learn about IPv6 ACLs. As you learn about IPv6, you will notice subtle differences about IPv6 that have direct functional relationships with IPv4 protocol operations. Similarly, there are subtle similarities and differences between the way that IPv4 ACLs and IPv6 ACLs operate. Following are the ways that IPv4 and IPv6 are similar:

- Both match on the source address or the destination address in the protocol header.
- Both match individual host addresses or subnets/prefixes.
- Both can be applied directionally (inbound and outbound) to a router's interface.
- Both can match on transport layer protocol information such as TCP or UDP source or destination port numbers.
- Both can match on specific ICMP message types and codes.
- Both have an implicit deny statement at the end of the ACL that matches all remaining packets.
- Both support time ranges for time-based ACLs.

Of course, there are key differences between IPv4 and IPv6 ACLs as well. IPv4 ACLs match IPv4 packets only (and not IPv6), and match special fields found only in IPv4 headers. Likewise, IPv6 ACLs match against IPv6 address fields as well as other fields unique to an IPv6 header. The following is a summary of the key differences:

- IPv4 ACLs can only match IPv4 packets and IPv6 ACLs can only match IPv6 packets.
- IPv4 ACLs can be identified by number or name, while IPv6 ACLs use names only.
- IPv4 ACLs identify that an ACL is either standard or extended based on the ACL number range or by using the standard or extended keyword. IPv6 ACLs have a similar standard and extended ACL concept, but do not differentiate the styles with a different configuration keyword.
- IPv4 ACLs can match on specific values unique to an IPv4 header (e.g., option, precedence, ToS, TTL, fragments).
- IPv6 ACLs can match on specific values unique to an IPv6 header (e.g., flow label, DSCP) as well as extension and option header values.
- IPv6 ACLs have some implicit **permit** statements at the end of each ACL, just before the implicit deny all at the end of the ACL, while IPv4 ACLs do not have implicit **permit** statements.

Figure 25-2 points out some of the more common matching options specific to IPv6 extended ACL permit and deny commands when using the **tcp**, **udp**, and **icmp** keywords. When using any protocol keyword other than **icmp6**, the permit or deny command then matches a subset of IPv6 packets. For instance, using the **tcp** keyword as the protocol matches all IPv6 packets with a TCP header. Additionally, as with IPv4 ACLs, to match TCP port numbers, you must use the **tcp** keyword in the permit or deny command. Likewise, the command must use the **udp** keyword to match UDP port numbers, and the **icmp** keyword to then match ICMP message types.

| Command | Port Matching |
|---|---|
| `permit tcp...` | `[eq \| gt \| lt \| neq {port \| protocol}] [range {port \| protocol}]` |
| `permit udp...` | `[eq \| gt \| lt \| neq {port \| protocol}] [range {port \| protocol}]` |

| Command | ICMP Message Types |
|---|---|
| `permit icmp...` | `[icmp-type [icmp-code] \| icmp-message]` |

**Figure 25-2**  *ICMP, TCP, and UDP Matching Fields in Extended IPv6 ACLs*

In this section, practice getting comfortable with the syntax of the **ipv6 access-list permit** or deny ACL entry, particularly with choosing the correct matching logic. First, the following list summarizes some important tips to consider when choosing matching parameters to any **ipv6 access-list permit** or deny ACL entries:

- To match a specific address, just list the address after the host keyword.
- To match any and all addresses, use the any keyword.
- To match based only on the IPv6 prefix, use the “/slash” notation to designate the number of bits in the prefix length. For example, a /64 prefix length matches the first 64 bits of the 128-bit IPv6 address, and any Interface Identifier (IID) within the least-significant 64 bits of that address falls within that prefix range.
