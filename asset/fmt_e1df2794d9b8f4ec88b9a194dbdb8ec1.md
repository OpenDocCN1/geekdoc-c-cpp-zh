
Line 9: `a = 37`, `b = 653`, `c = 30`, `d = 40`

在此示例运行中，第二个输入值是 653.89。`cin` 尝试将其输入变量 `b`。然而，由于 `b` 是 `int` 变量，输入流进入失败态。注意 `c` 和 `d` 的值没有改变，如第 9 行语句的输出所示。

## 失败态

输入流进入失败态时到底发生了什么？一旦输入流进入失败态，所有使用该流的 I/O 语句将被忽略。遗憾的是，程序会带有变量中存储的任何值静地继续执行并产生错误的结果。要从失败态恢复，你必须使用输入流的 `clear()` 成员函数。

你可以配合 `cout` 和插入操作符使用 `setprecision` 操纵符。例如，语句：

```
cout << setprecision(2);
```

会将小数的输出格式化为两位小数，直到后续类似的语句更改精度。请注意，小数位数（或精度值）是作为参数传递给 `setprecision` 的。

要使用 `setprecision` 操纵符，程序必须包含头文件 `iomanip`。因此，需要以下包含语句：

```cpp
#include <iomanip>
```

## `fixed` 操纵符

为了控制浮点数的输出，你可以使用其他操纵符。要以固定小数格式输出浮点数，例如，你可以使用 `fixed` 操纵符。以下语句将标准输出设备上的浮点数输出设为固定小数格式：

```cpp
cout << fixed;
```

在前述语句执行后，所有浮点数将以固定小数格式显示，直到禁用 `fixed` 操纵符。你可以通过流成员函数 `unsetf` 禁用 `fixed` 操纵符。要禁用标准输出设备上的 `fixed` 操纵符，你可以使用以下语句：

```cpp
cout.unsetf(ios::fixed);
```

禁用 `fixed` 操纵符后，浮点数的输出将恢复默认设置。`scientific` 操纵符用于以科学计数法输出浮点数。

> 注意：在某些编译器上可能不支持 `scientific`。在这种情况下，你可以用 `cout.setf(ios::fixed)` 代替 `cout << fixed;`，用 `cout.setf(ios::scientific)` 代替 `cout << scientific;`

以下示例展示了在不使用 `setprecision` 操纵符的情况下，`scientific` 和 `fixed` 操纵符是如何工作的。

## 示例 3-10

```cpp
//Example: scientific and fixed
#include <iostream>

using namespace std;

int main() {
    double hours = 35.45;
    double rate = 15.00;
    double tolerance = 0.01000;

    cout << "hours = " << hours << " << rate = " << rate;
    cout << ", pay = " << hours << " * rate;
    cout << ", tolerance = " << tolerance << endl << endl;

    cout << "Scientific notation: " << endl;
    cout << "hours = " << hours << " << rate = " << rate;
    cout << ", pay = " << hours << " * rate;
    cout << ", tolerance = " << tolerance << endl << endl;

    cout << "fixed:";
    cout << "Fixed decimal notation: " << endl;
    cout << "hours = " << hours << " << rate = " << rate;
    cout << ", pay = " << hours << " * rate;
    cout << ", tolerance = " << tolerance << endl << endl;

    return 0;
}
```

## 示例运行:

`hours = 35.45, rate = 15, pay = 531.75, tolerance = 0.01`

`Scientific notation:`

`hours = 3.545000e+01, rate = 1.50000e+01, pay = 5.31750e+02, tolerance = -1.00000e-002`

`Fixed decimal notation:`

`hours = 35.450000, rate = 15.000000, tolerance = 0.010000`

示例运行显示，`rate` 和 `tolerance` 的值在没有设置 `scientific` 或 `fixed` 操纵符的情况下打印，且不会显示末尾零；在 `rate` 的情况下，不会显示小数点。在设置了操纵符后，值将保留六位小数输出。在下一节中，我们将描述 `showpoint` 操纵符，它用于强制系统显示小数点和末尾零。随后，我们将提供一个如何使用 `setprecision`、`fixed` 和 `showpoint` 操纵符获取所需输出的示例。

## `showpoint` 操纵符

假设小数的小数部分为零。在这种情况下，如果你指示计算机以固定小数格式输出该小数，输出可能不会显示小数点和小数。为了强制输出显示小数点和末尾零，你可以使用 `showpoint` 操纵符。以下语句将标准输出设备上的小数输出设为带有小数点和末尾零：

