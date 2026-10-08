
Line 23: Division by!

前面的程序工作原理如下：第 17 行的语句中，`divZero`是类名，`divZero`类没有成员，所以我们无法对抛出的对象进行。因此，在第 21 行的`catch`块中，我们只指定数据类型而不

# 创建你自己的类

示例 14-10 设计并使用的异常类没有成员。接下来，我们说明如何创建带有成员的异常类。

如果你想在异常类中包含成员，通常会包含构造函数和`what`函数。考虑以下`divisionZero`类的定义。

// 用户自定义异常类。

```cpp
#include <iostream>                          //Line 1
#include <string>                              //Line 2

using namespace std;                            //Line 3

class divisionZero                             //Line 4
public:
    divisionByZero()                           //Line 5
    {                               //Line 6
        message = "Division by zero";         //Line 7
    }                                          //Line 8
                                                //Line 9, 10
    divisionByZero(string str)                //Line 11
    {                               //Line 12
        message = str;                         //Line 13
    }                                          //Line 14

    string what()                               //Line 15
    {                               //Line 16
        return message;                        //Line 17
    }                                          //Line 18

private:
    string message;                                //Line 19
};                                              //Line 20, 21
```

`divisionZero`类的定义两个构造函数：默认构造函数和带参数的构造函数。对象中的 "Division by zero"。带参数的构造函数允许用户创建自己的错误消息。`what`函数用于返回存储在对象中的字符串。

> 在`divisionZero`类的定义中，构造函数也可以是：

`divisionByZero() : message("Division by zero") {}`

`divisionByZero(string str) : message(str){}`

示例 14-11 中的程序使用前面的类来抛出异常。

# 示例 14-11

```cpp
// 使用用户定义的异常类 divisionByZero 以及
// 默认错误消息。
```

```cpp
#include <iostream>
#include "divisionByZero.h"

namespace std;

int main() {
    int dividend, divisor, quotient;

    try {
        cout << "Line 9: Enter the dividend: ";
        cin >> dividend;
        cout << endl;

        cout << "Line 12: Enter the divisor: ";
        cin >> divisor;
        cout << endl;

        if (divisor == 0)
            throw divisionByZero();

        quotient = dividend / divisor;
        cout << "Line 18: Quotient = " << quotient;
        cout << endl;
    } catch (divisionByZero divByZeroObj) {
        cout << "Line 22: In the divisionByZero ";
        cout << "catch block: ";
        cout << divByZeroObj.what() << endl;
    }

    return 0;
}
```

示例运行 1：在本次示例运行中，输入为阴影部分。

Line 9: Enter the dividend: 28

Line 12: Enter the divisor: 5

Line 18: Quotient = 4

# 示例运行 2：在本次示例运行中，用户输入为阴影部分。

Line 9: Enter the dividend: 35

Line 12: Enter the divisor: 0

Line 22: In the divisionByZero catch block: Division by zero

在该程序中，如果用户为除数输入 0，第 16 行的语句将抛出一个`divisionByZero`类的对象（异常）。此抛出的异常被第 20 行的`catch`块捕获并处理。`catch`中的参数`divByZeroObj`捕获了抛出对象的值，并使用函数`what()`返回对象中存储的字符串。第 22 行的语句输出相应的错误消息。

14-12 中的程序与示例 14-11 中的程序相似。在这里，抛出的对象仍然是一个匿名对象，但错误消息是由用户指定的（请参见第 10 行的语句）。

![](img/d998292a174f7bfd8a26bfbada3d454e_1060_0.png)

```cpp
// 使用用户定义的异常类 divisionByZero 以及
// 特定的错误消息。

#include <iostream> // Line 15
#include "divisionByZero.h" // Line 16

using namespace std; // Line 3

int main() // Line 4
{
    int dividend, divisor, quotient; // Line 5-6

    try { // Line 7
        cout << "Line 9: Enter the dividend: "; // Line 8
        cin >> dividend; // Line 10
        cout << endl; // Line 11

        cout << "Line 12: Enter the divisor: "; // Line 12
        cin >> divisor; // Line 13
        cout << endl; // Line 14

        if (divisor == 0)
            throw divisionByZero("Found division by 0"); // Line 16

        quotient = dividend / divisor; // Line 17
        cout << "Line 18: Quotient = " << quotient // Line 18
        cout << endl; // Line 19
    }
```

## 1012 | 第 14 章：异常处理

```cpp
catch(divisionByZero divByZeroObj)
{
    cout << "Line 22: In the divisionByZero "
    << "catch block: " << divByZeroObj.what() << endl;

    return 0;
}
```

**示例运行 1：**在本次运行中，用户输入为阴影部分。

