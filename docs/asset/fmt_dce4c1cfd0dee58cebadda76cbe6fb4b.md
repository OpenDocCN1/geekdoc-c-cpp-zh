
```c
#include <stdio.h>
#include <conio.h>

void main()
{
    int i;
    long digit, term, pos, neg;
    clrscr();

    i=1;
    pos=0;
    digit=1;
    while(i<=25)
    {
        term=digit*digit; //此处原文为*，但根据逻辑应为*
        pos=pos+term;
        i++;
    }
    i=3;
    digit=3;
    while(i<=25)
    {
        term=digit*digit;
        neg=neg+term;
        i++;
    }
    sum=pos-neg;
    printf("Sum of series = %ld",sum);
    getch();
}
```

# Q.5 (f) 程序

```c
#include <stdio.h>
#include <conio.h>

void main()
{
  int num1=0,num2=1,n,fib;
  clrscr();

  printf("\enter the value of n: %d");
  scanf("%d",&n);

  for(i = 1; i <= n-2; i++)
  {
    fib=num1 + num2;
    num1=num2;
    num2=fib;
  }

  printf("\nthonacci number (for n = %d) = %d",n,fib);
  getch();
}
```

# Q.5 (g) 程序

```c
#include <stdio.h>
#include <conio.h>

void main() {
    char str[50][30]
}
```

# 答案解析 (Solved Question Paper)

B. Tech.

(SEM. 1) 秋季考试

2010-11

# 计算机概念与 C 语言编程

时间：3 小时    总分：100

说明：(1) 本试卷包含三个部分。

(2) 完成所有题目。

# 第一部分 (SECTION-A)

## 1. 有 10 道单选题。只有一个正确答案：(10 × 1 = 10)

- (a) 以下哪项不是操作系统？
  (A) Linux (B) JAVA (C) DOD (D) WINDOWS
- (b) 高级语言编写的程序通过什么转换为机器码：
  (A) 操作系统 (B) 汇编器 (C) 编译器 (D) 机器语言
- (c) 以下哪项在执行时不使用条件？
  (A) 循环 (B) Case (C) 函数 (D) 决策
- (d) 以下哪项不是二进制数？
  (A) 0 (B) 1 (C) 2 (D) 10
- (e) 以下哪项用于包含 I/O 函数库？
  (A) include #io.h> (B) include <stdio.h> (C) include <stdio.h> (D) 以上都不是
- (f) 以下哪项是 IF THEN ELSE 语句中检查条件的正确语句？
  (A) IF (A = B) (B) IF (A = B) (C) IF (A & B) (D) IF (A * B)
- (g) 使用哪个关键字定义结构？
  (A) structure (B) STRUCTURE (C) STRUCT (D) 以上都不是
- (h) 栈（stack）使用哪种输入输出方法？
  (A) 先入先出 (B) 先入后出 (C) A&B (D) 以上都不是
- (i) A[5][5] 数组中有多少元素？
  (A) 5 (B) 25 (C) 50 (D) 以上都不是
- (j) 在 C 程序中，语句 (i=0;i<5;i++) 将循环循环：
  (A) 4 次 (B) 5 次 (C) 6 次 (D) 以上都不是

## 2. 判断以下陈述对或错 (5 × 1 = 5)

- (a) C 语言中的标识符必须以字母或下划线开头。不允许有空格或连字符。
- (b) 数组所有元素的初始化可以在声明时完成。
- (c) 列表（List）是非线性数据结构。
- (d) C 语言中的函数不能被其他函数调用。
- (e) 数组名是指向第一个元素的指针，而不是整个数组。

## 3. 填空：(5 × 1 = 5)

- (a) `________` 从键盘读取数据。
- (b) `________` 是一系列运算符和操作数的序列，可还原为单个值。
- (c) 语句 `________` 将 `pa` 声明为字符变量的指针。
- (d) 模式 `________` 以只读打开现有文件。
- (e) `________` 是 C 预处理器的预定义宏。

# 第二部分 (SECTION-B)

# 4. 有七 (07) 部分。完成任意五 (05) 部分。(6 × 5 = 30)

(i) 搜索和排序之间有什么区别？编写一个算法对包含十个数字的列表进行排序。

(ii) 数组（Array）和结构体（Structures）之间有什么区别？请举例说明。

(i) 什么是指针？在 C 语言中如何声明指针？请用合适的示例进行说明。

(ii) 写一个 C 语言程序段，使用指针交换两个变量的值。

(i) 栈（Stack）和列表（List）之间有什么区别？解释如何从栈和列表中删除元素。

(ii) 什么是 C 预处理器？请给出任意两个预处理器指令的示例。

## C 部分 (SECTION-C)