```
cout << showpoint;
```

当然，以下语句将标准输出设备上的浮点数输出设为带有小数点和末尾零的小数格式：

```
cout << fixed << showpoint;
```

示例 3-11 中的程序说明了如何使用 `setprecision`、`fixed` 和 `showpoint` 操纵符。

## 示例 3-11

```cpp
//Example: setprecision, fixed, showpoint
#include <iostream>
#include <iomanip>
using namespace std;
const double PI = 3.14159265;
int main() {
    double radius = 12.67;
    double height = 12.00;
    cout << fixed << showpoint;
    cout << setprecision(2) << endl;
    // Line 10: setprecision(2) << endl;
    // Line 11: cout << "radius = " << radius << endl;
    // Line 12: cout << "height = " << height << endl;
    // Line 13: cout << "volume = " << PI * radius * radius * height << endl;
    // Line 14: cout << "PI = " << PI << endl;
    // Line 15: setprecision(3);
    // Line 16: cout << "radius = " << radius << endl;
    // Line 17: cout << "height = " << height << endl;
    // Line 18: cout << "volume = " << PI * radius * radius * height << endl;
    // Line 19: cout << "PI = " << PI << endl;
    // Line 20: setprecision(4);
    // Line 21: cout << "radius = " << radius << endl;
    // Line 22: cout << "height = " << height << endl;
    // Line 23: cout << "volume = " << PI * radius * radius * height << endl;
    // Line 24: cout << "PI = " << PI << endl;
```

## 示例运行:

`Line 10: setprecision(2)`

`Line 11: radius = 12.67`

`Line 12: height = 12.00`

`Line 13: volume = 601.80`

`Line 14: PI = 3.14`

`Line 15: setprecision(3)`

`Line 16: radius = 12.670`

`Line 17: height = 12.000`

`Line 18: volume = 601.797`

`Line 19: PI = 3.142`

`Line 20: setprecision(4)`

`Line 21: radius = 12.6700`

`Line 22: height = 12.0000`

`Line 23: volume = 601.7969`

`Line 24: PI = 3.1416`

在此程序中，第 2 行包含了头文件 `iomanip`，第 4 行声明了常量 `PI` 并将其值设置为八位小数。第 7-8 行初始化了 `radius` 和 `height`。第 9-10 行将浮点数的输出设为带有末尾零的固定格式。第 11-14 行以两位小数输出 `radius`、`height` 和 `PI`。

第 16-19 行以三位小数输出 `radius`、`height`、`volume` 和 `PI`。第 21-24 行以四位小数输出 `radius`、`height`、`volume` 和 `PI`。

## `setw`

`setw` 操纵符用于在指定的列中输出表达式的值。表达式的值可以是字符串也可以是数字。`setw(n)` 表达式在 `n` 列中输出下一个表达式的值。输出是右对齐的。因此，如果你指定列数为 8（例如），而输出只需要四列，那么前四列将留空。此外，如果指定的列数小于输出所需的列数，输出将自动扩展到所需的列数；输出不会被截断。例如，如果 `x` 是一个 `int` 变量，以下语句在标准输出上以五列输出 `x` 的值：

```
cout << setw(5) << x << endl;
```

与控制直到下次重置的所有浮点数输出的 `precision` 不同，`setw` 只控制下一个表达式的输出。

## 示例 3-12

```cpp
//Example: setw
#include <iostream>
#include <iomanip>
```

输出与输出格式 | 143

`using namespace std;`

```cpp
int main() {
    int x = 19;
    int a = 345;
    double y = 76.384;

    cout << fixed << showpoint << "\n";
    cout << "12345678901234567890" << endl;

    cout << setw(5) << x << endl;
    cout << setw(5) << a << setw(5) << endl;
    cout << setw(5) << x << endl << endl;

    cout << precision(2);
    cout << setw(6) << x << y;
    cout << setw(6) << x << endl;
    cout << setw(6) << y << setw(6) << a;
    cout << setw(6) << y << endl << endl;

    cout << setw(5) << a << x << endl;
    cout << setw(2) << a << setw(4) << x << endl;

    return 0;
}
```

# 3

示例运行：

`12345678901234567890`

`19`

`HI 19`

`345 76.38 19`

`19 345 76.38`

`34519`

`19`

