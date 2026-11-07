

## 运算符函数的语法

运算的结果是一个值。因此，运算符函数是一个返回值函数。

运算符函数头的语法为：

```
returnType operator operatorSymbol(formal parameter list)
```

在 C++ 中，`operator` 是保留字。

回顾一下，类上唯一的内置操作是赋值（=）和成员选择。要在类对象上使用其他运算符，必须显式重载它们。运算符重载为用户定义的数据类型提供了与内置数据类型相同的简洁表达式。

要为类重载运算符：

- 1. 在类的定义中包含声明该运算符重载函数（即运算符函数）的函数原型的语句。
- 2. 编写该运算符函数的定义。

在类定义中包含运算符函数时，必须遵循某些规则。这些规则将在本章后面的“运算符函数作为成员函数和非成员函数”一节中描述。

## 重载运算符：一些限制

重载运算符时，请记住以下几点：

- 1. 不能改变运算符的优先级。
- 2. 不能改变结合性。（例如，算术运算符加法的结合性是从左到右的，并且不能改变。）
- 3. 重载运算符不能使用默认参数。
- 4. 不能改变运算符所接收的参数个数。
- 5. 不能创建新运算符。只能重载已有的运算符。
- 6. 不能重载的运算符包括：
    - `.` `.*` `::` `?:` `sizeof`
- 7. 运算符作用于内置类型（如 `int`）时的含义保持不变。也就是说，不能重新定义运算符作用于内置数据类型的方式。
- 8. 既可以针对用户定义类型的对象重载运算符，也可以针对用户定义类型对象与内置类型对象的组合重载运算符。

## 示例 13-1

在本章开头，我们提到，如果能为类重载各种运算符，就可以提高类的灵活性。既然我们已经了解了为类重载运算符的语法以及运算符重载的某些限制，在本例中，我们只说明如何为类 `clockType` 重载关系运算符 `==`。在一般性地讨论与运算符重载相关的各种概念之后，本章后面的编程示例 clockType 将展示如何为类 `clockType` 重载其他运算符，例如 `>>`、`<<` 和 `++`（前置递增）。

为类 `clockType` 重载相等运算符的函数原型是：

```cpp
bool operator==(const clockType& otherClock) const;
```

因此，这条语句必须包含在类 `clockType` 的定义中。由于在本例中我们只说明如何重载运算符 `==`，所以不包含递增时间的函数。因此，考虑以下类 `clockType` 的定义：

```cpp
class clockType
{
public:
    void setTime(int hours, int minutes, int seconds);
    void printTime() const;

    bool operator==(const clockType& otherClock) const;
        //Overload the operator ==

    clockType(int = 0, int = 0, int = 0);

private:
    int hr;
    int min;
    int sec;
};
```

接下来，我们必须编写函数 `operator==` 的定义，如下所示：

```cpp
bool clockType::operator==(const clockType& otherClock) const
{
    return (hr == otherClock.hr && min == otherClock.min
            && sec == otherClock.sec);
}
```

请注意，函数 `operator==` 的函数体与第 10 章给出的函数 `equalTime` 的函数体相同。此外，类 `clockType` 的其他函数的定义也与第 10 章给出的定义相同。

以下程序说明如何使用类 clockType 的修改后定义：

```cpp
#include <iostream>
#include "clockType.h"

using namespace std;

int main()
{
        clockType myClock(8, 23, 50);
        clockType yourClock(8, 23, 50);
        clockType tempClock(9, 16, 25);

        cout << "Line 6: myClock: ";
        myClock.printTime();
        cout << endl;

        cout << "Line 9: yourClock: ";
        yourClock.printTime();
        cout << endl;

        cout << "Line 12: tempClock: ";
        tempClock.printTime();
        cout << endl;

                //Compare myClock and yourClock
        if (myClock == yourClock) {
                cout << "Line 16: The time of myClock and "
                     << "yourClock are equal." << endl;
        }
        else
                cout << "Line 18: The time of myClock and "
                     << "yourClock are not equal." << endl;

                //Compare myClock and tempClock
        if (myClock == tempClock)
                cout << "Line 20: The time of myClock and "
                     << "tempClock are equal." << endl;
        else
                cout << "Line 22: The time of myClock and "
                     << "tempClock are not equal." << endl;

        return 0;
}//end main
```

