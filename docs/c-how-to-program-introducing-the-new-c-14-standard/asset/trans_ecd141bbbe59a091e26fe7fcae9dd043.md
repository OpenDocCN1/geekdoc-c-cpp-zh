

图 13.14 使用成员函数 `fill` 和流操纵符 `setfill` 更改大于打印值的字段的填充字符。

## 13.7.4 整型流基数（`dec`、`oct`、`hex`、`showbase`）

C++ 提供了流操纵符 `dec`、`hex` 和 `oct`，分别指定整数以十进制、十六进制和八进制值显示。如果未使用这些操纵符中的任何一个，流插入*默认为十进制*。对于流提取，前缀为 `0`（零）的整数被视为*八进制*值，前缀为 `0x` 或 `0X` 的整数被视为*十六进制*值，所有其他整数被视为*十进制*值。一旦为流指定了特定的基数，该流上的所有整数都将使用该基数处理，直到指定不同的基数或程序终止为止。

流操纵符 `showbase` 强制输出整型值的*基数*。十进制数默认输出，八进制数以 `0` 开头输出，十六进制数以 `0x` 或 `0X` 开头输出（正如我们在**13.7.6 节**所讨论的，流操纵符 `uppercase` 决定选择哪种形式）。**图 13.15** 演示了使用流操纵符 `showbase` 强制整数以十进制、八进制和十六进制格式打印。要重置 `showbase` 设置，请输出流操纵符 `noshowbase`。

```cpp
// Fig. 13.15: Fig13_15.cpp
// Stream manipulator showbase.
#include <iostream>
using namespace std;

int main() {
    int x{100};

    // use showbase to show number base
    cout << "Printing octal and hexadecimal values with showbase:\n"
         << showbase;

    cout << x << endl; // print decimal value
    cout << oct << x << endl; // print octal value
    cout << hex << x << endl; // print hexadecimal value
}
```

```text
Printing octal and hexadecimal values with showbase:
100
0144
0x64
```

图 13.15 流操纵符 `showbase`。

## 13.7.5 浮点数；科学计数法和定点表示法（`scientific`、`fixed`）

当浮点数显示时未指定其格式，则由该值决定输出格式——有些数字以科学计数法显示，有些以定点表示法显示。粘性流操纵符 `scientific` 和 `fixed` 控制浮点数的输出格式。流操纵符 `scientific` 强制浮点数的输出以科学格式显示。流操纵符 `fixed` 强制浮点数以定点表示法显示，小数点右侧保留特定数量的数字——由成员函数 `precision` 或流操纵符 `setprecision` 指定。

**图 13.16** 演示了使用流操纵符 `scientific`（第 16 行）和 `fixed`（第 20 行）以定点格式和科学格式显示浮点数。科学计数法中指数的格式可能因编译器而异。

```cpp
// Fig. 13.16: Fig13_16.cpp
// Floating-point values displayed in system default,
// scientific and fixed formats.
#include <iostream>
using namespace std;

int main() {
   double x{0.001234567};
   double y{1.946e9};

   // display x and y in default format
   cout << "Displayed in default format:\n" << x << '\t' << y;

   // display x and y in scientific format
   cout << "\n\nDisplayed in scientific format:\n"
        << scientific << x << '\t' << y;

   // display x and y in fixed format
   cout << "\n\nDisplayed in fixed format:\n"
        << fixed << x << '\t' << y << endl;
}
```

```text
Displayed in default format:
0.00123457        1.946e+09

Displayed in scientific format:
1.234567e-03    1.946000e+09

Displayed in fixed format:
0.001235        1946000000.000000
```

图 13.16 以系统默认、科学计数法和定点格式显示的浮点值。

## 13.7.6 大写/小写控制（`uppercase`）

流操纵符 `uppercase` 分别输出十六进制整数值或科学计数法浮点值的大写 `X` 或 `E`（图 13.17）。使用流操纵符 `uppercase` 还会使十六进制值中的所有字母变为大写。默认情况下，十六进制值的字母和科学计数法浮点值中的指数以*小写*形式出现。要重置 `uppercase` 设置，请输出流操纵符 `nouppercase`。

