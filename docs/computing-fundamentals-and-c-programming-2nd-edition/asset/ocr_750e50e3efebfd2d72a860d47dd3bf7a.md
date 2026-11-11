During running of a program when a statement like

`goto begin;`

is met, the flow of control will jump to the statement immediately following the label **begin**. This happens unconditionally.

Note that a **goto** breaks the normal sequential execution of the program. If the *label:* is before the statement **goto label;** a loop will be formed and some statements will be executed repeatedly. Such a jump is known as a **backward jump**. On the other hand, if the *label:* is placed after the **goto label;** some statements will be skipped and the jump is known as a **forward jump**.

A **goto** is often used at the end of a program to direct the control to go to the input statement, to read further data. Consider the following example:

```
```c
main()
{
    double x, y;
    read:
    scanf("%f", &x);
    if (x < 0) goto read;
    y = sqrt(x);
    printf("%f %f\n", x, y);
    goto read;
}
```
```

This program is written to evaluate the square root of a series of numbers read from the terminal. The program uses two **goto** statements, one at the end, after printing the results to transfer the control back to the input statement and the other to skip any further computation when the number is negative.

Due to the unconditional **goto** statement at the end, the control is always transferred back to the input statement. In fact, this program puts the computer in a permanent loop known as an *infinite loop*. The computer goes round and round until we take some special steps to terminate the loop. Such infinite loops should be avoided. Worked-Out Problem 7.9 illustrates how such infinite loops can be eliminated.

# WORKED-OUT PROBLEM 7.9

Program presented in Fig. 7.15 illustrates the use of the **goto** statement. The program evaluates the square root for five numbers. The variable **count** keeps the count of numbers read. When **count** is less than or equal to 5, **goto read;** directs the control to the label **read**; otherwise, the program prints a message and stops.

```
```c
Program

#include <math.h>
main()
{
    double x, y;
    int count;
    count = 1;
    printf("Enter FIVE real values in a LINE \n");
read:
```
```