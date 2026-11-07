

### 19.6.7 填充（fill, setfill）

fill 成员函数指定用于对齐字段的填充字符，并返回之前的填充字符。默认使用空格进行填充。setfill 操纵器也设置填充字符。图 19.13 演示了使用 fill（第 29 行）和 setfill（第 33 和 38 行）设置填充字符。

```cpp
1 // fig19_13.cpp
2 // Using member function fill and stream manipulator setfill to change
3 // the padding character for fields larger than the printed value.
4 #include <iomanip>
5 #include <iostream>
6
7 int main() {
8    int x{10000};
9
10    // display x
11    std::cout << x << " printed as int right and left aligned\n"
12        << "and as hex with internal alignment.\n"
13        << "Using the default pad character (space):\n";
14
15    // display x
16    std::cout << std::setw(10) << x << "\n";
17
18    // display x with left alignment
19    std::cout << std::left << std::setw(10) << x << "\n";
20
21    // display x with base as hex with internal alignment
22    std::cout << std::showbase << std::internal << std::setw(10)
23              << std::hex << x << "\n\n";
24
25    std::cout << "Using various padding characters:\n";
26
27    // display x using padded characters (right alignment)
28    std::cout << std::right << std::setw(10);
29    std::cout.fill('*');
30    std::cout << std::setw(10) << std::dec << x << "\n";
31
32    // display x using padded characters (left alignment)
33    std::cout << std::left << std::setw(10) << std::setfill('%')
34              << x << "\n";
35
36    // display x using padded characters (internal alignment)
37    std::cout << std::internal << std::setw(10)
38              << std::setfill('^') << std::hex << x << "\n";
39 }
```

```text
10000 printed as int right and left aligned
and as hex with internal alignment.
Using the default pad character (space):
       10000
10000
0x     2710

Using various padding characters:
********10000
10000%%%%%%
0x^^^^^^2710
```

**图 19.13** | 使用成员函数 `fill` 和流操纵器 `setfill` 更改大于所打印值的字段的填充字符。

### 19.6.8 整型流基数（dec, oct, hex, showbase）

C++ 提供了流操纵器 dec、oct 和 hex，分别指定整数应显示为十进制、十六进制和八进制值。整数默认以十进制（基数为 10）显示。使用流提取时，以 0 为前缀的整数被视为八进制值，以 0x 或 0X 为前缀的整数被视为十六进制值，所有其他整数被视为十进制值。一旦指定了流的基数，它将使用该基数处理所有整数，直到指定了另一个基数或程序终止。

流操纵器 showbase 使八进制数以 0 开头输出，十六进制数以 0x 或 0X 开头输出——19.6.10 节表明，流操纵器 uppercase 决定十六进制值选择哪种选项。图 19.14 演示了 showbase。要重置 showbase 设置，请在流中插入流操纵器 noshowbase。

```cpp
// fig19_14.cpp
// Stream manipulator showbase.
#include <iostream>

int main() {
    int x{100};

    // use showbase to show number base
    std::cout << "Printing octal and hexadecimal values with showbase:\n"
              << std::showbase;

    std::cout << x << "\n"; // print decimal value
    std::cout << std::oct << x << "\n"; // print octal value
    std::cout << std::hex << x << "\n"; // print hexadecimal value
}
```

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1178_0.png)

**图 19.14** | 流操纵器 showbase。

### 19.6.9 浮点数；科学计数法与定点表示法（scientific, fixed）

当您显示浮点数而未指定其格式时，其值将决定输出格式。某些数字以科学计数法显示，其他数字以定点表示法显示。粘性流操纵器 scientific 和 fixed 控制浮点数的输出格式：

- `scientific` 强制浮点数以科学计数法格式显示。
- `fixed` 强制浮点数以定点表示法显示，小数点右侧的数字位数由成员函数 `precision` 或流操纵器 `setprecision` 指定。

图 19.15 使用流操纵器 scientific（第 15 行）和 fixed（第 19 行）以固定格式和科学计数法格式显示浮点数。科学计数法中的指数格式可能因编译器而异。

