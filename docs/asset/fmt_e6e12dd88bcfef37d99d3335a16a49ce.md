
```
    // display x and y in default format

    cout << "Displayed in default format:" << endl

         << x << '\t' << y << endl;

    // display x and y in scientific format

    cout << "\nDisplayed in scientific format:" << endl

         << scientific << x << '\t' << y << endl;

    // display x and y in fixed format

    cout << "\nDisplayed in fixed format:" << endl

         << fixed << x << '\t' << y << endl;

    return 0;

} // end main
```

```
Displayed in default format:
0.00123457      1.946e+009

Displayed in scientific format:
1.234567e-003   1.946000e+009

Displayed in fixed format:
0.001235        1946000000.000000
```

Fig. 15.18 | Floating-point values displayed in default, scientific and fixed formats.

```
// Fig. 15.19: Fig15_19.cpp
// Stream manipulator uppercase.
#include <iostream>
using std::cout;
using std::endl;
using std::hex;
using std::showbase;
using std::uppercase;
```

Fig. 15.19 | Stream manipulator uppercase. (Part 1 of 2.)

```
int main()
{
    cout << "Printing uppercase letters in scientific" << endl
        << "notation exponents and hexadecimal values:" << endl;

    // use std::uppercase to display uppercase letters; use std::hex and
    // std::showbase to display hexadecimal value and its base
    cout << uppercase << 4.345e10 << endl
        << hex << showbase << 123456789 << endl;
    return 0;
} // end main
```

```
Printing uppercase letters in scientific

notation exponents and hexadecimal values:

4.345E+010
0X75BCD15
```

Fig. 15.19 | Stream manipulator uppercase. (Part 2 of 2.)

## 15.7.7 Specifying Boolean Format (`boolalpha`)

C++ provides data type `bool`, whose values may be `false` or `true`, as a preferred alternative to the old style of using `0` to indicate `false` and nonzero to indicate `true`. A `bool` variable outputs as `0` or `1` by default. However, we can use stream manipulator `boolalpha` to set the output stream to display `bool` values as the strings `"true"` and `"false"`. Use stream manipulator `noboolalpha` to set the output stream to display `bool` values as integers (i.e., the default setting). The program of Fig. 15.20 demonstrates these stream manipulators. Line 14 displays the `bool` value, which line 11 sets to `true`, as an integer. Line 18 uses manipulator `boolalpha` to display the `bool` value as a string. Lines 21–22 then change the `bool`’s value and use manipulator `noboolalpha`, so line 25 can display the `bool` value as an integer. Line 29 uses manipulator `boolalpha` to display the `bool` value as a string. Both `boolalpha` and `noboolalpha` are “sticky” settings.

### Good Programming Practice 15.1

> Displaying `bool` values as `true` or `false`, rather than nonzero or `0`, respectively, makes program outputs clearer.

```
// Fig. 15.20: Fig15_20.cpp
// Demonstrating stream manipulators boolalpha and noboolalpha.
#include <iostream>

using std::boolalpha;
using std::cout;
using std::endl;
using std::noboolalpha;

int main()
{
    bool booleanValue = true;
```

Fig. 15.20 | Stream manipulators `boolalpha` and `noboolalpha`. (Part 1 of 2.)

```
    // display default true booleanValue
    cout << "booleanValue is " << booleanValue << endl;

    // display booleanValue after using boolalpha
    cout << "booleanValue (after using boolalpha) is "
        << boolalpha << booleanValue << endl << endl;

    cout << "switch booleanValue and use noboolalpha" << endl;
    booleanValue = false; // change booleanValue
    cout << noboolalpha << endl; // use noboolalpha

    // display default false booleanValue after using noboolalpha
    cout << "booleanValue is " << booleanValue << endl;

    // display booleanValue after using boolalpha again
    cout << "booleanValue (after using boolalpha) is "
        << boolalpha << booleanValue << endl;
    return 0;
} // end main
```

```
booleanValue is 1

booleanValue (after using boolalpha) is true

switch booleanValue and use noboolalpha

booleanValue is 0

booleanValue (after using boolalpha) is false
```

Fig. 15.20 | Stream manipulators `boolalpha` and `noboolalpha`. (Part 2 of 2.)

