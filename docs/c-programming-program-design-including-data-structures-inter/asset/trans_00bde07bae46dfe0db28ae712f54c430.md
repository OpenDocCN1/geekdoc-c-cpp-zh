

回顾一下，提取运算符（extraction operator）会跳过任何前导空白字符，并且在遇到空白字符时停止读取。因此，你不能使用提取运算符来读取包含空格的字符串。例如，假设变量 `name` 按前面所述定义。如果输入是：

```text
Alice Wonderland
```

那么在语句：

```cpp
cin >> name;
```

执行后，变量 `name` 的值为 "Alice"。

要读取包含空格的字符串，可以使用 `getline` 函数。

使用 `getline` 函数的语法是：

```cpp
getline(istreamVar, strVar);
```

其中 `istreamVar` 是输入流变量，`strVar` 是字符串变量。读取以换行符 `'\n'` 作为定界符。

`getline` 函数会一直读取，直到到达当前行的末尾。换行符也会被读取，但不会存储在字符串变量中。

考虑以下语句：

```cpp
string myString;
```

如果输入是 29 个字符：

```text
bbbbHello there. How are you?
```

其中 b 代表空格，在执行语句：

```cpp
getline(cin, myString);
```

之后，`myString` 的值是：

```text
myString = "    Hello there. How are you?"
```

所有 29 个字符，包括前四个空格，都被存储到 `myString` 中。

类似地，你可以使用输出流变量（如 `cout`）和插入运算符 `<<` 来输出 `string` 数据类型变量的内容。

## 调试：理解逻辑错误并用 cout 语句调试

在第 2 章的调试部分，我们演示了如何理解和修正语法错误。正如我们所见，语法错误由编译器报告，编译器不仅报告语法错误，还会对错误给出一些解释。另一方面，逻辑错误通常不会被编译器捕获，除了一些简单的问题，比如使用未正确初始化的变量。在本节中，我们演示如何使用 `cout` 语句来发现和修正逻辑错误。假设我们要编写一个程序，输入华氏温度并输出对应的摄氏温度。转换公式为：摄氏温度 = 5 / 9 * (华氏温度 − 32)。考虑以下程序：

```cpp
#include <iostream> //Line 1

using namespace std; //Line 2

int main() //Line 3
{
    int fahrenheit; //Line 5
    int celsius; //Line 6

    cout << "Enter temperature in Fahrenheit: "; //Line 7
    cin >> fahrenheit; //Line 8
    cout << endl; //Line 9

    celsius = 5 / 9 * (fahrenheit - 32); //Line 10

    cout << fahrenheit << " degree F = " //Line 11
         << celsius << " degree C." << endl;

    return 0; //Line 12
} //Line 13
```

**示例运行 1：** 在此示例运行中，用户输入以阴影显示。

Enter temperature in Fahrenheit: **32**

32 degree F = 0 degree C.

**示例运行 2：** 在此示例运行中，用户输入以阴影显示。

Enter temperature in Fahrenheit: **110**

110 degree F = 0 degree C.

第一次计算显示的结果看起来是正确的。然而，第二次计算的结果显然不正确，尽管使用了相同的公式，因为 110 华氏度等于 43 摄氏度。这意味着第 10 行计算的 `celsius` 值不正确。现在，`celsius` 的值由表达式 `5 / 9 * (fahrenheit - 32)` 给出。所以我们应该仔细看这个表达式。为了查看这次计算的效果，我们可以分别打印两个表达式 `5 / 9` 和 `fahrenheit - 32` 的值。这可以通过临时插入一条输出语句来实现，如下面的程序所示：

