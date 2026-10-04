
# 第 3 章

程序输出的数字格式化

## 信息点

### 什么是标志 (Flag)？

在当前的编程用法中，“标志”（flag）一词指的是一个项，例如变量或参数，用于设置一个通常被认为是激活或非激活的条件。虽然这个词在编程中的起源尚不清楚，但它可能源于使用真实的标志来信号信号，例如赛车中使用的停止（Stop）、前进（Go）、小心（Caution）和冠军（Winner）。

同样，`setios()` 操符的每个标志参数都会激活特定的条件。例如，`ios::dec` 将标志格式设为十进制，而 `ios::oct` 激活八进制显示格式。这些条件是互斥的（同一时间只能激活一个），激活此类标志会自动去激活其他标志。

互不互斥的标志（例如 `ios::dec`、`ios::showpoint` 和 `ios::fixed`）可以同时设置。你可以通过使用三个单独的 `setflags()` 或将所有参数合并到一个调用中来实现这一点：

```cpp
cout << setflags(ios::dec | ios::showpoint);
```

## 表 3.3 用于 setflags() 的标志格式

| 标志 | 含义 |
|---|---|
| ios::fixed | 如果必要，始终显示小数点并在小数点后保留六位数字。如果与 `ios::showpoint` 标志一起设置，则在小数点前填充尾零具有优先级。 |
| ios::scientific | 在输出中使用科学计数法显示。 |
| ios::showpoint | 始终显示小数点和总共六个有效数字（整数部分和小数部分的组合）。必要时，在小数点后填充尾零。对于较大的整数值，除非设置了 `ios::fixed`，否则参考科学计数法。 |
| ios::showpos | 当数字为正时显示前导正号。 |
| ios::left | 输出左对齐。 |
| ios::right | 输出右对齐。 |

由于表 3.3 中的标志用作 `setflags()` 的参数，且“参数”（argument）和“参数”（parameter）是同义词，因此使用参数的操符方法的另一种名称是“参数化操符”。以下是参数化操符的示例：

```cpp
cout << setflags(ios::showpoint) << setprecision(4);
```

该语句强制所有发送到输出流的后续浮点数以带有和四位小数的形式显示。如果数字有四位小数，则用尾零填充。

## 124 赋值、格式化和交互式输入

除了以十进制法输出整数外，`oct` 和 `hex` 操符还用于转换为八进制和十六进制；程序 3.7 使用了这些标志。由于十进制是默认值，因此第一个输出流中不需要 `dec` 操符。

## 程序 3.7

```cpp
// 一个演示输出转换的程序
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
	cout << "The decimal (base 10) value of 15 is " << 15 << endl;
	cout << "The octal (base 8) value of 15 is " << oct << 15 << endl;
	cout << "The hexadecimal (base 16) value of 15 is " << hex << 15 << endl;

	return 0;
}
```

程序 3.7 产生的输出如下：

- The decimal (base 10) value of 15 is 15
- The octal (base 8) value of 15 is 017
- The hexadecimal (base 16) value of 15 is 0xf

在三种可能的数字系统（十进制、八进制和十六进制）之一中显示整数值不会影响数字在计算机中的存储方式。所有数字都由计算机的内部代码恢复。操符被设置为告知对象如何转换内部代码以输出显示。

除了以八进制或十六进制形式打印整数外，程序中也可以以这些形式编写。要指定八进制整数，数字必须有一个前导零。例如，数字 023 是 C++ 中的八进制数。十六进制数以前导 0x 表示。程序 3.8 显示了如何使用八进制和十六进制整数，并产生以下输出：

- The decimal value of 025 is 21
- The decimal value of 0x37 is 55

## 格式化 cout 流数据

cout 输出流中的浮点数据可以以精确的方式进行格式化。例如，一种常见的格式要求是显示金额，并在小数点后保留两位数字，例如 123.45。你可以通过以下语句实现：

```cpp
cout << setflags(ios::fixed)
<< setflags(ios::showpoint)
<< setprecision(2);
```

第一个操符标志 `ios::fixed` 强制 cout 中的所有浮点数以十进制表示法显示。该标志还防止了科学计数法。下一个标志 `ios::showpoint` 告诉流始终在小数点后显示两位数字。`setprecision` 操符告诉流始终在小数点后显示两位数字。与其使用操符，可以使用 `cout` 的 `set()` 和 `precision()` 方法。例如，之前的格式化也可以此代码实现：

```cpp
cout.set(ios::fixed);
cout.set(ios::showpoint);
out.precision(2);
```
