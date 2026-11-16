Below is a program using the if-else construct to calculate wages based upon a pay rate and the number of hours worked:

```
// Program to Calculate Wages

#include <stdio.h>

int main (void)
{
    float payRate, hours, wages;

    printf("Enter hourly salary: ");
    scanf("%f", &payRate);

    printf("Enter number of hours worked: ");
    scanf("%f", &hours);

    if (hours <= 40)
        wages = hours * payRate;
    else
        wages = (40 * payRate) + (hours - 40) * 1.5 * payRate;

    printf("The employee's weekly wages are $%6.2f\n", wages);
    return 0;
}
```

# Nested If Statement

Whenever an if statement is nested within another if statement, put braces around the nested if statement. Additionally, an else clause is associated with the most recent "un-elsed" if statement that is in the same scope:

```
// incorrect nesting

if (num > 0)
    if (num % 2 == 0)
        printf("Positive and even.\n");
else
    printf("Not positive.\n");

// correct nesting

if (num > 0) {
    if (num % 2 == 0)
        printf("Positive and even.\n");
}
else
    printf("Not positive. ");
```