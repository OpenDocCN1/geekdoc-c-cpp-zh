
# C 语言循环与无条件语句习题解析

## 循环结构习题

### 16. 输出是什么？

```c
#include <stdio.h>

void main(void)
{
  int x=0;
  for ( ; ;x)
    printf("INDIA\n");
}
```

**输出：**
```
INDIA
ODISHA
```

### 17. 输出是什么？

```c
#include <stdio.h>

void main(void)
{
    for(x=0;x<2)
    printf("INDIA\n");
}
```

**输出：**
```
INDIA
INDIA
```

### 18. 输出是什么？

```c
#include <stdio.h>

void main(void)
{
    int y=1,z=1;
    for(y;z;printf("%d\n",y))
    {
        z=y++;
    }
}
```

**输出：**
```
2
3
4
5
6
7
8
```

### 19. 输出是什么？

```c
#include <stdio.h>

void main(void)
{
    short int y=0;
    for(y<=5&&y>=-1; ++y)
        printf("%u",y);
}
```

**输出：**
无限循环

### 20. 输出是什么？

```c
#include<stdio.h>

void main(void)
{
    for(int x=0;x<=5;x++)
    printf("%d",x);
}
```

**输出：**
```
6
```

### 21. 输出是什么？

```c
#include<stdio.h>

void main(void)
{
    for(int x=0;x<=6;x++)
    printf(" %d",x);
}
```

**输出：**
```
0 1 2 3 4 5
```

### 22. 输出是什么？

```c
#include<stdio.h>

void main(void)
{
    int x=0;
    for(;;x++);printf("%d",x);
}
```

**输出：**
```
1
```

### 23. 输出是什么？

```c
#include<stdio.h>

void main(void)
{
    int x=1;
    for(;x<=4;x++)
    {
        printf("%d ",x);
    }
}
```

**输出：**
```
1 2 3 4 
```

### 24. 输出是什么？

```c
#include <stdio.h>

void main(void)
{
    int x;
    for(x++;
    printf(x);
    n*(n+1)/2.
}
```

**输出：**
```
n*(n+1)/2.
```

### 25. 解释 C 语言中的循环结构。

---

# 9 无条件语句

## 9.1 简介

无条件语句是仅当程序在不检查测试条件下跳转到程序的另一部分时使用的语句。这些语句中断程序的顺序执行。无条件语句的示例有：`break`、`goto`、`continue`、`exit(0)`。

### 9.1.1 break 语句

`break` 语句用于 `while`、`do while`、`for` 循环或 `switch` 语句。当在循环内部识别到 `break` 语句时，它会立即停止循环，程序控制从循环后的后续语句继续。`break` 语句通常与 `if` 语句关联。

> **break 语句的语法：**
> ```c
> break;
> ```

> **记忆技巧**  
> 解决方案：`break` 仅在 `if` 语句写在循环内部时与 `if` 语句配合使用。

#### break 语句示例

**Q1. 使用 break 语句检查数字是否为质数的程序。**

```c
/************************************************************************************************************************************
FILE NAME: uncl.c
## 无条件语句

作者详情：x 先生，第一学期，计算机科学与工程专业，ABC 工程学院
程序执行日期：2015年5月8日
程序名称：使用 break 语句检查数字是否为质数的 C 程序
************************************************************************************************************************************/

#include<stdio.h>

void main(void) {
    int x,j;
    printf("Input the number:");
    scanf("%d",&x);
    j=2;
    while(j<=x-1) {
        if (x%j==0) {
            printf("Inputted %d is not a prime",x);
            break;
        }
        j++;
    }
    if(j==x)
    printf("Inputted %d is a prime number",x);
}
```

**输出：**
```
Input the number: 3
Input 3 is a prime number
```

**解释：**  
在上述程序中，当找到 `break` 语句时，它会停止循环或 `if` 语句。如果我们移除 `break` 语句，上述程序将显示两个语句。

**示例：**
```
Input the number: 4
Input 4 is not a prime number
Input 4 is a prime number
```

## 9.1.2 goto 语句

`goto` 语句用于无条件地从程序的某部分跳转到程序的另一部分。在 C、C++、Java 等高级编程语言中，使用 `goto` 语句可能并非必需。但在编程语言中，它有时是有用的。

