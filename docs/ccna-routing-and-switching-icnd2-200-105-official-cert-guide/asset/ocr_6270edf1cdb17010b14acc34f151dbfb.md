you might look for one type of root cause; but if R1 uses the lower route through five routers, you might look for a different root cause.

![](bbox=[0.161, 0.139, 0.759, 0.348])

**Figure 23-11**  *Competing Long and Short Routes from R1 to Subnet 33*

When a router simply has no route to a given subnet—for instance, if R1 has no route at all for subnet 33—do the following:

# **Key Topic**

+   1. **Step 1.** Check the routers with interfaces directly connected to that IPv6 prefix. A router must have OSPFv3 enabled on that interface before OSPFv3 will advertise about the subnet.
+   
+   2. **Step 2.** Check OSPFv3 neighbor relationships for all routers between the local router and the routers with an interface connected to IPv6 prefix X.

For instance, in Figure 23-11, if Router R3 did not have an **ipv6 ospf process-id area area-id** command on its LAN interface, all seven routers could be working neighbor relationships, but R3 still would not advertise about subnet 33.

If a router has a route, but it appears to be the wrong (suboptimal) route, take these steps:

# **Key Topic**

+   1. **Step 1.** Check for broken neighbor relationships over what should be the optimal path from the local router and prefix X.
+   
+   2. **Step 2.** Check the OSPFv3 cost settings on the interfaces in the optimal path.

For instance, in Figure 23-11, suppose that R1 indeed has one route for subnet 33, pointing over the lower route, with R4 as the next-hop router. The root cause of that choice could be the following:

+   - The R2-R3 neighbor relationship is not working.
+   - The sum of the costs for the top route is larger (worse) than the sum of the costs for the lower route. (Note that the figure shows an asterisk beside each interface whose cost is part of the calculation.)