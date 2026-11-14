
## rate multiplier

A scheme to select a fractional portion of a clock signal is called a rate multiplier. The block diagram for such a circuit is given in Figure 3.45.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_199_0.png)

A rate multiplier is simply a combinational logic block combined with an N-bit counter. The period of the counter will be 2^n, that is, the counter will cycle through all of its states every 2^n clock pulses. The N-bit selector also permits 2^n combinations. For each of the 2^n combinations on the selector input, the device will output that many pulses. Thus, if N is 4, the counter will be 4 bits and there will be 4 selector lines. If the counter is a binary counter, and the selector pattern is 0101, binary 5, then for every 16 clock pulses coming into the counter, there will be 5 output pulses. The output frequency will be 5/16 of the input frequency. The design of the rate multiplier is such that the selected number of output pulses is evenly distributed across the period of the clock, as illustrated in the timing diagram in Figure 3.46 for a selector pattern of binary 5.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_199_1.png)

If one is using a high-frequency oscillator as the primary clock source in a design but a portion of the application requires a significantly lower frequency, a ripple counter can provide a very effective means of developing such a signal. Twelve- to fourteen-stage ripple counters are commonly found as a single MSI part. By using such a counter, one can easily divide the high-frequency source by as much as 16 K. When doing so, however, one must be aware that there will be a substantial skew between the edge of the input signal and the resulting edge of any of the lower frequency signals coming out of the counter because of the ripple delay through the device. The application of such a divider is illustrated in the logic diagram in Figure 3.47. The effect of edge skew is reflected in the subsequent timing diagram in Figure 3.47 for an asynchronous binary up counter.

The timing diagram illustrates the propagation delay for the first four stages as the counter changes from a count of binary 7 to binary 8. Observe that the interstage delay accumulates as subsequent flip-flops change state. In this example, the change in state of the third stage is delayed by four propagation delays following the causative event in the first stage. It doesn't take too much imagination to visualize the situation in which the least significant stage may have changed states twice before the nth stage is able to change.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_200_0.png)

Figure 3.47 Timing Diagram Illustrating the Accumulation of Delays in an Asynchronous Ripple Counter

### 3.8.1.2 Precision and Stability

The simplest kinds of clock sources use resistor and capacitor combinations to set their output frequency. Although such devices may be perfectly reasonable for controlling windshield wipers or a door bell, they should never be used in critical hard real-time applications. Capacitors have wide tolerances and are subject to humidity, brownout, or low-voltage levels, as well as a number of environmental effects.

Crystal-based sources are generally the best solution for stable and accurate timing signals. When using such devices, one can start either with the basic crystal and then design the analog electronics necessary to implement the desired oscillator or buy a prepackaged oscillator. Each crystal or oscillator has different stability and accuracy specifications. If the application demands greater accuracy and stability than are available with standard devices, the next step is to use temperature-compensated designs. Such sources utilize a small heater to minimize the effects of temperature variation of the oscillator.

## 3.8.2 Designing a Clock System

### 3.8.2.1 Single-Phase Clocks

A single-phase clock should start with the crystal oscillator. Such an approach gives stability and repeatability to any clocking and timing that need to be in the embedded application. Variations on the circuit in Figure 3.48 should never be used.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_200_1.png)

Figure 3.48 A Simple Clock Generator

The design is trying to do a digital job with analog parts. Adding the R and C as shown can significantly affect the rise and fall times of the input signals to the buffer. As the transition times increase, so does the probability of the circuit becoming metastable.

### 3.8.2.2 Multiple-Phase Clocks

Contemporary digital systems frequently require more precise resolution in time than can be achieved with a single-phase clock. Consider the basic clock waveform in Figure 3.49.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_201_0.png)

A decision can be made in four places within a single clock period:

- 1. The rising edge
- 2. The falling edge
- 3. The high level
- 4. The low level

One cannot tell the difference in time between the edge at 1a and that at 1b. The best resolution we have is a half period.

The simplest multiple-phase clock generator is given in Figure 3.50. The circuit generates two nonoverlapping clock signals as output. The structural Verilog model for the clock generator is given in the code module in Figure 3.51.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_201_1.png)