`goto` 语句需要一个标签（label）来搜索要跳转的位置。标签是一个变量，后面必须跟一个冒号。标签可以放置在程序的任何位置。基本上，它可以放置在 `goto` 标签语句之前，也可以放在之后。当标签放置在 `goto` 标签语句之前时，将生成循环并重复执行该语句。这种跳转被称为“向后跳转”（backward jump）。如果标签放置在 `goto` 语句之后，某些语句将被跳过，这种跳转被称为“向前跳转”（forward jump）。

**向前跳转**
```c
goto label;
block of statements;
label:
statement-1;
```

**向后跳转**
```c
label:
statement-1;
block of statements;
goto label;
```

![](img/15f2d3c4e623a0624f0481e94908bbcb_225_0.png)

在向前跳转的情况下，光标在执行 `goto` 标签语句后直接到达 `statement-1`，并跳过语句块。在向后跳转的情况下，`statement-1` 和语句块将被重复执行。

> **记忆技巧：** 在编程中不要使用 `goto` 语句。如果某个程序难以调试，则可以使用它。

#### Q2 使用 goto 语句显示 1 到 15 数字的 C 程序。

```c
/********************************************************************
文件名：unc2c
作者详情：x 先生，第一学期，计算机科学与工程专业，ABC 工程学院
程序执行日期：2015年5月8日
程序名称：使用 goto 语句显示 1 到 15 数字的 C 程序
********************************************************************/

#include<stdio.h>

void main(void)
{
    int x=0;
    y:
    x++;
    printf("%d\t",x);
    if(x<=15)
        goto y;
}
```

**输出：**
```
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
```

**解释：**  
此程序是一个向后跳转的 `goto` 语句。

## 9.1.3 continue 语句

在执行循环时，有时需要在某些特定条件下跳过循环体内部的一些语句。在这种情况下，`continue` 语句非常有用。`continue` 语句向编译器提供信息，在跳过循环体部分中间的语句后，从下一次迭代继续循环。因此，`continue` 关键字之后的语句将不会执行，而 `continue` 之前的语句将执行。如果在 `while` 和 `do` 循环中使用 `continue` 语句，控制将移动到循环的条件部分，然后继续该循环。如果在 `for` 循环中使用 `continue` 语句，控制将移动到循环的增量部分以便在测试条件之前执行。

**continue 的语法：**
```c
continue;
```

**循环内部 continue 语句的语法：**
```c
1)
while (condition1)
{
  if(condition2)
  continue;
}

2)
do
{
  if(condition1)
  continue;
}
while (condition2);

3)
for(initialization; condition; increment/decrement)
{
  if(condition1)
  continue;
}
```

#### Q3. 使用 continue 语句寻找 1 到 15 奇数的 C 程序。

```c
/********************************************************************
文件名：Unc3.C
作者详情：X 先生，第一学期，计算机科学与工程专业，ABC 工程学院
程序执行日期：2015年5月8日
程序名称：使用 continue 语句寻找 1 到 15 奇数的 C 程序
********************************************************************/

#include <stdio.h>

void main(void)
{
    int x;
    for (x=1;x<=15;x++)
    {
        if(x%2==0)
        {
            continue;
            printf("GCE, KEONHAR");
        }
        else
        {
            printf("%d\t",x);
        }
    }
}
```

**输出：**
```
1 3 5 7 9 11 13 15
```

**解释：**  
在上述程序中，`2%2==0` 条件满足，开始执行 `if` 语句。由于在 `continue` 语句之前没有语句，在这种情况下控制跳转到增量部分并进行下一次迭代。这里，`printf` 语句不会打印 "GCE, KEONHAR" 消息，因为它写在 `continue` 语句之后。

#### Q4. continue 语句的 C 程序。

```c
/********************************************************************
文件名：unc4.c
作者详情：X 先生，第一学期，计算机科学与工程专业，ABC 工程学院
程序执行日期：2015年5月8日
程序名称：continue 语句的 C 程序
********************************************************************/

#include<stdio.h>

void main(void)
{
    int x;
    for (x=1;x<=15;x++)
    {
        if(x%2==0)
        {
            continue;
            printf("GCE, KEONHAR");
        }
        else
        {
            printf("%d\t",x);
        }
    }
}
```

