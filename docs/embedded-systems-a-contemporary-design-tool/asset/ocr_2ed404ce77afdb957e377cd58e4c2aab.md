![](bbox=[0.28, 0.08, 0.78, 0.43])

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