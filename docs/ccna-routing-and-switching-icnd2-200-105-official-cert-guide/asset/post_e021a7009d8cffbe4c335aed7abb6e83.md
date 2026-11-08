
![](img/79473ea15699e01619d2aa789f5bd43b_291_0.png)

**Figure 9-9**  _Full and Partial EIGRP Updates_

Note that EIGRP refers to the information exchanged in the updates as topology information. The information is not nearly as detailed as OSPF LS topology data, and it does not attempt to describe every router and link in the network. However, it does describe more than just a distance (metric) and vector (next-hop router) for the local router—a local router also learns the metric as used by the next-hop router. This added information is used to help EIGRP converge quickly, without causing loops, as discussed in the upcoming section “EIGRP Convergence.”

## Calculating the Best Routes for the Routing Table

EIGRP calculates the metric for routes much differently than any other routing protocol. For instance, with OSPF, anyone with a network diagram and knowledge of the configured OSPF interface costs can calculate the exact OSPF metric (cost) for each route. EIGRP uses a math equation and a composite metric, making the exact metric value hard to predict.

## The EIGRP Metric Calculation

The EIGRP composite metric means that EIGRP feeds multiple inputs (called metric components) into the math equation. By default, EIGRP feeds two metric components into the calculation: bandwidth and delay. The result of the calculation is an integer value and is the composite metric for that router.

Note that EIGRP includes other options for how it could calculate the metric, but those options are not normally used. EIGRP supports also using the interface load and interface reliability in the metric calculation. EIGRP also advertises the maximum transmission unit (MTU) associated with the route—that is, the longest IP packet allowed over the route—but does not support using the MTU when calculating the metric. For this book’s purposes, EIGRP uses the default settings, calculating the composite metric based on the bandwidth and delay.

EIGRP’s metric calculation formula actually helps describe some of the key points about the composite metric. (In real life, you seldom if ever need to sit down and calculate what a router will calculate with this formula.) The formula, assuming that the default settings that tell the router to use just bandwidth and delay, is as follows:

$$\text{Metric} = \left(\frac{10^7}{\text{least-bandwidth}} + \text{cumulative-delay}\right) \times 256$$

In this formula, the term *least-bandwidth* represents the lowest-bandwidth link in the route, using a unit of kilobits per second. For instance, if the slowest link in a route is a 10-Mbps Ethernet link, the first part of the formula is 10⁷ / 10⁴, which equals 1000. You use 10⁴ in the formula because 10 Mbps is equal to 10,000 Kbps (10⁴ Kbps).

The cumulative-delay value used in the formula is the sum of all the delay values for all outgoing interfaces along the route, with a unit of “tens of microseconds.”

Using these two inputs helps EIGRP pick the best route with a little more balance than does OSPF. Using the least bandwidth lets EIGRP avoid routes with the slowest individual links, which are usually the links with the most congestion. At the same time, the delay part of the equation adds the delay for every link, so that routing with a large number of links will be relatively less desirable than a route with fewer links.

You can set both bandwidth and delay for each link, using the cleverly named **bandwidth** and **delay** interface subcommands.

> **NOTE**  Most show commands, including *show ip eigrp topology* and *show interfaces*, list delay settings as the number of microseconds of delay. Note that the EIGRP metric formula uses a unit of tens of microseconds.

## An Example of Calculated EIGRP Metrics

Now that you have an idea of how the router’s EIGRP math works, next consider an example that connects what a router learns in an EIGRP update message, local configuration settings, and the calculation of the metric for a single route.

To calculate the metric, a local router must consider the information received from the neighboring router as well as its local interface settings. First, EIGRP update messages list the subnet number and mask, along with all the metric components: the cumulative delay, minimum bandwidth, along with the other usually unused metric components. The local router then considers the bandwidth and delay settings on the interface on which the update was received, and calculates a new metric.

For example, Figure 9-10 shows Router R1 learning about subnet 10.1.3.0/24 from Router R2. The EIGRP update message from R2 lists a minimum bandwidth of 100,000 Kbps, and a cumulative delay of 100 microseconds. R1’s S0/1 interface has an interface bandwidth set to 1544 Kbps—the default bandwidth on a serial link—and a delay of 20,000 microseconds.

![](img/79473ea15699e01619d2aa789f5bd43b_292_0.png)

**Figure 9-10**  *How R1 Calculates Its EIGRP Metric for 10.1.3.0/24*

