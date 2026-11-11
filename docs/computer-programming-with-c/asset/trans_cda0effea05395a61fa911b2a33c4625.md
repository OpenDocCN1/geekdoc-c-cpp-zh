

```c
for(j=1;j<=i+1; j++)
{
    printf("%d",value);
    value++;
}
printf("\n");
}
```

### 输出

```text
Enter the number of rows: 4
1
1    2
1    2    3
1    2    3    4
```

### 草稿

现在不再打印星号图案，而是需要打印题目中所示的整数值图案。因此，我们创建一个名为 `value` 的变量，其初始值为 1。我们还在每一行的开头将该变量的值设置为 1。这可以通过在外层 `for` 循环体内编写以下语句来实现：

```c
value=1;
```

此外，内层 `for` 循环每在计算机屏幕上打印一个数字，就会递增变量 `value`。从而使用如下所示的语句在三角形的一行内打印连续数字：

```c
printf("%d",value);
value++;
```

因此，我们得到如下图案：

```text
1
1       2
1       2       3
1       2       3       4
```

因为每次开始处理新的一行时，我们都会将 value 重置为 1。

## 已解决示例 5.6

编写一个程序，从用户处输入行数，并在计算机屏幕上打印以下图案：

```text
a    a    a    a
b    b    b
c    c
 d
```

```c
#include<stdio.h>
void main()
{
int i,j,r;
char v = 'a';
printf("Enter the number of rows:");
scanf("%d",&r);
    for(i=0; i<=r-1; i++)
    {
        for(j=1;j<=r-i; j++)
        {
            printf("%c",v);
        }
        v=v+1;
        printf("\n");
    }
}
```

### 输出

```text
Enter the number of rows:4
aaaa
bbb
cc
d
```

### 草稿

现在不再打印星号图案，而是需要打印题目中所示的从 ‘a’ 开始的字符图案。因此，我们创建一个名为 v 的变量，其初始值为 ‘a’。此外，我们还在每一行的开头递增变量 v 的值。这可以通过在外层 for 循环体内编写以下语句来实现。

```c
v=v+1;
```

内层 for 循环在每次迭代时都会在计算机屏幕上打印变量 v 的值。从而使用如下所示的语句在三角形的一行内打印相同的字符：

```c
printf("%c",v);
```

因此，我们得到如下图案：

```text
a        a        a        a
b        b        b
c        c
d
```

注意，字符可以像整数一样递增。这是因为 C/C++ 实际上在内存中存储的是字符的 ASCII 值。由于我们在每一行的开头递增 v 的值，因此图案的每一行都会打印新的字符。

## 已解决示例 5.7

编写一个程序，从用户处输入 n 的值，并打印以下级数的结果：

2! - 4! + 6! - 8! + 10! ....n!

```c
#include<stdio.h>
void main()
{
int k,n;
float f,s=0.0,x,sign=-1;
printf("Enter the value of n:");
scanf("%d",&n);
    for(k=2; k<=n; k+=2)
    {
        x=k;
        f=1.0;
/*Calculate the factorial of 'x'*/
        while(x>0)
        {
            f=f*x;
            x--;
        }
        sign=sign*(-1);
        s=s+f*sign;
    }
printf("Result of the series is %f",s);
}
```

### 输出

```text
Enter the value of n:6
Result of the series is 698.000000
```

### 草稿

为了在级数中得到 “+” 和 “-” 交替的模式，我们创建一个名为 sign 的变量，其初始值为 -1。在 for 循环的每次迭代中，我们再将变量 sign 的值乘以 -1。因此，在偶数次迭代中每次乘以 -1 都会使 sign 变为正值，而在奇数次迭代中每次乘以 -1 都会使 sign 变为负值。从而计算出带有交替 + 和 - 符号的级数值。

## 已解决示例 5.8

编写一个程序，从用户处输入 n 的值，并打印以下级数的结果：

x²/2! - x³/3! + x⁴/4! - x⁵/5! + x⁶/6! ....xⁿ/n!

```c
#include<stdio.h>
#include<math.h>
void main()
{
    int k,n,t;
    float f,s=0.0,x,sign=1;
    printf("Enter the value of n:");
    scanf("%d",&n);
    printf("Enter the value of x:");
    scanf("%f",&x);
        for(k=2; k<=n; k++)
        {
            t=k;
            f=1.0;
            /*Calculate the factorial of 't'*/
                while(t>0)
                {
                    f=f*t;
                    t--;
                }
            sign=sign*(-1);
            s=s+ pow(x,k)/f*sign;
        }
    printf("Result of the series is %f",s);
}
```

### 输出

```text
Enter the value of n:5
Enter the value of x:3
Result of the series is -1.350000
```

### 草稿

函数 pow(x,k) 可用于计算 x 的 k 次方。该函数定义在头文件 math.h 中，我们已在代码中包含该头文件。此外，将变量 sign 的值与比值 pow(x,k)/f 相乘，以便像代码中所示那样计算带有交替 “+” 和 “-” 符号的级数。因此，在 for 循环的每次迭代中执行以下语句时：

s=s+pow(x,k)/f*sign;

循环完成后，我们将在变量 s 中得到所需级数的结果。

## 已解决示例 5.9

编写一个程序，从用户处输入行数，并在计算机屏幕上打印以下图案：

```c
#include<stdio.h>
void main()
{
    int width,height,i,j;
    printf("Enter the width and height of the rectangle:");
    scanf("%d %d",&width,&height);
    /*Print a rectangle*/
    for(i=0; i<height; i++)
    {
        for(j=0; j<width; j++)
        {
            printf("*");
        }
        printf("\n");
    }
}
```

### 输出

```text
Enter the width and height of the rectangle: 10 3
**********
**********
**********
```

### 草稿

要打印的行数由矩形的高度指定，而要打印的列数由矩形的宽度指定。因此，外层 for 循环的总迭代次数与矩形的高度相同，而内层 for 循环的总迭代次数与矩形的宽度相同。每一行要打印 width 个星号，因此循环如代码中所示那样嵌套。

## 已解决示例 5.11

编写一个程序，对用户在程序运行时输入的所有整型值执行加法。当用户输入值 0 时，程序应停止执行加法并打印最终结果。

```c
#include<stdio.h>
void main()
{
    int number, s = 0;
    printf("Enter a number:\n");
    scanf("%d",&number);
    /*Take a number as input until user enters 0*/
    while(number!=0)
    {
        s=s+number;
        printf("Enter next number:\n");
        scanf("%d",&number);
    }
    printf("Result of addition is %d",s);
}
```

### 输出

```text
Enter a number:
10
Enter next number:
20
Enter next number:
30
Enter next number:
40
Enter next number:
0
Result of addition is 100
```

### 草稿

如代码中所示，我们在 while 循环的每次迭代中接收变量 number 的值。程序读取的变量 number 的每个值都会加到变量 s 的值上，变量 s 表示用户到目前为止输入的数字之和。当用户输入值 0 时，while 循环终止，该值表示输入数据的结束。

## 已解决示例 5.12

编写一个程序来打印弗洛伊德三角形。程序应从用户处读取行数作为输入，并打印如下所示的弗洛伊德三角形（下面的三角形假定高度为 5。）：

```text
1
2      3
4      5      6
7      8      9      10
11     12     13     14     15
```

```c
#include<stdio.h>
void main()
{
int i,j,r,value=1;
printf("Enter the number of rows:");
scanf("%d",&r);
    for(i=0 ; i<=r-1 ; i++)

