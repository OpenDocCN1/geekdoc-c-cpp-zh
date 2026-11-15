variables. The system is ill-conditioned, or does not have a unique solution, if all the coefficients for a variable are zero or are very close to zero.

A process called pivoting can be applied to improve the accuracy of Gauss elimination. Row pivoting involves reordering the rows before performing Gauss elimination, and column pivoting involves reordering both rows and columns. These processes are discussed in the problems at the end of the chapter.

# PRACTICE!

Use the Gauss elimination numerical technique to find the solution to these sets of simultaneous linear equations:

+   1. -2x + y = -3
+      x + y = 3.
+   
+   2. 3x + 5y + 2z = 8
+      2x + 3y - z = 1
+      x - 2y - 3z = -1.

# 5.12 Problem Solving Applied: Electrical Circuit Analysis*

The analysis of an electrical circuit frequently involves finding the solution to a set of simultaneous equations. These equations are often derived using either current equations that describe the currents entering and leaving a node or using voltage equations that describe the voltages around mesh loops in the circuit. For example, consider the circuit shown in Figure 5.6. The voltages around the three loops can be described with the following equations:

```
-V1 + R1 i1 + R2(i1 - i2) = 0,
R2(i2 - i1) + R3 i2 + R4(i2 - i3) = 0,
R4(i3 - i2) + R5 i3 + V2 = 0.
```

![](bbox=[0.28, 0.68, 0.85, 0.83])

Figure 5.6 Circuit with two voltage sources.

*Optional section.