
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

图 3.5 程序：Average.c

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_41_0.png)

## switch

**switch** 语句是另一种条件语句，用于针对多个条件测试一个变量，并针对每个条件执行不同的操作。**switch** 语句的一般格式如下：

```c
switch (variable)
{
    condition 1: do some statements
    condition 2: do some statements
    condition 3: do some statements
    default: do some statements
}
```

注意，**default** 是可选的；如果没有任何条件满足，则执行 **default** 下的语句。

### 示例 3.4

编写一个计算器程序，执行加、减、乘、除运算。用户应输入第一个数字、所需运算，然后输入第二个数字。结果应显示在屏幕上。

### 解答 3.4

图 3.7 显示了所需程序（程序：calculator.c）。scanf 函数用于在同一行读取两个数字和所需运算。switch 语句用于执行所需计算。注意，条件使用 case 语句指定，后跟条件。例如，如果用户输入 +，则将两个数字相加，和存储在变量 result 中，然后显示。break 语句确保在执行完某个条件的内容后终止 switch 块。

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

图 3.7 程序：calculator.c

图 3.8 显示了程序的一次示例运行。

```text
Enter first number, operation, and second number: 12*8

Result =  96.00
pi@raspberrypi:~ $ █
```

图 3.8 程序示例运行

## while

此流程控制语句通常用于循环（重复）。只要条件为真，就执行花括号内的语句。注意，如果条件在花括号内没有变为真，循环将永远执行。此外，如果进入循环时条件为假，则循环内的语句永远不会执行。该语句的一般格式如下：

```c
while(condition is true)
{
    execute these statements
}
```

### 示例 3.5

要求编写一个程序，计算多个串联电阻的总电阻。编写一个程序，接受电阻数量，并输入每个电阻的值。总电阻应显示在屏幕上。

### 解答 3.5

串联电阻的总电阻通过将所有电阻的值相加来计算。图 3.9 显示了所需程序清单（程序：SerialResistors.c）。程序开始时，要求用户输入串联电阻的数量，并将其存储在变量 no 中。然后形成一个 while 循环，在此循环内，要求用户输入每个电阻的值。总电阻存储在变量 Total 中，并显示在屏幕上。

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

图 3.9 程序：SerialResistors.c

图 3.10 显示了三个串联电阻时程序的一次示例运行。

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

图 3.10 程序示例运行

## do...while

此语句类似于 **while** 语句，但循环内的语句至少执行一次。这是因为退出循环的条件在循环末尾进行测试。该语句的一般格式如下：

```
do
{
    execute these statements
}while(condition is true)
```

### 示例 3.6

重复示例 3.5，但这次循环使用 **do...while** 语句。

### 解答 3.6

图 3.11 显示了程序清单（程序：**SerialResistors2.c**）。如你所见，终止循环的条件在循环末尾进行测试。程序的一次示例运行与图 3.10 相同。

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

图 3.11 程序 SerialResistors2.c

## for

for 循环可能是最常用的迭代语句之一。该语句的一般格式为：

```c
for(initial-condition; increment; termination condition)
{
    execute these statements until the condition is true
}
```

### 示例 3.7

重复示例 3.5，但这次循环使用 for 语句。

### 解答 3.7

图 3.12 显示了程序清单（程序：SerialResistors3.c）。如你所见，在此程序中，for 循环从 1 运行到 3（包含 3）。程序的一次示例运行与图 3.10 相同。

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

图 3.12 程序 SerialResistors3.c

### 示例 3.8

编写一个程序，显示 1 到 10 的整数平方表。

### 解答 3.8

所需程序清单（程序：squares.c）如图 3.13 所示。使用 for 语句形成一个循环，在此循环内，将 1 到 10 的整数及其对应的平方列成表格。
