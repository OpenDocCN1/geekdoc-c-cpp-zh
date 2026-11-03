
| 表达式 |  | 结果 | 表达式的值 |
|---|---|---|---|
| !a | !true | 假 | 0 |
| !c | !false | 真 | 1 |
| !(b>c) | !true | 假 | 0 |
| !(a && c) | !false | 真 | 1 |

## 4.9 条件运算符

条件运算符是一个三元运算符（? 和 :），它需要三个表达式作为操作数。写法为- 测试表达式 ? 表达式1 : 表达式2。首先对测试表达式进行求值。

- (i) 如果测试表达式为真（非零），则求值表达式1，并且它成为整个条件表达式的值。
- (ii) 如果测试表达式为假（零），则求值表达式2，并且它成为整个条件表达式的值。

例如考虑这个条件表达式- a > b ? a : b。这里首先求值表达式 a > b，如果值为真则变量 a 的值成为条件表达式的值，否则变量 b 的值成为条件表达式的值。假设 a = 5 且 b = 8，我们在语句中使用上述条件表达式如下- max = a > b ? a : b ; 首先求值表达式 a > b，因为它是假的，所以 b 的值成为条件表达式的值并赋给变量 max。

在我们的下一个示例中，我们在条件表达式后加上分号写了一个条件语句。a < b ? printf("a is smaller") : printf("b is smaller"); 由于表达式 a < b 为真，所以第一个 printf 函数被执行。

```
/*P4.6 Program to print the larger of two numbers using conditional operator */
#include<stdio.h>
main()
{
    int a,b,max;
    printf("Enter values for a and b : ");
    scanf("%d %d",&a,&b);
    max = a>b ? a:b;    /*ternary operator*/
    printf("Larger of %d and %d is %d\n",a,b,max);
}
```

输出：
输入 a 和 b 的值 : 12 7
12 和 7 中较大的是 12

## 4.10 逗号运算符

逗号运算符（ , ）用于允许在只会使用一个表达式的情况下出现不同的表达式。表达式由逗号运算符分隔。分隔的表达式从左到右求值，整个复合表达式的类型和值是右most 表达式的类型和值。

例如考虑这个表达式-
a = 8, b = 7, c = 9, a+b+c

这里我们组合了 4 个表达式。最初 8 被赋给变量 a，然后 7 被赋给变量 b，9 被赋给变量 c，之后求值 a+b+c，它成为整个表达式的值。所以上述表达式的值为 24。现在考虑这个语句-
sum = ( a = 8, b = 7, c = 9, a+b+c );

这里右侧整个表达式的值将被赋给变量 sum，即 sum 将被赋值为 24。由于逗号运算符的优先级低于赋值运算符，因此这里需要括号。逗号运算符有助于使代码更紧凑，例如如果不使用逗号运算符，上述任务将需要在 4 条语句中完成。

```
a = 8;
b = 7;
c = 9;
sum = a+b+c;
```

```
/*P4.7 Program to understand the use of comma operator */
#include<stdio.h>
main()
{
    int a,b,c,sum;
    sum = (a=8,b=7,c=9,a+b+c);
    printf("Sum = %d\n",sum);
}
```

输出：
和 = 24

```
/* P4.8 Program to interchange the value of two variables using comma operator*/
#include<stdio.h>
main()
{
    int a=8,b=7,temp;
    printf("a = %d, b = %d\n",a,b);
    temp=a, a=b, b=temp;
    printf("a = %d, b = %d\n",a,b);
}
```

输出：
a = 8, b = 7
a = 7, b = 8

逗号运算符也用于循环，我们将在下一章学习关于它的内容。

## 4.11 sizeof 运算符

sizeof 是一个一元运算符。该运算符以字节为单位给出其操作数的大小。操作数可以是变量、常量或任何数据类型（ int, float, char 等）。例如 sizeof(int) 给出 int 数据类型占用的字节数，即 2。

```
/*P4.9 Program to understand the sizeof operator*/
#include<stdio.h>
main()
{
    int var;
    printf("Size of int = %d",sizeof(int));
    printf("Size of float = %d",sizeof(float));
    printf("Size of var = %d",sizeof(var));
    printf("Size of an integer constant = %d",sizeof(45));
}
```

