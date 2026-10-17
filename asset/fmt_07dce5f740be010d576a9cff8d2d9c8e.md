
```
// display value with internal spacing and plus sign
cout << internal << showpos << setw(10) << 123 << endl;
```

| 123 |

Fig. 13.13 | Printing an integer with internal spacing and plus sign.

### 13.7.3 填充（fill, setfill）

成员函数`fill`指定与对齐字段一起使用的填充字符；默认情况下使用空格进行填充。该函数返回之前的填充字符。`setfill`操纵符也设置填充字符。图 13.14 演示了函数`fill`（第 29 行）和流操纵符`setfill`（第 33 行和第 36 行）来设置填充字符。

## 第13章 流输入/输出：更深入的探讨

```
// Fig. 13.14: Figl13_cpp.cpp
// Using member function fill and stream manipulator setfill to change
// the padding character for fields larger than the printed value.
#include <iostream>
#include <iomanip>
using namespace std;
int main() {
    int x{10000};
    display x
    cout << x << " printed as int and left justified\n"
         << "and as hex with internal justification.\\n"
         << "Using the default pad character (space):\n";
    display x
    cout << setw(10) << x << x << "\n";
    display x with left justification
    cout << showcase << internal << setw(10) << hex << x << "\n";
    display x with hex with internal justification
    cout << "Using various padding characters:" << endl;
    display x using padded characters (right justification)
    cout << rightfill('#');
    cout << setw(10) << dec << x << "\n";
    display x using padded characters (left justification)
    cout << left << setw(10) << setfill('%') << x << "\n";
    display x using padded characters (internal justification)
    cout << internal << setw(10) << setfill('0') << hex << x << endl;
}
```

| 10000 printed as int right and left justified |
| and as hex with internal justification. |
| Using the default pad character (space): |
| 10000 |
| 0x 2710 |
| Using various padding characters: |
| *****10000 |
| 10000%%%%%% |
| 0x^^^2710 |

> Fig. 13.14 | Using member function fill and stream manipulator setfill to change the padding character for fields larger than the printed values.

### 13.7 流格式状态和流操纵符 637

### 13.7.4 整数流基数（dec, oct, hex, showbase）

C++ 提供了流操纵符 `dec`、`hex` 和 `oct` 来指定整数分别以十进制、十六进制和八进制值显示。如果未使用这些操纵符，流插入默认使用十进制。在流提取时，以 0（零）为前缀的整数被视为八进制值，以 `0x` 或 `0X` 为前缀的整数被视为十六进制值，其他所有整数被视为十进制值。一旦为流指定了特定基数，所有整数都将使用该基数进行处理，直到指定不同的基数或程序终止。

流操纵符 `base` 强制整数值的基数输出。默认情况下十进制数输出，八进制数输出时带有前导 0，十六进制数输出时带有前导 `0x` 或前导 `0X`（正如我们在第 13.7 节中讨论的，流操纵符更新选择哪个选项）。图 13.15 演示了使用流操纵符 `base` 强制整数以十进制、八进制和十六进制格式打印。要尊重 `showbase` 设置，请输出流操纵符 `noshowbase`。

```
// Fig. 13.15: Fig13_15.cpp
// Stream manipulatorbase.
#Include <iostream>
using namespace std;

int main() {
int x[100];

// use showbase to show number base
cout << "Printing octal and hexadecimal values with showbase:\n"
cout << showbase;

cout << dec << x << endl; // print decimal value
cout << oct << x << endl; // print octal value
cout << hex << x << endl; // print hexadecimal value
}
```

Printing octal and hexadecimal values with showbase:
100
0144
0x64

Fig. 13.15 | Stream manipulatorbase.

### 13.7.5 浮点数；科学计数法和定点计数法（scientific, fixed）

当浮点数在不指定其格式的情况下显示时，值决定输出格式——某些数字以科学计数法显示，其他数字以定点计数法显示。粘性流操纵符 `scientific` 和 `fixed` 控制浮点数的输出。流操纵符 `scientific` 强制浮点数以科学格式输出。流操纵符

## 638 第13章 流输入/输出：更深入的探讨

`fixed` 强制浮点数以定点计数法显示，小数点右侧的位数由成员函数 `precision` 或流操纵符 `presetprecision` 指定。

图 13.16 演示了使用流操纵符 `scientific`（第 16 行）和 `fixed`（第 20 行）在固定和科学格式中显示浮点数。科学计数法中的指数格式可能因编译器而异。

```
// Fig.13.16: Fig13_16.cpp
// Floating-point values displayed in system default,
// scientific and fixed formats.
#include <iostream>
using namespace std;
int main() {
    double x(0.001234567);
    double y(1.946e9);
    // display x and y in default format
    cout << "\nDisplayed in default format:\n" << x << "\t" << y;
    // display x and y in scientific format
    cout << "\nDisplayed in scientific format:\n" << scientific << x << "\t" << y;
    // display x and y in fixed format
    cout << "\nDisplayed in fixed format:\n" << fixed << x << "\t" << y << endl;
}
```

| Displayed in default format: 0.001234567 Displayed in scientific format: 1.234567e-03 1.9460000e+09 Displayed in fixed format: 0.001235 194600000.000000 |

**Fig. 13.16** | Floating-point values displayed in system default, scientific and fixed formats.

### 13.7.6 大小写控制（uppercase）