5. 本部分包含七（07）道编程题。尝试其中五（05）题。（5 × 10 = 50）

- (a) 绘制流程图并用 C 语言编写一个函数计算给定数的阶乘，并编写一个程序使用上述函数计算以下数列的和：S=1! + 2! + 3! + ... + N!
- (b) 写一个 C 语言程序，接受一个百人规模的学生的学号、姓名，以及他们在物理、化学和数学科目上的得分。按成绩优劣顺序打印前十名学生的学号和姓名。成绩优劣的依据是这三门科目分数的总和。
- (c) 写一个 C 语言程序，接受矩形的长度和宽度并打印面积。矩形的面积通过一个函数计算并将其值返回给主程序进行打印。矩形的长度和宽度从键盘读取。同时给出流程图和算法。
- (d) 写一个 C 语言程序，计算以下级数的前 $n^{th}$ 项和：F(x)=x^1 - x^2 + x^3 - x^4 + ...
- (e) 绘制流程图并用 C 语言编写一个程序，计算两个大小为 $N \times N$ 的矩阵 A 和 B 的乘积。
- (f) 绘制流程图并用 C 语言编写一个程序，计算前 100 项斐波那契数列的和。
- (g) 使用动态内存分配，写一个 C 语言程序接受一个 $3 \times 3$ 矩阵的元素并打印其转置。

## Q.18 计算机概念与 C 语言编程

## 卷答案

## A 部分 (SECTION-A)

- 1. 单选题答案
  - (a) B (b) C (c) C (d) C (e) C (f) A (g) C (h) B (i) B (j) B
- 2. 判断题答案
  - (a) 正确 (b) 正确 (c) 错误 (d) 错误 (e) 正确
- 3. 空空题答案
  - (a) `scanf` (b) `expression` (c) `char *pa;` (d) `r` (e) `_FILE_`

## B 部分 (SECTION-B)

- 4. (a)

### GUI 与 CUI 界面的区别

| GUI | CUI |
| --- | --- |
| 代表图形用户界面。 | 代表命令行用户界面。 |
| 它在屏幕上呈现图形界面，用户通过界面与计算机系统交互。 | 它在屏幕上呈现命令行界面，用户通过界面与计算机系统交互。 |
| 它通过指向设备（如鼠标）以及键盘接收指令。 | 它仅通过键盘接收指令。 |
| 支持 GUI 的操作系统示例有 Windows、Linux、Mac OS 等。 | 支持 MUI 的操作系统示例有 DOS、Unix 等。 |

- (ii) 十进制转二进制

### 575

给定的十进制数为 575。下表列出了将该十进制数转换为二进制等值的步骤：

| 十进制数 | 除数 | 商 | 余数 |
| --- | --- | --- | --- |
| 575 | 2 | 287 | 1 |
| 287 | 2 | 143 | 1 |
| 143 | 2 | 71 | 1 |
| 71 | 2 | 35 | 1 |
| 35 | 2 | 17 | 1 |
| 17 | 2 | 8 | 1 |
| 8 | 2 | 4 | 0 |
| 4 | 2 | 2 | 0 |
| 2 | 2 | 1 | 1 |
| 1 | 2 | 0 | 1 |

现在，从上往下读取表中计算出的余数以获得二进制值，即 10001111。因此，$(575)_{10} = (10001111)_2$。

### 311.55

给定的十进制数为 311.55。下表列出了转换小数部分（311）的步骤：

| 十进制数 | 除数 | 商 | 余数 |
| --- | --- | --- | --- |
| 311 | 2 | 155 | 1 |
| 155 | 2 | 77 | 1 |
| 77 | 2 | 38 | 1 |
| 38 | 2 | 19 | 0 |
| 19 | 2 | 9 | 1 |
| 9 | 2 | 4 | 1 |
| 4 | 2 | 2 | 0 |
| 2 | 2 | 1 | 1 |

## (ii) 数组与结构体的区别

| 数组 (ARRAY) | 结构 (STRUCTURE) |
|---|---|
| 数组是相同类型相关数据元素的集合。 | 结构是逻辑相关项的集合，可以是不同类型。 |
| 数组是一种派生数据类型。 | 结构是程序员定义的数据类型。 |
| 数组具有类似于内置的数据类型，我们只需要声明数组变量并使用它。 | 结构需要先进行设计和声明，才能声明并使用该类型的变量。 |

示例：

`int a[3] = {1,2,3};`

示例：

```c
struct test {
int a;
char b;
float c;
}
struct test t1;
t1.a = 99;
t1.b = 'c';
t1.c = 88.79;
```

## 4. (f) 指针及其声明

(i) 参见节 13.1 和 13.4 

(ii) 程序

