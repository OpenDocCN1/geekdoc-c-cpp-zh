```
```c
/* second_prog.c: Uses decision making to validate user input.
   Introduces the scanf function for taking user input. */
#include <stdio.h>
int main(void)
{
    int your_number;

    /* Take user input first */
    printf("Enter an integer greater than 47: ");       /* No \n here */
    scanf("%d", &your_number);                  /* Note that scanf requires the & */

    /* Decision making statement */
    if (your_number > 47)                 /* Beginning of control block */
        printf("The number you entered is %d\n", your_number);
        printf("ASCII value of '%c' = %d\n", your_number, your_number);
    }                                      /* End of control block */
    else
        printf("You entered a number less than 48\n");

    return 0;
}
```
```

| PROGRAM 4.2: **second_prog.c** | |
|---|---|
| Enter an integer greater than 47: 48<br>The number you entered is 48<br>ASCII value of '0' = 48 | *First invocation* |
| Enter an integer greater than 47: 65<br>The number you entered is 65<br>ASCII value of 'A' = 65 | *Second invocation* |
| Enter an integer greater than 47: 97<br>The number you entered is 97<br>ASCII value of 'a' = 97 | *Third invocation* |
| Enter an integer greater than 47: 47<br>You entered a number less than 48 | *Fourth invocation* |

# PROGRAM OUTPUT: **second_prog.c**

The input value is now validated with a decision making construct—the **if** statement. This statement uses a boolean expression (your_number > 47) that yields a true or false value. This value determines whether or not the statements in the following *control block* are executed. This block is delimited by a matched pair of curly braces ({ and }).

Like **if**, many C constructs as well as functions work with blocks. If you enter a number that is less than 48, the condition is not satisfied (false) and the statement following the **else** keyword is executed. This is evident from the fourth invocation of the program.