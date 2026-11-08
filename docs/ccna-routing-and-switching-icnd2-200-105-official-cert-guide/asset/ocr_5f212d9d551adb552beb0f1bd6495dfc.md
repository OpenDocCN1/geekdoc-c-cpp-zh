# Foundation Topics

# EIGRP and Distance Vector Routing Protocols

IPv4's long history has resulted in many competing interior gateway protocols (IGP). Each of these different IPv4 IGPs differs in some ways, including the underlying routing protocol algorithms like link state and distance vector. This first section of the chapter looks at how EIGRP acts like distance vector routing protocols to some degree, while at the same time, EIGRP does not fit easily into any category at all.

In particular, this first section positions EIGRP against the other common IPv4 routing protocols. Then this section looks at basic DV concepts as implemented with RIP. Using the simpler RIP to learn the basics helps the discussion focus on the DV concepts. This section ends then with a discussion of how EIGRP uses DV features but in a more efficient way than RIP uses them.

# Introduction to EIGRP

Historically speaking, the first IPv4 routing protocols used DV logic. RIP Version 1 (RIPv1) was the first popularly used IP routing protocol, with the Cisco-proprietary Interior Gateway Routing Protocol (IGRP) being introduced a little later, as shown in Figure 9-1.

![](bbox=[0.13, 0.47, 0.76, 0.66])

Figure 9-1 *Timeline for IP IGPs*

By the early 1990s, business and technical factors pushed the IPv4 world toward a second wave of better routing protocols. RIPv1 and IGRP had some technical limitations, even though they were great options for the technology levels of the 1980s. The world needed better routing protocols due to the widespread adoption and growth of TCP/IP in enterprise networks in the 1990s. Many enterprises migrated away from older vendor-proprietary networks to instead use networks built with routers, LANs, and TCP/IP. These businesses needed better performance from their routing protocols, including better metrics and better convergence. All these factors led to the introduction of a new wave of IPv4 interior routing protocols: RIP Version 2 (RIPv2), OSPF, and EIGRP.

Even today, EIGRP and OSPF remain the two primary competitors as the IPv4 routing protocol to use in a modern enterprise IPv4 internetwork. RIPv2 has fallen away as a serious competitor, in part due to its less robust hop-count metric, and in part due to its slower (worse) convergence time. Even today, you can walk in to most corporate networks and find either EIGRP or OSPF as the routing protocol used throughout the network.