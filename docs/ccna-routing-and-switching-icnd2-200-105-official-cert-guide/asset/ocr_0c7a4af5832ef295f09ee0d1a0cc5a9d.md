If a router has a route, but it appears to be the wrong (suboptimal) route, take these steps:

+   1. **Step 1.** Check for broken neighbor relationships over what should be the optimal path from the local router and prefix Y.
+   2. **Step 2.** Check the OSPFv3 cost settings on the interfaces in the optimal path.

For instance, in Figure 23-11, suppose that R1 indeed has one route for subnet 33, pointing over the lower route, with R4 as the next-hop router. The root cause of that choice could be the following:

+   - The R2-R3 neighbor relationship is not working.
+   - The sum of the costs for the top route is larger (worse) than the sum of the costs for the lower route. (Note that the figure shows an asterisk beside each interface whose cost is part of the calculation.)