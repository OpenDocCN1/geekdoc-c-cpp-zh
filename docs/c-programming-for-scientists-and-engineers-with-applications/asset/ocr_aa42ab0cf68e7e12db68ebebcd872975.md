5. Write the C code for the following:
a. The computed roots of a quadratic $ax^2 + bx + c = 0$ are given by
the formulas

```
$x_1 = \frac{-b+\sqrt{b^2-4ac}}{2a}, \quad x_2 = \frac{-b-\sqrt{b^2-4ac}}{2a}$$
```

These formulas cannot be used if the value of $a$ is 0, and the
answers are complex if the value of $b^2 - 4ac$ is negative. Print the
two real roots if they exist; otherwise print appropriate messages.

b. If the salesman of a Farm Equipment Company sells $100,000 or
more, his commission is 25%. If he sells less than $100,000, his
commission is 15%. Print the amount of sales and the commission.

c. The formula for the area of any triangle is:

```
$Area = \sqrt{s(s-a)(s-b)(s-c)}$$\nWhere $s = \frac{a+b+c}{2}$
```

Given the $a, b,$ and $c$ of a triangle, determine whether it is a
right triangle. Print the sides and the area. A triangle is a right tri-
angle if $c^2 = a^2 + b^2$ where $c$ is the longest side.

# 4.3 Repetition Structures

The repetition control structure is used to execute one or more instructions
more times. A repetition structure is also called a looping structure. There are two
types of loops: iterative loops and conditional loops. The iterative loops, which are
controlled by counting, are for loops. These call for a block of instructions to be
executed a predetermined number of times. The conditional loops, which are con-
trolled by the value of a condition, are *while* and *do while* loops. These call for
a block of instructions to be executed repeatedly, as long as the condition is true.
The looping structures may be stacked or nested depending on the complexity of the
alg. In the following sections conditional loops are presented in detail.