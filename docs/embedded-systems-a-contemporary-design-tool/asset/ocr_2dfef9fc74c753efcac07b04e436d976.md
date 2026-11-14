(a) Reduce the equation for the circuit output to its simplest sum of form.
(b) The reduced equation in part (a) should give you three different, but logically equivalent, equations. Give the logic diagram for each. Assume a delay equal for each gate as five time units. Analyze the three circuits, commenting on and comparing the different path delays through each and the susceptibility of each to both static and dynamic hazards.

2.15 Repeat Problem 2.14, using the min-typical or typical-max delay ranges from the vendor's data sheets for the parts you are using.

2.16 The circuit fragment in Figure P2.8 implements the basic RS latch.

![](bbox=[0.18, 0.3, 0.4, 0.46])

(a) Analyze the circuit and draw a detailed timing diagram. Assume that there is a delay of five time units for each gate and that the Q output and the R and S are initially 0. Base your analysis on the following input sequence: (R,S) = (0,0), (0,1), (0,0), (1,0), and (0,0).
(b) Repeat the analysis, using the min-typical or typical-max delay ranges from the vendor's data sheets for the parts you are using.
(c) Verify your analysis using a Verilog structural model for the circuit and the vendor's data sheets.

# Digital Signals – A Dynamic View

2.17 The circuit in Figure P2.9 has been proposed for turning a level into a pulse.

![](bbox=[0.09, 0.68, 0.49, 0.78])

(a) Analyze the circuit using the min-typical or typical-max delay ranges from the vendor's data sheets for the parts you are using.
(b) What is the worst case variation on the width of the pulse based on your analysis?
(c) What are your thoughts on the design?

2.18 A junior engineer has proposed the design in Figure P2.10 for a portion of a circuit she is working on. She has said the design works perfectly, but asks that you to review it anyway. She gives you the information shown in the figure from the vendor's data sheet.

![](bbox=[0.58, 0.17, 0.82, 0.28])

```
t_pdHL = 10ns // Propagation delay from a high input to a low output
t_pdLH = 15ns // Propagation delay from low input to a high output
```

(a) Using the information from the data sheets, complete the timing diagram in Figure P2.11 for the identified signals based on the conditions shown.

![](bbox=[0.58, 0.42, 0.82, 0.6])

Assume each square is 10 ns.
(b) Based on your analysis, what can you tell her about the design?

2.19 For the circuit in Figure P2.12:

![](bbox=[0.51, 0.69, 0.91, 0.89])