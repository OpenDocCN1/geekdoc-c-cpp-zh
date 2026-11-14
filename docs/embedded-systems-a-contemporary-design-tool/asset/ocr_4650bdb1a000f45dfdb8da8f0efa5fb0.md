From the execution of the code fragment in Figure A.25, the results are given in Figure A.26.

| time | a | b | c | d | e | f | g | h | i | j | k | l |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 10 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 12 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 16 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 18 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 20 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| 26 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |
| 28 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 |
| 32 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 |
| 42 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 0 |
| 44 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 0 |
| 48 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |

Figure A.26 System Output from the Module in Figure A.25.

The major differences between the two implementations are reflected in the evaluation times for the variables d, e, f, g, h, and i.

# A.4.3.3.3 COMBINATIONAL LOGIC

The next example, in Figure A.27, implements the earlier NandNor combinational logic circuit using a behavioral model and utilizing both the blocking and nonblocking assignments with the right- and left-hand side delays.

```
module blocking_nonblocking();
reg b, AandB, AorB, AandNAndB, AorNAndB;
reg e, f, EnforEf; EnforEf; EnforEf;
// Blocking Assignment
initial
begin
t = b = 1;
// Delay on the right hand side
AandB = #10 a & b;
// Delay on the left hand side
#10 Delay = a & b;
#10 AorB = a|b;
#11 AandNAndB = ~AorB;
end
// Non-Blocking Assignment
initial
begin
e = t = 1;
// Delay on the right hand side
// Delay on the left hand side
EnforEf <= #11 e&f;
// Delay on the left hand side
#12 EforF <= e~f;
#13 EorF <= e~f;
end
initial
begin
$display("t time a b, \tAandB, \tAorB, \tAandNAndB, \tW, \tEnforEf, \tEforF");
$monitor(Sime, " (%b) (%b) (%b) (%b) (%b) (%b) (%b) (%b) (%b) (%b) (%b) (%b)", a, b, AandB, AorB, AandNAndB, AorNAndB, e, f, EnforEf, EforF, EorF);
#50 $finish(1);
end
endmodule
```

Figure A.27 A Combinational Logic Module using a Behavioral Verilog Model with Blocking and Nonblocking Assignment.