**输出：**
```
1 3 5 7 9 11 13 15
```

**解释：**  
在上述程序中，`2%2==0` 条件满足，开始执行 `if` 语句。由于在 `continue` 语句之前没有语句，在这种情况下控制跳转到增量部分并进行下一次迭代。这里，`printf` 语句不会打印 "GCE, KEONHAR" 消息，因为它写在 `continue` 语句之后。

## 9.1.4 exit() 语句

使用 `break` 或 `goto` 语句跳出循环。类似地，程序员可以使用库函数 `exit()` 跳出程序，`exit()` 函数接受一个整数值作为参数。通常用 `0` 表示终止。我们可以这样写该函数：

| exit() 的通用形式为： |
| :--- |
| `exit(int);` |

**示例：**
```c
exit(0);
```

#### Q5. exit() 函数的示例。

```c
/********************************************************************
文件名：unc5.c
作者详情：x 先生，第一学期，计算机科学与工程专业，ABC 工程学院
程序执行日期：2015年5月8日
程序名称：exit() 函数的示例
********************************************************************/

#include <stdio.h>
#include <stdlib.h>

int main (void)
{
    printf("I LOVE MY INDIA\n");
    printf("I AM PROUD TO BE AN INDIAN\n");
    exit(0);
    printf("THANKS\n");
    return(0);
}
```

**输出：**
```
I LOVE MY INDIA
AM PROUD TO BE AN INDIAN
```

**解释：**  
在上述示例中，`exit(0)` 函数在放置时会停止程序执行。因此，消息“thanks”不会被打印。

#### Q6. 使用函数的 exit 函数示例。

```c
/******************************************************************
文件名：unc6.c
作者详情：x 先生，第一学期，计算机科学与工程专业，ABC 工程学院
程序执行日期：2015年5月8日
程序名称：使用函数的 exit 函数示例。
******************************************************************/

#include <stdio.h>
#include <stdlib.h>

void x(void)
{
    printf("I am user-defined function");
    exit(0);
}

void main(void)
{
    x();
    printf("I am main function");
}
```

**输出：**
```
I am user-defined function
```

---

## 总结

1. `continue` 语句用于继续循环。`continue` 之后的语句将不会执行，而 `continue` 之前的语句将执行。
2. `goto` 是一种无条件语句，可以将控制流转移到程序的另一个部分。
3. `break` 语句用于终止 `switch` 语句或循环，并将控制立即转移到该循环或 `switch` 语句之后的后续语句。
4. `exit(0)` 函数用于退出程序。

## 简答

1. 无条件语句的作用是什么？
2. 什么是 `break` 语句？写出它的语法。
3. 什么是 `continue` 语句？给出它的语法。
4. 什么是 `goto` 语句？
5. 什么是 `exit` 函数？

## 论题

1. 条件语句和无条件语句之间有什么区别？给出合适的例子。
2. 为以下内容编写短记：
   - (a) `continue` 语句，
   - (b) `goto` 标签语句
   - (c) `break` 语句

## 单选题及答案

### 1. 输出结果是什么？

```c
#include <stdio.h>

void main(void)
{
    int x=5;
    if(x==5)
    {
        printf("INDIA");
        continue;
    }
}
```

**输出：**
```
编译时错误
```

**解释：**  
`continue` 语句仅适用于循环中。因此，发生了编译错误。

### 2. 输出结果是什么？

```c
#include <stdio.h>

void main(void)
{
    int x=1;
    do {
        x++;
        if (x==4)
        {
            printf("INDIA");
            continue;
        }
    } while (x<4);
}
```

**输出：**
```
INDIA
```

### 3. 输出结果是什么？

```c
#include <stdio.h>

void main(void)
{
    int x=0,y=0;
    for(x;x<2;x++)
    {
        for(y;y<3;y++)
        {
            printf("*\n");
            break;
        }
        printf("*\n");
    }
    printf("INDIA\n");
}
```

**输出：**
```
*
*
*
*
INDIA
```

### 4. 输出结果是什么？

```c
#include <stdio.h>
```