流操纵符 `uppercase` 输出十六进制整数值或科学计数法浮点值的大写 X 或（Fig. 13.17）。使用流操纵符 `uppercase` 会使十六进制值中的所有字母大写。默认情况下，十六进制值的字母和科学计数法中的指数以小写形式出现。要重置 `uppercase` 设置，请输出流操纵符 `nouppercase`。

## 13.7 流格式状态和流操纵符

```
// Fig. 13.17: Fig13_17.cpp
// Stream manipulator uppercase.
#include <iostream>
using namespace std;
int main() {
    cout << "Printing uppercase letters in scientific\n";
    cout << "notation exponents and hexadecimal values:\\n";
    // use std::uppercase to display uppercase letters; use std::hex
    // std::showbase to display hexadecimal value and its base
    cout << uppercase << 3.435e+10 << "\n";
    cout << hex << showbase << 123456789 << endl;
}
```

Printing uppercase letters in scientific
notation exponents and hexadecimal values:
3.435E+10
0X75BCD15

Fig. 13.17 | Stream manipulator uppercase.

### 13.7.7 指定布尔格式 (boolalpha)

C++ 提供了数据类型 `bool`，其值可以为 `false` 或 `true`，作为使用 0 表示 `false` 而任何非零值表示 `true` 的旧式方法的首选替代方案。`bool` 输出默认情况下为 0 或 1。然而，我们可以使用流操纵符 `boolalpha` 来设置输出以将 `bool` 值显示为字符串 `"true"` 和 `"false"`。使用流操纵符 `noboolalpha` 可将输出设置回以整数形式显示 `bool` 值（即默认设置）。图 13.18 的程序演示了这些操纵符。第 10 行以整数形式显示设置为 `true` 的 `bool` 值。第 14 行使用操纵符将 `bool` 值显示为字符串。第 17–18 行随后更改 `bool` 的值并使用操纵符 `noboolalpha`，第 21 行可以以整数形式显示 `bool` 值。第 25 行使用操纵符 `boolalpha` 将 `bool` 值显示为字符串。`boolalpha` 和 `noboolalpha` 都是粘性的。

> Good Programming Practice 13.1
Displaying bool values as true or false, rather than nonzero or 0, respectively, makes
program outputs clearer.

```
// Fig. 13.18: Fig13_18.cpp
// Stream manipulators boolalpha and noboolalpha.
#include <iostream>
using namespace std;
int main() {
    bool booleanValue{true};
}
```

Fig. 13.18 | Stream manipulators boolalpha and noboolalpha (Part I of 2).

## Chapter 13 Stream Input/Output: A Deeper Look

```
8 // display default booleanValue
9 cout << "booleanValue is " << booleanValue;
10
11 // display booleanValue after using boolalpha
12 cout << "booleanValue (after using boolalpha) is " 
13 << boolalpha << booleanValue;
14
15
16 cout << "\n\nswitch booleanValue and use noboolalpha\n";
17 booleanValue = false; // change booleanValue
18 cout << noboolalpha; // use noboolalpha
19
20 // display default booleanValue after using noboolalpha
21 cout << "\nbooleanValue is " << booleanValue;
22
23 // display booleanValue after using boolalpha again
24 cout << "\nbooleanValue (after using boolalpha) is " 
25 << boolalpha << booleanValue << endl;
26 }
```

booleanValue is 1
booleanValue (after using boolalpha) is true
switch booleanValue and use noboolalpha
booleanValue is 0
booleanValue (after using boolalpha) is false

Fig. 13.18 | Stream manipulators boolalpha and noboolalpha. (Part 2 of 2.)

## 13.7. 通过成员函数 flags 设置和重置格式状态

在第 13.7 节中，我们一直使用流操纵符来更改输出格式特性。现在我们讨论如何在应用多个操纵之后将输出流的格式恢复到其默认状态。无参数的成员函数 `flags` 返回当前格式设置作为 `fmtflags` 数据类型，它表示格式状态。带 `fmtflags` 参数的成员函数 `flags` 根据参数指定的格式设置格式状态并返回先前的状态设置。`flags` 返回的值的初始设置因编译器而异。13.19 的程序使用成员函数 `flags` 保存流的原始格式状态（第 16 行），然后恢复原始格式（第 24 行）。

```
// Fig. 13.19: Fig13_19.cpp
// flags member function.
#include <iostream>
using namespace std;

int main() {
```

Fig. 13.19 | Flags member function. (Part I of 2.)

The value of the flags is: 513
Print int and double in original format:
1000 0.0947628

The value of the flags variable is: 012011
Print int and double in a new format:
01750 9.476280e-02

The restored value of the flags variable is: 513
Print values in original format again:
1000 0.0947628

Fig. 13.19 | flags member function. (Part 2 of 2.)

## 13.8 流错误状态

每个流对象都包含一个状态位的状态，表示流的状态——粘性格式设置、错误指示等。书中前面我们指出，例如，输入是否成功。你可以测试类 `ios_base` 的这些位——流类的基类。流提取在输入错误类型的数据时将流的 `failbit` 设置为 `true`。类似地，提取在操作以不可恢复的方式失败时将流的 `badbit` 设置为 `true`——例如，当程序从磁盘读取文件时磁盘出现故障。图 13.20 显示了如何使用 `failbit` 和 `badbit` 等位来确定流的状态。在工业级代码中，你需要在每次 I/O 操作上执行类似的测试。第 22 章详细讨论了位和位操作。

- 1. 此程序的实际输出可能因编译器而异。

```
// Fig. 13.20: Fig13_20.cpp
// Testing stream error states.
#include <iostream>
using namespace std;
```
