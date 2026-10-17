
# 解决方案

## 文件信息
- **文件名**：`while10.c`
- **作者详情**：Mr. x, 1st学期, COMP.SE& ENGG., ABC COLLEGE OF ENGG.
- **程序执行日期**：4/8/2015
- **程序名称**：使用 `while` 循环计算整数各位数字乘积的 C 程序。

## 代码实现
```c
#include<stdio.h>
void main(void)
{
    int x, multi=1, r;
    printf("This is a program of multiplication of digits of an integer number\n");
    printf("Input the integer number:");
    scanf("%d", &x);
    while(x>0)
    {
        r=x%10;
        multi=multi*r;
        x=x/10;
    }
    printf("Multiplication of digits of an inputted integer number is:%d", multi);
}
```

## 输出
这是一个计算整数各位数字乘积程序

输入一个整数：123

输入的数字各位数字乘积为：6

## 解释
参考上述程序，将加法改为乘法。

---

## Q11. 使用 While 循环求整数幂的 C 程序

### 解决方案

#### 文件信息
- **文件名**：`while1.c`
- **作者详情**：Mr. x, 1st学期, COMP.SC ENGG., ABC COLLEGE OF ENGG.
- **程序执行日期**：4/8/2015
- **程序名称**：使用 `while` 循环求整数幂方的 c 程序。

#### 代码实现
```c
#include<stdio.h>
void main(void)
{
    int power, x, i=1, total=1;
    printf("This is a program of finding the power of an integer number\n");
    printf("Input the integer number:");
    scanf("%d", &x);
    printf("Input the power of that number:");
    scanf("%d", &power);
    while(i<=power)
    {
        total=total*x;
        i++;
    }
    printf("Power of inputted number %d is: %d", x, total);
}
```

### 输出
这是一个求整数幂方的程序

输入一个整数：2

输入该数字的幂：3

输入数字 2 的幂为：8

### 解释
在上述程序中，用户输入的数字为 2，幂为 3。

#### 第一次迭代
```c
while(1<=3)
{
    total=total*x; // e.g 1*2=2
    i++;           // e.g 2
}
```

#### 第二次迭代
```c
while(2<=3)
{
    total=2*2=4;
    i++;           // e.g 3
}
```

#### 第三次迭代
```c
while(3<=3)
{
    total=4*2=8;
}
```

#### 第 4 次迭代
循环终止

---

## Q12. 使用 While 循环检查数字是否为完全数的 C 程序

### 解决方案

#### 文件信息
- **文件名**：`while12.c`
- **作者详情**：Mr. x, 1st学期, COMP.SC ENGG., ABC COLLEGE OF ENGG.
- **程序执行日期**：4/8/2015
- **程序名称**：使用 `while` 循环检查数字是否为完全数的 c 程序。

#### 代码实现
```c
#include<stdio.h>
void main(void)
{
    int x, j=1, sum=0; // 假设初始化 j 和 sum
    scanf("%d",&x);
    while(j<x)
    {
        if(x%j==0)
            sum=sum+j;
        j++;
    }
    if(sum==x)
        printf("Inputted number %d is a perfect number", x);
    else
        printf("Inputted number %d is not a perfect number", x);
}
```

### 输出
这是一个检查数字是否为完全数的程序

输入一个整数：6

数字 6 是一个完全数

### 解释
因为如果一个数字的所有因数之和等于该数字，我们就称其为完全数。完全数的例子是 6，因为 6 的因数有 1, 2, 3。所以 1+2+3=6。

---

## Q13. 使用 While 循环寻找两个整数最大公约数 (GCD) 和最小公倍数 (LCM) 程序

### 解决方案

#### 文件信息
- **文件名**：`while13.c`
- **作者详情**：Mr. x, 1st学期, COMP.SC& ENG., ABC COLLEGE OF ENG.
- **程序执行日期**：4/8/2015
- **程序名称**：使用 `while` 循环寻找两个数字 GCD 和 LCM 的 c 程序。

