We back up to the next equation, which is the last equation in this example:

```
3x + 2y - z = 10.
```

Substituting the values already determined, we have

```
3x + 2(5) - (-6) = 10,
```

or

```
3x = -6
```

Thus, the value of x is -2.

The Gauss elimination technique thus has two parts: elimination and back substitution. First, the equations are modified such that the kth variable is eliminated in all equations following the kth equation. Then, starting with the last equation, we compute the value of the last variable. Next, using this value and the next-to-last equation, we compute the value of the next-to-last variable. This back substitution continues until we have determined the values of all the variables. The system is **ill conditioned** or does not have a unique solution if all the coefficients for a variable are zero or very close to zero.

ill conditioned
pivoting

A process called **pivoting** can be applied to improve the accuracy of Gauss elimination. Row pivoting involves reordering the rows before performing Gauss elimination, and column pivoting involves reordering the columns before performing the process. Complete pivoting involves reordering both rows and columns. These processes are discussed in the problems at the end of the chapter.

# Practice!

Use the Gauss elimination numerical technique to find the solution of the following sets of simultaneous linear equations:

+   1. -2x + y = -3
+      x + y = 3
+   
+   2. 3x + 5y + 2z = 8
+      2x + 3y - z = 1
+      x - 2y - 3z = -1

# 8.6 Problem Solving Applied: Electrical Circuit Analysis

The analysis of an electrical circuit frequently involves finding the solution of a set of simultaneous equations. These equations are often derived using either current equations that describe the currents entering and leaving a node or voltage equations that describe the voltages around mesh loops in the circuit. For example, consider the circuit shown in Figure 8.4. The equations that describe the voltages around the three loops are the following: