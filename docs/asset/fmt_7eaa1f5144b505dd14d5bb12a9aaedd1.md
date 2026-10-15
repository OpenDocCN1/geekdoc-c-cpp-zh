
**图 15.12** | 来自 `<iostream>` 的格式状态流操纵符。（第 2 部分，共 2 部分。）

## 15.7.1 尾随零和小数点 (`showpoint`)

流操纵符 `showpoint` 强制浮点数输出时带小数点及尾随零。例如，浮点数值 79.0 在不使用 `showpoint` 时打印为 79，而使用 `showpoint` 时打印为 79.000000（或按当前精度指定的尽可能多的尾随零）。要重置 `showpoint` 设置，请输出流操纵符 `noshowpoint`。图 15.13 中的程序演示了如何使用流操纵符 `showpoint` 控制浮点数值的尾随零和小数点的打印。回顾一下，浮点数的默认精度为 6。当既不使用 `fixed` 也不使用 `scientific` 流操纵符时，精度表示要显示的有效数字位数（即要显示的总位数），而不是小数点后要显示的位数。

```
// Fig. 15.13: Fig15_13.cpp
// Using showpoint to control the printing of
// trailing zeros and decimal points for doubles.
#include <iostream>
using std::cout;
using std::endl;
using std::showpoint;
```

**图 15.13** | 控制浮点数值中尾随零和小数点的打印。（第 1 部分，共 2 部分。）

```
8
9 int main()
10 {
11    // display double values with default stream format
12    cout << "Before using showpoint" << endl
13       << "9.9900 prints as: " << 9.9900 << endl
14       << "9.9000 prints as: " << 9.9000 << endl
15       << "9.0000 prints as: " << 9.0000 << endl << endl;
16
17    // display double value after showpoint
18    cout << showpoint
19       << "After using showpoint" << endl
20       << "9.9900 prints as: " << 9.9900 << endl
21       << "9.9000 prints as: " << 9.9000 << endl
22       << "9.0000 prints as: " << 9.0000 << endl;
23    return 0;
24 } // end main
```

使用 showpoint 之前

9.9900 打印为：9.99

9.9000 打印为：9.9

9.0000 打印为：9

使用 showpoint 之后

9.9900 打印为：9.99000

9.9000 打印为：9.90000

9.0000 打印为：9.00000

图 15.13 | 控制浮点数值中尾随零和小数点的打印。（第 2 部分，共 2 部分。）

## 15.7.2 对齐（`left`、`right` 和 `internal`）

流操纵符 `left` 和 `right` 分别使字段左对齐（右侧用填充字符填充）或右对齐（左侧用填充字符填充）。填充字符由 `fill` 成员函数或 `setfill` 参数化流操纵符（我们将在 15.7.3 节讨论）指定。图 15.14 使用 `setw`、`left` 和 `right` 操纵符在字段中左对齐和右对齐整数数据。

```
// Fig. 15.14: Fig15_14.cpp
// Demonstrating left justification and right justification.
#include <iostream>
using std::cout;
using std::endl;
using std::left;
using std::right;

#include <iomanip>
using std::setw;
```

图 15.14 | 使用流操纵符 `left` 和 `right` 进行左对齐和右对齐。（第 1 部分，共 2 部分。）

```cpp
int main()
{
   int x = 12345;

   // display x right justified (default)
   cout << "Default is right justified:" << endl
      << setw(10) << x;

   // use left manipulator to display x left justified
   cout << "\n\nUse std::left to left justify x:\n"
      << left << setw(10) << x;

   // use right manipulator to display x right justified
   cout << "\n\nUse std::right to right justify x:\n"
      << right << setw(10) << x << endl;
   return 0;
} // end main
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_660_0.png)

**图 15.14** | 使用流操纵符 `left` 和 `right` 进行左对齐和右对齐。（第 2 部分，共 2 部分。）

流操纵符 `internal` 表示数字的符号（或使用流操纵符 `showbase` 时的基数）应在字段内左对齐，数字的幅度应右对齐，中间空格用填充字符填充。图 15.15 展示了 `internal` 流操纵符指定内部间距（第 15 行）。注意，`showpos` 强制打印加号（第 15 行）。要重置 `showpos` 设置，请输出流操纵符 `noshowpos`。

```
// Fig. 15.15: Fig15_15.cpp
// Printing an integer with internal spacing and plus sign.
#include <iostream>
using std::cout;
using std::endl;
using std::internal;
using std::showpos;

#include <iomanip>
using std::setw;
```

**图 15.15** | 打印具有内部间距和加号的整数。（第 1 部分，共 2 部分。）

```cpp
int main()
{
   // display value with internal spacing and plus sign
   cout << internal << showpos << setw( 10 ) << 123 << endl;
   return 0;
} // end main
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_661_0.png)

**图 15.15** | 打印具有内部间距和加号的整数。（第 2 部分，共 2 部分。）

## 15.7.3 填充（`fill`、`setfill`）

`fill` 成员函数指定用于对齐字段的填充字符；如果未指定值，则使用空格进行填充。`fill` 函数返回先前的填充字符。`setfill` 操纵符也设置填充字符。图 15.16 演示了使用成员函数 `fill`（第 40 行）和流操纵符 `setfill`（第 44 行和第 47 行）来设置填充字符。

```
// Fig. 15.16: Fig15_16.cpp
// Using member function fill and stream manipulator setfill to change
// the padding character for fields larger than the printed value.
#include <iostream>
using std::cout;
using std::dec;
using std::endl;
using std::hex;
using std::internal;
using std::left;
using std::right;
using std::showbase;

#include <iomanip>
using std::setfill;
using std::setw;

int main()
{
   int x = 10000;

   // display x
   cout << x << " printed as int right and left justified\n"
        << "and as hex with internal justification.\n"
        << "Using the default pad character (space):" << endl;

   // display x with base
   cout << showbase << setw( 10 ) << x << endl;
```

**图 15.16** | 使用成员函数 `fill` 和流操纵符 `setfill` 为大于所打印值的字段更改填充字符。（第 1 部分，共 2 部分。）

```cpp
// display x with left justification
cout << left << setw( 10 ) << x << endl;

// display x as hex with internal justification
cout << internal << setw( 10 ) << hex << x << endl;

cout << "Using various padding characters:" << endl;

// display x using padded characters (right justification)
cout << right;
cout.fill( '*' );
cout << setw( 10 ) << dec << x << endl;

// display x using padded characters (left justification)
cout << left << setw( 10 ) << setfill( '%' ) << x << endl;

// display x using padded characters (internal justification)
cout << internal << setw( 10 ) << setfill( '^' ) << hex
     << x << endl;
return 0;
} // end main
```

```text
10000 printed as int right and left justified
and as hex with internal justification.
Using the default pad character (space):
     10000
10000
0x    2710

Using various padding characters:
*****10000
10000%%%%%
0x^^^^2710
```

**图 15.16** | 使用成员函数 `fill` 和流操纵符 `setfill` 为大于所打印值的字段更改填充字符。（第 2 部分，共 2 部分。）

## 15.7.4 整型流基数（`dec`、`oct`、`hex`、`showbase`）

C++ 提供了流操纵符 `dec`、`hex` 和 `oct` 来分别指定整数以十进制、十六进制和八进制值显示。如果未使用这些操纵符中的任何一个，流插入默认采用十进制。在流提取时，前缀为 0（零）的整数被视为八进制值，前缀为 0x 或 0X 的整数被视为十六进制值，所有其他整数被视为十进制值。一旦为流指定了特定的基数，该流上的所有整数都使用该基数处理，直到指定了不同的基数或程序终止。

流操纵符 `showbase` 强制输出整数值的基数。十进制数默认输出，八进制数以 0 开头输出，十六进制数以 0x 或 0X 开头输出（如我们在 15.7.6 节讨论的，流操纵符 `uppercase` 决定选择哪个选项）。图 15.17 演示了使用流操纵符 `showbase` 强制整数以

// Fig. 15.17: Fig15_17.cpp

// Using stream manipulator showbase.

#include <iostream>

using std::cout;

using std::endl;

using std::hex;

using std::oct;

using std::showbase;

int main()

{

    int x = 100;

    // use showbase to show number base

    cout << "Printing integers preceded by their base:" << endl

         << showbase;

    cout << x << endl; // print decimal value

    cout << oct << x << endl; // print octal value

    cout << hex << x << endl; // print hexadecimal value

    return 0;

} // end main

```
Printing integers preceded by their base:
100
0144
0x64
```

Fig. 15.17 | Stream manipulator showbase.

print in decimal, octal and hexadecimal formats. To reset the showbase setting, output the stream manipulator noshowbase.

## 15.7.5 Floating-Point Numbers; Scientific and Fixed Notation (`scientific`, `fixed`)

Stream manipulators `scientific` and `fixed` control the output format of floating-point numbers. Stream manipulator `scientific` forces the output of a floating-point number to display in scientific format. Stream manipulator `fixed` forces a floating-point number to display a specific number of digits (as specified by member function `precision` or stream manipulator `setprecision`) to the right of the decimal point. Without using another manipulator, the floating-point-number value determines the output format.

Figure 15.18 demonstrates displaying floating-point numbers in fixed and scientific formats using stream manipulators `scientific` (line 21) and `fixed` (line 25). The exponent format in scientific notation might differ across different compilers.

## 15.7.6 Uppercase/Lowercase Control (`uppercase`)

Stream manipulator `uppercase` outputs an uppercase X or E with hexadecimal-integer values or with scientific notation floating-point values, respectively (Fig. 15.19). Using stream manipulator `uppercase` also causes all letters in a hexadecimal value to be upper-

case. By default, the letters for hexadecimal values and the exponents in scientific notation floating-point values appear in lowercase. To reset the uppercase setting, output the stream manipulator `nouppercase`.

// Fig. 15.18: Fig15_18.cpp

// Displaying floating-point values in system default,

// scientific and fixed formats.

#include <iostream>

using std::cout;

using std::endl;

using std::fixed;

using std::scientific;

int main()

{

    double x = 0.001234567;

    double y = 1.946e9;
