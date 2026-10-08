
for ([Expression 1] ; [Expression 2] ; [Expression 3])
Action Block;

In the preceding syntax, it can be seen that the three expressions are separated by semicolons. Expression 1 is an initialization statement of loop counter, Expression 2 is a test condition statement that controls the loop, and Expression 3 is the statement that updates the loop counter. The action block contains single or compound statements that are to be repeated. Note that all the three expressions mentioned in the preceding syntax are optional, and hence shown enclosed within square brackets. Figure 4 illustrates the logical flow of the for loop:

![](img/5d422ba7108ffdf64376be51eaf0c459_145_0.png)

It can be seen in Figure 4 that Expression 1 is first evaluated, and it will be evaluated only once. Next, we evaluate Expression 2. If Expression 2 is evaluated to true, we step into the action block. If Expression 2 is evaluated to false, the loop terminates. After executing action block, we evaluate Expression 3. The process of evaluating Expression 2, executing action block, and evaluating Expression 3 becomes a cyclic process till Expression 2 is evaluated to false. Program 1 illustrates the use of for loop:

## Program 1

```c
/* Program to calculate the sum of numbers 1 to 10 using the for loop */
#include <stdio.h>

/* Beginning of main function */
main()
{
    /* Declare variable */
    int i_ctr, i_sum=0;

    /* Find sum of numbers 1 to 10 */
    for(i_ctr = 1 ; i_ctr <= 10; i_ctr++)
    {
        i_sum = i_sum + i_ctr;
    }

    /* Print the value of sum */
    printf("Sum of numbers 1 to 10 is %d\n", i_sum);
    return;
}
/* End of main function */
```

**Output:**
Sum of numbers 1 to 10 is 55

It can be observed in Program 1 that we have not taken any input from the user. The value of i_ctr is initialized to 1 within the for loop. The loop will be repeated 10 times, and finally, we will get the sum of numbers 1 to 10. Every time we execute this program, we are going to get the same result (in this case 55). Let us modify this program such that we get different values of the sum based on the number entered by the user. Program 2 illustrates this change:

## Program 2

```c
/* Program to calculate the sum of numbers 1 to i_num using the for loop */
/* The value of i_num is accepted from user */
#include <stdio.h>

/* Beginning of main function */
main()
{
    /* Declare variable */
    int i_ctr, i_sum=0, i_num;
    
    /* Input Data */
    printf("Enter a number: ");
    scanf("%d", &i_num);

    /* Find sum of numbers 1 to i_num */
    for(i_ctr = 1 ; i_ctr <= i_num; i_ctr++)
    {
        i_sum = i_sum + i_ctr;
    }

    /* Print the value of sum */
    printf("Sum of numbers 1 to %d is %d\n", i_num, i_sum);
    return;
}
/* End of main function */
```

**Output 1:**
Enter a number: 5
Sum of numbers 1 to 5 is 15

**Output 2:**
Enter a number: 50
Sum of numbers 1 to 50 is 1275

**Output 3:**
Enter a number: 10
Sum of numbers 1 to 10 is 55

Observe the difference in Programs 1 and 2. In Program 2, we have accepted the value of i_num from the user. This value tells the compiler how many times the loop will be repeated. In Output 1, the value of i_num is 5; hence, we get the sum of numbers from 1 to 5. In Output 2, the value of i_num is 50; hence, we get the sum of numbers from 1 to 50; and in Output 3, the value of i_num is 10; hence, we get the sum of numbers from 1 to 10. Every time we enter a new value of i_num, we will get different values of sum.

In both the preceding programs, the initialization of the loop counter variable started from 1. To update the loop counter, we added 1 to it. Program 2 can be written in a different manner, and we can still obtain the same result. Program 3 illustrates the change in use of the for loop:

## Program 3

```c
/* Program to calculate the sum of numbers 1 to i_num using the for loop */
/* The value of i_num is accepted from user */

#include <stdio.h>

/* Beginning of main function */
main()
{
    /* Declare variable */
    int i_ctr, i_sum=0, i_num;

    /* Input Data */
    printf("Enter a number: ");
    scanf("%d", &i_num);

    /* Find sum of numbers 1 to i_num */
    for(i_ctr = i_num ; i_ctr >= 1; i_ctr--)
    {
        i_sum = i_sum + i_ctr;
    }

    /* Print the value of sum */
    printf("Sum of numbers %d to 1 is %d\n", i_num, i_sum);
    return;
}
/* End of main function */
```

**Output 1:**
Enter a number: 5
Sum of numbers 5 to 1 is 15

**Output 2:**
![](img/5d422ba7108ffdf64376be51eaf0c459_148_0.png)

**Output 3:**
![](img/5d422ba7108ffdf64376be51eaf0c459_148_1.png)

