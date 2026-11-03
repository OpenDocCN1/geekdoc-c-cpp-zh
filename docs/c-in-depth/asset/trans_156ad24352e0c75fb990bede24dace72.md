
```c
x=i+j+1;
    printf("x = %d\n",x);
}
```

```c
(13)main()
{
    int i,index=0;
    for(i=0;i<10;i++)
    {
        int i=0;
        while(i++<5)
            index++;
    }
    printf("index = %d\n",index);
}
```

```c
(14)main()
{
    int i;
    for(i=1;i<10;i++)
    {
        if(i==3)
            continue;
        printf("%d ",i);
    }
}
```

```c
(15)main()
{
    int i=1;
    while(i<10)
    {
        if(i==3)
            continue;
        printf("%d ",i);
        i++;
    }
}
```

```c
(16)main()
{
    int i,sum;
    for(i=0;i<10;i+=3)
        sum +=i*i;
    printf("%d",sum);
}
```

```c
(17)main()
{
    int c=50;
    for( ;c ; )
        c--;
    printf("c = %d\n",c);
}
```

```c
(18)main()
{
    char ch='A';
    switch(ch)
    {
        case 'A':  case 'B':
            ch++;
            continue;
        case 'C':  case 'D':
            ch++;
    }
}
```

```c
(19)main()
{
    int var=2,x=1,y=2;
    switch(var)
    {
        case x:
            x++;
        case y:
            y++;
    }
}
```

```c
(20)main()
{
    char ch='A';
    while(ch<='D')
    {
        switch(ch)
        {
            case 'A':  case 'B':
                ch++;
                continue;
            case 'C':  case 'D':
                ch++;
        }
        printf("%c",ch);
    }
}
```

```c
(21)main()
{
    int n,sum=0;
    for( ; ; )
    {
        scanf("%d", &n);
        sum+=n;
        if(sum>100)
            break;
    }
}
```

```c
(22)main()
{
    int i,sum1=0,sum2=0;
    for(i=1;i<5;i++)
        sum1+=i;
    i=1;
    while(i<5)
    {
        i++;
        sum2+=i;
    }
    printf("%d  %d\n",i,sum1,sum2);
}
```

## 编程练习

- 1. 编写一个程序，打印 1 到 99 之间的素数。（提示：参见 P5.27，不要输入数字，而是使用一个生成 1 到 99 数字的 for 循环）
- 2. 编写一个程序，输入一个数并求该数的逆序数。
- 3. 输入一个数和一个数字，判断该数字是否出现在这个数中；如果出现，则统计它在这个数中出现的次数。
- 4. 编写一个程序，接受任意数 n，并打印从 1 到 n 的所有数的平方和。
- 5. 编写一个程序，接受任意数 n，并打印从 1 到 n 的所有能被 3 整除的数的立方。
- 6. 编写一个程序，接受任意六位数，并打印该数中所有偶数位数字之和以及所有奇数位数字之积。
- 7. 编写一个程序，求 x 的 y 次幂的值，其中 x 和 y 是正整数。
- 8. 编写一个程序，接受最多六位的任意数，并用英文单词打印该数。
  例如：1265 = one two six five
- 9. 编写一个程序，输入一个数并测试它是否为斐波那契数。
- 10. 编写一个程序，打印所有小于 50 的勾股三元组。如果 x < y < z 且 x²+y² = z²，则任意三个数 x、y、z 称为勾股三元组。
- 11. 求以下级数前 n 项之和，其中 x 是用户输入的整数。
  - 1 + 2 + 4 + 7 + 11 + 16 + ........
  - 1 + 11 + 111 + 1111 + .....
  - x + x² +x³ +x⁴........
  - x + x² -x³ + x⁴........
  - 1/x - 1/x² +1/x³ -1/x⁴

## 答案

- (1) 友善很重要
  变量 a 被赋值为 5，因此 if 条件变为真。
- (2) 20 8
- (3) 困难使我们更优秀
- (4) 11
  if 部分后面有一个分号，它被视为空语句。
- (5) 0, 1
- (6) 5 4 3 2 1
- (7) 该程序无限运行，因为 goto 语句不在 if 结构内部。
- (8) a 不等于 2。
  这里 else 部分与第二个 if 配对；如果我们想让它与第一个 if 配对，就应该把第二个 if 括在括号中。