### 示例运行：

```
Line 6: myClock: 08:23:50
Line 9: yourClock: 08:23:50
Line 12: tempClock: 09:16:25
Line 16: The time of myClock and yourClock are equal.
Line 22: The time of myClock and tempClock are not equal.
```

该示例运行很容易理解。但请注意，第 15 行的语句使用运算符 `==` 比较 myClock 和 yourClock 的时间。同样，第 19 行的语句使用运算符 `==` 比较 myClock 和 tempClock 的时间。第 16 行和第 22 行的语句输出表明，运算符 `==` 已成功为类 `clockType` 重载。

在一般性地讨论运算符重载之前，接下来两节将讨论与运算符重载相关的两个重要概念。

### 指针 `this`

类的成员函数可以（间接）访问该类的给定对象的成员变量。有时，成员函数需要将对象作为一个整体来引用，而不是引用对象的各个成员变量。在成员函数的定义中，如何将对象作为一个整体（即作为一个单一单元）来引用，尤其是在对象未作为参数传递时？类的每个对象都维护一个指向自身的（隐藏）指针，这个指针的名称是 `this`。在 C++ 中，`this` 是保留字。指针 `this`（在成员函数中）可供你使用。当对象调用成员函数时，该成员函数会引用该对象的指针 `this`。例如，假设 `test` 是一个类，并且有一个名为 `one` 的成员函数。再假设 one 的定义如下所示：

```cpp
test test::one()
{
    .
    .
    .
    return *this;
}
```

如果 x 和 y 是 test 类型的对象，则语句：

```cpp
y = x.one();
```

将对象 x 的值复制到对象 y 中。也就是说，x 的成员变量被复制到 y 的相应成员变量中。当对象 x 调用函数 one 时，成员函数 one 定义中的指针 `this` 指向对象 x，因此 `this` 表示 x 的地址，而 `*this` 表示 x 的内容。另一方面，在语句

```cpp
x = y.one();
```

中，成员函数 one 定义中的指针 `this` 指向对象 y，因此 `this` 表示 y 的地址，而 `*this` 表示 y 的内容。所以该语句将对象 y 的内容复制到对象 x 中。

以下示例说明指针 `this` 如何工作。

## 示例 13-2

在第 11 章中，我们定义了 `class` rectangleType。我们将向该类添加一个函数，以说明指针 `this` 如何工作。我们不给出该类的完整定义。我们只展示使用指针 `this` 返回整个对象的函数。完整定义可在本书的配套网站上找到。

```cpp
class rectangleType
{
public:
    //The functions setDimension, getLength, getWidth, area,
    //perimeter, print, and the constructors are the same as before.

    rectangleType doubleDimensions();
    //Postcondition: length = 2 * length;
    //              width = 2 * width;

private:
    double length;
    double width;
};
```

假设成员函数 `doubleDimensions` 的定义是：

```cpp
rectangleType rectangleType::doubleDimensions()
{
    length = 2 * length;
    width = 2 * width;

    return *this;
}
```

函数 `doubleDimensions` 将对象的长度和宽度都加倍，并使用指针 `this` 返回整个对象的值。

考虑以下函数 main：

```cpp
//Chapter 13: this pointer illustration

#include <iostream>                              //Line 1
#include <iomanip>                               //Line 2
#include "rectangleType.h"                       //Line 3

using namespace std;                             //Line 4

int main()                                       //Line 5
{                                                //Line 6
    rectangleType oldYard(20.00, 10.00);         //Line 7
    rectangleType newYard;                       //Line 8

    cout << fixed << showpoint << setprecision(2); //Line 9
```

