A fall through in a switch statement is a case that does not include a break statement, there by causing control to the next case statement. Program 1.10, helps you to understand things better.

```
Program 1.10 :

/* Program to demonstrate the use of switch without break */
/* no_break.c */
#include<stdio.h>
void main()
{
    int choice = 2;
    switch(choice)
    {
        case 1: printf("\n This is Case 1 ...");
        case 2: printf("\n This is Case 2 ...");
        case 3: printf("\n This is Case 3 ...");
        default: printf("\n This is Default ...");
    }
}
```

The program displays the following output

This is Case 2 ...
This is Case 3 ...
This is Default ...

Output of Program 1.10, is definitely not what we have expected. We have expected the printf() function in case 2 to be executed but not, other lines. This has happened because we haven't included a break statement at the end of each case statement and hence the subsequent case statements including the default statement have been executed.

# Limitations of using a switch statement

+   - Only one variable can be tested with the available case statements with the values stored in them (i.e., you cannot use relational operators and combine two or more conditions as in the case of if or if-else statements).
+   - Floating-point, double, and long type variables cannot be used as cases in the switch statement.
+   - Multiple statements can be executed in each case without the use of a pair of braces as in the case of if or if-else statement.

# Important points to be noted while using a switch statement

+   - Character values are also allowed in cases. You can also mix integer and character constants in different cases of switch.
+   - Integer expression used in different case statements can be specified in any order.