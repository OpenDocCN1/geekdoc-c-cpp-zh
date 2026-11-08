![](bbox=[0.067, 0.091, 0.752, 0.297])

**Figure 9-9**  _Full and Partial EIGRP Updates_

Note that EIGRP refers to the information exchanged in the updates as topology information. The information is not nearly as detailed as OSPF LS topology data, and it does not attempt to describe every router and link in the network. However, it does describe more than just a distance (metric) and vector (next-hop router) for the local router—a local router also learns the metric as used by the next-hop router. This added information is used to help EIGRP converge quickly, without causing loops, as discussed in the upcoming section “EIGRP Convergence.”

# Calculating the Best Routes for the Routing Table

EIGRP calculates the metric for routes much differently than any other routing protocol. For instance, with OSPF, anyone with a network diagram and knowledge of the configured OSPF interface costs can calculate the exact OSPF metric (cost) for each route. EIGRP uses a math equation and a composite metric, making the exact metric value hard to predict.

# The EIGRP Metric Calculation

The EIGRP composite metric means that EIGRP feeds multiple inputs (called metric components) into the math equation. By default, EIGRP feeds two metric components into the calculation: bandwidth and delay. The result of the calculation is an integer value and is the composite metric for that router.

Note that EIGRP includes other options for how it could calculate the metric, but those options are not normally used. EIGRP supports also using the interface load and interface reliability in the metric calculation. EIGRP also advertises the maximum transmission unit (MTU) associated with the route—that is, the longest IP packet allowed over the route—but does not support using the MTU when calculating the metric. For this book’s purposes, EIGRP uses the default settings, calculating the composite metric based on the bandwidth and delay.

EIGRP’s metric calculation formula actually helps describe some of the key points about the composite metric. (In real life, you seldom if ever need to sit down and calculate what a router will calculate with this formula.) The formula, assuming that the default settings that tell the router to use just bandwidth and delay, is as follows:

$$\text{Metric} = \left(\frac{10^7}{\text{least-bandwidth}} + \text{cumulative-delay}\right) \times 256$$