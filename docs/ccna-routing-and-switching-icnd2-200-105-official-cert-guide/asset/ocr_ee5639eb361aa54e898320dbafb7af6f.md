how DV protocols work. In particular, the next examples show routes that use RIP’s simple hop-count metric, which, although a poor option in real networks today, is a much simpler option for learning than EIGRP’s more complex metric.

# The Concept of a Distance and a Vector

The term *distance vector* describes what a router knows about each route. At the end of the process, when a router learns about a route to a subnet, the all router knows is some measurement of distance (the metric) and the next-hop router and outgoing interface to use for that route (a vector, or direction).

Figure 9-3 shows a view of both the vector and the distance as learned with RIP. The figure shows the flow of RIP messages that cause R1 to learn some IPv4 routes, specifically three routes to reach subnet X:

+   - The four-hop route through R2
+   - The three-hop route through R5
+   - The two-hop route through R7

![](bbox=[0.139, 0.414, 0.814, 0.664])

**Figure 9-3**  *Information Learned Using DV Protocols*

DV protocols learn two pieces of information about a possible route to reach a subnet: the distance (metric) and the vector (the next-hop router). In this case, R1 learns three routes to reach subnet X. When only one route for a single subnet exists, the router chooses that one route. However, with the three possible routes in this case, R1 picks the two-hop route through next-hop Router R7, because that route has the lowest RIP metric.

While Figure 9-3 shows how R1 learns the routes with RIP updates, Figure 9-4 gives a better view into R1’s distance vector logic. R1 knows three routes, each with

# Key Topic

**Distance:** The metric for a possible route

**Vector:** The direction, based on the next-hop router for a possible route

Note that R1 knows no other topology information about the internetwork. Unlike LS protocols, RIP’s DV logic has no idea about the overall topology, instead just knowing about next-hop routers and metrics.