- Line 9: Enter the dividend: 28

Line 12: Enter the divisor: 6

Line 18: Quotient = 4

**示例运行 2：**在本次运行中，用户输入为阴影部分。

- Line 9: Enter the dividend: 35

Line 12: Enter the divisor: 0

Line 22: In the divisionByZero catch block: Found division by 0

该程序的工作原理与示例 14-11 中的程序相同。细节留给你们进行练习。

在示例 14-11 和 14-12 的程序中，数据处理是在`main`函数中完成的。因此，异常在`main`函数中抛出、捕获并处理。示例 14-13 中的程序使用了用户定义的函数`doDivision`来处理数据。因此，异常在`doDivision`函数中抛出、捕获并处理。

> 示例 14-13

```cpp
// 处理函数抛出的异常

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision();

int main()
{
    doDivision();
    return 0;
}
```

```cpp
void doDivision() {
    // Line 10
    int dividend, divisor, quotient;
    // Line 11
    // Line 12
    try {
        // Line 13
        cout << "Line 15: Enter the dividend: ";
        // Line 14
        cin >> dividend;
        // Line 15
        cout << endl;
        // Line 16
        cout << "Line 18: Enter the divisor: ";
        // Line 17
        cin >> divisor;
        // Line 18
        cout << endl;
        // Line 19
        if (divisor == 0)
            throw divisionByZero("Found division by 0"); // Line 20

        // Line 21
        quotient = dividend / divisor;
        // Line 22
        cout << "Line 23: Quotient = " << quotient // Line 23
        cout << endl; // Line 24
    } catch (divisionByZero divByZeroObj) {
        cout << "Line 25: In the divisionByZero ";
        cout << "catch block: " << divByZeroObj.what() << endl; // Line 26
    }
}
```

示例运行 1：在本次示例运行中，输入为阴影部分。

Line 9: Enter the dividend: 28

Line 12: Enter the divisor: 5

Line 18: Quotient = 4

示例运行 2：在本次示例运行中，输入为阴影部分。

Line 9: Enter the dividend: 35

Line 12: Enter the divisor: 0

Line 22: In the divisionByZero catch block: Division by zero

// 用户定义的异常类。

```cpp
#include <iostream>
#include <string>

using namespace std;

class negativeNumber {
public:
    negativeNumber() : message("Division by zero") {}
    negativeNumber(string str) : message(str) {}
    string what() {
        return message;
    }

private:
    string message;
};
```

// 注意`negativeNumber`的定义与`divisionZero`的定义相似。

```cpp
class circleType {
public:
    circleType() : radius(0) {}

    void setRadius(double r) {
        if (r < 0)
            throw negativeNumber("Radius cannot be negative");
        radius = r;
    }

    double getRadius() {
        return radius;
    }

    double area() {
        return 3.14159 * radius * radius;
    }

    double circumference() {
        return 2 * 3.14159 * radius;
    }

private:
    double radius;
};
```

## 重新抛出和抛出异常

圆的周长。如果用户输入负数，第 16 行的语句将抛出一个异常，这是一个`negativeNumber`对象，`catch`块将处理该异常。在示例运行 1 中，用户输入 5.25（非负数），程序输出圆的面积和周长。在示例运行 2 中，用户输入 -2.5（这是一个负数），第 21 行的语句输出半径不能为负。

当`try`块中发生异常时，控制会立即传递到其中一个`catch`块。通常，`catch`块要么处理异常，要么部分处理异常后抛出相同的异常，要么抛出另一个异常以便让调用环境处理该异常。示例 14-4 到 14-14 中的`catch`块处理重新抛出或抛出异常，这在以下情况下非常有用：如果`catch`块捕获了异常但无法处理它，或者`catch`块判断异常应该由调用块或环境来处理。这允许程序员在统一的地方提供异常处理的调用代码。

要重新抛出或抛出异常，我们使用`throw`语句。通过`catch`块抛出异常的通用语法是：

```
throw;
```

（在这种情况下，重新抛出相同的异常）或

```cpp
throw expression;
```

其中`expression`是常量值、变量或对象。被抛出的对象可以是特定对象，也可以是匿名对象。

函数在它的头部使用`throw`子句来指定它所抛出的异常（以便在某处处理）。例如，除法函数在头部中指定了`int`、`string`和`divisionByZero`类型的异常，其中`divisionByZero`是之前定义的类。

```
void expThrowExec(int x) throw (int, string, divisionByZero)
{
  .
  .
  //包含适当的 throw 语句
  .
  .
}
```

示例 14-15 中的程序进一步解释了函数如何指定它所抛出的异常。

## 示例 14-15
