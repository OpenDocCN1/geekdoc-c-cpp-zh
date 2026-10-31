# Variability in CEP Architectures

The core CEP process (Figure 3-1) is always the same: Some event is sensed, it is analyzed in the context of some reference data to determine whether something of business interest has occurred, and some decision is made about what the nature of the response ought to be. Yet despite the fact that the core process is always the same, there are many different architectures for complex-event processing. Why?

There are two dominant reasons for the variability in CEP architectures: the handling of reference data and the partitioning of functionality.

# Handling Reference Data

The first area of variability centers around the relationship between the reference data and the events being analyzed: Does the stream of events alter the reference data that is used to interpret subsequent events? Applications in which the stream of events does not alter the reference data are relatively straightforward. The primary challenge in these applications is obtaining access to the reference data, which almost always originates elsewhere, and making access to the data efficient during the analysis and response activities.

On the other hand, applications in which the stream of events modifies the reference data are much more complicated. The portion of the reference data that represents the history of prior events does not have a system of record, at least without additional design. If it is unacceptable to lose this historical data when systems are shut down or fail, then the CEP solution must now include a system of record for the historical data. The system of record requires careful and clever design to ensure that it can handle the stream of data changes efficiently and robustly—and still make the data efficiently accessible to the analysis and response activities (Figure 3-2).

![](bbox=[0.28, 0.88, 0.72, 0.94])

Figure 3-1: Core CEP Process