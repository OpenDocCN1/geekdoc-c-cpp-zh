The single-subnet-per-VC subnetting design uses the same logic as a set of point-to-point links. Using multiple subnets instead of one larger subnet does waste some IP addresses. However, using a single subnet in the partial-mesh design of Figure H-12 introduces several problems with routing protocols because not all routers in the subnet can send messages directly to each other. Partial-mesh designs work better with a single-subnet-per-VC approach.

![](bbox=[0.088, 0.195, 0.867, 0.456])

**Figure H-12**  *Partial Mesh with IP Addresses*

Table H-4 shows the IP addresses for the partially meshed Frame Relay network shown in Figure H-12.

# **Table H-4**  IP Addresses with Point-to-Point Subinterfaces

| Router | Subnet | IP Address |
|---|---|---|
| Atlanta | 140.1.1.0 | 140.1.1.1 |
| Charlotte | 140.1.1.0 | 140.1.1.2 |
| Atlanta | 140.1.2.0 | 140.1.2.1 |
| Nashville | 140.1.2.0 | 140.1.2.3 |
| Atlanta | 140.1.3.0 | 140.1.3.1 |
| Boston | 140.1.3.0 | 140.1.3.4 |

Cisco IOS software has a configuration feature called *subinterfaces* that creates a logical subdivision of a physical interface. Subinterfaces allow the Atlanta router to have three IP addresses associated with its serial 0/1/1 physical interface by configuring three separate sub-interfaces. A router can treat each subinterface, and the VC associated with it, as if it were a point-to-point serial link. Each of the three subinterfaces of serial 0/1/1 on Atlanta would be assigned a different IP address from Table H-5. (Example 14-8 in Chapter 14 shows Atlanta's configuration to match the address in Table H-5, including the subinterfaces of S0/1/1.)

> **NOTE**  The example uses IP address prefixes of /24 to keep the math simple. In production networks, point-to-point subinterfaces usually use a prefix of /30 (mask 255.255.255.252) because that allows for only four valid IP addresses—the exact number needed on a point-to-point subinterface. Of course, using different masks in the same network means that your routing protocol must also support VLSM.