

类将维护一个溢出标志，并在检测到溢出时在溢出标志中设置相应的位。使用 Pixel 类的应用程序负责检查溢出标志的状态。将提供公共方法以允许访问溢出标志，并将提供一个私有验证方法来帮助维护其状态。验证方法将由 Pixel 类的所有修改器方法调用。

扩展的 Pixel 类声明如下：

```cpp
/*
* ************************************************************************/
/* Pixel class declaration. */
/* File name: pixel.h */
/* This class implements the concept of a pixel */
*/
#ifndef PIXEL_H
#define PIXEL_H
#include <iostream> //Required for istream, ostream
using namespace std;
class Pixel
{
public:
static const unsigned int MAXVAL = 255;
//Constructors
Pixel(); //Default
Pixel(unsigned ); //Gray scale
Pixel(unsigned,unsigned,unsigned); //Full color range
//Overloaded operators.
Pixel operator+(const Pixel& p) const;
Pixel operator*(double v) const;
Pixel operator/(unsigned v) const;
//IO Operators.
friend istream& operator >>(istream& in, Pixel& p);
friend ostream& operator <<(ostream& out, const Pixel& p);
bool overflow() const; //check overflow state
void reset(); //reset overflow state
private:
unsigned int red, green, blue;
unsigned short overflowFlag;
static const unsigned short RMASK = 4;
static const unsigned short GMASK = 2;
static const unsigned short BMASK = 1;
static const unsigned short CHECK = 7;
void validate(); //set overflow bits
};
```

请注意，我们已向 Pixel 类添加了五个静态常量。公共常量 MAXVAL 设置为 255，是公共接口的一部分。四个私有位掩码常量在各种 `class` 方法中被引用，并被赋予整数值 1、2、4 和 7。回顾一下，8 位中的二进制值 1 可以表示为 00000001；二进制 2 为 00000010；二进制 4 为 00000100；二进制 8 为 00001000。这些常量用作 **位掩码** 来设置和检查 `overflowFlag` 的状态。位掩码是与位运算符一起使用的整数数据，用于在单个位运算中操作位。扩展的 `Pixel` 类的实现如下：

```cpp
#include "Pixel.h"
/* ----------------------------------------------------------- */
/* Pixel class implementation.                                 */
/* File name: Pixel.cpp                                        */
/* Addition (+) operator.                                      */
Pixel Pixel::operator+(const Pixel& p) const
{
    Pixel temp;
    temp.red = red + p.red;
    temp.green = green + p.green;
    temp.blue = blue + p.blue;
    temp.validate();
    return temp;
}
/* ----------------------------------------------------------- */
/* Multiplication (*) operator.                                */
Pixel Pixel::operator*(double v) const
{
    Pixel temp;
    temp.red = red*v;
    temp.green = green*v;
    temp.blue = blue*v;
    temp.validate();
    return temp;
}
/* ----------------------------------------------------------- */
/* Division (/) operator.                                      */
Pixel Pixel::operator/(unsigned int v) const
{
    Pixel temp;
    temp.red = red/v;
    temp.green = green/v;
    temp.blue = blue/v;
    temp.validate();
    return temp;
}
/* ----------------------------------------------------------- */
ostream& operator<<(ostream& out, const Pixel& p)
{
    out << p.red << ' ';
    out << p.green << ' ';
    out << p.blue;
    return out;
}
/*...........................................*/
```

```cpp
istream& operator>>(istream& in, Pixel& p)
{
    in >> p.red >> p.green >> p.blue;
    p.validate();
    return in;
}
/*...........................................*/
```

```cpp
Pixel::Pixel()
{
    //Black
    red=green=blue=0;
    return;
}
/*...........................................*/
```

```cpp
Pixel::Pixel(unsigned int value)
{
    //Gray scale
    red=green=blue=value;
    validate();
    return;
}
/*...........................................*/
```

```cpp
Pixel::Pixel(unsigned int r,unsigned int g,unsigned int b)
{
    //Full color range
    red=r;
    green=g;
    blue=b;
    validate();
    return;
}
/*...........................................*/
```

```cpp
bool Pixel::overflow() const
{
    return (overflowFlag & CHECK);
}
/*...........................................*/
```

```cpp
void Pixel::reset()
{
    if(red > MAXVAL) red = MAXVAL;
    if(green > MAXVAL) green = MAXVAL;
    if(blue > MAXVAL) blue = MAXVAL;
    overflowFlag = 0;
}
```

```cpp
/*---- Pixel::validate() -----------------------*/
void Pixel::validate()
{
    if(red > MAXVAL) overflowFlag = overflowFlag|RMASK;
    if(green > MAXVAL) overflowFlag = overflowFlag|GMASK;
    if(blue > MAXVAL) overflowFlag = overflowFlag|BMASK;
}
```