```c
#include <stdio.h>
#include <conio.h>

void swap(int*,int*);
void main() {
int num1,num2;
num1=10;
num2=20;
printf("Before Swap: %d\tnum1 = %d\tnum2 = %d",num1,num2);

swap(&num1,&num2);

printf("\nAfter Swap:\num1 = %d\tnum2 = %d",num1,num2);

getch();
}
```

## Q.24 计算机基础与C语言编程

```c
void swap(int *n1, int *n2)
{
    int temp = *n1;
    *n1 = *n2;
    *n2 = temp;
}
```

输出

Before Swap:

num1 = 10 num2 = 20

After Swap:

num1 = 20 num2 = 10

## 4. (g) 栈与列表的区别

| 栈 (STACK) | 列表 (LIST) |
| --- | --- |
| 栈将元素的插入或删除限制在列表的一个特定位置，即栈顶。 | 数组提供了在列表任何位置添加或删除数据元素的灵活性，即开头或中间的任何位置。 |
| 栈的使用场景存在于高级问题的解决方案中，例如递归控制、表达式求值等。 | 通过使用数组，程序员可以实现需要记录分组的常见场景，例如库存管理、员工记录管理等。 |

## 从栈和列表中删除元素

从列表中删除元素需要对相邻元素进行适当的移动，以填补被删除元素的位置。或者，从栈中删除元素需要更新栈指针，以确保它指向栈中的下一个栈顶元素。

## (ii) 预处理器

预处理器的功能是在源代码通过编译器之前对其进行处理。它在预处理器命令行和指令的控制下运行。预处理器指令被放置在源程序的主块之前。源代码在传递给编译器之前，会由预处理器检查是否存在任何预处理器指令。如果存在，则会（根据指令）采取适当的操作，然后将源程序交给编译器。预处理器指令分为三类：

- 宏替换指令
- 文件包含指令
- 预处理器条件指令

## 预处理器指令

参见节 16.2 和 16.3

## 5. (a) 流程图

![](img/38c1ca180054ae68e900b256db416b54_526_0.png)

## 计算数字阶乘的函数

```c
long factorial(int n)
{
  long fact;
  if (n == 0 )
    return(1);
  else
    fact = n*factorial(n - 1);
}
```

## 程序

```c
#include <stdio.h>
#include <conio.h>

long factorial(int);
void main(){
  long S=0;
  int i;
get();
}
```

## Q.26 计算机基础与C语言编程

```c
long factorial(int n)
{
  long fact;
  if(n == 0)
    return(1);
  else
    fact = n*factorial(n - 1);
  return(fact);
}
```

输出

Sum of series = 15

## 5. (b) 程序

```c
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
void main()
{
  struct student
  {
    char name[15];
    int rollino;
    int phy,che,mat;
    int merit;
  };
  struct student st[100];
  int count=0;
  int i,j;
  for(i=0;i<100;i++)
  {
    fflush(stdin);
    printf("enter the name of student %d: ",i+1);
    gets(st[i].name);
    fflush(stdin);
    printf("Enter the rollino of student %d: ",i+1);
    scanf("%d",st[i].rollino);
    printf("Enter physics marks: ");
    scanf("%d",st[i].phy);
    printf("Enter chemistry marks: ");
    scanf("%d",st[i].che);
    printf("Enter maths marks: ");
    scanf("%d",st[i].mat);
  }
  for(i=0;i<100;i++)
  {
    st[i].merit=(st[i].phy+st[i].mat)/3;
  }
  printf("\nThe top 10 students are:\n");
  for(j=100;j>0;j--)
  {
    for(i=0;i<100;i++)
    {
        if(st[i].merit==j)
        {
            printf("%s %d\n",st[i].name,st[i].rollino);
            count++;
        }
        if(count==10)
        {
            printf("Press any key to exit the program.");
            getch();
            exit(1);
        }
    }
  }
}
```

## 5. (c) 程序

```c
#include <stdio.h>
#include <conio.h>

int area(int,int);
void main()
{
int length, width;
int a;
printf("Enter the length and width of the rectangle\n");
scanf("%d %d",&length,&width);

a=area(length,width);
printf("Area = %d\n",a);
getch();
}

int area(int l, int w)
{
int ar=l*w;
return(ar);
}
```

## Q.8 计算机基础与C语言编程

# 算法

- Step 1 - 开始
- Step 2 - 接收矩形的长度和宽度 (length,width)
- Step 3 - 调用 area(length,width)
- Step 4 - 显示函数返回的值 (length,width)
- Step 5 - 停止

area(l,w)

- Step 1 - 开始
- Step 2 - 计算 ar=l*w
- Step 3 - 返回 ar

### 流程图

![](img/38c1ca180054ae68e900b256db416b54_529_0.png)

## 5. (d) 程序
