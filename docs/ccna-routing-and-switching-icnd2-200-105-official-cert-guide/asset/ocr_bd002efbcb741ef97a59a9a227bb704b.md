![](bbox=[0.11, 0.08, 0.57, 0.34])

| R8 Router LSA - Partial Contents | |
| :--- | :--- |
| Router ID: | 8.8.8.8 |
| Int. IP Address: | 172.16.3.1/24 |
| State: | UP |
| Cost: | 10 |

**Figure 7-5** Flooding LSAs Using a Link-State Routing Protocol

# ## Applying Dijkstra SPF Math to Find the Best Routes

The link-state flooding process results in every router having an identical copy of the LSDB in memory, but the flooding process alone does not cause a router to learn what routes to add to the IP routing table. Although incredibly detailed and useful, the information in the LSDB does not explicitly state each router's best route to a destination.

To build routes, link-state routers have to do some math. Thankfully, you and I do not have to know the math! However, all link-state protocols use a type of math algorithm, called the Dijkstra Shortest Path First (SPF) algorithm, to process the LSDB. That algorithm analyzes (with math) the LSDB, and builds the routes that the local router should add to the IP routing table—routes that list a subnet number and mask, an outgoing interface, and a next-hop router IP address.

Now that you have the big ideas down, the next several topics walk through the three main phases of how OSPF routers accomplish the work of exchanging LSAs and calculating routes. Those three phases are

+   *   **Becoming neighbors:** A relationship between two routers that connect to the same data link, created so that the neighboring routers have a means to exchange their LSDBs.
+   *   **Exchanging databases:** The process of sending LSAs to neighbors so that all routers learn the same LSAs.
+   *   **Adding the best routes:** The process of each router independently running SPF, on their local copy of the LSDB, calculating the best routes, and adding those to the IPv4 routing table.

# ## Becoming OSPF Neighbors

Of everything you learn about OSPF in this chapter, OSPF neighbor concepts have the most to do with how you will configure and troubleshoot OSPF in Cisco routers. You configure OSPF in ways that make routers become neighbors, and much of the LSA exchange process