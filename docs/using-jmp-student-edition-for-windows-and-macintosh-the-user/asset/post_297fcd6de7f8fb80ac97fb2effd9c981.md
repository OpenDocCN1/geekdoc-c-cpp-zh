
Figure 7.14 Individual Measurement and Moving Range Charts for Pickles Data

![](img/a858f3b35ed4923af65c22e8829ee5a8_129_0.png)

Note: If you choose a Median Moving range chart, the limits on the Individuals chart use the Median Moving Range as the sigma, rather than the Average Moving Range.

## Shewhart Control Charts for Attributes

In the previous types of charts, measurement data was the process variable. This data is often continuous, and the charts are based on continuous theory. Another type of data is count data, where the variable of interest is a discrete count of the number of defects or blemishes per subgroup. For discrete count data, attribute charts are applicable, as they are based on binomial and poisson models. Since the counts are measured per subgroup, it is important when comparing charts to determine whether you have similar number of items in the subgroups between the charts. Attribute charts, like variables charts, are classified according to the subgroup sample statistic plotted on the chart:

## Table 7.4 Determining which Attribute Chart to use

| Each item is judged as either conforming or non-conforming | For each item, the number of defects is counted |
| The subgroups are a constant size | The subgroups vary in size | The subgroups are a constant size | The subgroups vary in size |
| *np*-chart | *p*-chart | *c*-Chart | *u*-chart |

- p-charts display the proportion of nonconforming (defective) items in subgroup samples which can vary in size. Since each subgroup for a p-chart consists of N items, and an item is judged as either conforming or nonconforming, the maximum number of nonconforming items in a subgroup is N.
- np-charts display the number of nonconforming (defective) items in constant sized subgroup samples. Since each subgroup for an np-chart consists of Ni items, and an item is judged as either conforming or nonconforming, the maximum number of nonconforming items in subgroup i is Ni.
- c-charts display the number of nonconformities (defects) in a subgroup sample that usually consists of one inspection unit.
- u-charts display the number of nonconformities (defects) per unit in subgroup samples that can have a varying number of inspection units.

## p- and np-Charts

### Example. np-Charts

The Washers.jmp data in the Quality Control sample data folder contains defect counts of 15 lots of 400 galvanized washers. The washers were inspected for finish defects such as rough galvanization and exposed steel. If a washer contained a finish defect, it was deemed nonconforming or defective. Thus, the defect count represents how many washers were defective for each lot of size 400. To replicate this example, follow these steps:

- Choose the Graph > Control Chart > NP command.
- Choose # defects as the Process variable.
- Change the Constant Size to 400.
- Click OK.

The example here illustrates an np-chart for the number of defects.

Figure 7.15 np-Chart

![](img/a858f3b35ed4923af65c22e8829ee5a8_130_0.png)

### Example. p-Charts

Again, using the Washers.jmp data, we can specify a sample size variable, which would allow for varying sample sizes.

Note: This data contains all constant sample sizes. Follow these steps or submit the JSL script below:

- Choose the Graph > Control Chart > P command.
- Choose Lot as the Sample Label variable.
- Choose # defects as the Process variable.
- Choose Lot Size as the Sample Size variable.
- Click OK.

The chart shown here illustrates a p-chart for the proportion of defects.

Figure 7.16 p-Chart

![](img/a858f3b35ed4923af65c22e8829ee5a8_131_0.png)

Note that although the points on the chart look the same as the np-chart, the y-axis, Avg and limits are all different since they are now based on proportions

## u-Charts

The Braces.jmp data in the Quality Control sample data folder records the defect count in boxes of automobile support braces. A box of braces is one inspection unit. The number of boxes inspected (per day) is the subgroup sample size, which can vary. The u-chart, shown here, is monitoring the number of brace defects per subgroup sample size. The upper and lower bounds vary according to the number of units inspected.

Note: When you generate a u-chart, and select Capability, JMP-SE launches the Poisson Fit in Distribution and gives a Poisson-specific capability analysis.

- Click OK.

Figure 7.18 c-Chart

![](img/a858f3b35ed4923af65c22e8829ee5a8_133_0.png)

## Phases

A phase is a group of consecutive observations in the data table. For example, phases might correspond to time periods during which a new process is brought into production and then put through successive changes. Phases generate, for each level of the specified Phase variable, a new sigma, set of limits, zones, and resulting tests.

On the dialog for X̄-, r-, s-, IR-, p-, np-, c-, u-, Presummarized, and Levey-Jennings charts, a Phase variable button appears. If a phase variable is specified, the phase variable is examined, row by row, to identify to which phase each row belongs.

Saving to a limits file reveals the sigma and specific limits calculated for each phase.

### Example

Open Diameter.JMP, found in the Quality Control sample data folder. This data set contains the diameters taken for each day, both with the first prototype (phase 1) and the second prototype (phase 2).

- Select Graph > Control Chart > XBar.
- Choose DIAMETER as the Process, DAY as the Sample Label, and Phase as the Phase.
- Click OK.

Figure 7.19 Launch Dialog for Phases

![](img/a858f3b35ed4923af65c22e8829ee5a8_134_0.png)

The resulting chart has different limits for each phase

Figure 7.20 Phase Control Chart

![](img/a858f3b35ed4923af65c22e8829ee5a8_134_1.png)

Note: The sigma was calculated using the standard deviation.

## Cumulative Sum (Cusum) Charts

Cumulative Sum (Cusum) charts display cumulative sums of subgroup or individual measurements from a target value. Cusum charts are graphical and analytical tools for deciding whether a process is in a state of statistical control and for detecting a shift in the process mean.

JMP cusum charts can be one-sided, which detect a shift in one direction from a specified target mean, or two-sided to detect a shift in either direction. Both charts can be specified in terms of geometric parameters (h and k described in Figure 7.21); two-sided charts allow specification in terms of error probabilities α and β.

To interpret a two-sided Cusum chart, you compare the points with limits that compose a V-mask. A V-mask is formed by plotting V-shaped limits. The origin of a V-mask is the most recently plotted point, and the arms extended backward on the x-axis, as in Figure 7.21. As data are collected, the cumulative sum sequence is updated and the origin is relocated at the newest point.

Figure 7.21 Illustration of a V-Mask for a Two-Sided Cusum Chart

![](img/a858f3b35ed4923af65c22e8829ee5a8_135_0.png)

Shifts in the process mean are visually easy to detect on a cusum chart because they produce a change in the slope of the plotted points. The point where the slope changes is the point where the shift occurs. A condition is out-of-control if one or more of the points previously plotted crosses the upper or lower arm of the V-mask. Points crossing the lower arm signal an increasing process mean, and points crossing the upper arm signal a downward shift.

There are major differences between cusum charts and other control (Shewhart) charts:

- A Shewhart control chart plots points based on information from a single subgroup sample. In cusum charts, each point is based on information from all samples taken up to and including the current subgroup.
- On a Shewhart control chart, horizontal control limits define whether a point signals an out-of-control condition. On a cusum chart, the limits can be either in the form of a V-mask or a horizontal decision interval.
