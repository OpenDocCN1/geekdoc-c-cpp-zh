

```cpp
catch (divisionByZero divByZeroObj)                         //Line 13
{
    cout << "Line 14: In the divisionByZero "
         << "catch block: "
         << divByZeroObj.what() << endl;                    //Line 14

    return 0;                                               //Line 15
}
```

**示例运行 1：** 在此示例运行中，用户输入以底纹显示。

第 3 行：输入被除数：34

第 6 行：输入除数：5

第 12 行：商 = 6

**示例运行 2：** 在此示例运行中，用户输入以底纹显示。

第 3 行：输入被除数：56

第 6 行：输入除数：0

第 14 行：在 divisionByZero catch 块中：发现除数为零

该程序的工作方式与示例 14-11 中的程序相同。细节留作练习。

在示例 14-11 和 14-12 的程序中，数据操作在函数 main 中完成。因此，异常在函数 main 中抛出、捕获和处理。示例 14-13 中的程序使用用户自定义函数 doDivision 来操作数据。因此，异常在函数 doDivision 中抛出、捕获和处理。

### 示例 14-13

```cpp
// Handling an exception thrown by a function.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision();

int main()
{
    doDivision();                                             //Line 1

    return 0;                                                  //Line 2
}

void doDivision()
{
    int dividend, divisor, quotient;                         //Line 3

    try
    {
        cout << "Line 4: Enter the dividend: ";             //Line 4
        cin >> dividend;                                     //Line 5
        cout << endl;                                        //Line 6

        cout << "Line 7: Enter the divisor: ";              //Line 7
        cin >> divisor;                                      //Line 8
        cout << endl;                                        //Line 9

        if (divisor == 0)                                    //Line 10
            throw divisionByZero();                          //Line 11

        quotient = dividend / divisor;                        //Line 12
        cout << "Line 13: Quotient = " << quotient
             << endl;                                        //Line 13
    }
    catch (divisionByZero divByZeroObj)                       //Line 14
    {
        cout << "Line 15: In the function "
             << "doDivision: " << divByZeroObj.what() << endl; //Line 15
    }
}
```

**示例运行 1：** 在此示例运行中，用户输入以底纹显示。

第 4 行：输入被除数：34

第 7 行：输入除数：5

第 13 行：商 = 6

**示例运行 2：** 在此示例运行中，用户输入以底纹显示。

第 4 行：输入被除数：56

第 7 行：输入除数：0

第 15 行：在函数 doDivision 中：除数为零

### 示例 14-14

示例 10-8 定义了 **类** `circleType` 来实现圆的基本属性。如果一个 `circleType` 对象试图将半径设置为负数，则该类的函数 `setRadius` 会将半径设置为 0。在本例中，我们首先定义 **类** `negativeNumber` 来处理负数异常，然后使用该类在 `circleType` 对象试图将半径设置为负数时抛出异常。因此，考虑以下类：

```cpp
// User-defined exception class.

#include <iostream>
#include <string>

using namespace std;

class negativeNumber
{
public:
    negativeNumber()
    {
        message = "Number cannot be negative";
    }

    negativeNumber(string str)
    {
        message = str + " cannot be negative";
    }

    string what()
    {
        return message;
    }

private:
    string message;
};
```

注意，**类** `negativeNumber` 的定义与 **类** `divisionByZero` 的定义类似。

**类** `circleType` 的定义与示例 10-8 中相同，不同之处在于函数 `setRadius` 的定义。该函数的修改后定义如下：

```cpp
void circleType::setRadius(double r)
{
    if (r < 0)
        throw negativeNumber("Radius");

    radius = r;
}
```

如果参数 `r` 的值为负数，则函数 `setRadius` 抛出一个 `negativeNumber` 对象。在这种情况下，所抛出对象的实例变量 `message` 的值为 "Radius cannot be negative."。用户程序将处理该函数抛出的异常（如果有）。

