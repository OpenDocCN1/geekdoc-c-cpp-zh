
在例14-10中设计并使用的异常类 `divByZero` 没有成员。接下来，我们说明如何创建带成员的异常类。

如果希望在异常类中包含成员，通常需要包含构造函数和函数 `what`。请考虑以下类 `divisionByZero` 的定义。

```cpp
// User-defined exception class.

#include <iostream>
#include <string>

using namespace std;

class divisionByZero                 //Line 1
{
public:                              //Line 3
    divisionByZero()                 //Line 4
    {
        message = "Division by zero"; //Line 5
    }                                //Line 6

    divisionByZero(string str)       //Line 7
    {
        message = str;               //Line 8
    }                                //Line 10

    string what()                    //Line 11
    {
        return message;              //Line 13
    }                                //Line 14

private:                             //Line 15
    string message;                  //Line 16
};                                   //Line 17
```

类 `divisionByZero` 的定义包含两个构造函数：默认构造函数和带参数的构造函数。默认构造函数将字符串“Division by zero”存储到对象中。带参数的构造函数允许用户创建自己的错误消息。函数 `what` 用于返回对象中存储的字符串。

> 在类 `divisionByZero` 的定义中，构造函数也可以写成：
>
> ```cpp
> divisionByZero() : message("Division by zero"){}
> divisionByZero(string str) : message(str){}
> ```

例14-11中的程序使用前面的类来抛出异常。

### 例14-11

```cpp
// Using a user-defined exception class divisionByZero with
// default error message.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

int main()
{
    int dividend, divisor, quotient;                         //Line 1

    try                                                     //Line 2
    {
        cout << "Line 3: Enter the dividend: ";             //Line 3
        cin >> dividend;                                    //Line 4
        cout << endl;                                       //Line 5

        cout << "Line 6: Enter the divisor: ";              //Line 6
        cin >> divisor;                                     //Line 7
        cout << endl;                                       //Line 8

        if (divisor == 0)                                   //Line 9
            throw divisionByZero();                         //Line 10

        quotient = dividend / divisor;                      //Line 11
        cout << "Line 12: Quotient = " << quotient          //Line 12
             << endl;
    }
    catch (divisionByZero divByZeroObj)                    //Line 13
    {
        cout << "Line 14: In the divisionByZero "
             << "catch block:"
             << divByZeroObj.what() << endl;                //Line 14
    }

    return 0;                                               //Line 15
}
```

**示例运行1：** 在此示例运行中，用户输入以阴影显示。

第3行：输入被除数：36

第6行：输入除数：5

第12行：商 = 6

**示例运行2：** 在此示例运行中，用户输入以阴影显示。

第3行：输入被除数：56

第6行：输入除数：0

第14行：在 divisionByZero 的 catch 块中：除以零

在此程序中，如果用户为除数输入0，第10行的语句会抛出类 divisionByZero 的一个对象（异常）。这个被抛出的异常由第13行的 catch 块捕获并处理。catch 块中的参数 divByZeroObj 捕获所抛出对象的值，然后使用函数 what 返回对象中存储的字符串。第14行的语句输出相应的错误消息。

例14-12中的程序与例14-11中的程序类似。这里，抛出的对象仍然是一个匿名对象，但错误消息由用户指定（见第10行的语句）。

### 例14-12

```cpp
// Using user-defined exception class divisionByZero with a
// specific error message.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

int main()
{
    int dividend, divisor, quotient;                         //Line 1

                                                            //Line 2
    try                                                     
    {
        cout << "Line 3: Enter the dividend: ";             //Line 3
        cin >> dividend;                                     //Line 4
        cout << endl;                                        //Line 5

        cout << "Line 6: Enter the divisor: ";              //Line 6
        cin >> divisor;                                      //Line 7
        cout << endl;                                        //Line 8

                                                            //Line 9
        if (divisor == 0)                                    //Line 10
            throw divisionByZero("Found division by zero"); //Line 10

        quotient = dividend / divisor;                       //Line 11
        cout << "Line 12: Quotient = " << quotient
             << endl;                                        //Line 12
    }
    catch(divisionByZero divByZeroObj)                         //Line 13
    {
        cout << "Line 14: In the divisionByZero "
             << "catch block: "
             << divByZeroObj.what() << endl;                    //Line 14
    }

    return 0;                                                   //Line 15
}
```

**示例运行1：** 在此示例运行中，用户输入以阴影显示。

第3行：输入被除数：`34`

第6行：输入除数：`5`

第12行：商 = 6

**示例运行2：** 在此示例运行中，用户输入以阴影显示。

第3行：输入被除数：`56`

第6行：输入除数：`0`

第14行：在 divisionByZero 的 catch 块中：发现除以零

此程序的工作方式与例14-11中的程序相同。细节留作练习。

在例14-11和例14-12的程序中，数据操作在函数 main 中完成。因此，异常在函数 main 中被抛出、捕获和处理。例14-13中的程序使用用户定义的函数 doDivision 来操作数据。因此，异常在函数 doDivision 中被抛出、捕获和处理。

### 例14-13

```cpp
// Handling an exception thrown by a function.

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision();

int main()
{
    doDivision();                                      //Line 1

    return 0;                                           //Line 2
}

void doDivision()
{
    int dividend, divisor, quotient;                 //Line 3

    try
    {
        cout << "Line 4: Enter the dividend: ";     //Line 4
        cin >> dividend;                             //Line 5
        cout << endl;                                //Line 6

        cout << "Line 7: Enter the divisor: ";      //Line 7
        cin >> divisor;                              //Line 8
        cout << endl;                                //Line 9

        if (divisor == 0)                            //Line 10
            throw divisionByZero();                  //Line 11

        quotient = dividend / divisor;               //Line 12
        cout << "Line 13: Quotient = " << quotient   //Line 13
             << endl;
    }
    catch (divisionByZero divByZeroObj)              //Line 14
    {
        cout << "Line 15: In the function "
             << divByZeroObj.what() << endl;         //Line 15
    }
}
```

**示例运行1：** 在此示例运行中，用户输入以阴影显示。

第4行：输入被除数：**34**

第7行：输入除数：**5**

第13行：商 = 6

**示例运行2：** 在此示例运行中，用户输入以阴影显示。

第4行：输入被除数：**56**

第7行：输入除数：**0**

第15行：在函数 doDivision 中：除以零

### 例14-14

例10-8定义了类 circleType 来实现圆的基本属性。如果一个 circleType 对象试图将半径设置为负数，则该类的函数 setRadius 会将半径设置为0。在本例中，我们派生类 negativeNumber 来处理负数异常，然后使用该类在 circleType 对象试图将半径设置为负数时抛出异常。因此，请考虑以下类：
