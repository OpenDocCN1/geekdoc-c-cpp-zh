# 90 Problem Solving C++

```
char cn1 = 'P', cn2 = 'E', cn3 = 'R', cn4 = 'F', cn5 = 'E';
char cn6 = 'C', cn7 = 'T', key = '\\', sch = '\\', inc = 'A';
char incl1 = 'T';
```

b. Repeat Exercise 10a, but substitute the active pattern by a computer ASCII code would use store characters in each of the declared variables. (Hint: Use Table 2.3.)

11. (Practice) Using Figure 2.14 and assuming the variable name miles is assigned to byte by memory address 159, determine the addresses corresponding to each variable in the following statements:

```
float miles;
int count, num;
double dist, temp;
```

# 2.6 Case Study: Radar Speed Traps

In this section, the software development procedure explained in Section 1.3 is applied to a specific programming problem. Although each problem you explore in the case studies in Part One is different, you'll see that this software development procedure works for all of them to produce a complete program. It forms the foundation for all programs developed in Part One of this book.
A highway speed detection radar emits microwaves at a frequency designated as $f_c$. The beam is reflected off an approaching car, and the radar picks up and analyzes the reflected beam, $f_r$. The reflected beam's frequency is shifted slightly from $f_c$ to $f_r$ because of the car's motion. The relationship between the speed of the car, $v$, in miles per hour (mph), and the two microwaves is

```
v = (6685 \times 10^8) \frac{f_r - f_c}{f_r} mph
```

where the emitted waves have a frequency of $f_c = 2 	imes 10^{10}$ sec$^{-1}$. Using the given formula, you'll write a C++ program, using the software development procedure, to calculate and display the speed corresponding to a received frequency of $2.000004 	imes 10^{10}$ sec$^{-1}$.

# Step 1 Analyze the Problem

For this problem, a single output is required: the speed of the car. The input items required to solve for the speed is the emitted frequency, $f_c$, and the received frequency, $f_r$.

# Step 2 Develop a Solution

The algorithm for transforming the three input items into the required output item is by the formula $v = 6.685 	imes 10^8 (f_r - f_c) / (f_r + f_c)$. Therefore, the complete algorithm for the program solution is as follows:

+   Assign values to f_c and f_r
Calculate the speed using the formula $v = 6.685 	imes 10^8 (f_r - f_c) / (f_r + f_c)$
Display the speed