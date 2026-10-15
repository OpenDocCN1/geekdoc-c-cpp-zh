
```cpp
// Fig. 15.8: Fig15_08.cpp
// Using stream manipulators hex, oct, dec and setbase.
#include <iostream>
using std::cin;
using std::cout;
using std::dec;
using std::endl;
using std::hex;
using std::oct;

#include <iomanip>
using std::setbase;

int main()
{
    int number;

    cout << "Enter a decimal number: ";
    cin >> number; // input number

    // use hex stream manipulator to show hexadecimal number
    cout << number << " in hexadecimal is: " << hex
         << number << endl;

    // use oct stream manipulator to show octal number
    cout << dec << number << " in octal is: "
         << oct << number << endl;

    // use setbase stream manipulator to show decimal number
    cout << setbase( 10 ) << number << " in decimal is: "
         << number << endl;
    return 0;
} // end main
```

Fig. 15.8 | Stream manipulators hex, oct, dec and setbase. (Part 1 of 2.)

```
Enter a decimal number: 20
20 in hexadecimal is: 14
20 in octal is: 24
20 in decimal is: 20
```

**Fig. 15.8** | Stream manipulators hex, oct, dec and setbase. (Part 2 of 2.)

## 15.6.2 Floating-Point Precision (precision, setprecision)

我们可以使用 `setprecision` 流操纵符或 `ios_base` 的 *precision* 成员函数来控制浮点数的 *precision*（即小数点右侧的位数）。对其中任一的调用都会为所有后续的输出操作设置精度，直到下一次设置精度的调用为止。无参数的 `precision` 成员函数调用会返回当前的精度设置（这就是你需要使用的，以便在不再需要“粘性”设置后最终恢复原始精度）。图 15.9 的程序同时使用了成员函数 `precision`（第 28 行）和 `setprecision` 操纵符（第 37 行）来打印一张表格，显示 2 的平方根，精度从 0 到 9 变化。

```cpp
// Fig. 15.9: Fig15_09.cpp
// Controlling precision of floating-point values.
#include <iostream>
using std::cout;
using std::endl;
using std::fixed;

#include <iomanip>
using std::setprecision;

#include <cmath>
using std::sqrt; // sqrt prototype

int main()
{
    double root2 = sqrt( 2.0 ); // calculate square root of 2
    int places; // precision, vary from 0-9

    cout << "Square root of 2 with precisions 0-9:" << endl
         << "Precision set by ios_base member function "
         << "precision:" << endl;

    cout << fixed; // use fixed-point notation

    // display square root using ios_base function precision
    for ( places = 0; places <= 9; places++ )
    {
        cout.precision( places );
        cout << root2 << endl;
    }
} // end for
```

**Fig. 15.9** | Precision of floating-point values. (Part 1 of 2.)

```
32  cout << "\nPrecision set by stream manipulator "
33      << "setprecision:" << endl;
34
35  // set precision for each digit, then display square root
36  for ( places = 0; places <= 9; places++ )
37      cout << setprecision( places ) << root2 << endl;
38
39  return 0;
40 } // end main
```

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

Fig. 15.9 | Precision of floating-point values. (Part 2 of 2.)

## 15.6.3 Field Width (width, setw)

`width` 成员函数（基类 `ios_base` 的）设置字段宽度（即值应输出的字符位置数或应输入的最大字符数）并返回之前的宽度。如果输出的值比字段宽度窄，则会插入填充字符作为填充。比指定宽度更宽的值不会被截断——完整数字将被打印。无参数的 `width` 函数返回当前设置。

### Common Programming Error 15.1

> `width` 设置仅适用于下一次插入或提取（即 `width` 设置不是“粘性”的）；之后，宽度会隐式设置为 0（即输入和输出将以默认设置执行）。假设 `width` 设置适用于所有后续输出是一个逻辑错误。

### Common Programming Error 15.2

> 当字段不足以处理输出时，输出会打印得尽可能宽，这可能导致令人困惑的输出。

图 15.10 演示了 `width` 成员函数在输入和输出上的使用。请注意，在向 `char` 数组输入时，最多会读取比宽度少一个字符，因为为在输入字符串中放置空字符而预留了空间。记住流提取会在遇到非前导空白时终止。`setw` 流操纵符也可以用来设置字段宽度。

```cpp
// Fig. 15.10: Fig15_10.cpp
// Demonstrating member function width.
#include <iostream>
using std::cin;
using std::cout;
using std::endl;

int main()
{
    int widthValue = 4;
    char sentence[ 10 ];

    cout << "Enter a sentence:" << endl;
    cin.width( 5 ); // input only 5 characters from sentence

    // set field width, then display characters based on that width
    while ( cin >> sentence )
    {
        cout.width( widthValue++ );
        cout << sentence << endl;
        cin.width( 5 ); // input 5 more characters from sentence
    } // end while

    return 0;
} // end main
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
      widt
        h
        memb
          er
          func
          tion
```

