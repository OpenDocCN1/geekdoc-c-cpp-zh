```
```text
L    2001:DB8:1:5::1/128 [0/0]
         via Serial0/0/0, receive
D    2001:DB8:1:6::/64 [90/2681856]
         via FE80::FF:FE00:3, Serial0/0/1
         via FE80::FF:FE00:2, Serial0/0/0
D    2001:DB8:1:7::/64 [90/2681856]
         via FE80::FF:FE00:3, Serial0/0/1
D    2001:DB8:1:8::/64 [90/2681856]
         via FE80::FF:FE00:3, Serial0/0/1
D    2001:DB8:1:33::/64 [90/2684416]
         via FE80::FF:FE00:3, Serial0/0/1
         via FE80::FF:FE00:2, Serial0/0/0
L    FF00::/8 [0/0]
         via Null0, receive
```
```

The pair of highlighted lines about halfway through the example describes the one route to IPv6 subnet 3 (2001:DB8:1:3::/64). Each route lists at least two lines, with the first line listing the prefix/length and, in brackets, the administrative distance and the metric (feasible distance). The second line lists the forwarding instructions for a route.

When a router has multiple routes to reach one IPv6 prefix, the output shows one line with the prefix and then one line for each route. The line for each route lists the forwarding instructions (a neighbor’s link-local address and local router’s outgoing interface). The highlighted lines at the end of the example, for subnet 33, show one such example, with two routes, each with a different next-hop address and different outgoing interface.

As for troubleshooting IPv6 routes, again, most of the troubleshooting for routes begins with questions about neighbors. Thinking through a potential EIGRP for IPv6 problem actually follows the same logic as working through an OSPFv3 problem. Repeating some of the logic from the preceding chapter, when a router simply has no route to a given subnet—for instance, if R1 had no route at all for subnet 33—then do the following:

+   1. **Step 1.** Check the routers with interfaces directly connected to that IPv6 prefix. A router must have EIGRP for IPv6 enabled on that interface before EIGRP for IPv6 will advertise about the subnet.
+   2. **Step 2.** Check EIGRP for IPv6 neighbor relationships for all routers between the local router and the routers with an interface connected to IPv6 prefix X.

For instance, in Figure 24-2, if Router R4 did not have an ipv6 eigrp 1 command under its G0/0 interface, all the routers would have their correct EIGRP for IPv6 neighbor relationships, but R4 would not advertise about subnet 33.

If a router has a route but it appears to be the wrong (suboptimal) route, take these steps:

+   1. **Step 1.** Check for broken neighbor relationships over what should be the optimal path from the local router and prefix X.
+   2. **Step 2.** Check the interface bandwidth and delay settings. Pay particular attention to the lowest bandwidth in the end-to-end route, because EIGRP ignores the faster bandwidths, using only the lowest (slowest) bandwidth in its metric calculation.