It can be observed in Program 3 that the loop counter here is initialized to `i_num`, and at the time of update, its value is decreased by 1 for every iteration. This affects the test condition also; now, instead of checking the condition `i_ctr <= i_num`, we check `i_ctr >= 1`. The result of both the programs is still the same.

The initial programmers normally make a mistake of terminating the *for* statement with a semicolon. Program 4 illustrates this mistake:

## Program 4

```c
/* Program to print numbers from 1 to 50 using the for loop */
#include <stdio.h>
/* Beginning of main function */
main()
{
    /* Declare variable */
    int i_ctr;

    /* Print values from 1 to 50 */
    for(i_ctr = 1 ; i_ctr <= 50; i_ctr++);
    {
        printf("%02d ", i_ctr);

        if((i_ctr % 10) == 0)
            printf("\n");
    }

    return;
}
/* End of main function */
```

**Output:**
![](img/5d422ba7108ffdf64376be51eaf0c459_148_2.png)

Program 4 was written to print numbers from 1 to 50. However, the output of the program is only 51. The reason for this wrong output is the mistake that we made in statement `for(i_ctr = 1 ; i_ctr <= 50; i_ctr++)`. Here, we have terminated the *for* statement with a semicolon. The compiler did not generate any error in this case, as it assumed that there is no statement to be executed within the *for* loop. Even though no statements were executed within the loop, the loop counter was initialized to 1 and incremented by 1 until its value became 51, and the condition `i_ctr <= 50` evaluated to false. This kind of *for* loop is referred to as a delay loop. The delay loop does not execute any statement, but simply initializes, checks the test condition, and updates the value of the loop counter. The user has to be cautious in such cases as the mistake may not be visible at the first instance. Try to observe the output of Program 4 by removing the semicolon. You should get an output similar to the one shown in Figure 5:

![](img/5d422ba7108ffdf64376be51eaf0c459_149_0.png)

▲ Figure 5: Output of Program 4 after Removing the Semicolon

As mentioned earlier, all the three expressions of the for loop are optional. Program 5 illustrates how we can use a for loop that does not contain the three expressions:

## Program 5

```c
/* Program to print sum of odd numbers and sum of even numbers of all positive numbers entered by the user, till the user enters 0 */

#include <stdio.h>
/* Beginning of main function */
main()
{
    /* Declare variable */
    int i_num, i_osum = 0, i_esum = 0;

    /* Loop with no expressions */
    for( ; ; )
    {
        /* Input Data */
        printf("Enter a number: ");
        scanf("%d", &i_num);
        /* Check if number is positive */
        if(i_num >= 0)
        {
            if(i_num)
            {
                /* Check whether number is even or odd */
                if((i_num % 2) == 0)
                    i_esum++;
                else
                    i_osum++;
            }
        }
        else
            break; /* If number is 0 terminate the loop */
    }

    /* Print total even and odd number */
    printf("Total even numbers is %d\n", i_esum);
    printf("Total odd numbers is %d\n", i_osum);
    return;
}

/* End of main function */
```

**Output 1:**
```
Enter a number: 2
Enter a number: 5
Enter a number: 7
Enter a number: 9
Enter a number: 15
Enter a number: 0
Total even numbers is 1
Total odd numbers is 4
```

**Output 2:**
```
Enter a number: -1
Enter a number: 12
Enter a number: 19
Enter a number: 80
Enter a number: 0
Total even numbers is 2
Total odd numbers is 1
```

**Output 3:**
```
Enter a number: 0
Total even numbers is 0
Total odd numbers is 0
```

In Program 5, it is observed that we have used the statement `for( ; ; )` that does not contain any expression. As no expression is specified, there is no loop control variable, rather the loop is controlled by an event. The event here refers to a number 0 entered by the user. As the loop is controlled by event, this loop becomes an event-controlled loop. All the for loops used in programs preceding Program 5 were counter controlled.

It can be observed in Output 1 that the loop stops after the sixth iteration; in Output 2, it stops after the fifth iteration; and in Output 3, it stops after the first iteration itself. Note that in Output 2, even though we have entered four values, the total of both odd and even numbers is still 3. The negative number entered in Output 2 was not considered in the calculation due to the initial condition `if(i_num >= 0)`.

One has to be cautious about deciding the terminating condition while using the for loop as an event-controlled loop. In the case of Program 5, the loop terminates only when the user enters a number 0. When the user enters 0, the compiler evaluates the condition `if(i_num >= 0)` to true, then the condition `if(!i_num)` is evaluated to false; hence, the control gets transferred to the statement `else break;`. The `break` statement terminates the loop. If the user does not write a `break` statement, the loop will go in an infinite sequence.

It can be seen from the discussion made earlier that the for loop is a pretest loop, which can be used as a counter-controlled loop or an event-controlled loop. The next subsection discusses the concept of while loop.
