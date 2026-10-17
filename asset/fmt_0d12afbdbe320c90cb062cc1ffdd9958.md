
## Q4. 使用 if 语句寻找三个数中的最大值程序

**解决方案：**

```c
/****************************
文件名: if2c
作者信息: Mr. x, 1ST SEM, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
程序执行日期: 2015/3/8
程序名称: 使用 if 语句寻找三个数中的最大值
****************************/

#include <stdio.h>

void main(void)
{
    int x, y, z;

    printf("Input the three numbers:");
    scanf("%d%d%d", &x, &y, &z);

    if (x > y && x > z)
        printf("Among the inputted three numbers %d is the largest,", x);

    if (y > x && y > z)
        printf("Among the inputted three numbers %d is the largest,", y);

    if (z > x && z > y)
        printf("Among the inputted three numbers %d is the largest,", z);

    if (x == y && y == z)
        printf("All three numbers are equal=");
}
```

**输出：**
```
Input the three numbers:3 10 1
Among the input three integer 10 is the largest
```

## 7.2.3 if-else 语句的概念

if-else 语句是一种双路分支语句。当条件为真时，执行大括号内的单个语句或语句块；否则，条件为假，控制流移动到 else 块并执行。

if-else 语句的语法是：

```c
if (condition)
{
    statement block1;
}
else
{
    statement block2;
}
next statements;
```

## 7.2.4 if-else 语句的一些实用编程示例

### Q1. 检查数字是否为偶数的 C 程序

**解决方案：**

**输出：**
```
输入整数：4
输入 4 是偶数
```

**解释：**
这里假设用户输入的整数为 4。检查 `if` 条件，即 `if (4 % 2 == 0)`。由于该条件为真，所以 4 是偶数。这里 `%` 被称为模运算符或取余运算符。

### Q2. 使用 if-else 语句检查字符是否为元音或辅音的 C 程序

**解决方案：**

```c
/********************************************************************
FILE NAME: ifelse2.c
AUTHOR DETAILS: Mr. x, 1st SEM, COMP.SC ENGG., ABC COLLEGE OF ENGG.
DATE OF PROGRAM EXECUTION: 3/8/2015
NAME OF THE PROGRAM: 使用 if-else 语句检查字符是否为元音和辅音的 c 程序
*****************************************************************/

#include <stdio.h>

void main()
{
    char x;

    printf("Input a character:");
    scanf("%c", &x);

    if (x == 'a' || x == 'A' || x == 'e' || x == 'E' || x == 'i' || x == 'I' ||
        x == 'o' || x == 'O' || x == 'u' || x == 'U')
        printf("Inputted %c is the vowel \n", x);
    else
        printf("Inputted %c is the consonant \n", x);
}
```

**输出：**
```
Input a character: a
Inputted a is the vowel
```

**解释：**
这里用户输入字符 'a' 作为输入。由于 'a' 匹配了给定条件，所以 'a' 是元音。此后没有使用 `if` 语句的大括号，因为语句后面是一个简单的打印语句。因此，使用大括号是可选的。

### Q3. 检查字符是否为字母的 C 程序

**解决方案：**

```c
/****************************************************************
FILE NAME: ifelse3.c
AUTHOR DETAILS: Mr. x, 1ST SEM, COMP.SC& ENGG., COLLEGE OF ENG.
DATE OF PROGRAM EXECUTION: 3/8/2015
NAME OF THE PROGRAM: 检查字符是否为字母的 c 程序
******************************************************************/
```

**输出：**
```
Input the character (alphabet or any/'\'','"',etc) :.
Input is not the character
```

**解释：**
这里用户输入字符 () 作为输入。然后检查了 `if` 条件。`if` 条件不匹配 ()。因此执行了 `else` 块，即打印 () 不是字母。

### Q4. 使用 if-else 语句检查年份是否为闰年的 C 程序

**解决方案：**

```c
/********************************************************************************
FILE NAME: ifelse4.c
AUTHOR DETAILS: Mr. x, 1ST SEM, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
DATE OF PROGRAM EXECUTION: 3/8/2015
NAME OF THE PROGRAM: 使用 else 语句检查年份是否为闰年的 c 程序
********************************************************************************/

#include <stdio.h>

void main(void)
{
    int x;

    printf("Input the year to check leap year:");
    scanf("%d", &x);

    if ((x % 4 == 0 && x % 100 != 0) || (x % 400 == 0))
    {
        printf("Inputted %d is a leap year", x);
    }
    else
    {
        printf("Inputted %d is not a leap year", x);
    }
}
```

**输出：**
```
Input the year to check leap year: 2020
Input 2020 is a leap year
```

**解释：**
这里使用了年份 2020 来检查年份是否为闰年。该语句用于检查条件，即 `if ((2020 % 4 == 0 && 2020 % 100 != 0) || (2020 % 400 == 0))`。由于 `2020 % 4 == 0` 为真且 `2020 % 100 != 0` 为真，而条件 `2020 % 400 == 0` 为假。所以在语句中给出了两个条件，即括号内的第一个条件为真，括号内的第二个条件为假。由于两个条件之间的 OR 符号意味着两个条件中的任意一个，只要其中一个条件为真，表达式就为真。结果是 2020 年是闰年。

### Q5. 使用 if-else 语句求一元方程根的 C 程序

**解决方案：**

