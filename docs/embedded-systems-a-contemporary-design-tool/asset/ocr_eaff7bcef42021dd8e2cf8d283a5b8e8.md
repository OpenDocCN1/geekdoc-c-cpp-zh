```
// Dataflow Level Model
// Gated SR Latch

module gsrLatch(q, qnot, sg, rg, clr, enab);
input sg, rg, clr, enab;
output q, qnot;

wire rL, sL;

wire q, qnot;

// Build the gating logic
assign rL = rg & clr & enab;
assign sl = sg & clr & enab;

// Build the basic RS latch
assign q = ~(rL ~clr | qnot);
assign qnot = ~(sL 1 q);

endmodule
// Use two SR Latches in
// a master slave configuration to build a flip-flop

module srmsff(q, qnot, s, r, clk, clr);
input s, r, clk, clr;
output q, qnot;

gsrLatch master(qm, qmnot, s, r, clk, clk);
gsrLatch slave(q, qnot, qm, qmnot, clr, ~clk);
endmodule
// Build a synchronous two bit binary up counter
// using master slave SR flip-flops
module TwoBitCntr(qA, qB, clr, clk);
input clr, clk;
output qA, qB;
wire sA, rA;
wire qA, qB;
assign sA = qAnot & qB;
assign rA = qA & qB;
srmsff FFB(qB, qBnot, qBnot, qB, clk, clr);
srmsff FFA(qA, qAnot, sA, rA, clk, clr);
endmodule
```

Figure A.22 Dataflow Models of the SR Latch, Master-Slave Flip-Flop, and 2-Bit Binary up Counter.

# A.4.3.1 ALWAYS AND INITIAL STATEMENTS

initial always, separate flow of control At the behavioral level, a Verilog program is structured as a collection of initial and/or always blocks. Each such block expresses a separate flow of control, and each will finish execution independent of any other block. A module may define multiple initial and/or always blocks; however, such blocks cannot be nested. Beyond the input, output statements, and parameter declarations, all behavioral statements must be included in either one of these blocks.

initial block, begin, end The statements contained in an initial block (delimited by begin and end) are evaluated one time at the start of a simulation. The statements contained in an always block (delimited by begin and end) are evaluated continuously from the start of a simulation.