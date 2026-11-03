
后续输出操作，直到下一次设置精度调用。无参数调用成员函数 precision 会返回当前精度设置（这是你需要在粘性设置不再需要后最终恢复原始精度时使用的）。图 21.9 的程序同时使用成员函数 precision（第 22 行）和 setprecision 操纵符（第 31 行）打印一个表格，显示 2 的平方根，精度从 0 到 9 变化。

// Fig. 21.9: fig21_09.cpp
// Controlling precision of floating-point values.
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;

int main()
{
    double root2 = sqrt( 2.0 ); // calculate square root of 2
    int places; // precision, vary from 0-9

    cout << "Square root of 2 with precisions 0-9." << endl
         << "Precision set by ios_base member function "
         << "precision:" << endl;

    cout << fixed; // use fixed-point notation

    // display square root using ios_base function precision
    for ( places = 0; places <= 9; ++places )
    {
        cout.precision( places );
        cout << root2 << endl;
    } // end for

    cout << "\nPrecision set by stream manipulator "
         << "setprecision:" << endl;

    // set precision for each digit, then display square root
    for ( places = 0; places <= 9; ++places )
        cout << setprecision( places ) << root2 << endl;
} // end main

Square root of 2 with precisions 0-9.
Precision set by ios_base member function precision:
1
1.4
1.41
1.414
1.4142
1.41421
1.414214
1.4142136
1.41421356
1.414213562

**图 21.9** | 控制浮点值的精度。（第 1 部分，共 2 部分。）

Precision set by stream manipulator setprecision:
1
1.4
1.41
1.414
1.4142
1.41421
1.414214
1.4142136
1.41421356
1.414213562

**图 21.9** | 控制浮点值的精度。（第 2 部分，共 2 部分。）

## 21.6.3 字段宽度（width、setw）

成员函数 width（基类 ios_base 的）设置字段宽度（即，一个值应输出到的字符位置数，或应输入的最大字符数）并返回先前的宽度。如果输出的值比字段宽度窄，则插入填充字符作为填充。比指定宽度更宽的值不会被截断——将打印完整数字。无参数的 width 函数返回当前设置。

**常见编程错误 21.1**

宽度设置仅适用于下一次插入或提取（即，宽度设置不是粘性的）；之后，宽度隐式设置为 0（也就是说，输入和输出将使用默认设置执行）。假设宽度设置适用于所有后续输出是一个逻辑错误。

**常见编程错误 21.2**

当字段不够宽以处理输出时，输出将按所需宽度打印，这可能会产生令人困惑的输出。

图 21.10 演示了 width 成员函数在输入和输出上的使用。输入到 char 数组时，最多读取比宽度少一个的字符，因为要为放入输入字符串的空字符留出空间。记住，当遇到非前导空白时，流提取将终止。setw 流操纵符也可用于设置字段宽度。[注意：在图 21.10 中提示输入时，用户应输入一行文本，按 Enter，然后按文件结束符（在 Microsoft Windows 系统上为 <Ctrl> z，在 Linux 和 OS X 系统上为 <Ctrl> d）。]

```
// Fig. 21.10: fig21_10.cpp
// width member function of class ios_base.
#include <iostream>
using namespace std;
```

**图 21.10** | 类 ios_base 的 width 成员函数。（第 1 部分，共 2 部分。）

```
6 int main()
7 {
8     int widthValue = 4;
9     char sentence[10 ];
10
11     cout << "Enter a sentence:" << endl;
12     cin.width(5); // input only 5 characters from sentence
13
14     // set field width, then display characters based on that width
15     while ( cin >> sentence )
16     {
17         cout.width( widthValue++ );
18         cout << sentence << endl;
19         cin.width( 5 ); // input 5 more characters from sentence
20     } // end while
21 } // end main
```

```
Enter a sentence:
This is a test of the width member function
This
    is
     a
    test
    of
    the
    wid
     h
    memb
     er
    func
    tion
```

图 21.10 | 类 ios_base 的 width 成员函数。（第 2 部分，共 2 部分。）

## 21.6.4 用户定义的输出流操纵符

你可以创建自己的流操纵符。图 21.11 展示了如何创建和使用新的无参数流操纵符 bell（第 8–11 行）、carriageReturn（第 14–17 行）、tab（第 20–23 行）和 endLine（第 27–30 行）。对于输出流操纵符，返回类型和参数必须是 ostream & 类型。当第 35 行将 endLine 操纵符插入输出流时，会调用函数 endLine，第 29 行将转义序列 \n 和 flush 操纵符（它刷新输出缓冲区）输出到标准输出 cout。类似地，当第 35–44 行将操纵符 tab、bell 和 carriageReturn 插入输出流时，会调用它们对应的函数——tab（第 20 行）、bell（第 8 行）和 carriageReturn（第 14 行），这些函数随后输出各种转义序列。

