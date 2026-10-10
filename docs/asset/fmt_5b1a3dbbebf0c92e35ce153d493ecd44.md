
```cpp
try {
    cout << "Line 3: Enter the dividend: ";
    cin >> dividend;
    cout << endl;

    cout << "Line 6: Enter the divisor: ";
    cin >> divisor;
    cout << endl;

    if (divisor == 0)
        throw divByZero();

    quotient = dividend / divisor;
    cout << "Line 12: Quotient = " << quotient;
} catch (divByZero) {
    cout << "Line 14: Division by zero!"
    cout << endl;
}
return 0;
}
```

示例运行 1: 在此示例运行中，用户输入用虚线表示。

Line 3: Enter the dividend: 34

Line 6: Enter the divisor: 5

Line 12: Quotient = 6

示例运行 2: 在此示例运行中，用户输入用虚线表示。

Line 3: Enter the dividend: 56

Line 6: Enter the divisor: 0

Line 14: Division by zero:

上述程序的工作原理如下：如果用户为除数输入 0，第 10 行的语句将抛出一个 `divByZero` 类的匿名对象。`divByZero` 类没有成员，因此我们无法对抛出的对象做任何操作。因此，在第 13 行的 `catch` 块中，我们只指定数据类型而不参数名。第 14 行的语句输出适当的错误信息。

让我们再次考虑第 10 行的语句 `divByZero()`。注意在该语句中，`divByZero` 是类名，表达式 `divByZero()` 创建了该类的匿名对象，而 `throw` 语句抛出了该对象。

示例 16-10 中设计和使用的异常类 `divByZero` 没有成员。接下来，我们说明如何创建带有成员的异常类。

如果你想在异常类中包含成员，通常会包含构造函数和 `what` 函数。考虑以下 `divisionByZero` 类的定义：

```cpp
// 用户定义的异常类。
#include <iostream>
#include <string>

namespace std {
class divisionByZero {
public:
    divisionByZero() {
        message = "Division by zero";
    }
    divisionByZero(string str) {
        message = str;
    }
    string what() {
        return message;
    }
private:
    string message;
};
};
```

`divisionByZero` 类的定义包含两个构造函数：默认构造函数和带参数的构造函数。默认构造函数在对象中存储字符串 "Division by zero"。带参数的构造函数允许用户创建他们自己的错误信息。`what` 函数用于返回对象中的字符串。

> 注意 在 `divisionByZero` 类的定义中，构造函数也可以写为：

`divByZero() : message("Division by zero") {}`

`divByZero(string str) : message(str) {}`

示例 16-11 的程序使用上述类来抛出异常。

```cpp
EXAMPLE 16-11
// 使用带有默认错误信息的自定义异常类 divisionByZero

#include <iostream>
#include "divisionByZero.h"

using namespace std;

int main() {
    int dividend, divisor, quotient;
    try {
        cout << "Line 3: Enter the dividend: ";
        cin >> dividend;
        cout << endl;

        cout << "Line 6: Enter the divisor: ";
        cin >> divisor;
        cout << endl;

        if (divisor == 0)
            throw divByZero();

        quotient = dividend / divisor;
        cout << "Line 12: Quotient = " << quotient;
    } catch (divByZero) {
        cout << "Line 14: Division by zero!"
        cout << endl;
    }
    return 0;
}
```

示例运行 1: 在此示例运行中，用户输入用虚线表示。

Line 3: Enter the dividend: 34

Line 6: Enter the divisor: 5

Line 12: Quotient = 6

示例运行 2: 在此示例运行中，用户输入用虚线表示。

Line 3: Enter the dividend: 56

Line 6: Enter the divisor: 0

Line 14: Division by zero:

```cpp
void doDivision() {
    int dividend, divisor, quotient; //Line 3
    try {
        cout << "Line 4: Enter the dividend: "; //Line 4
        cin >> dividend; //Line 5
        cout << endl; //Line 6

        cout << "Line 7: Enter the divisor: "; //Line 7
        cin >> divisor; //Line 8
        cout << endl; //Line 9

        if (divisor == 0) {
            throw divisionByZero(); //Line 10-11
        }
        quotient = dividend / divisor; //Line 12
        cout << "Line 13: Quotient = " << quotient << endl; //Line 13
    } catch (divisionByZero divByZeroObj) {
        cout << "Line 15: In the function " << doDivision: << divByZeroObj.what() << endl; //Line 15
    }
}
```

示例运行 1：在本次运行中，用户输入被阴影显示。

Line 4: Enter the dividend: 34

Line 7: Enter the divisor: 5

Line 13: Quotient = 6

示例运行 2：在本次运行中，用户输入被阴影显示。

Line 4: Enter the dividend: 56

Line 7: Enter the divisor: 0

Line 15: In the function doDivision: Division by zero

# 重新抛出和抛出异常

当 `try` 块中发生异常时，控制会立即传递到其中一个 `catch` 块。通常，`catch` 块要么处理异常，要么部分处理异常并重新抛出相同的异常，或者在调用处理器中重新抛出另一个异常来处理异常。示例 16-4 到 16-13 中的 `catch` 块处理了异常。重新抛出或抛出异常的机制在 `catch` 捕获了异常但无法处理该异常，或者 `catch` 块决定异常应该由调用块或环境处理时是非常有用的。这允许程序员在一个地方提供异常处理代码。

要进行重新思考或抛出异常，我们使用 `throw` 语句。重新抛出由 `catch` 块捕获的异常的通用语法为：

```cpp
throw;
```

（在这种情况下，重新抛出相同的异常）或：

```cpp
throw expression;
```

