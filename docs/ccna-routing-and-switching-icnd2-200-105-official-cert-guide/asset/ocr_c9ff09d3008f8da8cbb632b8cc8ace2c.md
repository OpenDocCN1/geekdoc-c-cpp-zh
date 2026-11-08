![](bbox=[0.156, 0.092, 0.733, 0.283])

**Figure G-2**  *EIGRP Choosing the Longer but Better Route to Subnet 10.1.1.0*

# Distance Vector Basics

Each IGP can be categorized based on its internal logic, either distance vector (used by RIP) or link state. The next few pages explain more about how a DV protocol actually exchanges routing information, using RIPv2 as an example. The ICND2 book’s chapters about OSPF describe link state logic, and the ICND2 book’s chapters on EIGRP get into more detail about some advanced distance vector features.

# The Concept of a Distance and a Vector

The term *distance vector* describes what a router knows about each route. When a router learns about a route to a subnet, the routers learn three important facts related to each route: the destination subnet, the distance (that is, the routing protocol metric), and the vector (that is, the link and next-hop router to use as part of that route).

Figure G-3 begins to develop that concept showing RIP updates in the small boxes on the left. That is, Router R1 receives RIP updates from three neighboring routers. Each update describes a different route for subnet X, with a different metric. The fact that a particular router sends the RIP message identifies the next-hop router for the route. In this case, the three RIP updates advertise the following routes:

+   - The four-hop route (distance) through R2 (vector) for subnet X
+   - The three-hop route (distance) through R5 (vector) for subnet X
+   - The two-hop route (distance) through R7 (vector) for subnet X

![](bbox=[0.157, 0.718, 0.722, 0.898])

**Figure G-3**  *Information Learned Using DV Protocols*