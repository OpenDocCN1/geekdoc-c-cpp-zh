```
Syntax
assign destination net = source net expression
```

The left-hand side of the continuous assignment must be either a scalar or vector (multiple lines) net. The right-hand side of the expression can be a net, register, or function call return and must be of the same size as the left-hand side. A scalar cannot be assigned to a vector and vice versa, for example.

A continuous assignment is always active. A change on the right-hand side forces evaluation of the left-hand side, with the resulting assignment of the right-hand side value to the left-hand side net.

# A.4.2.1.1 COMBINATIONAL LOGIC

We illustrate a combinational dataflow model using the AndOr circuit designed earlier. That model, using the continuous assignment, is expressed in Figure A.17.

```
// continuous assignment
module AndOr(AandB, AorB, A, B);
output AandB, AorB;
input A, B;

wire AandB, AorB;
parameter delay0 = 10;

assign AandB = A&B;
assign AorB = A|B;
endmodule
```

Figure A.17 A Combinational Logic Module using a Dataflow Verilog Model.

The implementation of the function using the bitwise AND and OR operators should be familiar from earlier work with their C counterparts.

# A.4.2.2 Delays

Moving up one level of abstraction from the gate level does not preclude the need to model real-world effects on circuit behavior. The Verilog model for delay at the dataflow level follows naturally from that at the gate level.

The syntax is given as:

```
Syntax
assign #delay net
```

# EXAMPLE A.2

The model for the AndOr circuit designed earlier can include delays as seen in Figure A.18.