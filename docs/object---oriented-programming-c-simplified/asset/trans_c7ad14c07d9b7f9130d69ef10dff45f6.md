

## 按位与 (&)

它将两个位作为操作数，如果两者都是 1 则返回值为 1。如果其中任一为 0，结果为 0。

## 表 3.7：按位与真值表

| 第一个位 | 第二个位 | 结果 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

```
/*PROG 3.16 DEMO OF BITWISE OPERATOR &(BITWISE AND)*/

#include<iostream.h>
void main()
{
int a,b;
a=2;
b=3;
int c=a&b;
cout<<"The value of c :="<<c<<endl;
}
OUTPUT :
The value of c : =2
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_82_0.png)

图 3.16. 程序的输出屏幕。

解释：a=2 的二进制值为 0010，b=3 为 0011

对这些值进行按位与运算如下：

0 0 1 0
0 0 1 1
--------
0 0 1 0   (输出到 c 的值为十进制 2)

如果两个位都是 1，使用 & 运算符输出位将为 1，否则为 0。

## 按位或 (|)

它将两个位作为操作数，如果至少一个为 1 则返回值为 1。如果两者都为 0，则结果为 0，否则为 1。

## 表 3.8：按位或真值表

| 第一个位 | 第二个位 | 结果 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

```
/*PROG 3.17 DEMO OF BITWISE OPERATOR |(BITWISE OR)*/

#include<iostream.h>
void main()
{
int a,b;
a=12;
b=7;
int c= a|b;
cout<<"The value of c :="<<c<<endl;
}
OUTPUT :
The value of c :=15
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_83_0.png)

图 3.17. 程序的输出屏幕。

解释：a=12 的二进制值为 1100，b =7 为 0111

对这两个值进行或运算如下：
    1 1 0 0
    0 1 1 1
  ---------
    1 1 1 1   (输出到 c 的值为十进制 15)?

如果任一位为 1，使用或运算符输出将为 1。

## 按位异或 (^)

该运算符至少接受两个位（可能多于两个）。如果 1 的个数为奇数，则结果为 1，否则结果为 0。

## 表 3.9：按位异或真值表

| 第一个位 | 第二个位 | 结果 |
|-----------|------------|--------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

```
/*PROG 3.18 DEMO OF BITWISE OPERATOR ^(XOR)*/
#include <iostream.h>
void main()
{
int a,b;
a=5;b=6;
int c = a^b;
cout << "The value of c : " << c << endl;
}

OUTPUT :
The value of c : = 3
```

图 3.18. 程序的输出屏幕。

解释：a =5 的二进制值为 0101，b = 6 为 0110
对这两个值进行异或运算如下：

 0 1 0 1
 0 1 1 0
-----------
 0 0 1 1 
 (输出到 c 的值为十进制 3)

如果存在奇数个 1，使用异或运算符输出将为 1，否则输出为 0。

## 左移运算符 (<<)

我们之前在几乎所有程序中都见过这个运算符，它也被称为插入或 put to 运算符。该运算符用于移位其操作数的位。它写为 x<<num; 表示将 x 的位向左移动 num 次。最低有效位 (LSB) 位置会填入一个新零。 （见下面给出的程序）

```
/*PROG 3.20 DEMO OF BITWISE OPERATOR <<(LEFT SHIFT) VER 1*/

#include<iostream.h>
void main()
{
int a,b;
a=2;
b=a<<1;
cout<<"The value of b :="<<b<<endl;
}
OUTPUT :
The value of b : = 4
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_86_0.png)

图 3.20. 程序的输出屏幕。

解释：a<<1 表示将 ‘a’ 的内容向左移动 1 位。如果我们将数字 2 表示为二进制：

![](img/ad5299318df8d4d7c6df5eaa86590ea3_86_1.png)

其中 b0 是从左起的第一位，称为最低有效位 (LSB)，b3 称为最高有效位 (MSB)。向左移动 1 位会导致 b3 丢失其值并从 b2 获取，b2 从 b1 获取，b1 从 b0 获取，在 b0 插入一个新零。因此结果位模式为：

![](img/ad5299318df8d4d7c6df5eaa86590ea3_86_2.png)

如果您写：a<<2 表示将 a 的内容向左移动两次。

## 面向对象编程 C++ 简化

a 中的原始值为 0010

![](img/ad5299318df8d4d7c6df5eaa86590ea3_87_0.png)

移动一次

![](img/ad5299318df8d4d7c6df5eaa86590ea3_87_1.png)

移动第一步得到的值

![](img/ad5299318df8d4d7c6df5eaa86590ea3_87_2.png)

注意：向左移动一位会使数字乘以 2。

该运算符用于移位其操作数的位。它写为 x >> num; 表示将 x 的位向右移动 num 次。最高有效位 (MSB) 位置会填入一个新零。

见下面给出的程序：

```
/*PROG 3.21 DEMO OF BITWISE OPERATOR >>(RIGHT SHIFT)VER 1*/
#include <iostream.h>
void main()
{
int a=8,b;
a>>=1;
b=a>>1;
cout<<"The value of b :="<<b<<endl;
}

