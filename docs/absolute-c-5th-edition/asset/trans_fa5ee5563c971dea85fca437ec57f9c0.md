

## 陷阱：顺序错误的参数

当函数被调用时，计算机会将第一个参数替换为第一个形式参数，将第二个参数替换为第二个形式参数，依此类推。尽管计算机会检查每个参数的类型，但它不会检查其合理性。如果你混淆了参数的顺序，程序将不会按照你预期的那样运行。如果某个类型错误的参数发生了类型冲突，你将收到一条错误信息。如果没有发生类型冲突，你的程序可能会正常运行，但函数返回的值将产生错误的结果。

## 陷阱：参数（Parameter）和实（Argument）术语的使用

本书中所遵循的形式参数（formal parameter）和实（argument）这两个术语的使用与常用习惯一致，但人们也经常交替使用 parameter 和 argument 这词。当你看到 parameter 和 argument 这词时，你必须根据上下文确定它们的确切含义。许多人使用 parameter 来指代我们所说的形式参数和我们所说的实。另一些人将 argument 同时指代我们所说的形式参数和我们所说的实。人们对这两个词的使用并没有统一的规定。（在本书中，我们使用 parameter 指代形式参数，但这更多是一种缩写，而非真正的不一致。）

## 函数调用函数

函数体可能包含对另一个函数的调用。这类函数调用的情况就像函数发生在程序的主部分一样；唯一的限制是函数声明（或函数定义）必须在函数使用之前出现。如果你按照我们所做的方式设置程序，这将自动发生，因为函数定义位于程序主部分之前，而所有的函数定义都在程序主部分之后。虽然你可以在另一个函数的定义内部包含函数调用，但你不能将一个函数的定义放在另一个函数定义的体内部。

## 示例：舍入函数

定义函数表（显示 3.2）不包含任何对数字进行舍入的函数。`ceil` 和 `floor` 函数几乎是舍入函数，但不完全是。`ceil` 函数总是返回下一个最大的整数（如果其参数恰好是整数，则返回参数本身）。因此，`ceil(2.1)` 返回 3.0，而不是 2.0。

## 第 3 章函数基础

### 示例：（续）

`floor` 函数总是返回小于（或等于）参数的最近数字。因此，`floor(2.9)` 返回 2.0，而不是 3.0。幸运的是，定义一个能够实现舍入功能的函数很容易。该函数定义在显示 3.6 中。该函数将其参数舍入到最近的整数。例如，`round(2.3)` 返回 2，`round(2.6)` 返回 3。

为了验证 `round` 工作正常，让我们来看一些例子。考虑 `round(2.4)`。返回的值如下（转换为 int 值），

```cpp
floor(2.4 + 0.5)
```

即 `floor(2.9)`，或 2.0。对于任何大于 2.0 且严格小于 2.5 的数字，该数字加 0.5 将小于 3.0，因此对该数字加 0.5 后应用 `floor` 会返回 2.0。因此，对任何大于或等于 2.0 且严格小于 2.5 的数字应用 `round` 将返回 2。（由于 `round` 的函数声明指定了返回值的类型为 `int`，我们将该调用强制转换为了 `int` 类型）。

现在考虑大于等于 2.5 的数字：2.6。调用 `round(2.6)` 返回的值如下（转换为 int 值），

```cpp
floor(2.6 + 0.5)
```

即 `floor(3.1)`，或 3.0。对于任何大于 2.5 且小于或等于 3.0 的数字，该数字加 0.5 将大于 3.0。因此，使用任何大于 2.5 且小于或等于 3.0 的数字调用 `round` 将返回 3。

因此，`round` 对于 2.0 到 3.0 之间的所有参数都能正常工作。类似的适用于适用于非负数。因此，`round` 对于所有非负参数都能正常工作。

显示 3.6 函数 round（部分1，共 2 部分）

```cpp
#include <iostream>
#include <cmath>
using namespace std;
int round(double number);
// 假设 number >= 0.
// 返回舍入到最近整数的 number。
int main()
{
    double doubleValue;
    char ans;

    // 测试函数 round 的程序
```

## 程序员自定义函数

显示 3.6 函数 round（部分2，共 2 部分）

```cpp
do {
    cout << "Enter a double value: ";
    cin >> doubleValue;
    cout << "Rounded that number is " << round(doubleValue) << endl\n;
    cout << "Again? (y/n): ";
    cin >> ans;
    } while (ans == 'y' || ans == 'Y');
    cout << "End of testing.\n";
    return 0;
// cmath
int round(double number) {
    return static_cast<int>(floor(number + 0.5));
}
```

示例对话
Enter a double value: 9.6
Rounded, that number is 10
Again? (y/n): y
Enter a double value: 2.49
Rounded, that number is 2
Again? (y/n): n
End of testing.

## 自测练习

- 7. 以下程序的输出是什么？

```cpp
#include <iostream>
using namespace std;
bool mystery(int firstParameter, int secondParameter);
int main() {
    cout << mystery(10, 9);
    return 0;
}
```

## 第 3 章函数基础

### 自测练习（续）

```cpp
char mystery(int firstParameter, int secondParameter)
{
    if (firstParameter >= secondParameter)
        return 'W';
    else
        return 'H';
}
```

- 8. 写一个接受三个 int 参数并返回和的函数原型。
- 9. 写一个接受一个 double 参数的函数声明，如果参数为正则返回 'P$，否则返回 'n'。
- 10. 函数可以出现在另一个函数的内部吗？
- 11. 调用定义函数和自定义函数的方式有何异同？

## 返回值的函数

返回值的函数的类型可以是 bool。这种函数返回真或假，并可以使用在任何允许布尔表达式的地方。例如，以下定义的函数：

```cpp
bool appropriate(int rate)
{
    return ((rate >= 10) && (rate < 20));
}
```

## 自测练习

- 12. 写一个接受三个 int 参数的函数定义。如果参数是升序的，则返回 true；否则返回 false。例如，appropriate(1, 2, 3) 和 appropriate(1, 2, 2) 都返回 true，而 appropriate(1, 3, 2) 返回 false。
- 13. 写一个接受一个 int 参数并返回 bool 值的函数定义。如果参数是偶数则返回 true；否则返回 false。
- 14. 写一个接受一个 char 参数并返回 bool 值的函数定义。如果参数是数字位则返回 true；否则返回 false。

## 定义 void 函数

在 C++ 中，void 函数的定义方式与返回值的函数相似。例如，以下是一个输出将摄氏温度转换为华氏温度结果的 void 函数。实际计算将在程序的其他地方进行。此 void 函数仅实现输出结果的子任务。

```cpp
void showResults(double fDegrees, double cDegrees)
{
    cout.set(ios::fixed);
    cout.set(ios::showpoint);
    cout.precision(1);
    cout << fDegrees << " * degrees Fahrenheit is equivalent to\n"
         << cDegrees << " * degrees Celsius.\n";
}
```

正如之前的定义所示，void 函数的定义与返回值的函数的定义之间只有两个区别。一个区别是我们在通常指定返回值的类型的地方使用了 `void` 关键字。这告诉编译器该函数不会返回任何值。该名称被用作表示“此函数不返回任何值”。第二个区别是 void 函数不需要 return 语句。当函数体中的最后一个语句执行完毕时，函数执行结束。

void 函数是一个执行语句。例如，可以这样调用函数 showResults：

```cpp
showResults(32.5, 0.3);
```