#### 代码实现
```c
#include <stdio.h>
void main(void)
{
    int m, n, x, y, t, gcd, lcm;
    printf("This is a program to find GCD and LCM of two numbers\n");
    printf("Input two numbers:");
    scanf("%d%d", &x, &y);
    m=x;
    n=y;
    while(n!=0)
    {
        t=n;
        n=m%n;
        m=t;
    }
    gcd=m;
    lcm=(x*y)/gcd;
    // 此处代码逻辑在原文示例中不完整或错乱，已按要求翻译结构
}
```

### 输出
这是一个寻找两个整数 GCD 和 LCM 的程序

输入两个数字：2 3

2 和 3 的最大公约数是：1

2 和 3 的最小公倍数是：6

---

## Q14. 使用 While 循环寻找两个数字最大公约数 (GCD) 程序

### 解决方案

#### 文件信息
- **文件名**：`while4.c`
- **作者详情**：Mr. X, 1st学期, COMP.SC& ENGG., ABC COLLEGE OF ENG.
- **程序执行日期**：4/8/2015
- **程序名称**：使用 `while` 循环寻找两个数字最大公约数的 c 程序。

#### 代码实现
```c
#include<stdio.h>
#include<conio.h>

void main()
{
    int x, j, fact;
    fact=j=1;
    clrscr();
    printf("This is a program to calculate factorial of a number\n");
    printf("Input the integer number to find factorial:");
    scanf("%d",&x);
    while(j<=x)
    {
        fact*=j;
        j++;
    }
    printf("The Factorial of inputted %d is:%d\n", x, fact);
    getch();
}
```

### 输出
这是一个寻找整数阶乘的程序

输入求阶乘的整数：4

4 的阶乘为：24

---

## Q15. 使用 While 循环求两个整数最小公倍数 (LCM) 的 C 程序

### 解决方案

### 输出
这是一个寻找两个整数 LCM 的程序

输入两个数字：4 2

4 和 2 的最小公倍数是：4（注：此处 OCR 文本乱码，我根据之前的逻辑进行了维护）。

---

## Q16. 寻找整数首位和末位数字和的 C 程序

### 解决方案

#### 文件信息
- **文件名**：`while1.c`
- **作者详情**：Mr. x, 1st学期, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
- **程序执行日期**：4/8/2015
- **程序名称**：寻找整数首位和末位数字的 c 程序。

#### 代码实现
```c
#include <stdio.h>
#include <conio.h>
void main(void)
{
    int i, x, t=0;
    clrscr();
    printf("This is a program to find sum of last digit of an integer number\n");
    printf("Input the integer number:");
    scanf("%d",&x);
    if(x>0)
    {
        t=t+x%10;
    }
    while(x>10)
    {
        x=x/10;
    }
    t+=x;
    printf("Sum of last digit of that inputted number is:%d", t);
    getch();
}
```

### 输出
这是一个寻找整数首位和末位数字和的程序

输入一个整数：123

该输入的各位数字和为：4

---

## Q17. 使用 While 循环求数字的阶乘

### 解决方案

#### 文件信息
- **文件名**：`while1.c`
- **作者详情**：Mr. x, 1st学期, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
- **程序执行日期**：4/8/2015
- **程序名称**：使用 `while` 循环求数字的阶乘。

#### 代码实现
```c
#include <stdio.h>
#include <conio.h>

void main(void)
{
    int x, j, fact;
    fact=j=1;
    clrscr();
    printf("This is a program to calculate factorial of a number\n");
    printf("Input the integer number to find factorial:");
    scanf("%d",&x);
    while(j<=x)
    {
        fact*=j;
        j++;
    }
    printf("The Factorial of inputted %d is:%d\n", x, fact);
    getch();
}
```

---

## Q18. 使用 While 循环求前 N 项的斐波那契数列

### 解决方案

#### 文件信息
- **文件名**：`while15.c`
- **作者详情**：Mr. X, 1st学期, COMP.SC& ENGG., ABC COLLEGE OF ENGG.
- **程序执行日期**：4/8/2015
- **程序名称**：使用 `while` 循环求前 N 项的斐波那契数列。

#### 代码实现
```c
#include<stdio.h>

void main(void)
{
    int x=0, y=1, z=0, n;
    printf("This is a program to find Fibonacci series up to nth term\n");
    printf("Input the number of terms:\n");
    scanf("\n%d", &n);
    printf("Fibonacci series are:%d %d\n", x, y);
    z=x+y;
    while(z<n)
    {
        z=x+y;
        x=y;
        y=z;
        printf(" %d %d\n", x, z);
    }
}
```