OUTPUT :
The value of b : = 4
```

图 3.21. 程序的输出屏幕。

解释：a>>=1 表示将 'a' 的内容向右移动 1 位。如果我们将数字 8 表示为二进制：

![](img/ad5299318df8d4d7c6df5eaa86590ea3_87_3.png)

![](img/ad5299318df8d4d7c6df5eaa86590ea3_87_4.png)

向右移动 **1 位** 会导致 **b0** 丢失其值并从 **b1** 获取，**b1** 从 **b2** 获取，**b2** 从 **b1** 获取，在 **b3** 插入新零。因此结果位模式为：

| b3 | b2 | b1 | b0 |
|---|---|---|---|
| 1 | 0 | 0 | 0 |

| b3 | b2 | b1 | b0 |
|---|---|---|---|
| 0 | 1 | 0 | 0 |

如果您写 a>>2，表示将 ‘a’ 的内容向右移动两次
a 中的原始值 =1000

| b3 | b2 | b1 | b0 |
|---|---|---|---|
| 1 | 0 | 0 | 0 |

移动一次后

| b3 | b2 | b1 | b0 |
|---|---|---|---|
| 0 | 1 | 0 | 0 |  → (十进制 4)

移动第一步得到的值。

| b3 | b2 | b1 | b0 |
|---|---|---|---|
| 0 | 0 | 1 | 0 |

即十进制 2，是最终输出。

注意：向右移动一位会使数字除以 2。

## sizeof 运算符

该运算符用于查找特定类型或常量的特定变量在内存中占用的字节数。这是唯一既可作为运算符又可作为函数工作的运算符。

```
/*PROG 3.22 DEMO OF SIZEOF OPERATOR VER 1*/

#include <iostream.h>
void main()
{
short int a;
int b;
float c;
double e;
cout << "Size of short int variable  a :=" << sizeof(a) << endl;
cout << "size of int variable        b :=" << sizeof(b) << endl;
cout << "Size of float variable      c :=" << sizeof(c) << endl;
cout << "Size of double variable e :=" << sizeof(e) << endl;
cout << endl;
}
OUTPUT :
Size of short int variable  a : =2
size of int variable        b : =4
Size of float variable      c : =4
Size of double variable     e : =8
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_89_0.png)

图 3.22. 程序的输出屏幕。

解释：该程序给出不同类型变量占用的内存字节数。Turbo C/C++ 中 int 变量的大小为 2 字节，而在 Windows 中为 4 字节。

```
/*PROG 3.23 DEMO OF SIZEOF OPERATOR VER 2*/

#include <iostream.h>
void main()
{
cout << "Size of char constants  : = " << sizeof('A') << endl;
cout << "Size of int variable    : = " << sizeof(14) << endl;
cout << "Size of float variable  : = " << sizeof(5.6F) << endl;
cout << "Size of double variable : = " << sizeof(56.78) << endl;
cout << endl;
}
OUTPUT :
Size of char constants  : = 1
Size of int variable    : = 4
Size of float variable  : = 4
Size of double variable : = 8
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_91_0.png)

# 图 3.24. 程序的输出屏幕。

逗号运算符的结合性（见下一节）是从左到右，最右值赋给 x，即上述程序中 c 的值。

```
/*PROG 3.25 DEMO OF COMMA OPERATOR VER 2*/
#include <iostream.h>
void main()
{
int a=2,b=3,c=4,x=2;
x=(c--,c++,c++,+a);
cout<<"The value of x :="<<"<x<"<<"\nThe value of c :="
<<c<<endl;
cout<<endl;
}

OUTPUT :
The value of x : = 3
The value of c : = 4
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_91_1.png)

# 图 3.25. 程序的输出屏幕。

如前所述，逗号运算符从左到右工作。因此 c 在 c-- 后变为 3，在 c++ 后再次变为 4。‘a’ 的值由于 ++a 变为 3，该值被赋给 x，因此输出。

## 3.3 声明常量

常量是不可更改的值。例如，π 的值为 22/7 或 3.14，这是一个常量。为了在程序中使用常量，C 主要定义了三种声明常量的方法。我们逐一讨论它们。

