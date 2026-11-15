
```cpp
/**
 * Input (>>) operator.
 * Expected Pixel format is 100:150:100
 * File name: Pixel.cpp
 */
istream& operator>>(istream& in, Pixel& p)
{
    // Declare local objects.
    char ch;

    // Input integer value for red data member.
    in >> p.red;

    // Input colon. If colon not encountered,
    // set error state and return.
    in >> ch;
    if (ch != ':')
    {
        in.setstate(ios::failbit);
        return in;
    }

    // Input integer value for green data member.
    in >> p.green;

    // Input colon. If colon not encountered,
    // set error state and return.
    in >> ch;
    if (ch != ':')
    {
        in.setstate(ios::failbit);
        return in;
    }

    // Input integer value for blue data member.
    in >> p.blue;

    return in;
}
/**********************************************************************/
```

在这个函数定义中，函数 setstate() 用于将 istream 置于失败状态。函数 setstate() 是 istream 类的成员函数。在语句

```
in.setstate(ios::failbit);
```

中，由 in 引用的 istream 对象调用 setstate 函数，并将 failbit 设置为 true。

使用 `Pixel` 类时的另一个潜在错误是将大于 255 的值赋给一个或多个数据成员。潜在溢出错误的处理将在下一节中讨论。

## 验证对象

回顾，我们将像素定义为红、绿、蓝三元组，其中三元组中的每个值范围为 0 到 255。`Pixel` 类包含三个类型为 unsigned int 的数据成员（red、green 和 blue）。数据类型 unsigned int 防止出现负值，但不能防止值超过最大值 255。请考虑使用 `Pixel` 类的以下示例：

```cpp
/*
 * Program chapter10_1
 *
 * Driver program for testing Pixel class
 *
 * #include "Pixel.h" //Required for Pixel
 * #include <iostream> //Required for cout
using namespace std;
int main()
{
 //Test constructors
 Pixel defaultP;
 Pixel grayP(100);
 Pixel redP(255,0,0);

//Test output operator
cout << "Default pixel: " << defaultP << endl;
cout << "Gray pixel: " << grayP << endl;
cout << "Red pixel: " << redP << endl;

//Test arithmetic operators
//Addition
defaultP = grayP + redP;
cout << "After addition, defaultP: " << defaultP << endl;

return 0;
}
```

此程序的示例运行如下：

```
Ingbers-MacBook-Pro:Programs jaingber$ g++ main.cpp Pixel.cpp
Ingbers-MacBook-Pro:Programs jaingber$ ./a.out
Default pixel: 0 0 0
Gray pixel: 100 100 100
Red pixel: 255 0 0
After addition, defaultP: 355 100 100
```

我们看到 `defaultP` 的红色值已超过最大值 255。如果 `Pixel` 对象的任何数据成员超过最大值，处理图像时可能会出现意外结果。为处理这种情况，我们将遵循前一节中讨论的 `istream` 类模型。`Pixel` 类将维护一个溢出标志，并在每次检测到溢出时设置溢出标志中的相应位。使用 `Pixel` 类的应用程序负责检查溢出标志的状态。将提供公共方法以允许访问溢出标志，并将提供一个 `private` 验证方法来帮助维护其状态。验证方法将由 `Pixel` 类的所有修改方法调用。下面提供了扩展的 `Pixel` 类声明：

```cpp
/*---------------------------------------*/
/* Pixel class declaration.              */
/* File name: Pixel.h                    */
/* This class implements the concept of a pixel */
/*---------------------------------------*/
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
    Pixel(unsigned); //Gray scale
    Pixel(unsigned,unsigned,unsigned); //Full color range

    //Overloaded operators.
    Pixel operator+(const Pixel& p) const;
    Pixel operator*(double v) const;
    Pixel operator*(unsigned v) const;

    //IO Operators.
    friend istream& operator>>(istream& in, Pixel& p);
    friend ostream& operator<<(ostream& out, const Pixel& p);

    bool overflow() const; //check overflow state
    void reset(); //reset overflow state

private:
    unsigned int red, green, blue;
    unsigned short overflowFlag;

    static const unsigned short RMASK = 4;
    static const unsigned short GMASK = 2;
    static const unsigned short BMASK = 1;
    static const unsigned short CHECK = 7;
    static const unsigned MAXVAL = 255;

    void validate(); //set overflow bits
};
```

