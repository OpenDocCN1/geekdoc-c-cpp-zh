If a router has a route but it appears to be the wrong (suboptimal) route, take these steps:

+   1. **Step 1.** Check for broken neighbor relationships over what should be the optimal path from the local router and prefix Y.
+   2. **Step 2.** Check the interface bandwidth and delay settings. Pay particular attention to the lowest bandwidth in the end-to-end route, because EIGRP ignores the faster bandwidths, using only the lowest (slowest) bandwidth in its metric calculation.