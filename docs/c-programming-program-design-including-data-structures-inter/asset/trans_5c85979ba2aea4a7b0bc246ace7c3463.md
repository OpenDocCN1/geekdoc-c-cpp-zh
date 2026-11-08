

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

注意，类 negativeNumber 的定义与类 divisionByZero 的定义类似。

类 circleType 的定义与示例 10-8 中相同，只是函数 setRadius 的定义不同。该函数修改后的定义如下：

```cpp
void circleType::setRadius(double r)
{
    if (r < 0)
        throw negativeNumber("Radius");
    radius = r;
}
```

如果参数 r 的值为负数，则函数 setRadius 会抛出一个 negativeNumber 对象。在这种情况下，所抛出对象的实例变量 message 的值为“Radius cannot be negative.”。用户程序将处理该函数抛出的异常（如果有）。

考虑以下程序：

```cpp
// The user program that uses the class circleType

#include <iostream>
#include <iomanip>
#include "circleType.h"
#include "negativeNumber.h"

using namespace std;

int main()
{
    circleType circle;
    double radius;
    cout << fixed << showpoint << setprecision(2);
    try
    {
        cout << "Line 8: Enter the radius of a circle: ";
        cin >> radius;
        cout << endl;

        circle.setRadius(radius);

        cout << "Line 12: circle - "
             << "radius: " << circle.getRadius()
             << ", area: " << circle.area()
             << ", circumference: "
             << circle.circumference() << endl;
    }
    catch (negativeNumber obj)
    {
        cout << "Line 16: " << obj.what() << endl;
    }

    return 0;
}//end main
```

**示例运行 1：** 在此示例运行中，用户输入以阴影显示。

第8行：输入圆的半径：**4.75**

第12行：circle - 半径：4.75，面积：70.88，周长：29.85

**示例运行 2：** 在此示例运行中，用户输入以阴影显示。

第8行：输入圆的半径：**-2.65**

第16行：半径不能为负数。

前面的程序工作方式如下。第3行中的语句创建 circleType 对象 circle，并使用默认构造函数将半径设置为 0.0。第4行中的语句声明 double 变量 radius。第7行到第17行之间的 try/catch 块包含提示用户输入圆半径的代码，并根据用户输入的值生成输出。例如，如果用户输入非负半径，第11行中的语句设置圆的半径，第12行中的语句输出圆的半径、面积和周长。如果用户输入负数，第11行中的语句抛出一个异常，即 negativeNumber 对象，catch 块会处理该异常。在示例运行 1 中，用户输入 4.75（非负数），程序输出圆的半径、面积和周长。在示例运行 2 中，用户输入 −2.65（负数），第16行中的语句输出半径不能为负数。

## 重新抛出和抛出异常

当 try 块中发生异常时，控制权会立即转移到某个 catch 块。通常，catch 块要么处理异常，要么部分处理异常后重新抛出同一异常，要么重新抛出另一个异常，以便调用环境处理该异常。示例 14-4 到 14-14 中的 catch 块处理异常。在 catch 块捕获异常但无法处理异常，或者 catch 块决定应由调用块或调用环境处理异常的情况下，重新抛出或抛出异常的机制非常有用。这使程序员能够在一个地方提供异常处理代码。

要重新抛出或抛出异常，我们使用 throw 语句。重新抛出 catch 块捕获的异常的一般语法是：

```cpp
throw;
```

（在这种情况下，重新抛出同一异常）或者：

```cpp
throw expression;
```

其中 expression 是常量值、变量或对象。被抛出的对象可以是特定对象，也可以是匿名对象。

函数在其头部使用 throw 子句指定它会抛出（需在某处处理的）异常。例如，以下函数指定它会抛出 int、string 和 divisionByZero 类型的异常，其中 divisionByZero 是前面定义的类。

```cpp
void expThrowExcep(int x) throw (int, string, divisionByZero)
{
    .
    .
    //include the appropriate throw statements
    .
    .
}
```

示例 14-15 中的程序进一步说明了函数如何指定它抛出的异常。

### 示例 14-15

```cpp
// Handling an exception, in the main function, thrown by another
// function. The function that throws the same exception object.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision() throw (divisionByZero);

int main()
{
    try                                      //Line 1
    {
        doDivision();                        //Line 2
    }
    catch (divisionByZero divByZeroObj)      //Line 3
    {
        cout << "Line 4: In main: "
             << divByZeroObj.what() << endl; //Line 4
    }

    return 0;                                //Line 5
}

void doDivision() throw (divisionByZero)
{
    int dividend, divisor, quotient;         //Line 6

    try                                      //Line 7
    {
        cout << "Line 8: Enter the dividend: "; //Line 8
        cin >> dividend;                     //Line 9
        cout << endl;                        //Line 10

        cout << "Line 11: Enter the divisor: "; //Line 11
        cin >> divisor;                      //Line 12
        cout << endl;                        //Line 13

        if (divisor == 0)                    //Line 14
            throw divisionByZero("Found division by 0!"); //Line 15

        quotient = dividend / divisor;       //Line 16
        cout << "Line 17: Quotient = " << quotient //Line 17
             << endl;
    }
    catch (divisionByZero)                   //Line 18
    {
        throw;                               //Line 19
    }
}
```

**示例运行 1：** 在此示例运行中，用户输入以阴影显示。

```
Line 8: Enter the dividend: 34

Line 11: Enter the divisor: 5

Line 17: Quotient = 6
```

**示例运行 2：** 在此示例运行中，用户输入以阴影显示。

第8行：输入被除数：`56`

第11行：输入除数：`0`

第4行：在 main 中：发现除以 0！

在此程序中，如果 divisor 的值为 0，第15行中的语句会抛出 divisionByZero 类型的异常，该异常是此类的一个匿名对象，其消息字符串为：

“发现除以 0！”

第19行中 catch 块内的语句抛出相同的异常值，在此情况下是一个对象。

在示例运行 1 中，没有抛出异常。

让我们看看示例运行 2 中会发生什么。函数 main 在 try 块中调用函数 doDivision。在函数 doDivision 中，divisor 的值为 0，因此第15行中的语句抛出异常。该异常被第18行中的 catch 块捕获。第19行中的语句重新抛出同一异常。换句话说，catch 块捕获并重新抛出同一异常。因此，第2行中的函数调用语句会导致抛出同一异常。该异常被第3行中的 catch 块捕获并处理。

### 示例 14-16

```cpp
// Handling exception, in the main function, thrown by another
// function. The function throws a different exception object.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision() throw (divisionByZero);

int main()
{
    try
    {
        doDivision();                         //Line 1
    }                                        //Line 2
    catch (divisionByZero divByZeroObj)       //Line 3
    {
        cout << "Line 4: In main: "
             << divByZeroObj.what() << endl;  //Line 4
    }

    return 0;                                 //Line 5
}
```

