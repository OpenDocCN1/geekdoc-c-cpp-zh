# ■ **The While Loop**

The while loop is a pretest loop that is used when the number of times the statement needs to be executed cannot be predetermined. The syntax of the while loop is as follows:

```
while (test condition)
   Action block;
```

The test condition mentioned in the preceding syntax is a relational expression or a positive constant. The action block of the while loop is executed only when the test condition is evaluated to true. Figure 6 illustrates the logical flow of the while loop:

![](bbox=[0.44, 0.33, 0.68, 0.5])

▲ **Figure 6: Logical Flow of the While Loop**

As the test condition is checked at the entry point, the while loop is considered to be an entry-controlled loop. If the test condition is evaluated to false at first time itself, the action block of the loop will not be executed at all. Program 6 illustrates the use of while loop to calculate the greatest common divisor of two positive numbers.

# ▶ **Program 6**

```
/* Program to calculate the greatest common divisor of two positive
    numbers using the while loop */

#include <stdio.h>

/* Beginning of main function */
main()
{
   /* Declare variable */
   int i_num1, i_num2,i_remainer, i_temp;
   /* Input Data */
   printf("Enter the first number: ");
   scanf("%d",&i_num1);

   printf("Enter the second number: ");
   scanf("%d",&i_num2);
   /* Check if both numbers are positive and greater than 0 */
   if((i_num1 > 0) && (i_num2 > 0))
   {
      /* Swap values if needed */
```