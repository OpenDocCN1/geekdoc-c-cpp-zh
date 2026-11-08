
适当的信息。`exception` 类的所有派生类都会重写函数 `what`，以输出各自对应的错误消息。

有两个类直接派生自 `exception` 类：`logic_error` 和 `runtime_error`。这两个类都定义在头文件 `stdexcept` 中。

为了处理程序中的逻辑错误，例如字符串下标越界或函数调用中的无效参数，有多个类派生自 `logic_error` 类。例如，`invalid_argument` 类用于处理函数调用中使用的非法参数。`out_of_range` 类处理字符串下标越界错误。如果使用的长度大于字符串对象所允许的最大长度，则由 `length_error` 类处理该错误。例如，回想一下，每个 string 对象都有一个最大长度（参见第 7 章）。如果使用的长度大于字符串所允许的最大长度，就会生成 `length_error` 异常。如果运算符 new 无法分配内存空间，该运算符会抛出 `bad_alloc` 异常。

`runtime_error` 类用于处理只能在程序执行期间检测到的错误。例如，为了处理算术溢出和下溢异常，`overflow_error` 和 `underflow_error` 类派生自 `runtime_error` 类。

示例 14-8 和 14-9 说明了如何使用 C++ 的异常类来处理程序中的异常。

示例 14-8 中的程序展示了如何处理 `out_of_range` 和 `length_error` 异常。注意，在这个程序中，这些异常由 string 函数 `substr` 和字符串连接运算符 `+` 抛出。由于异常是由这些函数抛出的，因此 `try` 块中不包含任何 `throw` 语句。

### 示例 14-8

```cpp
// Handling out_of_range and length_error exceptions.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string sentence;                           //Line 1
    string str1, str2, str3;                    //Line 2

    try                                        //Line 3
    {
        sentence = "Testing string exceptions!"; //Line 4
        cout << "Line 5: sentence = " << sentence //Line 5
             << endl;
        cout << "Line 6: sentence.length() = "
             << static_cast<int>(sentence.length())
             << endl;                         //Line 6

        str1 = sentence.substr(8, 20);         //Line 7
        cout << "Line 8: str1 = " << str1
             << endl;                         //Line 8

        str2 = sentence.substr(28, 10);        //Line 9
        cout << "Line 10: str2 = " << str2
             << endl;                         //Line 10

        str3 = "Exception handling. " + sentence; //Line 11
        cout << "Line 12: str3 = " << str3
             << endl;                         //Line 12
    }
    catch (out_of_range re)                //Line 13
    {
        cout << "Line 14: In the out_of_range "
             << "catch block: " << re.what()
             << endl;                      //Line 14
    }
    catch (length_error le)                //Line 15
    {
        cout << "Line 16: In the length_error "
             << "catch block: " << le.what()
             << endl;                      //Line 16
    }

    return 0;                              //Line 17
}
```

**运行示例：**

```text
Line 5: sentence = Testing string exceptions!
Line 6: sentence.length() = 26
Line 8: str1 = string exceptions!
Line 14: In the out_of_range catch block: invalid string position
```

在这个程序中，第 7 行的语句使用函数 substr 确定 string 对象 sentence 中的一个子串。字符串 sentence 的长度为 26。由于子串的起始位置为 8，小于 26，因此不会抛出异常。然而，在第 9 行的语句中，子串的起始位置为 28，大于 26（sentence 的长度）。因此，函数 substr 抛出一个 out_of_range 异常，该异常由第 13 行的 catch 块捕获并处理。注意，在第 14 行的语句中，对象 re 返回错误消息 invalid string position。

示例 14-9 中的程序说明了如何处理由运算符 new 抛出的 bad_alloc 异常。

### 示例 14-9

```cpp
// Handling bad_alloc exception thrown by the operator new.

#include <iostream>

using namespace std;

int main()
{
    int *list[100];                         //Line 1

    try                                      //Line 2
    {
        for (int i = 0; i < 100; i++)       //Line 3
        {
            list[i] = new int[50000000];    //Line 4
            cout << "Line 4: Created list[" << i
                 << "] of 50000000 components." //Line 5
                 << endl;
        }
    }
    catch (bad_alloc &be)                   //Line 6
    {
        cout << "Line 7: In the bad_alloc catch "
             << "block: " << be.what() << "."
             << endl;                       //Line 7
    }

    return 0;                               //Line 8
}
```