```cpp
#include <iostream> //Line 1

using namespace std; //Line 2

int main() //Line 3
{
    int fahrenheit; //Line 5
    int celsius; //Line 6

    cout << "Enter temperature in Fahrenheit: "; //Line 7
    cin >> fahrenheit; //Line 8
    cout << endl; //Line 9

    cout << "5 / 9 = " << 5 / 9
         << "; fahrenheit - 32 = "
         << fahrenheit - 32 << endl; //Line 9a

    celsius = 5 / 9 * (fahrenheit - 32); //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C. " << endl; //Line 11

    return 0; //Line 12
} //Line 13
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Enter temperature in Fahrenheit: 110

5 / 9 = 0;  fahrenheit - 32 = 78
110 degree F = 0 degree C.
```

让我们看一下示例运行。我们看到 `5 / 9 = 0`，`fahrenheit - 32 = 78`。因为 `fahrenheit = 110`，表达式 `fahrenheit - 32` 的值是正确的。现在再看表达式 `5 / 9`。该表达式的值是 0。因为运算符 `/` 的两个操作数 5 和 9 都是整数，使用整数除法，该表达式的值为 0。也就是说，表达式 `5 / 9 = 0` 的计算也是正确的。因此，根据运算符的优先级，无论 `fahrenheit` 的值是多少，表达式 `5 / 9 * (fahrenheit - 32)` 的值都将始终为 0。所以问题出在整数除法上。我们可以将表达式 `5 / 9` 替换为 `5.0 / 9`。在这种情况下，表达式 `5.0 / 9 * (fahrenheit - 32)` 的值将是一个十进制数。因为 `fahrenheit` 和 `celsius` 是 `int` 变量，我们可以使用强制转换运算符将该值转换为整数，即使用以下表达式：

```cpp
celsius = static_cast<int> (5.0 / 9 * (fahrenheit - 32) + 0.5);
```

（注意，在前面的表达式中，我们添加了 0.5 以将该数字四舍五入到最接近的整数。）

修改后的程序是：

```cpp
#include <iostream> //Line 1

using namespace std; //Line 2

int main() //Line 3
{
    int fahrenheit; //Line 4
    int celsius; //Line 5

    cout << "Enter temperature in Fahrenheit: "; //Line 7
    cin >> fahrenheit; //Line 8
    cout << endl; //Line 9

    celsius = static_cast<int>
              (5.0 / 9 * (fahrenheit - 32) + 0.5); //Line 10

    cout << fahrenheit << " degree F = "
         << celsius << " degree C." << endl; //Line 11

    return 0; //Line 12
} //Line 13
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

Enter temperature in Fahrenheit: 110

110 degree F = 43 degree C.

正如我们所见，使用临时的 `cout` 语句，我们找到了问题所在。修正问题后，临时的 `cout` 语句被删除。

温度转换程序包含的是逻辑错误，而不是语法错误。使用 `cout` 语句打印表达式和/或变量的值来查看计算结果，是一种发现和修正逻辑错误的有效方法。

## 文件输入/输出

前面的章节详细讨论了如何从键盘（标准输入设备）获取输入以及将输出发送到屏幕（标准输出设备）。然而，从键盘获取输入和向屏幕发送输出有一些局限性。只要输入量很小，从键盘向程序输入数据是很方便的。如果数据量不大（不超过屏幕大小），并且你不想以打印格式向他人分发输出，那么将输出发送到屏幕效果很好。

但是，如果输入数据量很大，每次运行程序时都在键盘上键入这些数据效率就很低。除了输入大量数据的不便之外，键入还可能产生错误，并意外地导致错误的结果。你必须有一些方法从其他来源将数据传入程序。通过使用替代数据源，你可以在运行程序之前准备好数据，程序每次运行时都可以访问这些数据。

假设你想在会议上展示程序的输出。分发程序输出的打印副本是比在屏幕上显示输出更好的方法。例如，在一次重要会议之前，你可能会给委员会的每位成员一份打印报告。此外，有时必须保存输出，以便一个程序产生的输出可以用作其他程序的输入。

本节讨论如何从其他输入设备（如磁盘，即辅助存储器）获取数据，以及如何将输出保存到磁盘。C++ 允许程序从

