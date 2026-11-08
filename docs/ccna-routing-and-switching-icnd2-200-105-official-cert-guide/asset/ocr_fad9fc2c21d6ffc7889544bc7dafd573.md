This first section, from this page up to the heading “Troubleshooting IPv6,” repeats concepts discussed in the ICND1 book. If you are using both books, you might need to go back and review, or you might be ready to skip this section, as suggested here:

**Skip to “Troubleshooting IPv6”:** If you know IPv6 well, right now, skip ahead. For instance, maybe you are following a reading plan under which you just finished reading the ICND1 book’s IPv6 chapters and the material is fresh in your mind. Just know that this first section introduces no new concepts as compared to the ICND1 book’s IPv6 chapters.

**Read this section:** If you remember some of your IPv6 knowledge, but not all, this section is built for you. Keep reading!

**Go back and review the ICND1 book:** If you have not thought about IPv6 for quite a while, and you really do not remember much at all about it, you might be better off reviewing the IPv6 chapters in the ICND1 book first.

So, what is in this section? It hits the highlights of IPv6. Of course, it reviews IPv6 unicast addressing and subnetting. This section also discusses host IPv6 configuration, including stateless address autoconfiguration (SLAAC) and stateful Dynamic Host Configuration Protocol (DHCP). It reviews basic protocols, like Neighbor Discovery Protocol (NDP), and commands, like ping and traceroute. This section also reviews router configuration for addressing and static routes.

# Unicast IPv6 Addresses and IPv6 Subnetting

IPv6 defines two major types of unicast IPv6 addresses. *Global unicast addresses* work like public IPv4 addresses in that the enterprise obtains a unique prefix with all addresses inside the enterprise beginning with that prefix. With all companies using unique prefixes, all addresses in the IPv6 Internet should be unique.

*Unique local unicast addresses* work more like private addresses. A company can randomly create a prefix and assign addresses that begin with that prefix. Unique local addresses let companies avoid having to register a prefix while still having a good statistical chance of not using the same address range as other companies.

To create subnets with global unicast addresses, a company starts with the global routing prefix—the prefix assigned to the enterprise—and then breaks the address structure into three parts. In almost all cases, including most cases in this book and the ICND1 book, the combined global routing prefix and subnet part of the address makes up the first half (64 bits) of the address structure. The subnet part gives the enterprise network engineer a place to number each subnet with a different value, uniquely identifying each subnet. Then, the remainder of the structure leaves room for a 64-bit interface ID (or host field). Figure 22-1 summarizes these rules.

For example, a company might receive a global routing prefix of 2001:DB8:1111::/48. That is, all addresses must begin with those 12 hex digits. The subnet part of the address exists in the entire fourth quartet. Those subnet numbers can be (hex) 0000, 0001, 0002, and so on, up through FFFF, for 65,536 possible subnets in this example. As a result, the company might end up with a subnet design as shown in Figure 22-2.