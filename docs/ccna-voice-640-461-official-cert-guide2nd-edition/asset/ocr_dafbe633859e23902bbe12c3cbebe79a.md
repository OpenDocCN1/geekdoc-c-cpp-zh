When you specify that certain network traffic should go into the priority queue, the router then not only guarantees traffic bandwidth, it guarantees the first band-width. For example, using CBWFQ, Citrix traffic might be guaranteed 50 percent of the bandwidth, but it may get that bandwidth after the router has fulfilled some other traffic guarantees. When using LLQ, the priority traffic always gets before any other traffic guarantees are fulfilled. As you might guess, this works very well for VoIP, making LLQ the preferred queuing algorithm for voice.

Although there are many queuing algorithms available, these three encompass the methods used by most modern networks.

# Applying QoS

By nature, you can apply most of the QoS mechanisms discussed as the network traffic leaves a router (because you cannot control the order the router receives traffic; it simply arrives). Table 6-7 summarizes the QoS methods discussed and the direction you can apply them on your router.

Table 6-7 Applying QoS to Input and Output Interfaces of a router

| QoS Methods Applied as Traffic Enters the Router (Input) | QoS Methods Applied as Traffic Leaves the Router (Output) |
|---|---|n| Classification | Congestion Management |
| Marking | Marking |
| Policing | Congestion Avoidance |
| | Shaping |
| | Policing |
| | Compression |
| | Fragmentation and Interleaving

As you can see, you can apply some QoS methods (such as policing) in either direction.

# Using Cisco AutoQoS

Deploying QoS can be complex (which is why there's a difficult CCNP Voice exam dedicated just to the topic). To help ease the learning curve for QoS, Cisco created a mechanism called AutoQoS, which allows you to enable a variety of QoS mechanisms with little QoS knowledge. AutoQoS works well out of the box that many network administrators have full knowledge of the QoS capabilities and configuration on Cisco devices use it. AutoQoS moved to this acclaimed status because it deploys a template QoS configuration in line with Cisco best practices based on the bandwidth and encapsulation under each of your router or switch interfaces. This template-based QoS deployment offers multiple advantages to manual QoS configuration:

+   - Reduces the time of deployment: Entering a single command on a device is much less time consuming than the potentially complex QoS configurations.