```cpp
// Fig. 13.17: Fig13_17.cpp
// Stream manipulator uppercase.
#include <iostream>
using namespace std;

int main() {
   cout << "Printing uppercase letters in scientific\n"
        << "notation exponents and hexadecimal values:\n";

   // use std::uppercase to display uppercase letters; use std::hex and
   // std::showbase to display hexadecimal value and its base
   cout << uppercase << 4.345E10 << "\n"
        << hex << showbase << 123456789 << endl;
}
```

```text
Printing uppercase letters in scientific
notation exponents and hexadecimal values:
4.345E+10
0X75BCD15
```

图 13.17 流操纵符 `uppercase`。

## 13.7.7 指定布尔格式（`boolalpha`）

C++ 提供了数据类型 `bool`，其值可以是 `false` 或 `true`，作为旧式使用 `0` 表示 `false` 和任何非零值表示 `true` 的更好替代方案。`bool` 变量默认输出为 `0` 或 `1`。但是，我们可以使用流操纵符 `boolalpha` 将输出流设置为将 `bool` 值显示为字符串 `"true"` 和 `"false"`。使用流操纵符 `noboolalpha` 将输出流设置为将 `bool` 值显示为整数（即默认设置）。**图 13.18** 的程序演示了这些流操纵符。第 10 行将第 7 行设置为 `true` 的 `bool` 值作为整数显示。第 14 行使用操纵符 `boolalpha` 将 `bool` 值作为字符串显示。第 17–18 行随后更改 `bool` 的值并使用操纵符 `noboolalpha`，因此第 21 行可以将 `bool` 值作为整数显示。第 25 行使用操纵符 `boolalpha` 将 `bool` 值作为字符串显示。`boolalpha` 和 `noboolalpha` 都是粘性设置。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1715_0.png)

### 良好编程实践 13.1

将 `bool` 值显示为 `true` 或 `false`，而不是分别显示为非零值或 `0`，可以使程序输出更清晰。

```cpp
// Fig. 13.18: Fig13_18.cpp
// Stream manipulators boolalpha and noboolalpha.
#include <iostream>
using namespace std;

int main() {
   bool booleanValue{true};

   // display default true booleanValue
   cout << "booleanValue is " << booleanValue;

   // display booleanValue after using boolalpha
   cout << "\nbooleanValue (after using boolalpha) is "
      << boolalpha << booleanValue;

   cout << "\n\nswitch booleanValue and use noboolalpha\n";
   booleanValue = false; // change booleanValue
   cout << noboolalpha; // use noboolalpha

   // display default false booleanValue after using noboolalpha
   cout << "\nbooleanValue is " << booleanValue;

   // display booleanValue after using boolalpha again
   cout << "\nbooleanValue (after using boolalpha) is "
      << boolalpha << booleanValue << endl;
}
```

```text
booleanValue is 1
booleanValue (after using boolalpha) is true

switch booleanValue and use noboolalpha

booleanValue is 0
booleanValue (after using boolalpha) is false
```

图 13.18 流操纵符 `boolalpha` 和 `noboolalpha`。

## 13.7.8 通过成员函数 `flags` 设置和重置格式状态

在整个**13.7 节**中，我们一直在使用流操纵符来更改输出格式特性。我们现在讨论如何在应用了多种操作后将输出流的格式恢复为其默认状态。不带参数的成员函数 `flags` 以 `fmtflags` 数据类型返回当前格式设置，该数据类型表示**格式状态**。带 `fmtflags` 参数的成员函数 `flags` 按参数指定的方式设置格式状态，并返回先前的状态设置。`flags` 返回值的初始设置可能因编译器而异。**图 13.19** 的程序使用成员函数 `flags` 保存流的原始格式状态（第 16 行），然后恢复原始格式设置（第 24 行）。

