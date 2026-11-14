
```verilog
// Dataflow Level Model
// Gated SR Latch

module gsrLatch(q, qnot, sg, rg, clr, enab);
input sg, rg, clr, enab;
output q, qnot;

wire rL, sL;

wire q, qnot;

// Build the gating logic
assign rL = rg & clr & enab;
assign sL = sg & clr & enab;

// Build the basic RS latch
assign q = ~(rL | qnot);
assign qnot = ~(sL | q);

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

## A.4.3.1 ALWAYS AND INITIAL STATEMENTS

initial and always, separate flow of control At the behavioral level, a Verilog program is structured as a collection of initial and/or always blocks. Each such block expresses a separate flow of control, and each will finish execution independent of any other block. A module may define multiple initial and/or always blocks; however, such blocks cannot be nested. Beyond the input, output statements, and parameter declarations, all behavioral statements must be included in either one of these blocks.

initial block, begin, end The statements contained in an initial block (delimited by begin and end) are evaluated one time at the start of a simulation. The statements contained in an always block (delimited by begin and end) are evaluated continuously from the start of a simulation.

always, initial The always and initial statements are two of the many keywords in Verilog that allow one to set stimuli to a module. The syntax for the initial statement is given as:

```
Syntax
initial
begin
Initial statements
end
```

The syntax for the always statement is:

```
Syntax
always
begin
statements to always be executed
end
```

## A.4.3.2 Procedural Assignment

Assignment in the behavioral model differs from that in either the gate-level or dataflow model. In the behavioral model, procedural assignment statements are used to update the state circuit variables. In the dataflow model, the continuous assignment construct continually updates the value of the net on the left-hand side. In contrast, in the behavioral model, a value is only updated as the result of the execution of a procedural assignment statement.

Verilog supports two kinds of procedural assignment: blocking and nonblocking and two kinds of blocks: sequential and parallel. Statements in a sequential block, which is delimited by a begin and an end, are executed in sequence. Statements in a parallel block, which is delimited by a fork and a join, are executed in parallel.

Blocking assignment statements are executed in the order in which they are written in a sequential block. They will block the execution of subsequent statements that appear in the same sequential block; they will not block the execution of statements that appear in a parallel block. A nonblocking assignment will not block subsequent statements in a sequential block.

Put another way, a blocking assignment will successively evaluate the right-hand side and then the left-hand side of each assignment statement in a sequential block. A nonblocking assignment will evaluate all of the right-hand sides, then all of the left-hand sides of each statement in a sequential block.

The syntax for the two types of assignment is:

```
Syntax
Blocking
aVariable = aValue;
NonBlocking
aVariable <= aValue;
```

## A.4.3.3 Delays

### Syntax

```
Blocking
aVariable = #d aValue;
#d aVariable = aValue;
NonBlocking
aVariable <= #d aValue;
#d aVariable <= aValue
```

How each is interpreted can be a bit confusing.

### A.4.3.3.1 BLOCKING

The first statement says:
Evaluate aValue; then block for d time units before assigning aValue to aVariable. Any subsequent use of aVariable will get the new value.

The second statement says:
Block for d time units before evaluating aVariable = aValue. The variable aVariable will have the value aValue d time units in future.

### A.4.3.3.2 NONBLOCKING

The first statement says:
Evaluate aValue; Schedule aVariable to be updated d time units later; however, continue processing other statements. Any other variables using the value of aVariable within the next d time units will be assigned the old value.

The second statement says:
Wait d time units before evaluating aVariable = aValue. The variable aVariable will have the value aValue d time units in future.

The examples in Figures A.23 and A.25 will illustrate the behavior for each of the four cases in the same and in separate initial blocks.

### EXAMPLE A.4

From the execution of the code fragment in Figure A.23, we observe the output given in Figure A.24.

- The variables a and g from the two initial blocks change state at time 10. The variables (b and c) and (h and i) follow similarly according to their specified delays or two and four time units after a and g, respectively.
- After the blocking statements have been evaluated, the nonblocking statements are evaluated.
- The variable d is assigned the value 1, 10 time units after the blocking statements in the first initial block; the expression j <= 1 is evaluated 10 time units after the blocking statements in the second initial block.
- The variables e and f are evaluated two and four time units, respectively, after the blocking statements in the first initial block.
- Finally, the expressions k <= 1 and l <= 1 are evaluated two and four time units, respectively, after the blocking statements in the second initial block.

### EXAMPLE A.5

```
// Illustrate Procedural blocking and non-blocking assignment
// Separate initial block
module blockingNonblocking();
    //declare temp registers
    reg a,b,c,d,e,f,g,h,i,j,k,l;

    //initialize reg variables
    initial
    begin
        a = 0; b = 0; c = 0; d = 0; e = 0; f = 0;
        g = 0; h = 0; i = 0; j = 0; k = 0; l = 0;
    end

    initial
    begin // delay on right hand side
    // blocking
    a = #10 1;
    b = #2 1;
    c = #4 1;

    // non-blocking
    d <= #10 1;
    e <= #2 1;
    f <= #4 1;
    end

    // Illustrate Procedural blocking and non-blocking assignment
    // Separate initial block
    initial
    begin // delay on left hand side

    // blocking
    #10 g = 1;
    #2 h = 1;
    #4 i = 1;

    // non-blocking
    #10 j <= 1;
    #2 k <= 1;
    #4 l <= 1;
    end

    initial
    begin
    $display("time, va, vb, vc, vd, ve, vf, vg, vh, vi, vj, vk, vl");
    $monitor($time, "%b %b %b %b %b %b %b %b %b %b %b %b", a,b,c,d,e,f,g,h,i,j,k,l);
    #50 $finish(1);
    end
    endmodule
```

Figure A.23 Using Procedural Blocking and Nonblocking Assignment.

| time | a | b | c | d | e | f | g | h | i | j | k | l |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 10 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 |
| 12 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
| 16 | 1 | 1 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 0 | 0 |
| 18 | 1 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 |
| 20 | 1 | 1 | 1 | 0 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 |
| 26 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 |
| 28 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 |
| 32 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |

Figure A.24 System Output from the Module in Figure A.23.

### EXAMPLE A.6

```
// Illustrate Procedural blocking and non-blocking assignment
// Single initial block
module blockingNonblocking();
  // declare temp registers
  reg a,b,c,d,e,f,g,h,i,j,k,l;
  // initialize reg variables
  initial
    begin
    a = 0; b = 0; c = 0; d = 0; e = 0; f = 0;
    g = 0; h = 0; i = 0; j = 0; k = 0; l = 0;
    end
  initial
    begin
    // delay on right hand side
    // blocking
    a = #10 1;
    b = #2 1;
    c = #4 1;
    // non-blocking
    d = #40 1;
    e <= #2 1;
    f <= #4 1;
    // blocking left hand side
    // blocking
    #10 g = 1;
    #2 h = 1;
    #4 i = 1;
    // non-blocking
    #10 j = 1;
    #2 k <= 1;
    #4 l <= 1;
    end
  initial
    begin
    $display("Time, a, b, c, d, e, f, g, h, i, j, k, l");
    $monitor($time, " %b %b %b %b %b %b %b %b %b %b %b %b",
             a,b,c,d,e,f,g,h,i,j,k,l);
    #50 $finish(1);
    end
endmodule
```

Figure A.25 Using Procedural Blocking and Nonblocking Assignment.
