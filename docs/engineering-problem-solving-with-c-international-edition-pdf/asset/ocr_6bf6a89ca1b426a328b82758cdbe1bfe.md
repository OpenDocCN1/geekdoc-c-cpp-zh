![](bbox=[0.22, 0.09, 0.85, 0.25])

Figure 8.4 Circuit with two voltage sources.

-V_1 + R_1 i_1 + R_2(i_1 - i_2) = 0,
R_2(i_2 - i_1) + R_3 i_2 + R_4(i_2 - i_3) = 0,
R_4(i_3 - i_2) + R_5 i_3 + V_2 = 0.

If we assume that the values of the resistors ($R_1, R_2, R_3, R_4,$ and $R_5$) and the voltage sources ($V_1$ and $V_2$) are known, then the unknowns in the system of equations are the mesh currents ($i_1, i_2,$ and $i_3$). We can then rearrange the system of equations to the following form:

$(R_1 + R_2)i_1 - R_2 i_2 + 0i_3 = V_1,$
$-R_2 i_1 + (R_2 + R_3 + R_4)i_2 - R_4 i_3 = 0,$
$0i_1 - R_4 i_2 + (R_4 + R_5)i_3 = -V_2.$

Write a program that allows the user to enter the values of the five resistors and the values of the two voltage sources and store these values in a two-dimensional array. The program should then compute the three mesh currents.

# 1. PROBLEM STATEMENT

Compute the three mesh currents in the circuit shown in Figure 8.4.

# 2. INPUT/OUTPUT DESCRIPTION

The I/O diagram shows that the resistor values and the voltage values are the input values. The three mesh currents are the output values.

![](bbox=[0.23, 0.83, 0.5, 0.9])