考虑以下程序：

```cpp
// The user program that uses the class circleType

#include <iostream>
#include <iomanip>
#include "circleType.h"
#include "negativeNumber.h"

using namespace std;                                      //Line 1
int main()                                                //Line 2
{                                                         //Line 3
    circleType circle;

    double radius;                                         //Line 4

    cout << fixed << showpoint << setprecision(2);        //Line 5
    try                                                   //Line 6
    {                                                     //Line 7
        cout << "Line 8: Enter the radius of a circle: "; //Line 8
        cin >> radius;                                    //Line 9
        cout << endl;                                     //Line 10

        circle.setRadius(radius);                         //Line 11

        cout << "Line 12: circle - "
             << "radius: " << circle.getRadius()
             << ", area: " << circle.area()
             << ", circumference: "
             << circle.circumference() << endl;           //Line 12
    }                                                     //Line 13
    catch (negativeNumber obj)                             //Line 14
    {                                                     //Line 15
        cout << "Line 16: " << obj.what() << endl;        //Line 16
    }                                                     //Line 17

    return 0;                                             //Line 18
}//end main                                               //Line 19
```

**示例运行 1：** 在此示例运行中，用户输入以底纹显示。

第 8 行：输入圆的半径：4.75

第 12 行：circle - 半径：4.75，面积：70.88，周长：29.85

**示例运行 2：** 在此示例运行中，用户输入以底纹显示。

第 8 行：输入圆的半径：-2.65

第 16 行：半径不能为负数

前面的程序按如下方式工作。第 3 行中的语句创建 circleType 对象 circle，并使用默认构造函数将半径设置为 0.0。第 4 行中的语句声明 **double** 变量 radius。第 7 行到第 17 行之间的 **try/catch** 块包含提示用户输入圆半径的代码，并根据用户输入的值生成输出。例如，如果用户输入非负半径，则第 11 行中的语句设置圆的半径，第 12 行中的语句输出圆的半径、面积和周长。如果用户输入负数，则第 11 行中的语句抛出一个异常（即 negativeNumber 对象），并由 **catch** 块处理该异常。在示例运行 1 中，用户输入 4.75（一个非负数），程序输出圆的半径、面积和周长。在示例运行 2 中，用户输入 −2.65（一个负数），第 16 行中的语句输出半径不能为负数。

## 重新抛出和抛出异常

当 `try` 块中发生异常时，控制权会立即转移到某个 `catch` 块。通常，`catch` 块要么处理该异常，要么部分处理该异常后重新抛出同一异常，或者重新抛出另一个异常，以便调用环境处理该异常。示例 14–4 到 14–14 中的 `catch` 块会处理异常。在 `catch` 块捕获异常但无法处理异常，或者 `catch` 块决定该异常应由调用块或环境处理的情况下，重新抛出或抛出异常的机制非常有用。这允许程序员将异常处理代码集中在一处提供。

要重新抛出或抛出异常，我们使用 `throw` 语句。重新抛出由 `catch` 块捕获的异常的一般语法是：

```cpp
throw;
```

（在这种情况下，会重新抛出同一异常）或者：

```cpp
throw expression;
```

其中 `expression` 是常量值、变量或对象。被抛出的对象可以是特定对象，也可以是匿名对象。

函数在其头部使用 `throw` 子句指定它抛出的异常（以便在某处处理）。例如，以下函数指定它抛出 `int`、`string` 和 `divisionByZero` 类型的异常，其中 `divisionByZero` 是前面定义的类。

```cpp
void expThrowExcep(int x) throw (int, string, divisionByZero)
{
    .
    .
    .
    //include the appropriate throw statements
    .
}
```

示例 14–15 中的程序进一步解释了函数如何指定它抛出的异常。

### 示例 14-15

```cpp
// Handling an exception, in the main function, thrown by another
// function. The function throws the same exception object.

#include <iostream>
#include "divisionByZero.h"
```

