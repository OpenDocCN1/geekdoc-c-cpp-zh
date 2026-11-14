The timing diagram in Figure 3.56 illustrates the four different clock phases.

![](bbox=[0.27, 0.11, 0.82, 0.35])

# Figure 3.56 Timing Diagram for a Four-Phase Clock Generator Using a Johnson Counter

By incorporating additional phases, we have increased our control over the placement or sampling of events in time.

# 3.8.2.3 More Than Four Phases

Expanding the time base beyond four phases, we can continue to build on the Johnson counter. If such a design is utilized, the disconnected subgraph for each case will have to be managed. An alternative approach is to utilize a delay-based scheme such as a tapped delay line. The advantage of such an approach is that one can use a lower frequency clock. The Johnson counter used in the previous design requires a base clock that has a frequency that is four times the frequency of the phases.

# 3.8.2.4 Multiple Clocks Versus Multiple Phases

The major advantage of multiple phases when compared to multiple clocks is that all phases are derived from the same fundamental frequency. Clock noise can be filtered out much more easily. With multiple clocks, although all may be using the same frequency, they are all running asynchronous to each other.

# 3.8.2.5 Gating the Clock

The general rule of thumb is that gating the clock should never be done because of the high potential for hazards. If gating becomes essential, one should thoroughly understand the timing and change the control logic only when the clock in such a state that it cannot result in a change on the gate output. An example is the two-phase clock discussed earlier.

# 3.9 TESTING SEQUENTIAL CIRCUITS

Testing sequential circuits is much more complex than testing combinational circuitry. Sequential machines have memory; their behavior is determined by the values and the order in which the input signals occur. Combinational circuits can be tested very