第 1、2 和 3 行的语句声明了变量 `x`、`a` 和 `y`，并分别将变量初始化为 19、345 和 76.384。第 4 行的语句将浮点数的输出设置为固定小数格式，并带有数点和末尾零。第 5 行语句的输出显示了打印特定值时的列位置；这是输出的第一行。

第 6 行的语句在五列宽中输出 `x` 的值。因为 `x` 只有两位数字，所以只需要两列即可输出其值。因此，在输出的第二行中，前三列被留空。第 7 行的语句在前五列中输出 `a` 的值，在接下来的五列中输出字符串 "Hi"，然后在后续五列中输出 `x` 的值。因为字符串 "Hi" 只包含两个字符，而设置了五列来输出这两个字符，所以前三列被留空。见输出的第三行。第四行输出是空的，因为第 7 行语句中出现了两次 `endl` 操符。

第 8 行的语句将浮点数的输出设置为两位小数。第 9 行的语句在前几列中输出 `a` 的值，在接下来六列中输出 `y`，在随后的列中输出 `x`，形成了第五行输出。第 10 行语句的输出（即第六行）与第 9 行和第 10 行语句的输出相似。第七行输出是空的，因为第 10 行语句中出现了 `endl` 操符。

第 11 行的语句在五列中输出 `a` 的值以及 `x` 的值。注意，第 11 行语句中的 `setw` 操符只控制 `a` 的输出。因此，打印了 `a` 的值，并在当前光标位置（输出的第八行）打印了 `x` 的值。

在第 12 行的计数语句中，仅分配了两列来输出 `a` 的值。然而，`a` 的值有三数字，因此输出扩展到了三列。然后用四列宽打印 `x` 的值。因为 `x` 的值只有两位数字，所以只需要两列即可输出 `x` 值。因此，由于分配了四列来输出 `x` 的值，前两列被留空（见第九行输出）。

## 额外的输出格式工具

在上一节中，你学习了如何使用操符 `setprecision`、`fixed` 和 `showpoint` 来控制浮点数的输出，以及如何使用操符 `setw` 在特定列中显示输出。尽管这些操符已足够生成一份优雅的报告，但在某些情况下，你可能想做得更多。在本节中，你将学习额外的格式工具，让你对输出有更多的控制。

## `setfill` 操符

回想一下，在操符 `setw` 中，如果指定的列数超过所需的列数，输出将右对齐，且未使用的列将用空格填充。输出流变量可以使用 `setfill` 操符用空格以外的字符填充未使用的列。

使用 `setfill` 变量的语法为：

```cpp
ostreamVar << setfill(ch);
```

其中 `oVar` 是输出流变量，`ch` 是字符。例如，语句：

```cpp
cout << setfill('#');
```

输出流变量可以使用 `setfill` 操符用空格以外的字符填充未使用的列。要使用 `setfill` 操符，程序必须包含 `<iomanip>`。

# 示例 33: setfill

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

int main() {
    int x = 19;
    int a = 345;
    double y = 76.384;

    cout << fixed << showpoint << "\n";
    cout << "12345678901234567890" << endl;

    cout << setw(5) << x << endl;
    cout << setw(5) << a << setw(5) << endl;
    cout << setw(5) << x << endl << endl;

    cout << precision(2);
    cout << setw(6) << x << y;
    cout << setw(6) << x << endl;
    cout << setw(6) << y << setw(6) << a;
    cout << setw(6) << y << endl << endl;

    cout << setw(5) << a << x << endl;
    cout << setw(2) << a << setw(4) << x << endl;

    return 0;
}
```

# 第 3 章：输入/输出

```cpp
<< setw(8) << setfill('^') << "Warm"
<< endl;
```

```cpp
cout << right;
cout << setfill(' ');
```

```cpp
cout << setw(5) << x << setw(7) << y
<< setw(8) << "Warm" << endl;
```

```cpp
return 0;
}
```

# 示例运行：

```
12345678901234567890
15 ****7634 Warm
15***7634***Warm****
15***7634####Warm####
150@@7634####Warm^^^^
15 7634 Warm
```

该程序的输出与示例 3–11相同。唯一的区别在于对于第 4 行到第 9 行的语句，输出是左对齐的。鼓励你对该程序进行走读。

> 本章讨论了几个流函数和流操纵符。你可以在程序中使用 `get`、`ignore`、`fill` 和 `clear` 等流函数，程序必须包含头文件 `iostream`。
