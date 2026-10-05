

## 流 I/O 的工具 537

输出流除了 `precision` 和 `setf` 之外还有其他成员函数。一种常用的格式化方法是宽度设置。例如，考虑由流 `cout` 执行的以下 `width` 调用：

```
cout << "Start Now";
cout.width(4);
cout << 7 << endl;
```

这段代码将在屏幕上显示该行：

Start Now 7

此输出中，字母 'w' 和数字 7 之间恰好有三个空格。`width` 函数告诉流在输出项目时应使用多少个空间。在这种情况下，数字 7 仅占据一个空间，而 `width` 被设置为使用四个空间，因此其中三个空间是空白的。如果输出所需的空间大于你通过 `width` 参数中指定的空间，则将使用所需的额外空间。无论你提供什么参数，整个项目始终会被输出。

## ios 类

`ios` 类有许多重要的定义常量，例如 `ios::app`（用于指示你正在向文件追加内容）以及显示 12.5 中列出的标志。`ios` 类定义用于输出流，例如 `<iostream>` 和 `<fstream>`。为了让你的代码可以使用 `ios` 类以及所有这些常量（所有这些标志），可以使用以下语句：

```
#include <iostream> //或 #include <fstream> 或两者都包含
using std::ios;
```

取消任何已设置的标志。要取消标志，请使用 `unsetf` 函数。例如，以下代码将导致你的程序停止在输出到流 `cout` 的正整数加上加号：

```
unsetf(ios::showpos);
```

当一个标志被设置时，它将保持设置状态，直到被取消。调用 `precision` 的效果会一直有效直到重置精度。然而，成员函数 `width` 的行为则不同。调用 `width` 只适用于下一个输出的项目。如果你想输出 12 个数字，每个数字使用四个空格，那么你必须调用 12 次 `width`。如果这变成了一个麻烦，你可能更喜欢使用在下一个小节中描述的操纵符 `setw`。

## 538 第 12 章 流与文件 I/O

## 操纵符

操纵符是一种以非传统方式调用的函数。操纵符被放置在插入运算符之后，就像该操纵符函数调用了一个要输出的项目一样。像传统函数一样，操纵符可能有也可能没有参数。我们已经见过一个操纵符 `endl`。本小节将讨论 `setw` 和 `setprecision`。

操纵符 `setw` 和你已经看到的成员函数 `width` 执行的操作完全相同。你通过在插入运算符 `<<` 之后写入 `setw` 来调用它（如果发送到输出流），并在该调用中触发成员函数 `width`。例如，以下代码将使用宽度字段输出数字 10、20 和 30：

```
cout << "Start" << setw(4) << 10
<< setw(4) << 20 << setw(6) << 30;
```

前述语句将产生以下输出：

```
Start 10 20    30
```

（在 10 之前有两个空格，在 20 之前有两个空格，在 30 之后有四个空格。）

像成员函数 `width` 一，调用 `setw` 只适用于下一个项目，但比多次调用 `width` 更容易多次调用 `setw`。

操纵符 `setprecision` 的作用与成员函数 `precision`（你已经见过）相同。然而，调用 `setprecision` 写在插入运算符 `<<` 之后的，方式类似于你调用 `setw` 操纵符的方式。例如，以下代码将根据 `setprecision` 调用指定的小数点后的位数输出列出的数字：

```
cout(ios::fixed);
cout(ios::showpoint);
out << "$" << setprecision(2) << 10.3;
```

之前的语句将产生以下输出：

```
$10.30
$20.50
```

当你使用操纵符 `setprecision` 设置小数点后的位数时，就像使用成员函数 `precision` 一样，该设置一直有效，直到通过另一次调用将其重置。

要使用 `setw` 或 `setprecision` 操纵符，你必须在程序中包含以下指令：

```
#include <iomanip>
using namespace std;
```

或者，你必须使用以下其他指定名称和命名空间的方法：

```
#include <iomanip>
using std::setw;
using std::setprecision;
```

## 保存标志设置

函数不应该产生意外或意想不到的副作用。例如，输出金额的函数可能包含：

```
cout.setf(ios::fixed);
out.setf(ios::showpoint);
```

调用函数后，这些设置仍然有效。如果你不想副作用，可以保存并恢复原始设置。`precision` 函数被重载，因此不带参数时它返回当前精度，以便恢复设置。`cout.flags()` 成员函数返回一个所有标志的 `long` 值。使用此 `long` 值作为 `cout.flags()` 的参数可以重置标志。这些技术对于文件流和 `cout` 一样有效。例如，保存和恢复这些设置的结构如下：

```
void outputStream(ostream out)
{
    int precisionSetting = out.precision();
    long flagSettings = out.flags();
    out.setf(ios::fixed);
    out.setf(ios::showpoint);
    out.precision(2);
    // 在此处执行任何你想的操作
    out.precision(precisionSetting);
    out.flags(flagSettings);
}
```

另一种恢复设置的方法：

```
cout.setf(0, ios::floatfield);
```

带有这些参数的成员函数调用 `set` 将恢复默认设置（注意，而不是最后更改的设置）。此外，默认设置值取决于实现。最后，注意这不会重置 `precision` 设置或任何通过 `setf` 设置的设置。

## 更多输出流成员函数

显示 12.6 总结了 `ostream` 类的一些格式化成员函数和操纵符。记得使用以下操纵符（或类似的）：

```
#include <iomanip>
using namespace std;
```

显示 12.6 ostream 类格式化工具

| 函数 | 描述 | 对应的操纵符 |
|---|---|---|
| setf(ios_Flag) | 设置 12.5 中描述的标志 | setiosflags(ios_Flag) |
| unsetf(ios_Flag) | 取消标志 | resetiosflags(ios_Flag) |
| setf(0, ios::floatfield) | 恢复默认标志设置 | 无 |
| precision(int) | 设置浮点数输出精度 | setprecision(int) |
| precision() | 返回当前精度 | 无 |
| width(int) | 设置输出字段；仅适用于下一个项目 | setw(int) |
| fill(char) | 当输出字段大于值时指定填充字符；默认是空白 | setfill(char) |

## 自测练习

- 8. 执行以下行代码将产生什么输出？

```
cout << "*";
cout.width(5);
cout << 123;
cout << "*" << 123 << "*" << endl;
cout << "*" << setw(5) << 123
cout << "*" << 123 << "*" << endl;
```

## 自测练习（续）

- 9. 执行以下行代码将产生什么输出？

```
cout << "*" << setw(5) << 123;
cout.setf(ios::left);
cout << "*" << setw(5) << 123;
cout.setf(ios::right);
cout << "*" << setw(5) << 123 << "*" << endl;
```

- 10. 执行以下行代码将产生什么输出？

```
cout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
cout.setf(ios::showpos);
cout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
cout.unsetf(ios::showpos);
cout.setf(ios::left);
cout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
```

- 11. 执行以下行代码时，将向内容发送到文件 stuff.txt？

```
ofstream fout;
out.open("stuff.txt");
fout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
fout.setf(ios::showpos);
fout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
fout.unsetf(ios::showpos);
fout.setf(ios::left);
fout << "*" << setw(5) << 123 << "*"
<< 123 << "*" << endl;
```

- 12. 执行以下行代码时将产生什么输出（假设该行嵌入在具有正确指令的完整程序中）？

```
cout << "*" << setw(3) << 12345 << "*" << endl;
```