```cpp
// fig19_15.cpp
// Floating-point values displayed in system default,
// scientific and fixed formats.
#include <iostream>

int main() {
    double x{0.01234567};
    double y{1.946e9};
10  // display x and y in default format
11  std::cout << "Displayed in default format:\n" << x << '\t' << y;

13  // display x and y in scientific format
14  std::cout << "\nDisplayed in scientific format:\n"
15      << std::scientific << x << '\t' << y;

18  // display x and y in fixed format
19  std::cout << "\nDisplayed in fixed format:\n"
20      << std::fixed << x << '\t' << y << "\n";
21  }
```

```text
Displayed in default format:
0.00123457       1.946e+09

Displayed in scientific format:
1.234567e-03     1.946000e+09

Displayed in fixed format:
0.001235         1946000000.000000
```

**图 19.15** | 以系统默认、科学计数法和固定格式显示的浮点数。

### 19.6.10 大小写控制（uppercase）

流操纵器 uppercase 输出十六进制整数值时使用大写 X，输出科学计数法浮点值时使用大写 E（图 19.16；第 11 行）。使用 uppercase 还会以大写形式显示十六进制数字 A–F。这些数字默认以小写形式显示。要重置 uppercase 设置，请输出 nouppercase。

```cpp
1  // fig19_16.cpp
2  // Stream manipulator uppercase.
3  #include <iostream>
4
5  int main() {
6      std::cout << "Printing uppercase letters in scientific\n"
7          << "notation exponents and hexadecimal values:\n";
8
9      // use std::uppercase to display uppercase letters; use std::hex and
10     // std::showbase to display hexadecimal value and its base
11     std::cout << std::uppercase << 4.345e10 << "\n"
12         << std::hex << std::showbase << 123456789 << "\n";
13 }
```

```text
Printing uppercase letters in scientific
notation exponents and hexadecimal values:
4.345E+10
0X75BCD15
```

**图 19.16** | 流操纵器 uppercase。

### 19.6.11 指定布尔格式（boolalpha）

C++ bool 值可以为 false 或 true。请记住，0 也表示 false，任何非零值表示 true。bool 值默认显示为 0 或 1。您可以使用流操纵器 boolalpha 将输出流设置为将 bool 值显示为字符串 "true" 和 "false"，并使用流操纵器 noboolalpha 将输出流恢复为将 bool 值显示为整数 0 和 1。图 19.17 演示了这些流操纵器。第 9 行将 booleanValue（第 16 行将其设置为 true）显示为整数。第 13 行使用 boolalpha 将 bool 值显示为字符串。第 16–17 行随后将 booleanValue 更改为 false 并使用操纵器 noboolalpha，因此第 20 行可以将 bool 值显示为整数。第 24 行使用操纵器 boolalpha 将 bool 值显示为字符串。boolalpha 和 noboolalpha 都是粘性设置。

```cpp
// fig19_17.cpp
// Stream manipulators boolalpha and noboolalpha.
#include <iostream>

int main() {
   bool booleanValue{true};

   // display default true booleanValue
   std::cout << "booleanValue is " << booleanValue;

   // display booleanValue after using boolalpha
   std::cout << "\nbooleanValue (after using boolalpha) is "
      << std::boolalpha << booleanValue;

   std::cout << "\n\nswitch booleanValue and use noboolalpha\n";
   booleanValue = false; // switch booleanValue
   std::cout << std::noboolalpha; // use noboolalpha

   // display default false booleanValue after using noboolalpha
   std::cout << "\nbooleanValue is " << booleanValue;

   // display booleanValue after using boolalpha again
   std::cout << "\nbooleanValue (after using boolalpha) is "
      << std::boolalpha << booleanValue << "\n";
}
```

```text
booleanValue is 1
booleanValue (after using boolalpha) is true

switch booleanValue and use noboolalpha

booleanValue is 0
booleanValue (after using boolalpha) is false
```

**图 19.17** | 流操纵器 boolalpha 和 noboolalpha。

