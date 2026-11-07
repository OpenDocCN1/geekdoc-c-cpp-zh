
```cpp
cout << "*~*~*~*~* Testing Friend Function "
     << "two *~*~*~*~*" << endl << endl;    //Line 14

two(aObject);                              //Line 15

return 0;
}
```

### 示例运行：

```text
Line 11: aObject.x: In class classIllusFriend: x = 32

*~*~*~*~* Testing Friend Function two *~*~*~*~*

In class classIllusFriend: x = 45
Line 5: In Friend Function two accessing private member variable x = 45
In class classIllusFriend: x = 88
Line 8: In Friend Function two accessing private member variable x = 88
```

大部分情况下，输出本身就能说明问题。第15行的语句调用了函数 two（**类** classIllusFriend 的**友元**函数），并将对象 aObject 作为实参传入。注意，函数 two 生成了输出的最后四行。

本章后面你将学到，对于类而言，流插入运算符和流提取运算符只能重载为**友元**函数。

## 运算符函数作为成员函数和非成员函数

本章开头指出，在类的定义中包含运算符函数时必须遵循某些规则。本节将描述这些规则。

大多数运算符函数既可以是成员函数，也可以是非成员函数——即类的**友元**函数。要使运算符函数成为类的成员函数或非成员函数，请记住以下几点：

- 1. 为类重载运算符 `()`、`[]`、`->` 或 `=` 中任何一个的函数必须声明为该类的成员。
- 2. 假设为某个类重载运算符 op——比如 opOverClass。（这里，op 表示可重载的运算符，例如 + 或 >>。）
  - a. 如果 op 的最左操作数是不同类型的对象（即不是 opOverClass 类型），则为 opOverClass 重载运算符 op 的函数必须是非成员——即 **类** opOverClass 的友元。
  - b. 如果为 **类** opOverClass 重载运算符 op 的运算符函数是 **类** opOverClass 的成员，那么在对 opOverClass 类型的对象应用 op 时，op 的最左操作数必须是 opOverClass 类型。

在类定义中包含运算符函数时，必须遵循这些规则。

本章后面你会看到，为类重载插入运算符 << 和提取运算符 >> 的函数必须是非成员——即该类的友元函数。

除了前面提到的某些运算符外，运算符既可以重载为成员函数，也可以重载为非成员函数。下面的讨论将展示这两类函数之间的区别。

为了便于讨论运算符重载，我们将使用下面给出的类 rectangleType。（尽管第12章定义了这个类，但第12章不是本章的先修内容。为便于参考，我们重现该类的定义以及成员函数的定义。）

```cpp
class rectangleType
{
public:
    void setDimension(double l, double w);
        //Function to set the length and width of the rectangle.
        //Postcondition: length = l; width = w;

    double getLength() const;
        //Function to return the length of the rectangle.
        //Postcondition: The value of length is returned.

    double getWidth() const;
        //Function to return the width of the rectangle.
        //Postcondition: The value of width is returned.

    double area() const;
        //Function to return the area of the rectangle.
        //Postcondition: The area of the rectangle is
        //              calculated and returned.

    double perimeter() const;
        //Function to return the perimeter of the rectangle.
        //Postcondition: The perimeter of the rectangle is
        //              calculated and returned.

    void print() const;
        //Function to output the length and width of
        //the rectangle.

    rectangleType();
        //Default constructor
        //Postcondition: length = 0; width = 0;

    rectangleType(double l, double w);
        //Constructor with parameters
        //Postcondition: length = l; width = w;
```

```cpp
rectangleType::rectangleType()
{
    length = 0;
    width = 0;
}
```

类 `rectangleType` 有两个私有成员变量：length 和 width，二者均为 `double` 类型。在重载运算符时，我们将向类 `rectangleType` 添加运算符函数。

另外，假设你有以下语句：

```cpp
rectangleType myRectangle;
rectangleType yourRectangle;
rectangleType tempRect;
```

也就是说，`myRectangle`、`yourRectangle` 和 `tempRect` 是 `rectangleType` 类型的对象。

C++ 包含二元运算符和一元运算符。它还有三元运算符，但三元运算符不能被重载。接下来几节将讨论如何重载各种二元运算符和一元运算符。