// Fig. 21.11: fig21_11.cpp
// Creating and testing user-defined, nonparameterized
// stream manipulators.
#include <iostream>
using namespace std;

图 21.11 | 用户定义的、无参数流操纵符。（第 1 部分，共 2 部分。）

```
// bell manipulator (using escape sequence \a)
ostream& bell( ostream& output )
{
   return output << '\a'; // issue system beep
} // end bell manipulator

// carriageReturn manipulator (using escape sequence \r)
ostream& carriageReturn( ostream& output )
{
   return output << '\r'; // issue carriage return
} // end carriageReturn manipulator

// tab manipulator (using escape sequence \t)
ostream& tab( ostream& output )
{
   return output << '\t'; // issue tab
} // end tab manipulator

// endLine manipulator (using escape sequence \n and flush stream
// manipulator to simulate endl)
ostream& endLine( ostream& output )
{
   return output << '\n' << flush; // issue endl-like end of line
} // end endLine manipulator

int main()
{
   // use tab and endLine manipulators
   cout << "Testing the tab manipulator:" << endLine
      << 'a' << tab << 'b' << tab << 'c' << endLine;

   cout << "Testing the carriageReturn and bell manipulators:"
      << endLine << "............";

   cout << bell; // use bell manipulator

   // use carriageReturn and endLine manipulators
   cout << carriageReturn << "-----" << endLine;
} // end main
```

Testing the tab manipulator:
a       b       c
Testing the carriageReturn and bell manipulators:
.........

图 21.11 | 用户定义的、无参数流操纵符。（第 2 部分，共 2 部分。）

## 21.7 流格式状态和流操纵符

各种流操纵符可用于指定在流 I/O 操作期间要执行的格式类型。流操纵符控制输出的格式设置。图 21.12 列出了每个控制给定流格式状态的流操纵符。所有这些操纵符都属于类 ios_base。我们将在接下来几节中展示大多数这些流操纵符的示例。

| 操纵符 | 描述 |
|---|---|
| skipws | 跳过输入流上的空白字符。此设置通过流操纵符 noskipws 重置。 |
| left | 在字段中左对齐输出。如有必要，填充字符出现在右侧。 |
| right | 在字段中右对齐输出。如有必要，填充字符出现在左侧。 |
| internal | 指示数字的符号应在字段中左对齐，而数字的数值应在同一字段中右对齐（即，填充字符出现在符号和数字之间）。 |
| boolalpha | 指定 bool 值应显示为单词 true 或 false。操纵符 noboolalpha 将流恢复为将 bool 值显示为 1（true）和 0（false）。 |
| dec | 指定整数应被视为十进制（基 10）值。 |
| oct | 指定整数应被视为八进制（基 8）值。 |
| hex | 指定整数应被视为十六进制（基 16）值。 |
| showbase | 指定数字的基数应输出在数字前面（八进制为前导 0；十六进制为前导 0x 或 0X）。此设置通过流操纵符 noshowbase 重置。 |
| showpoint | 指定浮点数应带小数点输出。这通常与 fixed 一起使用，以保证小数点右侧有一定数量的数字，即使它们是零。此设置通过流操纵符 noshowpoint 重置。 |
| uppercase | 指定十六进制整数中应使用大写字母（即 X 和 A 到 F），并且以科学记数法表示浮点值时应使用大写 E。此设置通过流操纵符 nouppercase 重置。 |
| showpos | 指定正数前面应加上加号（+）。此设置通过流操纵符 noshowpos 重置。 |
| scientific | 指定以科学记数法输出浮点值。 |
| fixed | 指定以定点记数法输出浮点值，并在小数点右侧指定一定数量的数字。 |

图 21.12 | 来自 <iostream> 的格式状态流操纵符

### 21.7.1 尾随零和小数点（showpoint）

流操纵符 showpoint 是一个粘性设置，强制浮点数输出其小数点和尾随零。例如，浮点值 79.0 在不使用 showpoint 时打印为 79，在使用 showpoint 时打印为 79.00000（或当前精度指定的尽可能多的尾随零）。要重置 showpoint 设置，输出流操纵符 noshowpoint。图 21.13 中的程序展示了如何使用流操纵符 showpoint 控制浮点值的尾随零和小数点的打印。回想一下，浮点数的默认精度是