![](img/f2bfa570e453b020c16e048c79a3ea0e_526_0.png)

请注意，私有修改器方法 `void Pixel::validate()` 使用位运算符 `|` 来设置 `overflowFlag` 的状态。方法 `validate()` 必须由 `Pixel` 类的所有修改器方法调用，以保证 `overflowFlag` 的正确状态。公共访问器方法 `bool Pixel::overflow()` 使用位运算符 `&` 来返回 `overflowFlag` 的状态。我们将更详细地查看这两种方法，并讨论位运算符。

## 位运算符

位运算符对其操作数的每个位执行操作。C++ 支持三个二进制位运算符：按位或 (`|`)、按位与 (`&`) 和按位异或 (`^`)，以及一个一元按位非运算符(`~`)。这些运算符的操作数限定为整型，例如 `int` 或 `char`。表 10.2 提供了位运算符的真值表。

| A | B | ~A | A\|B | A^B | A&B |
|---|---|---|---|---|---|
| 0001 | 0001 | 1110 | 0001 | 0000 | 0001 |
| 0010 | 0010 | 1101 | 0010 | 0000 | 0010 |
| 0011 | 0100 | 1100 | 0111 | 0111 | 0000 |
| 0100 | 0111 | 1011 | 0111 | 0011 | 0100 |

为了说明位运算符的用法，假设已定义一个 `Pixel` 对象并具有以下值：

```
Pixel p1   278   unsigned red
           298   unsigned green
           150   unsigned blue
           0     unsigned short overflowFlag
```

语句 `p1.validate();` 会产生以下程序跟踪和内存快照：

| Validate() | 内存快照 |
|---|---|
| **步骤 1:** `if (red > MAXVAL)`<br>`overflowFlag = overflowFlag | RMASK;` | Pixel p1<br>278 无符号 red<br>298 无符号 green<br>150 无符号 blue<br>4 无符号短整型 overflowFlag |
| **步骤 2:** `if (green > MAXVAL)`<br>`overflowFlag = overflowFlag | GMASK;` | Pixel p1<br>278 无符号 red<br>298 无符号 green<br>150 无符号 blue<br>6 无符号短整型 overflowFlag |
| **步骤 3:** `if (blue > MAXVAL)`<br>`overflowFlag = overflowFlag | BMASK;` | |

在步骤 1 中，当对操作数 overflowFlag (00000000) 和 RMASK (00000100) 执行按位或运算时，结果为 4，如下所示：

```
00000000  overflowFlag
00000100  RMASK
----------
00000100  result of bitwise or
```

运算结果被赋值给 overflowFlag，从而替换之前的值。在步骤 2 中，当对操作数 overflowFlag (00000100) 和 GMASK (00000010) 执行按位或运算时，结果为 6，如下所示：

```
00000100  overflowFlag
00000010  GMASK
----------
00000110  result of bitwise or
```

overflowFlag 的结果值表明数据成员 red 中存在溢出，数据成员 green 中存在溢出，而数据成员 blue 中不存在溢出。因此，语句 p1.overflow() 将返回布尔值 true，如下所示：

```
00000100  overflowFlag
00000111  CHECK
----------
00000110  result of bitwise and
```

我们将编写一个小型驱动程序来测试 Pixel 类的新方法。

```cpp
/*---- program chapter10_3 ----------------------------*/
/* Program program10_3                                 */
/* Driver program to test overflow state of Pixel      */

#include "Pixel.h"
#include <iostream>
using namespace std;

int main()
{
    //Declare objects
    Pixel defaultP;
    Pixel grayP(100);
    Pixel redP(255,255,0);

    //Create overflow in red
    defaultP = grayP + redP;
    cout << defaultP << endl;
    if (defaultP.overflow())
    {
        defaultP.reset();
    }
    cout << defaultP << endl;

    return 0;
}
```

示例运行的输出如下：

```
Ingbers-MacBook-Pro:Programs jaingber$ g++ main.cpp Pixel.cpp
Ingbers-MacBook-Pro:Programs jaingber$ ./a.out
355 100 100
255 100 100
```

我们可以看到表达式 defaultP.overflow() 返回了 true 值，表明已检测到溢出，并且已执行语句 defaultP.reset()，将 defaultP 的值重置为有效状态。

## 修改！

- 1. 向 Pixel 类添加以下方法：

```cpp
bool checkRed() const;
bool checkGreen() const;
bool checkBlue() const;
```

每个方法都应检查调用对象的 overflowFlag，如果在指定数据成员中发生溢出则返回 true，否则返回 false。

