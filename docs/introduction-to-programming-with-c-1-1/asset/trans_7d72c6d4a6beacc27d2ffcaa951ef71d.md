

## 函数体：

紧跟在函数头后面的复合语句是函数体。它由 3 个元素组成。

- 声明：函数体中使用的所有变量都应在声明部分中声明。但是，函数头中使用的变量不应再次声明。
- 可执行部分：此部分包含执行指定活动的语句或指令。
- return：它是一个关键字。它用于将控制权连同/不带值返回给调用函数。

注意：如果函数不返回任何值，则我们需要将返回类型指定为 void。

如果未显式编写返回类型，则假定返回类型为整数。因此，整数是默认的返回值。

## 函数声明

函数应在被使用之前声明。在使用之前声明函数的过程称为函数原型或函数声明。

函数声明仅包含函数头但以分号结尾。它通知编译器关于

- 函数返回的值的类型
- 函数的名称
- 传递给该函数的参数的数量
- 函数头中每个参数的类型

## 语法：

```
type function-name(type p1, type p2, ........ type pn);   /*semi colon is must*/
```

其中

type – 是从函数返回的值的类型，例如 void、int、float 等。

function name- 函数的名称

p1,p2,........pn – 是参数。所有参数都必须分别声明，每个声明应由逗号分隔。

ex 1:    int add(int a, int b);

## 函数调用

调用函数以实现指定任务的方法称为函数调用。可以通过编写函数名称并传递适当数量的参数来调用函数。函数调用中参数的数量和类型应与函数定义中参数的数量和类型匹配。

```
/* program to demonstrate user defined function*/

#include<stdio.h>

int add(int a,int b);      /*function prototype*/

void main()
{
        int result;
        result=add(10,20);  /* function call*/
        printf("sum=%d\n",result);
}

int add(int a,int b)                 /*function definition*/
{
        return a+b;
}
```

此处执行的顺序为：

- 函数 add() 用两个参数 10 和 20 调用
- 控制权转移到函数 add()，值 10 和 20 使用变量 a 和 b 接收。
- 通过将 10 和 20 相加计算结果
- 结果返回到 main() 并复制到变量 result
- 结果在屏幕上显示

## 规则：

- 函数调用中的参数数量必须等于函数原型和头中的参数数量。
- 函数调用中参数的类型必须等于函数原型和头中参数的类型。
- void 函数不返回值。因此，当函数被调用时，它不能在表达式或打印语句中使用。它只能用作语句。
- 如果函数返回类型为 void，则不应返回任何值。它会导致语法错误。
- 函数最多只能返回一个值

## 形式参数和实际参数

### 形式参数/虚拟参数

在函数定义函数头中定义的变量称为形式参数。所有变量必须分别声明，每个声明必须由逗号分隔。形式参数从实际参数接收数据。

### 实际参数/参数

在函数调用中使用的变量称为实际参数。使用实际参数，可以将数据传输到函数。函数定义中相应的形式参数接收它们。实际参数和形式参数在数量和数据类型上应匹配。

## 函数的分类

根据参数和返回值，函数分类如下：

- 无参数且无返回值的函数。
- 无参数但有返回值的函数
- 有参数但无返回值的函数
- 有参数且有返回值的函数

## 无参数且无返回值的函数

此类称为“无参数的 void 函数”。调用函数和被调用函数之间没有数据传输。因此，调用函数不能发送值，被调用函数也不能接收数据。

```
/*program to demonstrate Function with no parameter and no return values*/
#include<stdio.h>

void add();

void main()
{
    add();      /*no arguments are passed*/
}

void add()
{
    int a,b,c;
    printf("enter two numbers\n");
    scanf("%d%d",&a,&b);
    c=a+b;
    printf("sum=%d\n",c);
    return;      /*returns nothing*/
}
```

## 有参数且无返回值的函数

这称为“有参数的 void 函数”。通过参数从调用函数向被调用函数进行数据传输。但，被调用函数到调用函数之间没有数据传输。

```
/*program to demonstrate Function with parameter and no return values*/
#include<stdio.h>

void add(int x,int y);
```
```c
void main()
{
    int a,b;
    printf("enter two numbers\n");
    scanf("%d%d",&a,&b);
    add(a,b);        /*two arguments are passed to called function*/
}

void add(int x, int y)
{
    int z;
    z=x+y;
    printf("sum=%d\n",z);
    return;           /*returns nothing*/
}
```

## 无参数且有返回值的函数

调用函数到被调用函数之间没有数据传输。但，被调用函数到调用函数之间有数据传输。当函数返回值时，调用函数从被调用函数接收一个值。

```
```c
/*program to demonstrate Function with no parameter and return values*/

#include<stdio.h>

int add();

void main()
{
    int z;
    z=add();    /*no arguments passed returned value will be saved in variable z*/
```
```
```
```c
printf("sum=%d\n",z);
}

int add()
{
    int a,b,c;
    printf("enter two numbers\n");
    scanf("%d%d",&a,&b);
    c=a+b;
    return c;    /* returns the result to the calling function*/
}
```
```

## 有参数且有返回值的函数

调用函数和被调用函数之间有数据传输。当传递参数时，被调用函数可以从调用函数接收值。当函数返回值时，调用函数可以从被调用函数接收值。

```
```c
/*program to demonstrate Function with parameter and return values*/

#include<stdio.h>

int add(int x,int y);

void main()
{
    int a,b,c;
    printf("enter two numbers\n");
    scanf("%d%d",&a,&b);
    c=add(a,b); /*two arguments are passed to the called function and result stored in c*/
```
```
```
printf("sum=%d\n",c);
}
```

```
int add(int x, int y)
{
    int z;
    z=x+y;
    return z;
}
```

## 向函数传递参数

向函数传递参数有两种方式

- 按值传递（按值调用）
- 按地址传递

## 按值传递

这里，实际参数的值被复制到形式参数中，即形式参数仅包含实际参数的副本。因此，即使在被调用函数中形式参数的值发生变化，实际参数的值也不会改变。

优点：

- 使函数更自成一体
- 保护它们免受意外更改。

缺点：

它不允许通过参数将信息传回调用函数。

```
/*program to demonstrate pass by value(swapping 2 numbers)*/
```
```c
#include<stdio.h>

void exchange(int m,int n);

void main()
{
    int a=10,b=20;
    exchange(a,b);
    printf("a=%d\nb=%d\n",a,b);
}

void exchange(int m,int n)
{
    int temp;
    temp=m;
    m=n;
    n=temp;
}
```
```

输出：

a=10

b=20

工作过程：

- 执行从 main() 开始，变量 a 和 b 分别被赋值为 10 和 20。
- 函数 exchange() 被调用，实际参数 a 和 b 的值分别为 10、20
- 在 exchange() 函数中，形式参数 m 和 n 分别接收 10 和 20。
- 此处 m 和 n 的值被交换。
- 但，函数 main() 中实际参数 a 和 b 的值未被交换。