输出：
int 的大小 = 2
float 的大小 = 4
var 的大小 = 2
一个整数常量的大小 = 2

通常 sizeof 运算符用于制作可移植程序，即可在不同机器上运行的程序。例如，如果我们编写程序假设 int 为 2 字节，那么它在 int 为 4 字节的机器上就不会正确运行。所以为了制作可在所有机器上运行的通用代码，我们可以使用 sizeof 运算符。

## 位运算符

C 具有支持在位级操作数据的能力。位运算符用于对单个位进行操作。位运算符仅对整数操作。位运算符如下-

| 位运算符 | 含义 |
|---|---|
| & | 按位与 |
| \| | 按位或 |
| ~ | 按位取反 |
| << | 左移 |
| >> | 右移 |
| ^ | 按位异或 |

这些位运算符将在第 13 章中详细讨论。

## 其他运算符

我们将在后续章节中学习许多其他运算符。本章要介绍的最后一个运算符是类型转换运算符。在学习它之前，我们将讨论 C 中的类型转换。

## 4.12 类型转换

C 提供了在表达式中混合不同类型变量和常量的功能。在这类操作中，一个操作数的的数据类型被转换为另一个操作数的数据类型。这称为类型转换。不同类型的类型转换如下-

![](img/a76c706396af8b310f291a5313a27079_58_0.png)

隐式类型转换由编译器完成，而显式类型转换是用户定义的转换。

### 4.12.1 隐式类型转换

这些转换是根据 C 语言的某些预定义规则由 C 编译器完成的。隐式类型转换的两种类型是自动类型转换和赋值中的类型转换。

### 4.12.2 自动转换

### 自动一元转换

所有类型为 char 和 short 的操作数在任何操作之前都会被转换为 int。某些编译器在任何操作之前都会将所有 float 操作数转换为 double。

### 自动二元转换

自动二元转换的规则如下-

- (i) 如果一个操作数是 long double，则另一个将被转换为 long double，结果为 long double。
- (ii) 否则如果一个操作数是 double，则另一个将被转换为 double，结果为 double。
- (iii) 否则如果一个操作数是 float，另一个将被转换为 float，结果为 float。
- (iv) 否则如果一个操作数是 unsigned long int，则另一个将被转换为 unsigned long int，结果为 unsigned long int。
- (v) 否则如果一个操作数是 long int，另一个是 unsigned int：
  - (a) 如果 long int 可以表示 unsigned int 的所有值，则 unsigned int 将被转换为 long int，结果为 long int。
  - (b) 否则两个操作数都将被转换为 unsigned long int，结果为 unsigned long int。
- (vi) 否则如果一个操作数是 long int，则另一个将被转换为 long int，结果为 long int。
- (vii) 否则如果一个操作数是 unsigned int，则另一个将被转换为 unsigned int，结果为 unsigned int。
- (viii) 否则两个操作数都是 int，结果为 int。

如果我们排除无符号变量，那么这些规则相当简单，可以通过为每种数据类型分配一个等级来总结。每当有两个不同数据类型的操作数时，等级较低的操作数将被转换为等级较高操作数的类型。这称为数据类型的提升。

![](img/a76c706396af8b310f291a5313a27079_59_0.png)

如果赋值表达式中两个操作数的类型不同，则右手操作数的类型将被转换为左手操作数的类型。这里如果右手操作数的等级较低，则它将被提升到左手操作数的等级，如果它等级较高，则它将被降级到左手操作数的等级。

- 1. 当 long 转换为 int，或 int 转换为 short int 或 char 时，一些高位可能会被丢弃。
- 2. 在 float 类型转换为 int 类型期间，小数部分可能会被截断。
- 3. 当 double 类型转换为 float 类型时，数字会被四舍五入。
- 4. 当有符号类型更改为无符号类型时，符号可能会被丢弃。
- 5. 当 int 转换为 float，或 float 转换为 double 时，精度或精确度不会增加。

```
/*P4.10 Program to understand the type conversion in assignment*/
main( )
{
char c1,c2;
int i1,i2;
float f1,f2;
c1='a';
i1=80.56; /*Demotion:float converted to int, only 80 assigned to i1*/
f1=12.6;
}
```