其中 `expression` 是常量值、变量或对象。被抛出的对象将是一个特定对象或一个匿名对象。

函数在它的头部中使用 `throw` 子句来指定它所抛出的异常（以便在某处处理）。例如，以下函数指定它会抛出类型为 `int`、`string` 和 `divisionByZero` 的异常，其中 `divisionByZero` 是之前定义的类。

```cpp
void expThrowExec(int x) throw (int, string, divisionByZero)
{
  .
  //包含适当的 throw 语句
  .
}
```

示例 16-14 中的程序进一步解释了函数如何指定它所抛出的异常。

# 示例 16-14

```cpp
// 在 main 函数中处理由另一个函数
// 抛出的异常。该函数抛出相同的异常对象。

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision() throw (divisionByZero);
```

```cpp
int main() {
    try {
        doDivision();
    } catch (divisionByZero divByZeroObj) {
        cout << "Line 4: In main: "
        << divByZeroObj.what() << endl;
    }
    return 0;
}

void doDivision() throw (divisionByZero) {
    try {
        int dividend, divisor, quotient;
        cout << "Line 8: Enter the dividend: "
        cin >> dividend;
        cout << endl;
        cout << "Line 11: Enter the divisor: "
        cin >> divisor;
        cout << endl;
        if (divisor == 0) {
            throw divisionByZero("Found division by 0!");
        }
        quotient = dividend / divisor;
        cout << "Line 17: Quotient = " << quotient << endl;
    } catch (divisionByZero) {
        throw;
    }
}
```

示例运行 1：在本次运行中，用户输入被阴影显示。

Line 8: Enter the dividend: 34

Line 11: Enter the divisor: 5

Line 17: Quotient = 6

示例运行 2：在本次运行中，用户输入被阴影显示。

Line 8: Enter the dividend: 56

Line 11: Enter the divisor: 0

Line 4: In main: Found 0!

在该程序中，如果 `divisor` 的值为 0，第 15 行的语句将抛出一个类型为 `divisionByZero` 的异常，这是该类的一个匿名对象，其消息为：“Found division by 0”。在示例运行 1 中，没有抛出异常。让我们看看示例运行 2 中发生了什么。函数在 `try` 块中调用了 `doDivision`。在 `doDivision` 中，`divisor` 的值为 0，第 15 行的语句抛出了异常。该异常被第 18 行的 `catch` 块捕获。第 19 行的语句重新抛出相同的异常。换句话说，`catch` 块捕获并重新抛出了相同的异常。因此，第 2 行的函数调用导致了异常的抛出。该异常被第 3 行的 `catch` 块捕获并处理。

# 示例 16-15

```cpp
// 在 main 函数中处理由另一个函数
// 抛出的异常。该函数抛出一个不同的异常对象。

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision() throw (divisionByZero);

int main() {
    try { // Line 1
        doDivision(); // Line 2
    } catch (divisionByZero divByZeroObj) { // Line 3
        cout << "Line 4: In main: " // Line 4
             << divByZeroObj.what() << endl;
    }
    return 0; // Line 5
}
```

```cpp
void doDivision() throw (divisionByZero)
{
    try { // Line 6
        int dividend, divisor, quotient; // Line 7
        cout << "Line 8: Enter the dividend: "; // Line 8
        cin >> dividend; // Line 9
        cout << endl; // Line 10
        cout << "Line 11: Enter the divisor: "; // Line 11
        cin >> divisor; // Line 12
        cout << endl; // Line 13
        if (divisor == 0) { // Line 14
            throw divisionByZero("Found division by 0!"); // Line 15
        }
        quotient = dividend / divisor; // Line 16
        cout << "Line 17: Quotient = " << quotient << endl; // Line 17
    } catch (divisionByZero) { // Line 18
        throw; // Line 19
    }
}
```

示例运行 1：在本次运行中，用户输入被阴影显示。

Line 8: Enter the dividend: 34

Line 11: Enter the divisor: 5

Line 17: Quotient = 6

示例运行 2：在本次运行中，用户输入被阴影显示。

Line 8: Enter the dividend: 56

Line 11: Enter the divisor: 0

Line 4: In main: Division by zero!

*(注：此处原文 `Found 0!` 疑似笔误，根据上下文推断翻译为 `Division by zero!`)*

在该程序中，如果 `divisor` 的值为 0，第 15 行的语句将抛出一个类型为 `divisionByZero` 的异常，这是该类的一个匿名对象，其消息为：“Found division by 0”。在示例运行 1 中，没有抛出异常。让我们看看示例运行 2 中发生了什么。函数在 `try` 块中调用了 `doDivision`。在 `doDivision` 中，`divisor` 的值为 0，第 15 行的语句抛出了异常。该异常被第 18 行的 `catch` 块捕获。第 19 行的语句重新抛出相同的异常。换句话说，`catch` 块捕获并重新抛出了相同的异常。因此，第 2 行的函数调用导致了异常的抛出。该异常被第 3 行的 `catch` 块捕获并处理。

*(注：此处提供的原始文本中示例 16-15 的代码块格式较为混乱，翻译时根据逻辑进行了结构对齐和修正)*

# 示例 16-15

```cpp
// 在 main 函数中处理由另一个函数
// 抛出的异常。该函数抛出一个不同的异常对象。

#include <iostream>
#include "divisionByZero.h"

using namespace std;

void doDivision() throw (divisionByZero);

int main() {
    try { // Line 1
        doDivision(); // Line 2
    } catch (divisionByZero divByZeroObj) { // Line 3
        cout << "Line 4: In main: " // Line 4
             << divByZeroObj.what() << endl;
    }
    return 0; // Line 5
}
```
