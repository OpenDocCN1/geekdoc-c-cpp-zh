# **Exercise 3.** Demonstrate basic arithmetic operations using arithmetic operators.

```
ArithmeticOperationsInteger.c
```

```
```c
#include <stdio.h>

int main() {

    int intNum1 = 6, intNum2 = 4;

    int intResult = -999; // initialize with unexpected value


    printf("Integer numbers: ");

    printf("\nintNum1 = %d, intNum2 = %d", intNum1, intNum2 );


    printf("\n\n");

    printf("Operations | Operator | Expression | Result\n");
    printf("-------------------------------------------\n");


    printf("Add       | +        | ");
    intResult = intNum1 + intNum2;
    printf("%d + %d   |  %d\n", intNum1, intNum2, intResult );


    printf("Subtract  | -        | ");
    intResult = intNum1 - intNum2;
    printf("%d - %d   |  %d\n", intNum1, intNum2, intResult );


    printf("Multiply  | *        | ");
    intResult = intNum1 * intNum2;
    printf("%d * %d   |  %d\n", intNum1, intNum2, intResult );


    printf("Divide    | /        | ");
    intResult = intNum1 / intNum2;
    printf("%d / %d   |  %d\n", intNum1, intNum2, intResult );
```
```