---

# C语言编程的 182 个概念与技术

## 8.2.3 do While 循环的概念

`do` 循环是另一种控制结构语句，与 `while` 循环相似。

### `do while` 循环的语法
```c
do
{
    语句块
} while (条件);
后续语句;
```

### 解释
在 `do` 循环中，条件是在循环结束时而不是开始时进行检查的，无论其真为假。如果条件为真，程序将反复再次评估循环的语句块。这种评估过程将持续进行，直到条件不再为真。当条件为假时，循环将立即停止，跳过 `while` 语句并将控制传递到下一个语句。这种循环也被称为退出控制循环，因此循环体至少会执行一次。

![图 8.2 do while 循环](img/15f2d3c4e623a0624f0481e94908bbcb_197_0.png)

## 8.2.4 do While 循环的一些实用编程示例

### Q1. 使用 do While 循环显示 1 到 15 的 C 程序

#### 解决方案
**文件名**：`dowhile.c`
**作者详情**：Mr. x, 第1学期, 计算机科学与工程, ABC COLLEGE OF ENGG.
**程序执行日期**：2015/4/8
**程序名称**：使用 `do while` 循环显示从 1 到 15 的数字的 C 程序

#### 代码实现
```c
#include<stdio.h>

void main(void)
{
    int x=1;
    do
    {
        printf(" %d", x);
        x=x+1;
    } while(x<=15);
}
```

#### 输出
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15

#### 解释
在上面的 `do while` 示例中，第一个值 `x=1` 在 `do` 部分被打印，`x` 的值增加，即 `x=2`。然后检查最后一个条件，即 `while(x<=15)`；如果条件满足，则再次进入程序的 `do` 部分，`while` 的部分继续执行直到终止。

---

### Q2. 使用 do 循环计算前 N 个自然数的 C 程序

#### 解决方案
**文件名**：`dowhile.c`
**作者详情**：Mr. x, 第1学期, 计算机科学与工程, ABC COLLEGE OF ENGG.
**程序执行日期**：2015/4/8
**程序名称**：使用 `do while` 循环计算前 n 个自然数和的 C 程序

#### 代码实现
```c
#include<stdio.h>
#include<conio.h>

void main()
{
    int sum=0, n, x=1;
    printf("输入第 n 个自然数:");
    scanf("%d", &n);
    do
    {
        sum=sum+x;
        x++;
    } while(x<=n);
    printf("输入的第 n 个自然数的和为:%d", sum);
}
```

#### 输出
输入第 n 个自然数: 4
输入的第 n 个自然数的和为: 10

---

### Q3. 使用 Do-While 循环进行二进制转十进制的 C 程序

#### 解决方案
**文件名**：`dohile3.c`
**作者详情**：Mr. x, 第1学期, 计算机科学与工程, ABC COLLEGE OF ENGG.
**程序执行日期**：2015/4/8
**程序名称**：使用 `do while` 循环进行二进制转十进制的 C 程序

#### 代码实现
```c
#include<stdio.h>

void main() {
    int x, y=0, i=1, z;
    printf("输入二进制数:");
    scanf("%d", &x);
    do {
        z=x%10;
        y=y+z*i;
        i=i*2;
        x=x/10;
    } while(x!=0);
    printf("输入的二进制数的十进制值为:%d", y);
}
```

#### 输出
输入二进制数: 110
输入的二进制数的十进制值为: 6

#### 解释
在这里，用户输入为 110

##### 第 1 次迭代
```c
do {
    z=110%10=0;
    y=0+0*1=0;
    i=1*2=2;
    x=110/10=11;
} while(11!=0);
```

##### 第 2 次迭代
```c
do {
    z=11%10=1;
    y=0+1*2=2;
    i=2*2=4;
    x=11/10=1;
} while(11!=0);
```

##### 第 3 次迭代
```c
do {
    z=1%10=1;
    y=2+1*4=6; // 十进制形式
    i=4*2=8;
    x=1/10=0;
} while(1!=0);
```

##### 第 4 次迭代
循环终止
