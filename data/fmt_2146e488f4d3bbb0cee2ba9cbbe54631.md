
`for(int n=1; n<=5; n++) {`

`cout.width(8);`

`cout << n;`

`cout.width(13);`

`cout << sqrt(n) << "\n";`

`}`

`cout << "\nPrecision set to 5 digits \n";`

`cout.precision(5); // precision parameter changed`

`cout << " " << sqrt(10) << " " << sqrt(10) << "\n";`

`cout.precision(0); // precision set to default`

`cout << " " << sqrt(10) << " " << sqrt(10) << " " (default setting)\n";`

`return 0;`

`}`

```
Program 10.5 的输出将为：
Precision set to 3 digits

| VALUE | SQRT_OF_VALUE |
| 1 | 1 |
| 2 | 1.41 |
| 3 | 1.73 |
| 4 | 2 |
| 5 | 2.24 |

Precision set to 5 digits
sqrt(10) = 3.1623
sqrt(10) = 3.162278 (default setting)
```

- 从输出中观察到以下几点：
1. 输出四舍五入到最接近的百分位（即，对于两位精度，1.6666 将为 1.67，但 1.3333 将为 1.33）。
2. 尾随零被截断。
3. 精度设置在被重置之前一直有效。
4. 默认精度为 6 位。

### Program 10.6 Width and Precision Manipulators

```
#include <iostream>

using namespace std;

int main()

{

    float pi=22.0/7.0;

    int i;

    cout<<"Value of PI:\n";

    for(i=1;i<=10;i++)

{

        cout.width(i+1);

        cout.precision(i);

    }

    cout<<pi<<"\n";

    return 0;

}
```

Program 10.6 的输出将为：

Value of PI:
3.1
3.14
3.143
3.1428
3.14286
3.142857
3.1428571
3.14285707
3.142857074

## Filling and Padding: `fill()`

我们使用比值所需更大的字段宽度来打印值。默认情况下，字段的未使用位置用空格填充。然而，我们可以使用 `fill()` 函数用任意所需字符填充未使用位置。它以以下形式使用：

```
cout.fill(ch);
```

其中 `ch` 表示用于填充未使用位置的字符。示例：

```
cout.fill('*');
cout.width(10);
cout << 5250 << "\n";
```

输出将为：

| * | * | * | * | * | 5 | 2 | 5 | 0 |

金融机构和银行在打印支票时使用这种填充方式，以便任何人无法轻易更改金额。像 `precision()` 一样，`fill()` 在我们更改它之前一直有效。请参阅 Program 10.7 及其输出。

### Program 10.7 Padding with `fill()`

```
#include <iostream>

using namespace std;

int main() {

    cout.fill('<');

    cout.precision(3);

    for(int n=1; n<=6; n++) {

        cout.width(5);

        cout << n;

        cout.width(10);

        cout << 1.0 / float(n) << "\n";

        if (n == 3)

            cout.fill('>');

    }

    cout << "\nPadding changed \n\n";

    cout.fill('#'); // fill() reset

    cout.width(15);

    cout << 12.345678 << "\n";

    return 0;

}
```

Program 10.7 的输出将为：

```
<<<<<<<<<<1

<<<<<<<<<<<0.5

<<<<<<<<<<<0.333

>>>>>>>>>>0.25

>>>>>>>>>0.2

>>>>>>>>>>0.167

Padding changed

#######12.346
```

## Formatting Flags, Bit-fields and `setf()`

我们已经看到，当使用 `width()` 函数时，值（无论是文本还是数字）都会在字段宽度内右对齐打印。但，通常的做法是打印左对齐的文本。我们如何使值左对齐？或者，我们如何使浮点数以科学记数法打印？

`setf()`，`ios` 类的成员函数，可以提供这些以及许多其他格式问题的答案。
`setf()` 代表 flags function 可以按如下方式使用：

```
cout.setf(arg1,arg2);
```

`arg1` 是在 `ios` 类中定义格式标志之一。格式标志指定输出所需的格式。另一个 `ios` 常量 `arg2`，称为位字段，指定格式所属的组。
Table 10.4 显示了位字段、标志及其格式操作。有位字段，每个位字段有一组互斥的标志。示例：

```
cout.setf(ios::left, ios::adjustfield);
cout.setf(ios::scientific, ios::floatfield);
```