```c
/********************************************************************************
FILE NAME: ifelse5.c
AUTHOR DETAILS: Mr. x, 1ST SEM, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
DATE OF PROGRAM EXECUTION: 3/8/2015
NAME OF THE PROGRAM: 使用 if-else 语句求一元方程根的 C 程序
******************************************************/

#include <stdio.h>
#include <math.h>

void main(void)
{
    float x, y, z, d, m1, m2;
    printf("input the floating values of x, y, z:");
    scanf("%f%f%f", &x, &y, &z);
    d = y * y - 4 * x;
    if (d > 0)
    {
        m1 = (-y + sqrt(d)) / (2.0 * x);
        m2 = (-y - sqrt(d)) / (2.0 * x);
        printf("root1 is:%2f, root2 is:%2f", m1, m2);
    }
    else
        printf("roots are imaginary");
}
```

**输出：**
```
Input the floating values of x, y, z: 2.0 4.0 -20.0
root1 is:2.32, root2:-4.32
```

**解释：**
这里用户输入浮点值 2.0, 4.0 和 -20.0 作为输入。然后计算判别式。由于判别值大于 0，所以满足条件并打印两个根。

### Q6. 使用 if-else 语句查找整数之间最大数的 C 程序

**解决方案：**

```c
/******************************************************
FILE NAME: elseif6.c
AUTHOR DETAILS: Mr. x, 1ST SEM, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
DATE OF PROGRAM EXECUTION: 3/8/2015
NAME OF THE PROGRAM: 使用 if-else 语句查找两个整数之间最大数的 C 程序
******************************************************/

#include <stdio.h>
#include <conio.h>

void main(void)
{
    int x, y;

    clrscr();

    printf("Input the integer numbers:");
    scanf("%d%d", &x, &y);

    if (x > y)
    {
        printf("%d is the greatest number", x);
    }
    else
    {
        printf("%d is the greatest number", y);
    }

    getch();
}
```

**输出：**
```
Input the integer numbers: 10 20
20 is the greatest number
```

## 嵌套 if-else 示例：查找三个整数中的最大值

```c
else
{
    if (y > z)
    {
        printf("Among the inputted three integer numbers %d is the greatest", y);
    }
    else
    {
        printf("Among the inputted three integer numbers %d is the greatest", z);
    }
}
```

**输出：**
```
输入三个整数：3 18 1
输入的三个整数中 18 是最大的
```

**解析：**
在此处输入了三个输入值，即 3、18 和 1。在嵌套的 if else 语句中，如果第一个条件为真，它将检查内部条件。由于第一个条件不为真，控制流转到 else 块。在 else 块中满足了 if 条件，即 `if (18 > 1)`，因此 18 是作为最大数字的结果。

## 7.2.7 else-if 语句/阶梯的概念

else-if 语句用于按顺序检查条件，即一个接一个语句地检查。当条件列表中的任何条件变为真时，就不需要检查下一个条件。当第一个条件变为假时，它会一个接一个检查所有条件，直到某个变为真。当所有条件都为假时，默认执行 else 块。

> else-if 语句的语法为：

```c
if (condition1)
    Statement block1;
else if (condition2)
    Statement block2;
else if (condition-n)
    Statement block-n;
else
    Default statement;
Next statement;
```

else if 是将 else 语句与 if 语句安排的方式。让我们在框中查看差异：

```c
if (x = 1)
    printf("good morning");
else
{
    if (x = 2)
        printf("good evening");
}
```

```c
if (x = 1)
    printf("good morning");
else if (x = 2)
    printf("good evening");
```

![](img/15f2d3c4e623a0624f0481e94908bbcb_152_0.png)

## 7.2.8 else-if 语句/阶梯的一些实用编程示例

### Q1. 使用 else if 语句查找三个数中最大数字的 C 程序

**解决方案：**

```c
/********************************************************************
FILE NAME: elseif1.c
DETAILS: Mr. x, 1ST SEM, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
DATE OF PROGRAM EXECUTION: 3/8/2015
NAME OF THE PROGRAM: 使用 else if 语句查找三个数中最大数字的 C 程序
****************************************************/

#include <stdio.h>

void main(void)
{
    int x, y, z;

    printf("Input the three integer numbers: ");
    scanf("%d%d%d", &x, &y, &z);

    if (x > y && x >= z)
        printf("Among the inputted three integer numbers %d is the greatest %d", x);
    else if (y > x && y >= z)
        printf("Among the inputted three integer numbers %d is the greatest %d", y);
    else if (z >= x && z >= y)
        printf("Among the inputted three integer numbers %d is the greatest %d", z);
    else
        printf("All the three integer numbers are equal");
}
```

**输出：**
```
输入三个整数：3 10 6
三个整数中 10 是最大的
```

**解析：**
此处输入值为 x 为 3，y 为 10，z 为 6。每个条件都会检查这些输入。当任何一个条件满足时，停止检查后续条件，控制流不会移动到语句。在上方检查了第一个条件，即 3 不大于 y 也不大于 6，因此第一个条件不满足。它将检查第二个条件，即 `10 > 3 且 10 > 6`。由于该条件满足，它将打印 10 为最大。

### Q2. 使用 else-if 语句判断是否为闰年的 C 程序

**解决方案：**

```c
/********************************************************************
FILE NAME: elseif2.c
AUTHOR DETAILS: Mr. x, 1ST SEM, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
DATE OF PROGRAM EXECUTION: 3/8/2015
NAME OF THE PROGRAM: 使用 else if 语句判断是否为闰年的 C 程序
****************************************************/

#include <stdio.h>
#include <conio.h>

int main(void)
{
    int y;

    clrscr();
```
