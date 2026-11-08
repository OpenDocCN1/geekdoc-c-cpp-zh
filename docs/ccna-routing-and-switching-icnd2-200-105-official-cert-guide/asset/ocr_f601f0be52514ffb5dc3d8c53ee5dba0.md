The BGP **network** command works differently than the **network** command supported by the various IGPs. This section details several examples to show the differences, as follows:

+   - Advertising a route for an entire classful network or public address block
+   - Advertising routes for subnets of the public address block
+   - Advertising routes for larger address blocks when only subnets exist in the routing table

# ### Injecting Routes for a Classful Network

To begin, consider this straightforward case of an eBGP connection. The enterprise uses a Class C public network (192.0.2.0/24), placing that entire Class C network in its DMZ, as shown in Figure 12-13.

![](bbox=[0.161, 0.316, 0.9, 0.49])

**Figure 12-13** *All of Class C Network 192.0.2.0/24 Used as DMZ Subnet*

R1 needs to advertise its public prefix (192.0.2.0/24) to the ISP. R1 also needs to avoid advertising its private address space to the ISP (10.0.0.0/8). Why? Routers in the Internet need to know how to forward packets to the enterprise's public address range. However, many companies use the same private IPv4 networks, such as IPv4 network 10.0.0.0, and by definition, these networks are not advertised into the Internet.

To advertise its public prefix, the enterprise network engineer can configure a BGP **network** command on R1. This command lets the engineer easily control which prefixes R1 adds to its BGP table. Once in the BGP table, the router then advertises the prefixes to the ISP. The **network** command basically tells BGP this:

> > Put this prefix/length into the BGP table, assuming that prefix/length is in the IP routing table.

Figure 12-14 details the logic of the BGP **network** *prefix mask DDN-mask* command. The **network** command lists a prefix and DDN-style mask (Step 1 in the figure), IOS then compares that prefix and mask to the prefix/mask for the routes in the IPv4 routing table. BGP looks for an exact match (Step 2), meaning that the BGP **network** command's prefix and mask both exactly match a prefix and mask in a route in the routing table. If a match is found (Step 3), BGP on that router creates a matching BGP table entry. BGP advertises the best valid routes from its BGP table to its BGP peers (Step 4).