```
module ClockTwoPhase(phase2, phase1, clk, por);
// declare inputs and outputs
input clk, por;
output phase2, phase1;

reg pullUp;
initial
pullUp = 1;

// build clock
not inv0(nclk, clk);
DFF f0(qF0, qBarF0, nclk, pullUp, por);
and andP1(phase1, qBarF0, qF0, clk);
and andP2(phase2, qBarF0, clk);
endmodule
```

Figure 3.51 A Structural Verilog Code Module for the Two-Phase Clock Generator

The timing diagram for the generator is given in Figure 3.52.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_202_0.png)

Figure 3.52 Timing Diagram for the Two-Phase Clock Generator

We can now see that over a two clock-cycle interval, we have eight different places that a logical decision can be made. Furthermore, the edge at t0 is distinguishable from the edge at t1; the same holds true for the remaining edges and levels along the two phases.

Using such a scheme, we can now use P2 as a causative edge and P1 as a sampling edge for example. P2 will affect an event or state change. The interval between P2 and P1 should be sufficient for all changing and propagating signals to settle before they are acted upon by the logic clocked by P1.

Although the circuit contains a race as illustrated in the logic diagram in Figure 3.53, the race is biased toward path2 so that there can never be a decoding spike on either of the two AND gates generating P1 and P2.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_202_1.png)

Figure 3.53 Critical Timing Paths in the Two-Phase Clock Generator

Another effective and flexible way to produce a multiple-clock phase time base is to use a Johnson counter. The two-stage counter is repeated and extended in the logic diagram shown in Figure 3.54. By decoding each of the four states in the counting sequence, we can generate four different phased clocks as we see in the figure.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_203_0.png)

Figure 3.54 Logic Diagram of a Four-Phase Clock Generator Using a Johnson Counter

The structural Verilog model follows in Figure 3.55.

```
module ClockFourPhase(phase4, phase3, phase2, phase1, clk, por);
// declare inputs and outputs
input clk, por;
output phase4, phase3, phase2, phase1;

reg pullUp;

initial
pullUp = 1;
// build clock
not n0(nclk, clk);
DFF f0(qF0, qBarF0, qBarF1, nclk, pullUp, por);
DFF f1(qF1, qBarF1, qF0, nclk, pullUp, por);

// build the four phases
and p0(phase1, qBarF0, qBarF1);
and p1(phase2, qF0, qBarF1);
and p2(phase3, qF0, qF1);
and p3(phase4, qBarF0, qF1);
endmodule
```

Figure 3.55 Structural Verilog Code Module for a Four-Phase Clock Generator Using a Johnson Counter

The timing diagram in Figure 3.56 illustrates the four different clock phases.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_204_0.png)

Figure 3.56 Timing Diagram for a Four-Phase Clock Generator Using a Johnson Counter

By incorporating additional phases, we have increased our control over the placement or sampling of events in time.

### 3.8.2.3 More Than Four Phases

Expanding the time base beyond four phases, we can continue to build on the Johnson counter. If such a design is utilized, the disconnected subgraph for each case will have to be managed. An alternative approach is to utilize a delay-based scheme such as a tapped delay line. The advantage of such an approach is that one can use a lower frequency clock. The Johnson counter used in the previous design requires a base clock that has a frequency that is four times the frequency of the phases.

### 3.8.2.4 Multiple Clocks Versus Multiple Phases

The major advantage of multiple phases when compared to multiple clocks is that all phases are derived from the same fundamental frequency. Clock noise can be filtered out much more easily. With multiple clocks, although all may be using the same frequency, they are all running asynchronous to each other.

### 3.8.2.5 Gating the Clock

The general rule of thumb is that gating the clock should never be done because of the high potential for hazards. If gating becomes essential, one should thoroughly understand the timing and change the control logic only when the clock in such a state that it cannot result in a change on the gate output. An example is the two-phase clock discussed earlier.

## 3.9 TESTING SEQUENTIAL CIRCUITS

Testing sequential circuits is much more complex than testing combinational circuitry. Sequential machines have memory; their behavior is determined by the values and the order in which the input signals occur. Combinational circuits can be tested very