Next, consider how R1 thinks about the least-bandwidth part of the calculation. R1 discovers that its S0/1 interface bandwidth (1544 Kbps, or 1.544 Mbps) is less than the advertised minimum bandwidth of 100,000 Kbps, or 100 Mbps. R1 needs to use this new, slower bandwidth in the metric calculation. (If R1's S0/1 interface had a bandwidth of 100,000 Kbps or more in this case, R1 would instead use the minimum bandwidth listed in the EIGRP update from R2.)

As for interface delay, the router always adds its interface delay to the delay listed in the EIGRP update. However, the unit for delay can be a bit of a challenge. The units, and their use, are as follows:

- **Unit of microseconds:** Listed in the output of show commands such as **show interfaces** and **show ip eigrp topology**, and in the EIGRP update messages
- **Unit of tens of microseconds:** Used by the interface mode configuration command (`delay`), with which to set the delay, and in the EIGRP metric calculation

Because of this weird difference in units, when looking at the delay, make sure you keep the units straight. In this particular example:

- R1 received an update that lists delay of 100 (microseconds), which R1 converts to the equivalent 10 tens of microseconds before using it in the formula.
- R1 sees its S0/1 interface setting of 20,000 microseconds, which equals 2000 tens of microseconds
- For the purposes of the calculation, R1 adds 10 tens of microseconds from the update message to 2000 tens of microseconds for the interface for a total delay of 2010 tens of microseconds.

This example results in the following metric calculation:

$$Metric = \left( \left( \frac{10^7}{1544} \right) + (10 + 2000) \right) * 256 = 2,172,416$$

> **NOTE** For those of you who repeat this math at home, IOS rounds down the division in this formula to the nearest integer before performing the rest of the formula. In this case, 10^7 / 1544 is rounded down to 6476, before adding the 2010 and then multiplying by 256.

If multiple possible routes to subnet 10.1.3.0/24 exist, Router R1 also calculates the metric for those routes and chooses the route with the best (lowest) metric to be added to the routing table.

> **NOTE** The examples in this chapter show routers with Gigabit interfaces, which default their delay settings to 10 microseconds. However, IOS adjusts the delay based on the actual speed of a LAN interface. In the examples in this chapter and the next, all the LAN interfaces happen to be running at 100 Mbps, making the delay be 100 microseconds.

## Caveats with Bandwidth on Serial Links

EIGRP's robust metric gives it the ability to choose routes that include more router hops but with faster links. However, to ensure that the right routes are chosen, engineers must

Replacing a failed route with a feasible successor takes a very short amount of time, usually less than a second or two. When queries and replies are required, convergence can take slightly longer, but in most networks, convergence can still occur in less than 10 seconds.

## Chapter Review

One key to doing well on the exams is to perform repetitive spaced review sessions. Review this chapter’s material using either the tools in the book, DVD, or interactive tools for the same material found on the book's companion website. Refer to the “Your Study Plan” element for more details. Table 9-3 outlines the key review elements and where you can find them. To better track your study progress, record when you completed these activities in the second column.

**Table 9-3**  Chapter Review Tracking

| Review Element | Review Date(s) | Resource Used |
|---|---|---|
| Review key topics |  | Book, DVD/website |
| Review key terms |  | Book, DVD/website |
| Answer DIKTA questions |  | Book, PCPT |
| Review memory tables |  | Book, DVD/website |

## Review All the Key Topics

![](img/79473ea15699e01619d2aa789f5bd43b_298_0.png)

**Table 9-4**  Key Topics for Chapter 9

| Key Topic Element | Description | Page Number |
|---|---|---|
| List | Key comparison points for EIGRP versus other routing protocols | 227 |
| List | Breakdown of the term *distance vector* | 228 |
| Figure 9-6 | Example of split horizon | 231 |
| Table 9-2 | More comparisons of IGPs | 233 |
| List | Reasons why EIGRP routers are prevented from becoming neighbors | 234 |
| Figure 9-9 | Depicts the normal progression through neighbor discovery, full routing updates, ongoing Hellos, and partial updates | 236 |
| List | Definitions of feasible distance and reported distance | 240 |
| Definition | Feasibility condition | 241 |
| Figure 9-14 | Example of how routers determine which routes are feasible successors | 242 |

## Key Terms You Should Know

convergence, distance vector, interior gateway protocol (IGP), partial update, poisoned route, split horizon, feasibility condition, feasible distance, feasible successor, full update, reported distance, successor
