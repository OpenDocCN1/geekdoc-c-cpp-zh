
```c
scanf("%f %f", &no1, &no2);
average = (no1 + no2) / 2.0;

if(average > 10)
    printf("Average is greater than 10\n");
else if(average < 10)
    printf("Average is less than 10\n");
else
    printf("Average is 10\n");

return 0;
}
```

Figure 3.5 Program: Average.c

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_41_0.png)

## switch

The **switch** statement is another conditional statement that is used to test a variable against several conditions, and do different things for each condition. The general format of the **switch** statement is as follows:

```c
switch (variable)
{
    condition 1: do some statements
    condition 2: do some statements
    condition 3: do some statements
    default: do some statements
}
```

Notice that **default** is optional and if none of the conditions are satisfied, the statements under **default** are executed.

### Example 3.4

Write a calculator program to perform the operations of addition, subtraction, multiplication, and division. The user should enter the first number, the required operation, followed by the second number. The result should be displayed on the screen.

### Solution 3.4

Figure 3.7 shows the required program (Program: calculator.c). The function scanf is used to read the two numbers and the required operation on the same line. A switch statement is used to perform the required calculation. Notice the conditions are specified using the case statement followed by the condition. If for example, the user entered +, the two numbers added together and the sum is stored in variable result, which is then displayed. The break statements make sure that the switch block terminates after the contents of a condition are executed.

```c
/*---------------------------------------------------------------
                    SIMPLE CALCULATOR
                    =============

This is a simple calculator program which can perform + - * /

Author: Dogan Ibrahim
File  : calculator.c
Date  : December 2020
---------------------------------------------------*/

#include <stdio.h>

int main(void)
{
    float no1, no2, result;
    char oper;

    printf("Enter first number, operation, and second number: ");
    scanf("%f%c%f", &no1,&oper,&no2);

    switch(oper)
    {
        case '+':
            result = no1 + no2;
            break;
        case '-':
            result = no1 - no2;
            break;
        case '*':
            result = no1 * no2;
            break;
        case '/':
            result = no1 / no2;
            break;
    }
printf("\nResult = %.2f\n", result);
return 0;
}
```

Figure 3.7 Program: calculator.c

Figure 3.8 shows an example run of the program.

```text
Enter first number, operation, and second number: 12*8

Result =  96.00
pi@raspberrypi:~ $ █
```

Figure 3.8 Example run of the program

## while

This flow control statement is usually used in loops (repetition). The statements inside the curly brackets are executed as long as the condition is true. Notice if the condition does not become true inside the curly brackets, the loop is executed forever. Also, if the condition is false on entry to the loop, the statements inside the loop are never executed. The general format of this statement is as follows:

```c
while(condition is true)
{
    execute these statements
}
```

### Example 3.5

It is required to write a program to calculate the total resistance of several resistors connected in series. Write a program to accept the number of resistors and enter the value of each resistor. Total resistance should be displayed on the screen.

### Solution 3.5

The total resistance of resistors connected in series is calculated by adding up the values of all the resistors. Figure 3.9 shows the required program listing (Program: SerialResistors.c). At the beginning of the program, the user is asked to enter the number of resistors connected in series and this is stored in variable no. A while loop is then formed and inside this loop, the user is asked to enter the value of each resistor. The total resistance is stored in the variable Total which is displayed on the screen.

```c
/*---------------------------------------------------------
       SERIALLY CONNECTED RESISTORS
       ==========================================
Total resistance of serially connected resistors

Author: Dogan Ibrahim
File  : SerialResistors.c
Date  : December 2020
---------------------------------------------------------*/
#include <stdio.h>

int main(void)
{
    int no, k, R, Total;

    printf("\nSerially Connected Resistors");
    printf("\n====================================\n");

    printf("How many resistors are there? ");
    scanf("%d", &no);

    k = 1;
    Total = 0;

    while(k <= no)
    {
        printf("Enter resistance (Ohms) of Resistor %d: ", k);
        scanf("%d", &R);
        Total = Total + R;
        k++;
    }

    printf("\nTotal resistance = %d Ohms\n", Total);
    return 0;
}
```

Figure 3.9 Program: SerialResistors.c

Figure 3.10 shows an example run of the program with three resistors connected in series.

```text
pi@raspberrypi:~ $ gcc -o Resistors SerialResistors.c
pi@raspberrypi:~ $ ./Resistors

  Serially Connected Resistors
  ============================
  How many resistors are there? 3
  Enter resistance (Ohms) of Resistor 1: 200
  Enter resistance (Ohms) of Resistor 2: 400
  Enter resistance (Ohms) of Resistor 3: 150

  Total resistance = 750 Ohms
pi@raspberrypi:~ $
```

Figure 3.10 Example run of the program

## do...while

This statement is similar to the **while** statement, but the statements inside the loop are executed at least once. This is because the condition to exit the loop is tested at the end of the loop. The general format of this statement is as follows:

```
do
{
    execute these statements
}while(condition is true)
```

### Example 3.6

Repeat Example 3.5, but this time use the **do...while** statement for the loop.

### Solution 3.6

Figure 3.11 shows the program listing (Program: **SerialResistors2.c**). As you can see, the condition to terminate the loop is tested at the end of the loop. An example run of the program is the same as in Figure 3.10.

```c
/*-----------------------------------------------------------------------
                SERIALLY CONNECTED RESISTORS
                ============================

Total resistance of serially connected resistors

Author: Dogan Ibrahim
File  : SerialResistors2.c
Date  : December 2020
-----------------------------------------------------------------------*/
#include <stdio.h>

int main(void)
{
    int no, k, R, Total;

    printf("\nSerially Connected Resistors");
    printf("\n==============================\n");

    printf("How many resistors are there? ");
    scanf("%d", &no);

    k = 1;
    Total = 0;

    do
    {
        printf("Enter resistance (Ohms) of Resistor %d: ", k);
        scanf("%d", &R);
        Total = Total + R;
        k++;
    }while(k <= no);

    printf("\nTotal resistance = %d Ohms\n", Total);
    return 0;
}
```

Figure 3.11 Program SerialResistors2.c

## for

The for loop is probably one of the most commonly used iteration statements. The general format of this statement is:

```c
for(initial-condition; increment; termination condition)
{
    execute these statements until the condition is true
}
```

### Example 3.7

Repeat Example 3.5, but this time use the for statement for the loop.

### Solution 3.7

Figure 3.12 shows the program listing (Program: SerialResistors3.c). As you can see, in this program, the for loop runs from 1 to 3 inclusive. An example run of the program is the same as in Figure 3.10.

```c
/*----------------------------------------

SERIALLY CONNECTED RESISTORS
============================

Total resistance of serially connected resistors

Author: Dogan Ibrahim
File : SerialResistors3.c
Date : December 2020
----------------------------------------*/

#include <stdio.h>

int main(void)
{
    int no, k, R, Total;

    printf("Serially Connected Resistors");
    printf("============================");

    printf("How many resistors are there? ");
    scanf("%d", &no);

    Total = 0;

    for(k = 1; k <= no; k++)
    {
        printf("Enter resistance (Ohms) of Resistor %d: ", k);
        scanf("%d", &R);
        Total = Total + R;
    }

    printf("Total resistance = %d Ohms", Total);
    return 0;
}
```

Figure 3.12 Program SerialResistors3.c

### Example 3.8

Write a program to display a table of the squares of integer numbers from 1 to 10.

### Solution 3.8

The required program listing (Program: squares.c) is shown in Figure 3.13. A loop is formed using a for statement and inside this loop, integer numbers from 1 to 10 are tabulated with their corresponding squares.
