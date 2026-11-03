
```
printf("\nFINAL VALUE OF N IS NOT SUFFICIENT\n");
printf("TO ACHIEVE DESIRED ACCURACY\n");
goto end;
output:
printf("\nEXIT FROM LOOP\n");
printf("Sum = %f; No. of terms = %d\n", sum, n);
end:
;
}
Output
Input value of x : 21
EXIT FROM LOOP
Sum = 1.265800; No. of terms = 7
Input value of x : 75
EXIT FROM LOOP
Sum = 3.999774; No. of terms = 34
Input value of x : 99
FINAL VALUE OF N IS NOT SUFFICIENT
TO ACHIEVE DESIRED ACCURACY
```

## Fig. 7.9 Use of goto to exit from a loop

The test of accuracy is made using an if statement and the goto statement exits the loop as soon as the accuracy condition is satisfied. If the number of loop repetitions is not large enough to produce the desired accuracy, the program prints an appropriate message.

Note that the break statement is not very convenient to use here. Both the normal exit and the break exit will transfer the control to the same statement that appears next to the loop. But, in the present problem, the normal exit prints the message "FINAL VALUE OF N IS NOT SUFFICIENT TO ACHIEVE DESIRED ACCURACY" and the forced exit prints the results of evaluation. Notice the use of a null statement at the end. This is necessary because a program should not end with a label.

## Skipping a Part of a Loop—The Continue Statement

During the loop operations, it may be necessary to skip a part of the body of the loop under certain conditions. For example, in processing of applications for some job, we might like to exclude the processing of data of applicants belonging to a certain category. On reading the category code of an applicant, a test is made to see whether his application should be considered or not. If it is not to be considered, the part of the program loop that processes the application details is skipped and the execution continues with the next loop operation.

Like the break statement, C supports another similar statement called the continue statement. However, unlike the break which causes the loop to be terminated, the continue, as the name implies, causes the loop to be continued with the next iteration after skipping any statements in between. The continue statement tells the compiler, "SKIP THE FOLLOWING STATEMENTS AND CONTINUE WITH THE NEXT ITERATION". The format of the continue statement is simply

## continue;

The use of the **continue** statement in loops is illustrated in Fig. 7.10. In **while** and **do** loops, **continue** causes the control to go directly to the *test-condition* and then to continue the iteration process. In the case of **for** loop, the *increment* section of the loop is executed before the *test-condition* is evaluated.

![](img/65953ea584e494f3d396b2252cb5ea53_185_0.png)

Fig. 7.10 Bypassing and continuing in loops

## Example 7.7

The program in Fig. 7.11 illustrates the use of **continue** statement.

The program evaluates the square root of a series of numbers and prints the results. The process stops when the number 9999 is typed in.

In case the series contains any negative numbers, the process of evaluation of square root should be bypassed for such numbers because the square root of a negative number is not defined. The **continue** statement is used to achieve this. The program also prints a message saying that the number is negative and keeps an account of negative numbers.

The final output includes the number of positive values evaluated and the number of negative items encountered.

```
Program
/***************************************************************/
/*              USE OF continue STATEMENT                     */
/***************************************************************/

#include <math.h>
main()
{
    int count, negative;
    double number, sqroot;
    printf("Enter 9999 to STOP\n");
    count = 0;
    negative = 0;
    while (count <= 100)
{
    printf("Enter a number : ");
    scanf("%lf", &number);
    if (number == 9999)
        break;    /* EXIT FROM THE LOOP */
    if (number <0)
    {
        printf("number is negative\n\n");
        negative++;
        continue;    /* SKIP REST OF THE LOOP */
    }
    sqroot = sqrt(number);
    printf("\nNumber    = %lf\nSquare root = %lf\n", number, sqroot);
    count++;
}
printf("Number of items done    = %d\n", count);
printf("\nNegative items          = %d\n", negative);
printf("END OF DATA\n");
```

Output
Enter 9999 to STOP
Enter a number : 25.0
Number        = 25.000000
Square root   = 5.000000
Enter a number : 40.5
Number        = 40.500000
Square root   = 6.363961
Enter a number : -9
Number is negative
Enter a number : 16
Number        = 16.000000
Square root   = 4.000000
Enter a number : -14.75
Number is negative
Enter a number : 80
Number        = 80.000000
Square root   = 8.944272
Enter a number : 9999
Number of items done    = 4
Negative items          = 2
END OF DATA

Fig. 7.11 Use of continue statement

## Avoiding goto

As mentioned earlier, it is a good practice to avoid using gotos. There are many reasons for this. When goto is used, many compilers generate a less efficient code. In addition, using many of them makes a
program logic complicated and renders the program unreadable. It is possible to avoid using goto by careful program design. In case any goto is absolutely necessary, it should be documented. The following goto jumps would cause problems and therefore must be avoided:

![](img/65953ea584e494f3d396b2252cb5ea53_187_0.png)

## Concise Test Expressions

We often use test expressions in the if, for, while and do statements that are evaluated and compared with zero for making branching decisions. Since every integer expression has a true/false value, we need not make explicit comparisons with zero. For instance, the expression x is true whenever x is not zero, and false when x is zero. Applying ! operator, we can write concise test expressions without using any relational operators.

```
if (expression == 0)
```

is equivalent to

```
if (! expression)
```

Similarly,

```
if (expression != 0)
```

is equivalent to

```
if (expression)
```

## Example

If (m%5 == 0 && n%5 == 0) is same as if (!(m%5) && !(n%5))

## 7.6 STRUCTURED PROGRAMMING

Structured programming is an approach to the design and development of programs. It is a discipline of making a program’s logic easy to understand by using only the basic three control structures:

- Sequence (straight line) structure
- Selection (branching) structure
- Repetition (looping) structure

While sequence and loop structures are sufficient to meet all the requirements of programming, the selection structure proves to be more convenient in some situations.

## Decision Making and Looping 7.21

The use of structured programming techniques helps ensure well-designed programs that are easier to write, read, debug and maintain compared to those that are unstructured. Structured programming discourages the implementation of unconditional branching using jump statements such as goto, break and continue. In its purest form, structured programming is synonymous with "goto less programming". Do not go to goto statement!

## CASE STUDIES

## 1. Table of Binomial Coefficients

Problem: Binomial coefficients are used in the study of binomial distributions and reliability of multicomponent redundant systems. It is given by B(m, x) = (m choose x) = m! / (x! (m-x)!) , m >= x

A table of binomial coefficients is required to determine the binomial coefficient for any set of m and x.

Problem Analysis: The binomial coefficient can be recursively calculated as follows: B(m, x) = B(m, x - 1) * [(m - x + 1) / x] , x = 1, 2, 3, ..., m

Further, B(m, 0) = 1 B(0, x) = 1

That is, the binomial coefficient is one when either x is zero or m is zero. The program in Fig. 7.12 prints the table of binomial coefficients for m = 10. The program employs one do loop and one while loop.

```
#include <stdio.h>
/* EVALUATION OF BINOMIAL COEFFICIENTS */
#define MAX 10
{
int m, x, binom;
printf("m x\n");
for (m=0; m<=10; ++m)
printf("%4d", m);
printf("\n");
m=0;
do {
printf("%4d ", m);
x=0; binom=1;
while (x <= m) {
printf("%4d", binom);
binom = binom * (m - x +1) / x;
x++;
}
printf("\n");
m++;
} while (m <=10);
}
```
