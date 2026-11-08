
The following troubleshooting checklist gives us a place to start when troubleshooting DHCP-related issues:

- **Step 1.** If using a centralized DHCP server, at least one router on each remote subnet that has DHCP clients must act as DHCP relay agent, and have a correctly configured `ip helper-address address` subcommand on the interface connected to that subnet.
- **Step 2.** Troubleshoot for any IP connectivity issues between the DHCP relay agent and the DHCP server, using the relay agent interface IP address and the server IP address as the source and destination of the packets.
- **Step 3.** Whether using a local DHCP server or centralized server, troubleshoot for any LAN issues between the DHCP client and the DHCP relay agent.
- **Step 4.** Troubleshoot incorrect server configuration.

IP subnetting rules require that the address ranges in the subnets used in an internetwork should not overlap. IOS sometimes can recognize when a new ip address command creates an overlapping subnet, but sometimes not, as follows:

- Preventing the overlap on a single router: IOS detects the overlap when the `ip address` command implies an overlap with another `ip address` command *on the same router*.
- Allowing the overlap on different routers: IOS cannot detect an overlap when an `ip address` command overlaps with an `ip address` command on another router.

## Chapter 22

Table 22-1 summarizes a few bits of reference information about global unicast and unique local unicasts for reference.

**Table 22-1** Summary of IPv6 Unicast Address Types

| Type | First Digits | Similar to IPv4 Public or Private? |
|---|---|---|
| Global unicast | 2 or 3¹ | Public |
| Unique local unicast | FD | Private |
| Link-local | FE80 | N/A |

¹ IANA actually defines the global unicast address range as any address not otherwise reserved for some other purpose. However, actual address assignments normally happen from 2000::/3 because that was the original range used for these addresses. Many IPv6 references simply quote 2000::/3 as the prefix, which means the first hex digit is either a 2 or 3.

The one noticeable difference between DHCPv4 and stateful DHCPv6 is that the stateful DHCPv6 server does not supply the default router information. Instead, a built-in protocol, NDP, lets the host ask the local routers to identify themselves. Otherwise, hosts use the same general process as with DHCPv4. Figure 22-5 shows a comparison of what is learned by a host using DHCPv4 and stateful DHCPv6.

![](img/79473ea15699e01619d2aa789f5bd43b_1384_0.png)

**Figure 22-5** *Sources of Specific IPv6 Settings When Using Stateful DHCP*

SLAAC defines an overall process that also uses NDP and DHCPv6 with a stateless service; the server keeps no state information. First, the process takes advantage of NDP, through which the host can learn the following from any router on the link: the IPv6 prefix (subnet ID), the prefix length (mask equivalent), and the default router IPv6 address. The host uses SLAAC rules to build the rest of its address. Finally, the host uses stateless DHCPv6 to learn the DNS server IPv6 addresses. Figure 22-7 summarizes these details for easy study and reference.

![](img/79473ea15699e01619d2aa789f5bd43b_1385_0.png)

**Figure 22-7** *Sources of Specific IPv6 Settings When Using SLAAC*

If the host uses the EUI-64 option, the address built by the host can be predicted. The prefix part of the address is the prefix as defined on the local IPv6 router. Then, the host’s MAC address feeds into a few EUI-64 (also called modified EUI-64) rules to change the 48-bit MAC address into a 64-bit interface ID, as follows:

- 1. Split the 6-byte (12 hex digits) MAC address in two halves (6 hex digits each).
- 2. Insert FF:FE in between the two, making the interface ID now have a total of 16 hex digits (64 bits).
- 3. Invert the seventh bit of the first byte.

Figure 22-8 shows the major pieces of how the address is formed.

![](img/79473ea15699e01619d2aa789f5bd43b_1387_0.png)

**Figure 22-8** *IPv6 Address Format with Interface ID and EUI-64*

Before getting into the specific scenarios, the following three lists break down some important facts that should be true about a working IPv6 network. Many of the root causes of problems in this section of the chapter happen because one of these rules was broken.

### Host-Focused Issues

- 1. Hosts should be in the same IPv6 subnet as their default router.
- 2. Hosts should use the same prefix length as their default router.
- 3. Hosts should have a default router setting that points to a real router’s address.
- 4. Hosts should have correct Domain Name Service (DNS) server addresses.

### Router-Focused Issues

- 1. Router interfaces in use should be in an up/up state.
- 2. Two routers that connect to the same data link should have addresses in the same IPv6 subnet.
- 3. Routers should have IPv6 routes to all IPv6 subnets as per the IPv6 subnet design.

### Filtering Issues

- 1. Watch for MAC address filtering on the LAN switches.
- 2. Watch for missing VLANs in switches.
- 3. Watch for IPv6 access control lists (ACL) in routers.

Figure 22-13 collects all the pieces that should match. The concepts mirror the same concepts in IPv4.

![](img/79473ea15699e01619d2aa789f5bd43b_1391_0.png)

**Figure 22-13** *Host IPv6 Settings Compared to What the Settings Should Match*

To find the problem, the engineer needs to start thinking outside the IPv6 world and start thinking about the LAN between the host and the router. In particular, the probable root causes can be broken down into these categories:

- 1. The router or host LAN interface is administratively disabled.
- 2. The LAN has some problem that prevents the flow of Ethernet frames.
- 3. The LAN has filtering (for example, port security) that filters the Ethernet frames.

These symptoms pretty clearly point to “some kind of name resolution problem.” However, that does not define the specific root cause that the engineer can go fix to get the user working again. In this case, the root causes could fall into these categories:

- 1. An incorrect host DNS server setting, as statically defined on the host
- 2. An incorrect host DNS server setting, as learned with (stateless or stateful) DHCPv6
- 3. An IPv6 connectivity problem between the user’s host and the DNS server

The two most likely root causes of a host failing to dynamically learn its IPv6 settings with stateful DHCPv6 are root causes 2A and 2B. For 2A, the solution requires a configuration command on the correct interface on each LAN that is remote from the DHCPv6 server. For instance, in Figure 22-16, host D sits on a LAN subnet on the left, with R1’s G0/0 interface connected to the same subnet. R1 should have the command listed at the bottom of the figure to enable the IPv6 DHCP relay function pointing to the DHCPv6 server on the right.

![](img/79473ea15699e01619d2aa789f5bd43b_1395_0.png)

Routing problems happen for many reasons. Some routing problems happen because routes are missing from a router (perhaps because of many specific root causes). Some routing problems happen because a router has an incorrect route. The following list gives just some of the reasons why a router might be missing a needed route or might have an incorrect route:

- Links between routers are down.
- Routing protocol neighbor problems exist.
- Routing protocol route filtering prevents the route from being added to the IPv6 routing table.
- Incorrect static routes send packets to the wrong next router.
- Poor subnet design duplicates subnets in different locations in the network, falsely advertising a subnet.
