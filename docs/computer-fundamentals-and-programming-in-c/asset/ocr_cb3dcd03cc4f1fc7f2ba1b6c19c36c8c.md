Suppose, for example, a and b are two integer variables known to be non-negative, and you want to test whether a+b might overflow. One obvious way to do it looks something like this:

```
```c
if (a + b < 0)
    printf("OVERFLOW");
```
```

In general, this does not work. The point is that once a + b has overflowed, all bits in the register holding the result will be zero. If the operation overflowed, the register would be in overflow state, and the test would fail. One correct way of doing this particular test relies on the fact that unsigned arithmetic is well defined for all values, as are the conversions between signed and unsigned values:

```
```c
if ((int) ((unsigned) a + (unsigned) b) < 0)
    printf("OVERFLOW");
```
```

# EXAMPLES

+   7. Suppose a C code has to be written that will calculate the earnings by workers who are paid an hourly wage, with weekly hours greater than 40 being paid time and a half. Suppose weekly hours and hourly rate are known in the program. Two options of the code to handle this situation are as follows:

**Option 1** Using simple statements:

```
```c
if(weeklyHours <= 40)
    earnings = hourlyRate * weeklyHours;
else
    earnings = 40 * hourlyRate + (weeklyHours -
    40) * hourlyRate* 1.5;
```
```

**Option 2** Using a simple and compound statement:

```
```c
if(weeklyHours <= 40)
    earnings = hourlyRate * weeklyHours;
else
{
    offHours = weeklyHours - 40;
    regpay = 40 * hourlyRate;
    earnings = regpay + offHours * hourlyRate *
    1.5;
}
```
```

A complete program in C is illustrated as follows.

+   8. Write a program that determines if a year is a leap year.

```
```c
#include<stdio.h>
int main()
{
    int year, rem_4, rem_100, rem_400;
    printf("Enter the year to be tested:");
    scanf("%d", &year);
    rem_4 = year % 4;
    rem_100 = year % 100;
    rem_400 = year % 400;
    if( (rem_4 == 0 && rem_100 != 0) || rem_400 == 0 )
        printf("It is a leap year.\n");
```
```

```
```c
    else
        printf("It is not a leap year.\n");
    return 0;
}
```
```

Given below are the outputs obtained for different inputs from the above program executed in a computer.

# Test run no. 1

```
```
Enter the year to be tested: 1955
It is not a leap year.
```
```

# Test run no. 2

```
```
Enter the year to be tested: 2000
It is a leap year.
```
```

# Test run no. 3

```
```
Enter the year to be tested: 1800
It is not a leap year.
```
```

# Multi-way decisions

Multi-way decision statements use if-else-if nested if or switch statements. They are used to evaluate a test expression that could have several possible values. if-else-if statements are often used to choose between ranges of values. Switch statements are discussed in the next section.

+   - **if-else-if ladder**
+   
+     The form of a multi-way decision construct using if-else-if statements is as follows:

```
```c
if(TestExpr1)
    stmtT1;
else if(TestExpr2)
    stmtT2;
else if(TestExpr3)
    stmtT3;

...

else if(TestExprN)
    stmtTN;
else
    stmtF;
```
```

If the first test expression TestExpr1 is evaluated to true, then stmtT1 is executed. If the second test expression TestExpr2 is true, then stmtT2 is executed, and so on. If none of the test expressions are true, then the statement stmtF is executed. The flowchart of the above construct is shown in Fig. 10.5.