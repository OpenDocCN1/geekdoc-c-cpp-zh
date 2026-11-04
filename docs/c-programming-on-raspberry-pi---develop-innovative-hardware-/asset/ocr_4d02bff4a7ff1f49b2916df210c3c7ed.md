```
```c
{
    execute these statements
    ......................
    ......................
}
```
```

If there is only one statement inside an if block, there is no need to use a curly bracket:

```
```c
if(condition is true)
    execute a single statement;
```
```

or,    `if(condition is true) execute a single statement;`

# ### Example 3.3

Write a program to read two numbers from the keyboard and calculate their average. If the average is greater than 10, display **Average is greater than 10.** If on the other hand the average is less than 10, display **Average is less than 10.** If on the other hand, the average is equal to 10, display **Average is 10.**

# ### Solution 3.3

Figure 3.5 shows the program listing (Program: **Average.c**). The program reads two floating-point numbers into variables **no1** and **no2**. The average is calculated and stored in variable **average**. A message is then displayed depending on whether the average is equal to 10, greater than 10, or less than 10. Figure 3.6 shows an example run of the program.

```
```c
/*------------------------------------------------------------
                    AVERAGE OF 2 NUMBERS
                    ====================

This program calculates the average of two numbers read from
the keyboard and compares it with 10

Author: Dogan Ibrahim
File  : Average.c
Date  : December 2020
-------------------------------------------------------------*/
#include <stdio.h>

int main(void)
{
    float no1, no2, average;
    printf("\nAverage of two numbers\n\n");
    printf("Enter two numbers: ");
```
```