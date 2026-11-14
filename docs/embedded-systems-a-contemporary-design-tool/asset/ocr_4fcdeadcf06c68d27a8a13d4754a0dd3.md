The outputs of the system will now change 10 time units after either of the input signals changes and reflect the rise and fall times as well, as illustrated in Figure A.21.

| Time, | A, | B, | AandB, | AorB |
|---|---|---|---|---|
| 0 | 1, | 1, | x, | x |
| 5 | 1, | 1, | 1, | 1 |
| 10 | 0, | 1, | 1, | 1 |
| 17 | 0, | 1, | 0, | 1 |
| 20 | 0, | 0, | 0, | 1 |
| 30 | 0, | 1, | 0, | 0 |

Figure A.21 System Output from the Circuit Module in Figure A.20.

# A.4.2.3 Operators

The syntax and operators used in Verilog at the dataflow level follow that of the C language very closely. Table A.2 gives the most commonly used operators.

| Operator | Symbol | Operation | Operator | Symbol | Operation |
|---|---|---|---|---|---|
| Arithmetic | + | Add | Equality | == | Equal |
| | - | Subtract | | != | Not equal |
| | / | Divide | Logical | ! | Logical negation |
| | * | Multiply | | && | Logical AND |
| | % | Modulus | | || | Logical OR |
| Relational | > | Greater than | Bitwise | ~ | Bitwise negation |
| | < | Less than | | & | Bitwise AND |
| | >= | Greater than or Equal | | | Bitwise OR |
| | <= | Less than or Equal | Shift | << | Shift left |
| | | | | >> | Shift right |

# A.4.2.3.1 SEQUENTIAL LOGIC

The following three code modules in Figure A.22 evolve the dataflow implementations of the gated SR latch, the master-slave SR flip-flop, and the 2-bit binary counter designed earlier at the gate level.

# A.4.3 The Behavioral Model

The behavioral model increases the design abstraction by an additional level. Our thinking about the design now moves above considerations of the flow of data within the system to the algorithms that express the behavior of the system. At the behavioral level, the model begins to take on more of the guise of a C or C++ program than a digital circuit. Flow of control through the system is expressed in the familiar looping and branching constructs rather than in logic gates.

# A.4.3.1 Program Structure

At the behavioral level, one of the major differences between languages such as C or C++ becomes clear. Unlike either C or C++, in which flow of control is generally sequential, flow of control in Verilog is concurrent. Statements in C or C++ execute in series; those in Verilog execute in parallel.

sequential concurrent