**运行示例：**

```text
Line 4: Created list[0] of 50000000 components.
Line 4: Created list[1] of 50000000 components.
Line 4: Created list[2] of 50000000 components.
Line 4: Created list[3] of 50000000 components.
Line 4: Created list[4] of 50000000 components.
Line 4: Created list[5] of 50000000 components.
Line 4: Created list[6] of 50000000 components.
Line 4: Created list[7] of 50000000 components.
Line 7: In the bad_alloc catch block: bad allocation.
```

前面的程序按如下方式工作。第 1 行的语句将 list 声明为包含 100 个指针的数组。第 3 行 for 循环的循环体设计为执行 100 次。对于 for 循环的每次迭代，第 4 行的语句使用运算符 new 分配一个包含 50000000 个 int 类型元素的数组。如运行示例所示，运算符 new 能够创建八个各含 50000000 个 int 分量的数组。在第 9 次迭代中，运算符 new 无法创建该数组，并抛出一个 bad_alloc 异常。该异常由第 6 行的 catch 块捕获并处理。注意，表达式 `be.what()` 返回字符串 bad allocation。（此外，`be.what()` 返回的字符串长度为 11 个字符。某些 IDE 可能返回字符串 bad_alloc。）第 7 行的语句执行后，控制流退出 try/catch 块，第 8 行的语句终止程序。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1018_0.png)

## 创建自己的异常类

每当你创建自己的类或编写程序时，异常都有可能发生。如你所见，C++ 提供了许多异常类来处理这些情况。然而，它并不会提供你将来需要的所有异常类。因此，C++ 允许程序员创建自己的异常类，以处理 C++ 异常类未覆盖的异常以及他们自己的异常。本节介绍如何创建自己的异常类。

C++ 处理你定义的异常时使用的机制与处理内置异常时相同。但是，你必须使用 throw 语句抛出自定义异常。

在 C++ 中，任何类都可以声明为异常类。因此，异常类就是一个普通的类。它不必从 exception 类继承。一个类之所以成为异常类，取决于你如何使用它。

你定义的异常类可以非常简单，甚至不包含任何成员。例如，下面的代码可以被视为一个异常类：

```cpp
class dummyExceptionClass
{
};
```

示例 14-10 中的程序使用一个用户定义的类（不含成员）来抛出异常。

### 示例 14-10

```cpp
// Using a user-defined exception class.

#include <iostream>

using namespace std;

class divByZero
{};

int main()
{
    int dividend, divisor, quotient;             //Line 1

    try                                      //Line 2
    {
        cout << "Line 3: Enter the dividend: ";    //Line 3
        cin >> dividend;                              //Line 4
        cout << endl;                                 //Line 5

        cout << "Line 6: Enter the divisor: ";     //Line 6
        cin >> divisor;                               //Line 7
        cout << endl;                                 //Line 8

        if (divisor == 0)                             //Line 9
            throw divByZero();                        //Line 10

        quotient = dividend / divisor;                //Line 11
        cout << "Line 12: Quotient = " << quotient
             << endl;                                 //Line 12
    }
    catch (divByZero)                                 //Line 13
    {
        cout << "Line 14: Division by zero!"
             << endl;                                 //Line 14
    }

    return 0;                                         //Line 15
}
```

**运行示例 1：** 在此运行示例中，用户输入以底纹显示。

第 3 行：输入被除数：**34**

第 6 行：输入除数：**5**

第 12 行：商 = 6。

**运行示例 2：** 在此运行示例中，用户输入以底纹显示。

第 3 行：输入被除数：**56**

第 6 行：输入除数：**0**

第 14 行：除以零！

前面的程序按如下方式工作。如果用户为除数输入 0，第 10 行的语句会抛出一个 `divByZero` 类的匿名对象。`divByZero` 类没有成员，因此我们实际上无法对该抛出对象做任何操作。因此，在第 13 行的 catch 块中，我们只指定数据类型名称，而不指定参数名。第 14 行的语句输出相应的错误消息。

让我们再次考虑第 10 行中的语句 `throw divByZero();`。注意，在这个语句中，`divByZero` 是类名，表达式 `divByZero()` 创建该类的匿名对象，而 `throw` 语句抛出该对象。