请注意，我们已向 `Pixel` 类添加了五个 `static` 常量。公共常量 `MAXVAL` 设置为 255，是公共接口的一部分。四个私有位掩码常量在各种类方法中被引用，并被赋予整数值 1、2、4 和 7。回顾，8 位中的二进制值 1 可表示为 00000001；二进制 2 为 00000010；二进制 4 为 00000100；二进制 8 为 00001000。这些常量用作位掩码，用于设置和检查 overflowFlag 的状态。位掩码是与位运算符一起使用的整数数据，用于在单个位操作中操作位。下面提供了扩展 Pixel 类的实现：

```cpp
#include "Pixel.h"
/*
 * Pixel class implementation.
 * File name: Pixel.cpp.
 * Addition (+) operator.
 */
Pixel Pixel::operator+(const Pixel& p) const
{
    Pixel temp;
    temp.red = red + p.red;
    temp.green = green + p.green;
    temp.blue = blue + p.blue;
    temp.validate();
    return temp;
}
```

```cpp
/*
 * Multiplication (*) operator.
 */
Pixel Pixel::operator*(double v) const
{
    Pixel temp;
    temp.red = red*v;
    temp.green = green*v;
    temp.blue = blue*v;
    temp.validate();
    return temp;
}
```

```cpp
/*
 * Division (/) operator.
 */
Pixel Pixel::operator/(unsigned int v) const
{
    Pixel temp;
    temp.red = red/v;
    temp.green = green/v;
    temp.blue = blue/v;
    temp.validate();
    return temp;
}
```

```cpp
/*
 * operator<<(ostream& out, const Pixel& p)
 */
ostream& operator<<(ostream& out, const Pixel& p)
{
    out << p.red << ' ';
    out << p.green << ' ';
    out << p.blue;
    return out;
}
```

```cpp
istream& operator>>(istream& in, Pixel& p)
{
 in >> p.red >> p.green >> p.blue;
 p.validate();
 return in;
}
```

```cpp
Pixel::Pixel()
{
 //Black
 red=green=blue=0;
 return;
}
```

```cpp
Pixel::Pixel(unsigned int value)
{
 //Gray scale
 red=green=blue=value;
 validate();
 return;
}
```

```cpp
Pixel::Pixel(unsigned int r, unsigned int g, unsigned int b)
{
 //Full color range
 red=r;
 green=g;
 blue=b;
 validate();
 return;
}
```

```cpp
bool Pixel::overflow() const
{
 return (overflowFlag&CHECK);
}
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
/*---------------------------------------*/
void Pixel::validate()
{
    if(red > MAXVAL) overflowFlag = overflowFlag|RMASK;
    if(green > MAXVAL) overflowFlag = overflowFlag|GMASK;
    if(blue > MAXVAL) overflowFlag = overflowFlag|BMASK;
}
```

请注意，私有修改方法 `void Pixel::validate()` 使用位运算符 `|` 来设置 `overflowFlag` 的状态。方法 `validate()` 必须由 `Pixel` 类的所有修改方法调用，以保证 `overflowFlag` 的正确状态。公共访问方法 `bool Pixel::overflow()` 使用位运算符 `&` 来返回 `overflowFlag` 的状态。我们将更详细地查看这两种方法，并讨论位运算符。

## 位运算符

位运算符对其操作数的每个位执行操作。C++ 支持三个二进制位运算符：按位或 (`|`)、按位与 (`&`) 和按位异或 (`^`)，以及一元按位非运算符 (`~`)。这些运算符的操作数限制为整型，例如 `int` 或 `char`。表 10.2 提供了位运算符的真值表。

| A | B | ~A | A\|B | A^B | A&B |
|---|---|---|---|---|---|
| 0001 | 0001 | 1110 | 0001 | 0000 | 0001 |
| 0010 | 0010 | 1101 | 0010 | 0000 | 0010 |
| 0011 | 0100 | 1100 | 0111 | 0111 | 0000 |
| 0100 | 0111 | 1011 | 0111 | 0011 | 0100 |

为说明位运算符的用法，假设已定义一个 `Pixel` 对象并具有以下值：

| Pixel pl | |
|---|---|
| 278 | 无符号 red |
| 298 | 无符号 green |
| 150 | 无符号 blue |
| 0 | 无符号短整型 overflowFlag |

语句 `pl.validate();` 会产生以下程序跟踪和内存快照：
