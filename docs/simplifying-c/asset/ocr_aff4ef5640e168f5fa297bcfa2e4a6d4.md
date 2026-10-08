visible at the first instance. Try to observe the output of Program 4 by removing the semicolon. You should get an output similar to the one shown in Figure 5:

![](bbox=[0.41, 0.18, 0.67, 0.29])

▲ Figure 5: Output of Program 4 after Removing the Semicolon

As mentioned earlier, all the three expressions of the for loop are optional. Program 5 illustrates how we can use a for loop that does not contain the three expressions:

# ▶ Program 5

```
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
        scanf("%d",&i_num);
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
    printf("Total even numbers is %d\n",i_esum);
```