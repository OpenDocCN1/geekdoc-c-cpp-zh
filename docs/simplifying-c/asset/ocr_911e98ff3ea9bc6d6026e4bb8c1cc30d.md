```
for ( [Expression 1] ; [ Expression 2] ; [Expression 3] )
Action Block;
```

In the preceding syntax, it can be seen that the three expressions are separated by semicolons. Expression1 is an initialization statement of loop counter, Expression2 is a test condition statement that controls the loop, and Expression 3 is the statement that updates the loop counter. The action block contains single or compound statements that are to be repeated. Note that all the three expressions mentioned in the preceding syntax are optional, and hence shown enclosed within square brackets. Figure 4 illustrates the logical flow of the for loop:

![](bbox=[0.37, 0.3, 0.71, 0.58])

It can be seen in Figure 4 that Expression 1 is first evaluated, and it will be evaluated only once. Next, we evaluate Expression 2. If Expression 2 is evaluated to true, we step into the action block. If Expression 2 is evaluated to false, the loop terminates. After executing action block, we evaluate Expression 3. The process of evaluating Expression 2, executing action block, and evaluating Expression 3 becomes a cyclic process till Expression 2 is evaluated to false. Program 1 illustrates the use of for loop:

# Program 1

```
/* Program to calculate the sum of numbers 1 to 10 using the for loop */
#include <stdio.h>

/* Beginning of main function */
main()
{
/* Declare variable */
int i_ctr, i_sum=0;

/* Find sum of numbers 1 to 10 */
```