

## 示例

```c
for (i = 0; i<10; i = i+1)
{
printf("%d",i);
}
```

for 循环将执行 10 次。每次都会打印出一个等于 i 当前值的数值。

循环语句的各种形式如下：

- (a) `for(condition;increment/decrement)`

    `body;`

    第一个语句留空表示不进行初始化。

- (b) `for(initialization;condition;)`

    `body;`

    最后一个语句留空表示不执行递增/递减。

- (c) `for(initialization;increment/decrement)`

    `body;`

    第二个条件语句留空表示没有控制循环退出的测试条件。因此，在缺少第二个语句的情况下，需要在循环体内测试条件，否则会导致无限循环，控制永远无法退出循环。

- (d) `for(;;increment/decrement)`

    `body;`

    初始化需要在循环之前完成，测试条件在循环体内检查。

- (e) `for(initialization;;)`

    `body;`

    测试条件和控制变量的递增/递减需要在循环体内完成。

- (f) `for(;condition;)`

    `body;`

    初始化需要在循环之前完成，控制变量的递增/递减需要在循环体内完成。

- (g) `for(;;)`

    `body;`

    初始化需要在循环之前完成，测试条件和控制变量的递增/递减需要在循环体内完成。

## for 循环的附加特性

1. 在 for 语句中可以同时初始化多个变量。
   例如：
   `for (p=1,q=0; n<18; ++n)`

2. 与初始化部分一样，递增部分也可以有多个部分。
   例如，
   `for (a=2,b=30; n <= m; n=n+1,m=m-1)`

   ```c
   {
   p = b/a;
   printf("%d",p);
   }
   ```

3. 在初始化部分和递增部分的赋值语句中使用表达式也是允许的。
   例如
   `for (w = (a+b); w>0; w=w/2) is valid.` 是有效的。

4. 如有必要，for 语句中的一个或多个部分可以省略。
   例如，
   `e = 2;`
   `for (; e != 10 ;)`

   ```c
   {
   printf("%d",e);
   e = e + 2;
   }
   ```

在 for 语句中，初始化部分和递增部分都被省略了。在这种情况下，这些部分留空。但是，分隔各部分的分号必须保留。如果测试条件不存在，for 语句将构成一个无限循环。

## 编程问题

### 问题 1

编写一个程序，借助 for 循环只打印从 1 到 100 的数字。

### 解决方案

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
for(i=1;i<=100;i++)
printf("%d\n",i);
getch();
}
```

```c
if(i%2==1)
printf("\n%d",i);
}
getch();
}
```

### 问题 2

编写一个程序，借助 for 循环打印从 100 到 1 的数字。

### 解决方案

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
for(i=100;i>=1;i--)
printf("\n%d",i);
getch();
}
```

### 问题 3

编写一个程序，借助 for 循环只打印从 1 到 100 的偶数。

### 解决方案

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
for(i=1;i<=100;i++)
{
if(i%2==0)
printf("\n%d",i);
}
getch();
}
```

### 问题 4

编写一个程序，借助 for 循环只打印从 1 到 100 的奇数。

### 解决方案

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i;
for(i=1;i<=100;i++)
{
if(i%2==1)
printf("\n%d",i);
}
getch();
}
```

### 问题 5

使用 for 循环生成“N”个自然数的程序。

### 解决方案

```c
#include < stdio.h >
void main()
{
int n, i; //Declare and initialize the variables
printf("Enter the upper limit number"); // Message to the user
scanf("%d", &n); //read and store the number
for(i=1;i<=n;i++)
printf("\n%d",i);
getch();
}
```

### 问题 6

编写一个程序，输入一个数字，并借助 for 循环打印该数字的位数。

### 解决方案

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,digit=0;
clrscr();
printf("\n enter the number");
scanf("%d",&n);
for(;n>0;n=n/10)
{
digit++;
}
printf("\n the number of digits are %d",digit);
getch ();
}
```

### 问题 7

编写一个程序，输入一个数字，并借助 for 循环打印该数字各位数字之和。

### 解决方案

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int n,sum=0,r;
clrscr();
printf("\n enter the number");
scanf("%d",&n);
for(;n>0;n=n/10)
{
r=n%10;
sum=sum+r;
}
printf("\n the sum is %d",sum);
getch();
}
```

### 示例

编写一个程序，生成下面给出的模式：

