# Foundation Topics

# Comparing Dynamic Routing Protocol Features

Routers and IP routes to their routing tables using three methods: connected routes, static routes, and routes learned by using dynamic routing protocols. Before we get too far into the discussion, however, it is important to define a few related terms and clear up any misconceptions about the terms *routing protocol*, *routed protocol*, and *routable protocol*. The concepts behind these terms are not that difficult, but because the terms are so similar, and because many documents pay poor attention to when each of these terms is used, they can be a bit confusing. These terms are generally defined as follows:

+   - **Routing protocol:** A set of messages, rules, and algorithms used by routers for the overall purpose of learning routes. This process includes the exchange and analysis of routing information. Each router chooses the best route to each subnet (path selection) and finally places those best routes in its IP routing table. Examples include RIP, EIGRP, OSPF, and BGP.
+   - **Routed protocol and routable protocol:** Both terms refer to a protocol that defines a packet structure and logical addressing, allowing routers to forward or route the packets. Routers forward packets defined by routed and routable protocols. Examples include IP Version 4 (IPv4) and IP Version 6 (IPv6).

> **NOTE**  The term *path selection* sometimes refers to part of the job of a routing protocol, in which the routing protocol chooses the best route.

Even though routing protocols (such as OSPF) are different from routed protocols (such as IP), they do work together very closely. The routing process forwards IP packets, but if a router does not have any routes in its IP routing table that match a packet’s destination address, the router discards the packet. Routers need routing protocols so that the routers can learn all the possible routes and add them to the routing table, so that the routing process can forward (route) routable protocols such as IP.

# Routing Protocol Functions

Cisco IOS software supports several IP routing protocols, performing the same general functions:

+   1. Learn routing information about IP subnets from neighboring routers.
+   2. Advertise routing information about IP subnets to neighboring routers.
+   3. If more than one possible route exists to reach one subnet, pick the best route based on a metric.
+   4. If the network topology changes—for example, a link fails—react by advertising that some routes have failed and pick a new currently best route. (This process is called *convergence*.)

![](bbox=[0.069, 0.704, 0.126, 0.742])

> **NOTE**  A neighboring router connects to the same link as another router, such as the same WAN link in the Ethernet LAN.

Answers to the “Do I Know This Already?” quiz:

1 D  2 C,  3 B,  3 C,  4 C  5 B  6 C