## 15.7.8 Setting and Resetting the Format State via Member Function `flags`

Throughout Section 15.7, we have been using stream manipulators to change output format characteristics. We now discuss how to return an output stream’s format to its default state after having applied several manipulations. Member function `flags()` without an argument returns the current format settings as a `fmtflags` data type (of class `ios_base`), which represents the format state. Member function `flags(fmtflags)` sets the format state as specified by the argument and returns the prior state settings. The initial settings of the value that `flags()` returns might differ across several systems. The program of Fig. 15.21 uses member function `flags()` to save the stream’s original format state (line 22), then restore the original format settings (line 30).

```
// Fig. 15.21: Fig15_21.cpp
// Demonstrating the flags member function.
#include <iostream>

using std::cout;
using std::endl;
using std::ios_base;
```

Fig. 15.21 | `flags` member function. (Part 1 of 2.)

```
using std::oct;
using std::scientific;
using std::showbase;

int main()
{
    int integerValue = 1000;
    double doubleValue = 0.0947628;

    // display flags value, int and double values (original format)
    cout << "The value of the flags variable is: " << cout.flags()
        << "\nPrint int and double in original format:\n"
        << integerValue << '\t' << doubleValue << endl << endl;

    // use cout flags function to save original format
    ios_base::fmtflags originalFormat = cout.flags();

    cout << showbase << oct << scientific; // change format

    // display flags value, int and double values (new format)
    cout << "The value of the flags variable is: " << cout.flags()
        << "\nPrint int and double in a new format:\n"
        << integerValue << '\t' << doubleValue << endl << endl;

    cout.flags( originalFormat ); // restore format

    // display flags value, int and double values (original format)
    cout << "The restored value of the flags variable is: "
        << cout.flags()
        << "\nPrint values in original format again:\n"
        << integerValue << '\t' << doubleValue << endl;

    return 0;
} // end main
```

```
The value of the flags variable is: 513
Print int and double in original format:
1000    0.0947628

The value of the flags variable is: 012011
Print int and double in a new format:
01750   9.476280e-002

The restored value of the flags variable is: 513
Print values in original format again:
1000    0.0947628
```

Fig. 15.21 | `flags` member function. (Part 2 of 2.)

## 15.8 Stream Error States

The state of a stream may be tested through bits in class `ios_base`. In a moment, we show how to test these bits, in the example of Fig. 15.22.

The `eofbit` is set for an input stream after end-of-file is encountered. A program can use member function `eof()` to determine whether end-of-file has been encountered on a stream after an attempt to extract data beyond the end of the stream. The call

```
发生错误的输入操作之前：
cin.rdstate()：0
    cin.eof()：0
    cin.fail()：0
    cin.bad()：0
    cin.good()：1

需要输入一个整数，但输入一个字符：A

发生错误的输入操作之后：
cin.rdstate()：2
    cin.eof()：0
    cin.fail()：1
    cin.bad()：0
    cin.good()：0

执行 cin.clear() 之后
cin.fail()：0
cin.good()：1
```

**图 15.22** | 测试错误状态。（共 2 部分，第 2 部分。）

如果流没有设置 `eofbit`、`failbit` 或 `badbit` 中的任何一个位，则该流会设置 `goodbit`。

`good()` 成员函数在 `bad()`、`fail()` 和 `eof()` 函数都将返回 `false` 时返回 `true`。I/O 操作只能对“良好”流执行。

`rdstate()` 成员函数返回流的错误状态。例如，调用 `cout.rdstate()` 会返回流的状态；随后可以使用 `switch` 语句检查该状态，判断其中是否设置了 `eofbit`、`badbit`、`failbit` 和 `goodbit`。测试流状态的首选方式是使用成员函数 `eof()`、`bad()`、`fail()` 和 `good()`——使用这些函数不要求必须熟悉具体的状态位。

`clear()` 成员函数用于将流的状态恢复为“良好”，以便能够继续对该流执行 I/O 操作。`clear()` 的默认参数是 `goodbit`，因此以下语句

```
cin.clear();
```

会清除 `cin` 的状态，并为该流设置 `goodbit`。以下语句

```
cin.clear( ios::failbit )
```