- 1
- 1 2
- 1 2 3
- 1 2 3 4

```c
/* Program to print the pattern */
#include<stdio.h>
#include<conio.h>
void main()
{
int i,j;
clrscr();
for (i=1;i<=4;++i)
{
printf("%d \n",i);
for(j=1;j<=i;++j)
printf("%d ",j);
}
getch();
}
```

## 嵌套循环

嵌套循环是在一个循环中包含另一个循环语句的循环。这类循环用于创建矩阵。任何循环都可以在自身中包含多个循环语句。如果我们在循环中使用循环，就称为嵌套循环。其中，外层循环用于计算行数，内层循环用于计算列数。

嵌套循环的一般语法如下：

```c
for (initializing ; test condition ; increment / decrement) //Outer Loop
{
statement;
for (initializing ; test condition ; increment / decrement) // Inner Loop
{
body of inner loop;
}
statement;
}
```

嵌套循环的执行过程如下：

首先执行外层循环，根据外层循环执行内层循环，再根据内层循环执行语句。当内层循环终止时，指针会自动转到外层循环；当外层循环终止时，整个循环终止。

这里，*内层 for 循环* 编写在 *外层 for 循环* 内部。对于每一个 *i* 值，*j* 从 1 取值到 i，然后 i 的值递增，外层循环进入下一次迭代，j 的取值范围再次从 1 到 i。

## 编程问题

### 问题 1

编写一个程序，打印从 1 到 10 的乘法表。

### 解决方案

```c
#include<stdio.h>
#include<conio.h>
void main()
{
int i,j;
clrscr();
for(i=2;i<=10;i++)
{
for(j=1;j<=10;j++)
printf("\n%d",i*j);
}
getch();
}
```

```c
{
printf("%d ",i);
i=i+2;
if (i>=20)
goto outside;
}
outside : printf("over");
}
```

上述代码的输出如下：
2 4 6 8 10 12 14 16 18 20 over

## BREAK 语句

*break 语句* 允许你结束 *迭代语句（do、for 或 while）* 或 *switch 语句*，并在逻辑结束之外的任何点退出。**break** 只能出现在这些语句之一中。

**break** 语句的形式如下：

```c
break;
```

在迭代语句中，**break** 语句结束循环，并将控制权转移到循环外的下一条语句。在嵌套语句中，**break** 指令只结束最内层的 **do、for、switch 或 while** 指令。

在 **switch** 指令中，**break** 将控制权从 **switch** 体内转移到 **switch** 语句外的下一条语句。

### break 与 switch 语句一起使用

**break** 与条件 switch 语句以及 do、for 和 while 循环语句一起使用。在 **switch** 语句中，**break** 使程序执行 **switch** 之后的下一条语句。如果没有 **break** 语句，从匹配的 **case** 标签到 **switch** 结束（包括 **default**）的每一条语句都会被执行。

以下示例演示了 break 与 switch 语句一起使用的情况：

### 没有 break 的 switch

```c
switch(c)
{
case 1:printf("\n hello world");
case 2: printf("\n Hi");
case 3: printf("OOPs");
}
```

如果我们定义 c=1，那么输出将是 hello world Hi 和 Oops，因为我们没有使用 break 语句。

使用 break 语句。

### 带 break 的 switch

```c
switch(c)
{
case 1:printf("\n hello world");
    break;
case 2: printf("\n Hi");
    break;
case 3: printf("OOPs");
    break;
}
```

如果我们定义 c=1，那么输出将是 hello world，并且 switch 会自动终止；如果我们定义 c=2，那么输出将是 Hi，并且 switch 会自动终止；如果我们定义 c=3，那么输出将是 Oops，并且 switch 会自动终止。

### break 在循环中的使用

在循环中，**break** 终止最近的封闭 **do、for 或 while** 语句的执行。控制权传递给已结束语句之后的下一条语句（如果有的话）。

在嵌套语句中，**break** 语句只结束直接包含它的 **do、for、switch 或 while** 语句。你可以使用 **return** 或 **goto** 语句从嵌套更深的结构中转移控制权。

## 示例

以下示例演示了 break 语句与 for 循环一起使用的情况。

```c
#include <stdio.h>
void main()
{
int i;
for (i = 1; i < 10; i++)
{
printf("%d\n", i);
if (i == 4)
break;
}
getch();
// Loop exits after printing 1 through 4
```

上述程序的输出如下：
1
2

