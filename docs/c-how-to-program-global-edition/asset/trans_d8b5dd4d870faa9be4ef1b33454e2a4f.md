
数字是 6。当既未使用定点流操纵符也未使用科学计数法流操纵符时，精度表示要显示的有效数字位数（即要显示的总位数），*不是*小数点后要显示的位数。

```
~~~cpp
// Fig. 21.13: fig21_13.cpp
// Controlling the printing of trailing zeros and
// decimal points in floating-point values.
#include <iostream>
using namespace std;

int main()
{
   // display double values with default stream format
   cout << "Before using showpoint" << endl
      << "9.9900 prints as: " << 9.9900 << endl
      << "9.9000 prints as: " << 9.9000 << endl
      << "9.0000 prints as: " << 9.0000 << endl << endl;

   // display double value after showpoint
   cout << showpoint
      << "After using showpoint" << endl
      << "9.9900 prints as: " << 9.9900 << endl
      << "9.9000 prints as: " << 9.9000 << endl
      << "9.0000 prints as: " << 9.0000 << endl;
} // end main
~~~
```

```
~~~
Before using showpoint
9.9900 prints as: 9.99
9.9000 prints as: 9.9
9.0000 prints as: 9

After using showpoint
9.9900 prints as: 9.99000
9.9000 prints as: 9.90000
9.0000 prints as: 9.00000
~~~
```

图 21.13 | 控制浮点值中尾随零和小数点的打印。

### 21.7.2 对齐（左对齐、右对齐和内部对齐）

流操纵符 `left` 和 `right` 使字段能够分别以*填充字符*在*右侧*进行*左*对齐，或以*填充字符*在*左侧*进行*右*对齐。填充字符由 `fill` 成员函数或 `setfill` 带参数流操纵符指定（我们将在第 21.7.3 节讨论）。图 21.14 使用 `setw`、`left` 和 `right` 操纵符在字段中对整数数据分别进行左对齐和右对齐。

```
~~~cpp
// Fig. 21.14: fig21_14.cpp
// Left and right justification with stream manipulators left and right.
#include <iostream>
~~~
```

图 21.14 | 使用流操纵符 left 和 right 进行左对齐和右对齐。（第 1 部分，共 2 部分）

```
~~~cpp
 4  #include <iomanip>
 5  using namespace std;
 6
 7  int main()
 8  {
 9     int x = 12345;
10
11     // display x right justified (default)
12     cout << "Default is right justified:" << endl
13          << setw( 10 ) << x;
14
15     // use left manipulator to display x left justified
16     cout << "\n\nUse std::left to left justify x:\n"
17          << left << setw( 10 ) << x;
18
19     // use right manipulator to display x right justified
20     cout << "\n\nUse std::right to right justify x:\n"
21          << right << setw( 10 ) << x << endl;
22  } // end main
~~~
```

```
~~~text
Default is right justified:
     12345

Use std::left to left justify x:
12345

Use std::right to right justify x:
     12345
~~~
```

![](img/bf54db922e6fa8319cba11069e785521_857_0.png)

流操纵符 `internal` 表示数字的符号（或使用流操纵符 `showbase` 时的基数）应在字段内左对齐，数字的数值应右对齐，并且中间的间隔应使用填充字符填充。图 21.15 展示了使用 `internal` 流操纵符指定内部间距（第 10 行）。注意 `showpos` 强制打印加号（第 10 行）。要重置 `showpos` 设置，请输出流操纵符 `noshowpos`。

```
~~~cpp
 1  // Fig. 21.15: fig21_15.cpp
 2  // Printing an integer with internal spacing and plus sign.
 3  #include <iostream>
 4  #include <iomanip>
 5  using namespace std;
 6
 7  int main()
 8  {
 9     // display value with internal spacing and plus sign
10     cout << internal << showpos << setw( 10 ) << 123 << endl;
11  } // end main
~~~
```

![](img/bf54db922e6fa8319cba11069e785521_857_1.png)

![](img/bf54db922e6fa8319cba11069e785521_858_0.png)

图 21.15 | 打印带内部间距和加号的整数。（第 2 部分，共 2 部分）

### 21.7.3 填充（fill、setfill）

`fill` 成员函数指定用于对齐字段的填充字符；默认使用空格进行填充。该函数返回先前的填充字符。`setfill` 操纵符也可设置填充字符。图 21.16 演示了使用函数 `fill`（第 30 行）和流操纵符 `setfill`（第 34 行和第 37 行）设置填充字符。

