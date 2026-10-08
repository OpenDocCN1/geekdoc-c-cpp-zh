
# 2. Write code for the following selection structure flowchart.

![](img/8356e6c3bfe3b10354682c60b1e74b1d_235_0.png)

+ 3. Write the flowcharts and the code for the selection structures for the following statements:
a. If $x$ is greater than 25, add 20 to $y$.
b. If $z$ is less than 15, add $x$ to $y$.
c. If $p$ is 40, input values to $l$, $m$, and $r$.
d. If $p$ is greater than or equal to $r$, increment $r$ by 1.

4. Write the segment of C for the following:
a. If the compression stress is greater than 50,000, execute the following code.
```c
printf("stress = %d\n", stress);
printf("This stress is greater 50000\n", stress);
```
b. If the number of cars sold per month by XYZ Motor Company is greater than 10,000, add a 5% bonus to employees' monthly paychecks.
c. If the monthly sales of an employee exceeds $50,000, award a 10% bonus, if it exceeds $100,000 award a 15% bonus, if it exceeds $150,000, award a 20% bonus. If it is less than $10,000 there will be no bonus.

5. Write the C code for the following:
a. The computed roots of a quadratic $ax^2 + bx + c = 0$ are given by the formulas
```
$x_1 = \frac{-b+\sqrt{b^2-4ac}}{2a}, \quad x_2 = \frac{-b-\sqrt{b^2-4ac}}{2a}$
```
These formulas cannot be used if the value of $a$ is 0, and the answers are complex if the value of $b^2 - 4ac$ is negative. Print the two real roots if they exist; otherwise print appropriate messages.

b. If the salesman of a Farm Equipment Company sells $100,000 or more, his commission is 25%. If he sells less than $100,000, his commission is 15%. Print the amount of sales and the commission.

c. The formula for the area of any triangle is:
```
$Area = \sqrt{s(s-a)(s-b)(s-c)}$
Where $s = \frac{a+b+c}{2}$
```
Given the $a, b,$ and $c$ of a triangle, determine whether it is a right triangle. Print the sides and the area. A triangle is a right triangle if $c^2 = a^2 + b^2$ where $c$ is the longest side.

# 4.3 Repetition Structures

The repetition control structure is used to execute one or more instructions more times. A repetition structure is also called a looping structure. There are two types of loops: iterative loops and conditional loops. The iterative loops, which are controlled by counting, are for loops. These call for a block of instructions to be executed a predetermined number of times. The conditional loops, which are controlled by the value of a condition, are *while* and *do while* loops. These call for a block of instructions to be executed repeatedly, as long as the condition is true. The looping structures may be stacked or nested depending on the complexity of the algorithm. In the following sections conditional loops are presented in detail.

# 218 Control Structures

![](img/8356e6c3bfe3b10354682c60b1e74b1d_237_0.png)
Figure 4.8 Flowchart of a for loop

# 4.3.1 Iterative Loops

Iterative loops, also called counting loops, use the keyword for in in C. These loop control structures are used to control processing of a known number of data values, to assign index numbers to data or output, or to generate a set of equally spaced numbers.

The flowchart shown in Figure 4.8 might control the numbering of five lines or five pages of output. Or it might control the processing of five data values.

In C, the initialization of the count is retested, the testing of the count, and the increment of the count before it is retested, are all part of the loop header. The C form of this for loop is
```c
for(i = 1; i < 6; i++)
```
for is the keyword and i is the loop control variable. The first item specified inside the parentheses i = 1 initializes the loop variable i to a value, the second item i < 6 is a relational expression to control the execution of the loop, as long as the condition is true the loop will continue to execute. The last item i++ increments the loop variable. In the case of a for loop the initialization, relational condition, and the increment of the loop variable are done in one statement. Figure 4.8 shows the flowchart for the loop.

The code corresponding to the flowchart in Figure 4.8 is as follows:
```c
for(i = 1; i < 6; i++)
{
    funcall();
    printf("i = %d\n", i);
}
printf("i = %d\n", i);
```
The output is as follows:
- i = 1
i = 2
i = 3
i = 4
i = 5
i = 6

When the value of i is 6 the loop terminates without printing the value of 6. It is printed by the output statement following the loop. This is an increment loop where the loop variable i is incremented until the loop terminates. But the loop can be a decrement loop where the loop variable is decremented. The following example shows a decrement for loop.
```c
for(i = 4; i >= 0; i--)
{
    funcall();
    printf("i = %d\n", i);
}
printf("i = %d\n", i);
```
The output is as follows:
- i = 4
i = 3
i = 2
i = 1
i = 0
i = -1

# 4.3.2 Nested Loops

The for loops may be nested. For example, the nesting of for is shown in 4.9.
![](img/8356e6c3bfe3b10354682c60b1e74b1d_239_0.png)
Figure 4.9 Flowchart of nested loops

```c
for(i = 0; i < 3; i++)
{
    for(j = 0; j < 3; j++)
    {
        funcall();
        printf("i = %d, j = %d\n", i, j);
    }
}
```
The output is as follows:
- i = 0, j = 0
i = 0, j = 1
i = 0, j = 2
i = 1, j = 0
i = 1, j = 1
i = 1, j = 2
i = 2, j = 0
i = 2, j = 1
i = 2, j = 2

Notice that the inner loop is executed completely for each iteration of the outer loop. The inner loop variable j is distinct from the outer variable i.

# 222 Control Structures

![](img/8356e6c3bfe3b10354682c60b1e74b1d_241_0.png)

# 4.3.3 Conditional Loops

Conditional loops are loops controlled by an event. It may be a flag indicating the end of the input, a value indicating that an approximation is sufficient, the finding of a specific data, or an internal variable reaching a limit. Whatever variable is being tested for the termination condition must have an initial value. The keyword while implies that processing is to continue and the termination condition has not been met.

The following code corresponds to the flowchart of the conditional structure shown in 4.11. Notice that the entry to the structure is at the top and the exit is at the bottom.
```c
float r, a;
const float PI = 3.14159;

scanf("%f", &r);
while(r != 0) {
    a = PI * r * r;
    printf("radius = %f, area = %f\n", r, a);
    scanf("%f", &r);
}
```