- (9) a = 6, b = 4
  a = 3, b = 1
  a = 1, b = 1
  a = 0, b = 1
  a = 0, b = 1
  a = 0, b = 1
  ............
  b 的值永远不会变为零，因此条件永远不会变为假，导致无限循环。
- (10) 10 7 4 1 -2 -5 -8 ............
  i 的值永远不会变为零，导致无限循环。
- (11) 10 8 6 4 2
  当赋值表达式 ( i = j ) 的值为零时，循环终止。
- (12) x = 6
- (13) index = 50
- (14) 1 2 4 5 6 7 8 9
- (15) 该程序打印 1 2，然后进入无限循环。
- (16) 变量 sum 没有初始化为零；如果初始化为零，结果将是 126。
- (17) c = 0
- (18) 错误，continue 不能在 switch 内使用。
- (19) 错误，switch 中只能使用常量表达式。
- (20) DE
  这里 continue 语句位于 while 循环内。
- (21) 循环将输入数字，并在这些数字之和超过 100 时终止。
- (22) 5 10

## 第6章

## 函数

函数是一个自包含的子程序，用于完成某些特定的、定义明确的任务。一个程序由一个或多个函数组成。如果一个程序只有一个函数，那么它必须是 main() 函数。

### 6.1 使用函数的优点

- 1. 通常，一个困难的问题会被分解为若干子问题，然后分别求解。这种分治技术通过函数在 C 中实现。一个程序可以划分为多个函数，每个函数执行某些特定任务。因此，使用 C 函数可以将程序的工作模块化并加以划分。
- 2. 当某些特定代码需要在程序中的不同位置多次使用时，使用函数可以避免重复编写该代码。
- 3. 程序变得易于理解、修改，并且易于调试和测试。编写程序以及理解程序的每个部分完成什么工作都变得简单。
- 4. 函数可以存储在库中，从而实现可重用性。

C 程序有两类函数——

- 1. 库函数
- 2. 用户定义函数

### 6.2 库函数

C 具有提供库函数来执行某些操作的功能。这些函数存在于 C 库中，并且是预定义的。例如，sqrt() 是一个数学库函数，用于求任意数的平方根。函数 scanf() 和 printf() 是输入/输出库函数。类似地，我们有用于字符串操作的 strlen()、strcmp() 等函数。

要使用库函数，我们必须使用预处理指令 #include 包含相应的头文件。例如，要使用 printf()、scanf() 等输入/输出函数，我们必须包含 stdio.h。对于数学库函数，我们必须包含 math.h；对于字符串库，应包含 string.h。下面的程序演示了库函数 sqrt() 的使用。

```c
/*P6.1 Program to find the square root of any number.*/
#include<stdio.h>
#include<math.h>
main()
{
    double n,s;
    printf("Enter a number : ");
    scanf("%lf",&n);
    s=sqrt(n);
    printf("The square root of %.2lf is : %.2lf\n", n, s);
}
```

### 输出：

Enter a number : 16

The square root of 16.00 is : 4.00

在这个程序中，我们使用了三个库函数——printf()、scanf() 和 sqrt()。本章后面我们将进一步学习库函数。

### 6.3 用户定义函数

用户可以为执行程序中的任何特定任务创建自己的函数。这类函数称为用户定义函数。要创建和使用这些函数，我们应该了解以下三件事——

- 1. 函数定义
- 2. 函数声明
- 3. 函数调用

在讨论这三点之前，我们编写了两个简单程序，将用作参考。第一个程序画一条线，第二个程序将两个数相加。

```c
/*P6.2 Program to draw a line*/
#include<stdio.h>
void drawline(void); /*Function Declaration*/
main()
{
    drawline(); /*Function Call*/
}
void drawline(void) /*Function Definition*/
{
    int i;
    for(i=1;i<=80;i++)
        printf("-");
}
```

```c
/*P6.3 Program to find the sum of two numbers*/
#include<stdio.h>
int sum(int x,int y); /*Function declaration*/
main()
{
    int a,b,s;
    printf("Enter values for a and b : ");
    scanf("%d %d",&a,&b);
    s=sum(a, b); /*Function call*/
    printf("Sum of %d and %d is %d\n",a,b,s);
}
int sum(int x,int y) /*Function definition*/
{
    int s;
```