## 重载二元运算符

假设 `#` 表示要为类 `rectangleType` 重载的二元运算符（算术运算符，例如 +；或关系运算符，例如 ==）。该运算符既可以重载为类的成员函数，也可以重载为 `friend` 函数。我们将描述重载该运算符的两种方式。

### 将二元运算符重载为成员函数

假设 `#` 被重载为类 `rectangleType` 的成员函数。为类 `rectangleType` 重载 `#` 的函数名是：

```cpp
operator#
```

因为 `myRectangle` 和 `yourRectangle` 是 `rectangleType` 类型的对象，所以可以执行以下操作：

```cpp
myRectangle # yourRectangle
```

编译器将该表达式转换为以下表达式：

```cpp
myRectangle.operator#(yourRectangle)
```

这个表达式清楚地表明，函数 `operator#` 只有一个参数，即 `yourRectangle`。

因为 `operator#` 是类 `rectangleType` 的成员，而 `myRectangle` 是 `rectangleType` 类型的对象，所以在上述语句中，`operator#` 可以直接访问对象 `myRectangle` 的私有成员。因此，`operator#` 的第一个参数是调用函数 `operator#` 的对象，第二个参数则作为参数传递给该函数。

### 将二元（算术或关系）运算符重载为成员函数的一般语法

本节描述将二元运算符重载为类的成员函数时函数的一般形式。

**函数原型**（应包含在类的定义中）：

```cpp
returnType operator#(const className&) const;
```

其中，# 表示要重载的二元运算符（算术或关系运算符）；returnType 是函数返回值的类型；className 是为其重载该运算符的类的名称。

**函数定义：**

```cpp
returnType className::operator#
                 (const className& otherObject) const
{
    //algorithm to perform the operation

    return value;
}
```

> **注意**  重载关系运算符的函数的返回类型是 **bool**。

### 示例 14-4

让我们为类 rectangleType 重载 +、*、== 和 !=。这些运算符被重载为成员函数。

```cpp
class rectangleType
{
public:
    void setDimension(double l, double w);
    double getLength() const;
    double getWidth() const;
    double area() const;
    double perimeter() const;
    void print() const;

    rectangleType operator+(const rectangleType&) const;
    //Overload the operator +
    rectangleType operator*(const rectangleType&) const;
    //Overload the operator *
```

```cpp
bool rectangleType::operator!=
             (const rectangleType & rectangle) const
{
    return (length != rectangle.length ||
            width != rectangle.width);
}
```

（注意，在编写完重载运算符 == 的函数的定义后，你可以使用它来编写重载运算符 != 的函数的定义。我们将细节留作练习。）

考虑以下程序。（我们假设类 rectangleType 的定义位于头文件 rectangleType.h 中。）

```cpp
//This program shows how to use the class rectangleType.
#include <iostream>
#include "rectangleType.h"

using namespace std;

int main()
{
    rectangleType rectangle1(23, 45);              //Line 1
    rectangleType rectangle2(12, 10);              //Line 2
    rectangleType rectangle3;                      //Line 3
    rectangleType rectangle4;                      //Line 4

    cout << "Line 5: rectangle1: ";                //Line 5
    rectangle1.print();                             //Line 6
    cout << endl;                                   //Line 7

    cout << "Line 8: rectangle2: ";                //Line 8
    rectangle2.print();                             //Line 9
    cout << endl;                                   //Line 10

    rectangle3 = rectangle1 + rectangle2;          //Line 11

    cout << "Line 12: rectangle3: ";               //Line 12
    rectangle3.print();                             //Line 13
    cout << endl;                                   //Line 14

    rectangle4 = rectangle1 * rectangle2;          //Line 15

    cout << "Line 16: rectangle4: ";               //Line 16
    rectangle4.print();                             //Line 17
    cout << endl;                                   //Line 18

    if (rectangle1 == rectangle2)                   //Line 19
        cout << "Line 20: rectangle1 and "
             << "rectangle2 are equal." << endl;   //Line 20
    else                                            //Line 21
        cout << "Line 22: rectangle1 and "
             << "rectangle2 are not equal."
             << endl;                               //Line 22
}
```
