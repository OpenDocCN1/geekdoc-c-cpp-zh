![](bbox=[0.362, 0.119, 0.671, 0.357])

# FIGURE 25.16

CView waterfall graph axis.

As an example of what waterfall plots may look like for a sample NWChem run, Figure 25.17 shows multiple waterfall graphs depicting CPU utilizations across two Intel Xeon Phi processors, and one Intel Xeon processor.

The two graphs on the left represent CPU use by the two processors installed in the system. On the left side of each graph, a color-map line shows a legend for the scale. In this graph, the number of jiffies is used. A jiffy in Linux terms is the amount of time in one tick; on most Linux systems there are 100 ticks per second, each jiffy counted falls into one of many buckets, such as system time, user time, idle time, etc.

The bottom right chart represents power consumption, as reported by IPMI, on the host server. The red color indicates when the server reached 1500 W consumption.

The upper right chart represents the CPU consumption on the Intel Xeon processor-based host measured in jiffies.

The data represented in the visualization charts that follow was collected and supplied by the Pacific Northwest National Laboratory (PNNL).

The following are additional data representations showing what can be done when NWPerf and CView are combined, as described in the aforementioned steps. Figure 25.18 shows poor CPU usage across a set of nodes resulting from memory bandwidth issues (will show as cooler colors on a color chart and darker shades on a gray scale chart).

Similarly, you can represent power, CPU, and memory consumption, down to the coprocessor level for each individual node, as seen in the following two figures (Figures 25.19 and 25.20).

These waterfall graphs can be quickly created to compare different metrics simultaneously.

In our experience, the mere act of showing waterfall graphs to users has proven beneficial because they can now see when their jobs are running and what they are doing and can take charge of addressing inefficiencies in their software. Administrators can also monitor these waterfall graphs for behavior changes: in one instance, we found jobs that collectively were not using systems to their fullest extent because of a global synchronization issue; in another case, we found recurrent jobs were taking longer than usual to complete and root-caused the problem to a compile-time issue. The waterfall graphs