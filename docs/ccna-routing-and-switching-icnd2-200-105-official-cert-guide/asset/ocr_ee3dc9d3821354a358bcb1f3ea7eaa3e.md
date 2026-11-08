# Learning Default Routes from the ISP

Now turn the logic around, and think about what the ISP can and should advertise with *eBGP* to the enterprise. The Internet core routers have almost 600,000 IPv4 routes. An enterprise router at the Internet edge could learn all those routes from the ISP, and put those in its IPv4 routing table. Then, through a process called *redistribution*, that router could take all those BGP-learned routes and advertise them into the rest of the enterprise routers using the IGP.

However, what would all those new IP routes list as their next-hop addresses? All those new routes would send packets toward R1, and R1 would send them toward ISP1. Typically, the routers normally used by enterprises would not be designed to perform well with hundreds of thousands of routes in their routing tables.

Using a default route makes much more sense for a single-homed Internet edge design as compared with learning all those extra IP routes. The enterprise router that connects to the ISP needs one default route, so that for any unknown destinations, the packets are sent to the ISP. The idea is exactly what is discussed in regard to how OSPF advertises default routes back in Chapter 8.

When using a default routing strategy at the Internet edge, you can statically configure the default route, or learn it with eBGP. The OSPF chapter showed the static default route configuration, so of course, this chapter shows the effects of using eBGP.

Figure 12-9 shows the basic concept. At Step 1, the ISP advertises a default route with eBGP. At Step 2, router R1 takes the steps necessary with its IGP so that the IGP then reacts to the eBGP-learned default route, advertising a default route into the enterprise with the IGP.

![](bbox=[0.089, 0.559, 0.653, 0.686])

**Figure 12-9** *ISP Advertises a Default Route; IGP Propagates*

That concludes the overview of BGP and eBGP in preparation for the configuration and verification topics. The rest of the chapter focuses on the eBGP peering between the enterprise and the ISP, particularly on the configuration side of the configuration. That includes the details of configuring the peering relationship with the ISP router, advertising the public IP prefix (with the network BGP subcommand), and verifying the eBGP advertised and received routes.

# eBGP Configuration and Verification

eBGP configuration focuses on enabling the routing protocol on interfaces. The configuration may use the network router subcommand, which the router then compares to interface IPv4 addresses. Alternately, the IGP configuration may use an interface subcommand like