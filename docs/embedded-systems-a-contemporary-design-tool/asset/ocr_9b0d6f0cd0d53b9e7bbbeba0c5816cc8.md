# 3.7.2 Flip-Flops

**setup time hold time** The diagram in Figure 3.39 graphically illustrates the _setup_ and _hold time_ relationships for a positive edge-triggered flip-flop. The specification for the times is given at the 50% point of each signal.

![](bbox=[0.28, 0.18, 0.58, 0.28])

**Figure 3.39** Setup and Hold Times for a Positive Edge Triggered Flip-Flop

The need for and consequences of violating the setup and hold time constraints in the flip-flop are the same as those for the gated latch.

# 3.7.3 Propagation Delays

**minimum, typical maximum, causative edge** In combinational circuits, propagation delay specifies the interval following a change in state of an input signal to the device and the effect of that change appearing on the output of the device. Such an interval is characterized by _minimum_, _typical_, and _maximum_ values. In flip-flops, the measurement is made with respect to the causative edge of the clock.

The timing diagram in Figure 3.40 illustrates the minimum and maximum clock to Q output propagation delays for a low to high and a high to low transition on the flip-flop output.

![](bbox=[0.28, 0.56, 0.75, 0.7])

**Figure 3.40** Clock to Q Propagation Delays for a Positive Edge Triggered Flip-Flop

As with combinational logic, the delays are measured at the 50% point, between the causative and consequent edges of the signals; the two delays are generally not symmetric.

**Gate** The propagation delay specification for latches is slightly more complex. In addition to the delay from the causative edge (or level) of the gate, latch transparency requires that the delay from input to output when the _Gate_ is enabled be specified as well.