```
1 // Fig. 21.16: fig21_16.cpp
2 // Using member function fill and stream manipulator setfill to change
3 // the padding character for fields larger than the printed value.
4 #include <iostream>
5 #include <iomanip>
6 using namespace std;
7
8 int main()
9 {
10     int x = 10000;
11
12     // display x
13     cout << x << " printed as int right and left justified\n"
14         << "and as hex with internal justification\n"
15         << "Using the default pad character (space):" << endl;
16
17     // display x with base
18     cout << showbase << setw( 10 ) << x << endl;
19
20     // display x with left justification
21     cout << left << setw( 10 ) << x << endl;
22
23     // display x as hex with internal justification
24     cout << internal << setw( 10 ) << hex << x << endl << endl;
25
26     cout << "Using various padding characters:" << endl;
27
28     // display x using padded characters (right justification)
29     cout << right;
30     cout.fill( '*' );
31     cout << setw( 10 ) << dec << x << endl;
32
33     // display x using padded characters (left justification)
34     cout << left << setw( 10 ) << setfill( '%' ) << x << endl;
35
36     // display x using padded characters (internal justification)
37     cout << internal << setw( 10 ) << setfill( '^' ) << hex
38         << x << endl;
39 } // end main
```

图 21.16 | 使用成员函数 fill 和流操纵符 setfill 更改大于打印值的字段的填充字符。（第 1 部分，共 2 部分）

```
10000 printed as int right and left justified
and as hex with internal justification.
Using the default pad character (space):
    10000
10000
0x     2710

Using various padding characters:
****#10000
10000%0%0%
0x^^^2710
```

图 21.16 | 使用成员函数 fill 和流操纵符 setfill 更改大于打印值的字段的填充字符。（第 2 部分，共 2 部分）

### 21.7.4 整数流基数（dec、oct、hex、showbase）

C++ 提供了流操纵符 dec、hex 和 oct，分别用于指定整数以十进制、十六进制和八进制值显示。如果未使用这些操纵符中的任何一个，流插入默认采用十进制。对于流提取，以 0（零）为前缀的整数被视为八进制值，以 0x 或 0X 为前缀的整数被视为十六进制值，而所有其他整数被视为十进制值。一旦为某个流指定了特定基数，该流上的所有整数都会使用该基数处理，直到指定了不同的基数或程序终止。

流操纵符 showbase 强制输出整数值的基数。十进制数默认输出，八进制数输出时带前导 0，十六进制数输出时带前导 0x 或前导 0X（正如我们在第 21.7.6 节所讨论的，流操纵符 uppercase 决定选择哪个选项）。图 21.17 演示了使用流操纵符 showbase 强制整数以十进制、八进制和十六进制格式打印。要重置 showbase 设置，请输出流操纵符 noshowbase。

```
// Fig. 21.17: fig21_17.cpp
// Stream manipulator showbase.
#include <iostream>
using namespace std;

int main()
{
    int x = 100;

    // use showbase to show number base
    cout << "Printing integers preceded by their base:" << endl
         << showbase;

    cout << x << endl; // print decimal value
    cout << oct << x << endl; // print octal value
    cout << hex << x << endl; // print hexadecimal value
} // end main
```

图 21.17 | 流操纵符 showbase。（第 1 部分，共 2 部分）

```
```
Displayed in fixed format:
0.001235       1946000000.000000
```
```

**图 21.18** | 以默认、科学计数法和定点格式显示的浮点值。（第 2 部分，共 2 部分）

### 21.7.6 大写/小写控制（`uppercase`）

流操纵符 `uppercase` 分别在使用十六进制整数值或科学计数法浮点值时输出大写 X 或 E（图 21.19）。使用流操纵符 `uppercase` 还会使十六进制值中的所有字母变为大写。*默认情况下*，十六进制值的字母和科学计数法浮点值中的指数以小写形式出现。要重置大写设置，请输出流操纵符 `nouppercase`。

```
```cpp
1  // Fig. 21.19: fig21_19.cpp
2  // Stream manipulator uppercase.
3  #include <iostream>
4  using namespace std;
5
6  int main()
7  {
8     cout << "Printing uppercase letters in scientific" << endl
9        << "notation exponents and hexadecimal values: " << endl;
10
11   // use std::uppercase to display uppercase letters; use std::hex and
12   // std::showbase to display hexadecimal value and its base
13   cout << uppercase << 4.345e10 << endl
14      << hex << showbase << 123456789 << endl;
15 } // end main
```
```

```
```
Printing uppercase letters in scientific
notation exponents and hexadecimal values:
4.345E+10
0X75BCD15
```
```

**图 21.19** | 流操纵符 uppercase。

### 21.7.7 指定布尔格式（`boolalpha`）

C++ 提供了数据类型 `bool`，其值可以是 `false` 或 `true`，这是对使用 0 表示 false、非零表示 true 的旧式风格的一种首选替代方案。`bool` 变量*默认*输出 0 或 1。但是，我们可以使用流操纵符 `boolalpha` 将输出流设置为以字符串 "true" 和 "false" 显示 `bool` 值。使用流操纵符 `noboolalpha` 将输出流设置为以整数显示 `bool` 值（即默认设置）。图 21.20 的程序演示了这些流操纵符。第 11 行将第 8 行设置为 `true` 的 `bool` 值显示为整数。第 15 行使用操纵符 `boolalpha` 将 `bool` 值显示为字符串。然后第 18–19 行更改 `bool` 的值并使用操纵符 `noboolalpha`，因此第 22 行可以将 `bool` 值显示为整数。第 26 行使用操纵符 `boolalpha` 将 `bool` 值显示为字符串。`boolalpha` 和 `noboolalpha` 都是粘性设置。
