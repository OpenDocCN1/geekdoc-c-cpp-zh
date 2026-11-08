# IPv6 Routing Protocol Versions and Protocols

First, when most engineers refer to “OSPF,” they are likely referring to OSPF as used with IPv4, and specifically, OSPF Version 2 (OSPFv2). To appreciate why, consider a few branches of the history of OSPF.

Once, there was an OSPF version 1 (OSPFv1), but OSPFv2 followed soon afterward (with the original OSPFv2 RFC dated 1991). When OSPF became widely used as an IPv4 routing protocol, back in the early to mid-1990s, OSPFv2 was already defined, and the router vendors used OSPFv2 and not OSPFv1. So, even in the early days of OSPF, there was no need for people to talk about whether they used OSPFv1 or OSPFv2; everyone used OSPFv2, and they just called it OSPF.

Next, consider the timeline for the development of the original IPv6 protocols, also back in early to mid-1990s. The introduction of IPv6 meant that many other protocols needed to be updated to make IPv6 work: ICMP, TCP, UDP, and so on, including OSPF. When a working group updated OSPF to support IPv6, what did they call it? OSPF version 3, of course. Figure 23-1 shows those events on the left and center of the timeline, with OSPFv3 first reaching RFC status in 1999.

![](bbox=[0.157, 0.418, 0.834, 0.554])

For a little over 10 years, the OSPF version story could be told easily in one sentence. You used OSPFv2 to advertise IPv4 routes, and OSPFv3 to advertise IPv6 routes. In fact, OSPFv2 could advertise only IPv4 routes, with OSPFv3 supporting only IPv6 routes.

This particular story continued to change. Again based on RFC dates, in 2010, OSPFv3 added support for IPv4 through a feature called address families. Basically, if you want to run dual stack (that is, both IPv4 and IPv6 on your routers), then you can run OSPFv3 with address families. You treat IPv4 as one address family, IPv6 as another, but each router has one OSPFv3 routing protocol process. With these new features, now OSPFv3 supports the advertisement of both IPv4 and IPv6 routes.

# Two Options for Implementing Dual Stack with OSPF

As previously indicated, dual stack means that routers support both IPv4 and IPv6. To implement dual stack, each router needs to learn both IPv4 and IPv6 routes. For many years, the OSPF solution for dual stack was clear: Run both OSPFv2 and OSPFv3 on all routers, as shown in Figure 23-2.