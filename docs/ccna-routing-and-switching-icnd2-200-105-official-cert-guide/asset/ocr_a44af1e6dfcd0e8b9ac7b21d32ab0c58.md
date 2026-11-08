Routing protocols choose the best route to reach a subnet by choosing the route with the lowest metric. For example, RIP uses a counter of the number of routers (hops) between a router and the destination subnet. OSPF totals the cost associated with each interface in the end-to-end route, with the cost based on link bandwidth. Table 7-2 lists the most important IP routing protocols for the CCNA exams and some details about the metric in each case.

**Table 7-2  IP GP Metrics**

| IGP | Metric | Description |
|---|---|---|
| RIP-2 | Hop count | The number of routers (hops) between a router and the destination subnet |
| OSPF | Cost | The sum of all interface cost settings for all links in a route, with the cost defaulting to be based on interface bandwidth |
| EIGRP | Composite of bandwidth and delay | Calculated based on the route’s slowest link and the cumulative delay associated with each interface in the route |