Fig. 15.10 | width member function of class ios_base.

> [Note: When prompted for input in Fig. 15.10, the user should enter a line of text and press Enter followed by end-of-file (<Ctrl>-z on Microsoft Windows systems, <Ctrl>-d on UNIX and Macintosh systems).]

## 15.6.4 User-Defined Output Stream Manipulators

你可以创建自己的流操纵符。³ 图 15.11 显示了创建和使用新的非参数化流操纵符 `bell`（第 10–13 行）、`carriageReturn`（第 16–19 行）、`tab`（第 22–25 行）和 `endLine`（第 29–32 行）。对于输出流操纵符，返回类型和参数必须是 `ostream&` 类型。当第 37 行在输出流中插入 `endLine` 操纵符时，函数 `endLine` 被调用，第 31 行将转义序列 `\n` 和 `flush` 操纵符输出到标准输出流 `cout`。同样，当第 37–46 行在输出流中插入操纵符 `tab`、`bell` 和 `carriageReturn` 时，其对应的函数——`tab`（第 22 行）、`bell`（第 10 行）和 `carriageReturn`（第 16 行）被调用，进而输出各种转义序列。

```cpp
// Fig. 15.11: Fig15_11.cpp
// Creating and testing user-defined, nonparameterized
// stream manipulators.
#include <iostream>
using std::cout;
using std::flush;
using std::ostream;

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

// endLine manipulator (using escape sequence \n and member
// function flush)
ostream& endLine( ostream& output )
{
    return output << '\n' << flush; // issue endl-like end of line
} // end endLine manipulator
```

Fig. 15.11 | User-defined, nonparameterized stream manipulators. (Part 1 of 2.)

3. 你也可以创建自己的参数化流操纵符。本书的范围不包括这一概念。

```cpp
34  int main()

35  {

36      // use tab and endLine manipulators

37      cout << "Testing the tab manipulator:" << endLine

38           << 'a' << tab << 'b' << tab << 'c' << endLine;

39

40      cout << "Testing the carriageReturn and bell manipulators:"

41           << endLine << "-------";

42

43      cout << bell; // use bell manipulator

44

45      // use carriageReturn and endLine manipulators

46      cout << carriageReturn << "-----" << endLine;

47      return 0;

48  } // end main
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_657_0.png)

## 15.7 Stream Format States and Stream Manipulators

可以使用各种流操纵符来指定流 I/O 操作期间执行的格式化种类。流操纵符控制输出的格式设置。图 15.12 列出了控制给定流格式状态的每个流操纵符。所有这些操纵符都属于类 `ios_base`。我们在接下来的几节中展示了其中大多数流操纵符的示例。

| Stream manipulator | Description |
|---|---|
| `skipws` | Skip whitespace characters on an input stream. This setting is reset with stream manipulator `noskipws`. |
| `left` | Left justify output in a field. Padding characters appear to the right if necessary. |
| `right` | Right justify output in a field. Padding characters appear to the left if necessary. |
| `internal` | Indicate that a number’s sign should be left justified in a field and a number’s magnitude should be right justified in that same field (i.e., padding characters appear between the sign and the number). |
| `dec` | Specify that integers should be treated as decimal (base 10) values. |
| 流操纵符 | 描述 |
|---|---|
| `oct` | 指定整数应以八进制（基数为 8）值处理。 |
| `hex` | 指定整数应以十六进制（基数为 16）值处理。 |
| `showbase` | 指定在数字前面输出数字的基数（八进制数前导 0；十六进制数前导 0x 或 0X）。此设置可通过流操纵符 `noshowbase` 重置。 |
| `showpoint` | 指定浮点数输出时应带小数点。通常与 `fixed` 一起使用，以确保小数点右侧有特定数量的数字，即使它们是零。此设置可通过流操纵符 `noshowpoint` 重置。 |
| `uppercase` | 指定十六进制整数应使用大写字母（即 X 和 A 到 F），并且以科学计数法表示浮点数时，应使用大写 E。此设置可通过流操纵符 `nouppercase` 重置。 |
| `showpos` | 指定正数前应带有加号 (+)。此设置可通过流操纵符 `noshowpos` 重置。 |
| `scientific` | 指定以科学计数法输出浮点数值。 |
| `fixed` | 指定以定点表示法输出浮点数值，小数点右侧有特定数量的数字。 |