| Format required | Flag (arg1) | Bit-field (arg2) |
| --- | --- | --- |
| Left-justified output | `ios::left` | `ios::adjustfield` |
| Right-justified output | `ios::right` | `ios::adjustfield` |
| Padding after sign or base | `ios::internal` | `ios::adjustfield` |
| Indicator (like ##20) | | |
| Scientific notation | `ios::scientific` | `ios::floatfield` |
| Fixed point notation | `ios::fixed` | `ios::floatfield` |
| Decimal base | `ios::dec` | `ios::basefield` |
| Octal base | `ios::oct` | `ios::basefield` |
| Hexadecimal base | `ios::hex` | `ios::basefield` |

请注意，第一个参数应为第二个参数的成员组。

考虑以下代码段：

```
cout.fill('*');
cout.setf(ios::left, ios::adjustfield);
cout.width(15);
cout << "TABLE 1" << "\n";
```

这将产生以下输出：

| T | A | B | L | E | | | * | * | * | * | * |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

语句

```
cout.fill('*');
cout.precision(3);
cout.setf(ios::internal, ios::adjustfield);
cout.setf(ios::scientific, ios::floatfield);
cout.width(15);
cout << -12.34567 << "\n";
```

将产生以下输出：************

注意 符号左对齐，值右左对齐。它们之间的空格用星号填充。值以科学记数法打印，精确到三位小数。

### Program 10.8 Manipulation of Flag and Bit Fields

```
#include <iostream>

using namespace std;

int main() {

    int num;

    cout<<"Enter an integer value: ";

    cin>>num;

    cout<<"The hexadecimal, octal and decimal representation of "

<<num<<" is: " << "";

    cout.setf(ios::hex, ios::basefield);

    cout<<num<<", " << "";

    cout.setf(ios::oct, ios::basefield);

    cout<<num<<" and " << "";

    cout.setf(ios::dec, ios::basefield);

    cout<<num<<" respectively";

    return 0;

}
```

Program 10.8 的输出将为：
Enter an integer value: 92
The hexadecimal, octal and decimal representation of 92 is: 5c, 134 and 92 respectively

## Displaying Trailing Zeros and Plus Sign

如果我们使用宽度为 8 的字段打印数字 10.75、25.00 和 15.50，使用两位精度，则输出将如下所示：

| | 1 | 0 | - | 7 | 5 |
| | | | | | |
| | | | | 2 | 5 |
| | | | 1 | 5 | 5 |

请注意，第二项和第三项中的尾随零已被截断。

## 使用 C++ 进行面向对象编程

某些情况，例如商品价格列表或员工薪资报表，需要显示零。上述输出如果按如下方式打印会更好：

```
10.75

25.00

15.50
```

`setf()` 可以与标志 `ios::showpoint` 作为单个参数一起使用来实现这种形式的输出。例如，

```
cout.setf(ios::showpoint); // display trailing zeros
```

会使 `cout` 显示尾随零和尾随小数点。默认情况下，值 3.25 将显示为 3.250000。请记住，默认假设精度为六位数字。

同样，可以使用以下语句在正数前打印加号：

```
cout.setf(ios::showpos); // show +sign
```

对于示例，

```
cout.setf(ios::showpoint);
cout.setf(ios::showpos);
cout.precision(3);
cout.setf(ios::fixed, ios::floatfield);
cout.setf(ios::internal, ios::adjustfield);
cout.width(10);
cout << 275.5 << "\n";
```

将产生以下输出：

| + | 2 | 7 | 5 . | 5 | 0 | 0 |

诸如 `showpoint` 和 `showpos` 之类的标志没有位字段，因此作为参数用于 `setf()`。这是可能的，因为 `setf()` 已在类 `ios` 中声明为重载函数。表 10.5 列出了不具有命名位的标志。这些标志不是相互排斥的，因此可以独立设置或清除。

### 表 10.5 没有位字段的标志

| Flag | Meaning |
| `ios::showbase` | Use base indicator on output |
| `ios::showpos` | Print + before positive numbers |
| `ios::showpoint` | Show trailing decimal point and zeroes |
| `ios::uppercase` | Use uppercase letters for hex output |
| `ios::skipws` | Skip white space on input |
| `ios::unitbuf` | Flush all streams after insertion |
| `ios::stdio` | Flush stdout and stderr after insertion |

程序 10.9 演示了使用重载的 `setf()` 函数设置各种格式标志。

### 程序 10.9 使用 setf(i) 中的标志进行格式化

```
#include <iostream>
#include <cmath>

using namespace std;

int main()

{

    cout.fill('*');

    cout.setf(ios::left, ios::adjustfield);

    cout.width(10);

    cout << "VALUE";

    cout.setf(ios::right, ios::adjustfield);

    cout.width(15);

    cout << "SQRT OF VALUE" << "\n";

    cout.fill('.');

    cout.precision(4);

    cout.setf(ios::showpoint);

    cout.setf(ios::showpos, ios::floatfield);

    for (int n=1; n<=10; n++)

    {

        cout.setf(ios::internal, ios::adjustfield);

        cout.width(5);

        cout << n << "";

        cout.setf(ios::right, ios::adjustfield);

        cout.width(20);

        cout << sqrt(n) << "\n";

    }

    // floatfield changed

    cout.setf(ios::scientific, ios::floatfield);

    cout << "\nSQRT(100) = " << sqrt(100) << ".\n";

    return 0;

}
```

程序 10.9 的输出为：

VALUE*******SQRT OF VALUE
+1.......1.0000
+2.......+1.4142
+3.......+1.7321
+4.......+2.0000
+5.......+2.2361

![](img/20ee75c0321e4c9269cadbf08d7acd34_324_0.png)

```
...+6..............+2.4495

...7..............+2.5458

...8..............+2.8284

...+9..............+3.0000

...10.............+3.1621
```

```
SQRT(100) = +1.00000e+01
```

- Note
1. The flags set by set() remain effective until they are reset or unset.
2. A format flag can be reset any number of times in a program.
3. We can apply more than one format controls jointly on an output value.
4. The setf() sets the specified flags and leaves others unchanged.

### 10.6 使用操纵符管理输出

头文件 `iomanip` 提供了一组称为操纵符的函数，可用于操纵输出格式。它们提供了与 `ios` 成员函数相同的功能。一些操纵符比类 `ios` 中的对应项更方便。例如，可以将两个或多个操纵符作为链在一条语句中使用，如下所示：

```
cout << mani1 << mani2 << mani3 << item;
cout << mani1 << item1 << mani2 << item2;
```
