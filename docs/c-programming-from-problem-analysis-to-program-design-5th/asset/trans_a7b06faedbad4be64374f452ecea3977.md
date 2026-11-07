

## 头文件 `cctype` (`ctype.h`)

下表显示了头文件 `cctype` (`ctype.h`) 中的各种函数。

| 函数名称和参数 | 参数类型 | 函数返回值 |
|---|---|---|
| `isalnum(ch)` | ch 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 ch 是字母或数字字符，即（`'A'–'Z'`、`'a'–'z'`、`'0'–'9'`），则返回一个非零值（`true`）<br>• 否则为 0（`false`） |
| `iscntrl(ch)` | ch 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 ch 是一个控制字符（在 ASCII 中，字符值为 0–31 或 127），则返回一个非零值（`true`）<br>• 否则为 0（`false`） |
| `isdigit(ch)` | ch 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 ch 是一个数字（`'0'–'9'`），则返回一个非零值（`true`）<br>• 否则为 0（`false`） |
| `islower(ch)` | ch 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 ch 是小写字母（`'a'–'z'`），则返回一个非零值（`true`）<br>• 否则为 0（`false`） |
| `isprint(ch)` | ch 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 ch 是一个可打印字符，包括空格（在 ASCII 中，从 `' '` 到 `'~'`），则返回一个非零值（`true`）<br>• 否则为 0（`false`） |
| `ispunct(ch)` | ch 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 ch 是一个标点字符，则返回一个非零值（`true`）<br>• 否则为 0（`false`） |
| `isspace(ch)` | ch 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 ch 是一个空白字符（空格、换行、制表、回车、换页），则返回一个非零值（`true`）<br>• 否则为 0（`false`） |
| `isupper(ch)` | `ch` 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 `ch` 是一个大写字母（`'A'–'Z'`），则返回一个非零值（`true`）<br>• 否则为 `0`（`false`） |
| `tolower(ch)` | `ch` 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 `ch` 是一个大写字母，则返回 `ch` 对应的小写字母的 ASCII 值<br>• 否则返回 `ch` 的 ASCII 值 |
| `toupper(ch)` | `ch` 是一个 `char` 值 | 函数返回一个 `int` 值，如下：<br>• 如果 `ch` 是一个小写字母，则返回 `ch` 对应的大写字母的 ASCII 值<br>• 否则返回 `ch` 的 ASCII 值 |

## 头文件 `cfloat` (`float.h`)

在第2章中，我们列出了浮点数据类型的最大值和最小值。我们还提到过，这些值是系统相关的。这些最大值和最小值存储在命名常量中。头文件 cfloat 包含许多这样的命名常量。下表列出了其中一些常量。

| 命名常量 | 描述 |
|---|---|
| `FLT_DIG` | `float` 值中有效数字的近似位数 |
| `FLT_MAX` | 最大正 `float` 值 |
| `FLT_MIN` | 最小正 `float` 值 |
| `DBL_DIG` | `double` 值中有效数字的近似位数 |
| `DBL_MAX` | 最大正 `double` 值 |
| `DBL_MIN` | 最小正 `double` 值 |
| `LDBL_DIG` | `long double` 值中有效数字的近似位数 |
| `LDBL_MAX` | 最大正 `long double` 值 |
| `LDBL_MIN` | 最小正 `long double` 值 |

一个类似于下面的程序可以打印出这些命名常量在你的系统上的值。

```cpp
#include <iostream>
#include <cfloat>

using namespace std;

int main()
{
    cout << "Approximate number of significant digits "
         << "in a float value " << FLT_DIG << endl;
    cout << "Maximum positive float value " << FLT_MAX
         << endl;
    cout << "Minimum positive float value " << FLT_MIN
         << endl;
    cout << "Approximate number of significant digits "
         << "in a double value " << DBL_DIG << endl;
    cout << "Maximum positive double value " << DBL_MAX
         << endl;
    cout << "Minimum positive double value " << DBL_MIN
         << endl;
    cout << "Approximate number of significant digits "
         << "in a long double value " << LDBL_DIG << endl;
    cout << "Maximum positive long double value " << LDBL_MAX
         << endl;
    cout << "Minimum positive long double value " << LDBL_MIN
         << endl;

    return 0;
}
```

## 头文件 `climits` (`limits.h`)

在第2章中，我们列出了整数数据类型的最大值和最小值。我们还提到过，这些值是系统相关的。这些最大值和最小值存储在命名常量中。头文件 `climits` 包含许多这样的命名常量。下表列出了其中一些常量。

| 命名常量 | 描述 |
|---|---|
| `CHAR_BIT` | 一个字节中的位数 |
| `CHAR_MAX` | char 最大值 |
| `CHAR_MIN` | char 最小值 |
| `SHRT_MAX` | short 最大值 |
| `SHRT_MIN` | short 最小值 |
| `INT_MAX` | `int` 最大值 |
| `INT_MIN` | `int` 最小值 |
| `LONG_MAX` | `long` 最大值 |
| `LONG_MIN` | `long` 最小值 |
| `UCHAR_MAX` | `unsigned char` 最大值 |
| `USHRT_MAX` | `unsigned short` 最大值 |
| `UINT_MAX` | `unsigned int` 最大值 |
| `ULONG_MAX` | `unsigned long` 最大值 |

一个类似于下面的程序可以打印出这些命名常量在你的系统上的值。

```cpp
#include <iostream>
#include <climits>

using namespace std;

int main()
{
    cout << "Number of bits in a byte " << CHAR_BIT << endl;
    cout << "Maximum char value " << CHAR_MAX << endl;
    cout << "Minimum char value " << CHAR_MIN << endl;
    cout << "Maximum short value " << SHRT_MAX << endl;
    cout << "Minimum short value " << SHRT_MIN << endl;
    cout << "Maximum int value " << INT_MAX << endl;
    cout << "Minimum int value " << INT_MIN << endl;
    cout << "Maximum long value " << LONG_MAX << endl;
    cout << "Minimum long value " << LONG_MIN << endl;
    cout << "Maximum unsigned char value " << UCHAR_MAX
         << endl;
    cout << "Maximum unsigned short value " << USHRT_MAX
         << endl;
    cout << "Maximum unsigned int value " << UINT_MAX << endl;
    cout << "Maximum unsigned long value " << ULONG_MAX
         << endl;

    return 0;
}
```

| 函数名称和参数 | 参数类型 | 函数返回值 |
|---|---|---|
| `sqrt(x)` | x 是一个浮点表达式，其中 x ≥ 0.0 | x 的平方根 |
| `tan(x)` | x 是一个浮点表达式；x 以弧度为单位 | 角度的三角正切 |
| `tanh(x)` | x 是一个浮点表达式 | x 的双曲正切 |

## 头文件 `cstddef` (`stddef.h`)

此外，该头文件包含以下符号常量的定义：

`NULL`：系统相关的空指针（通常为 0）

## 头文件 `cstring` (`string.h`)

下表显示了各种字符串函数。

| 函数名称和参数 | 参数类型 | 函数返回值 |
|---|---|---|
| `strcat(destStr, srcStr)` | destStr 和 srcStr 是以空字符结尾的 char 数组；destStr 必须足够大以容纳结果 | 返回 destStr 的基地址；srcStr（包括空字符）被连接到 destStr 的末尾 |
| `strcmp(str1, str2)` | str1 和 str2 是以空字符结尾的 char 数组 | 返回值如下：<br>- 如果 `str1 < str2`，则返回一个小于 0 的 int 值<br>- 如果 `str1 = str2`，则返回一个等于 0 的 int 值<br>- 如果 `str1 > str2`，则返回一个大于 0 的 int 值 |
| `strcpy(destStr, srcStr)` | `destStr` 和 `srcStr` 是以空字符结尾的 `char` 数组 | 返回 `destStr` 的基地址；`srcStr` 被复制到 `destStr` 中 |
| `strlen(str)` | `str` 是以空字符结尾的 `char` 数组 | 返回一个 ≥ 0 的整数值，指定 `str` 的长度（不包括 `\0`） |

## 头文件 `string`

这个头文件——不要与头文件 `cstring` 混淆——提供了一个名为 `string` 的程序员自定义数据类型。与 string 类型相关的有数据类型 `string::size_type` 和命名常量 `string::npos`。它们的定义如下：

|  |  |
|---|---|
| `string::size_type` | 无符号整数类型 |
| `string::npos` | `string::size_type` 类型的最大值 |

`string` 类型包含几个用于字符串操作的函数。除了表 8-1 中列出的字符串函数外，下表描述了其他字符串函数。在此表中，我们假设 `strVar` 是一个 string 变量，而 `str` 是一个 string 变量、string 常量或字符数组。

| 表达式 | 作用 |
|---|---|
| `getline(istreamVar, strVar);` | `istreamVar` 是一个输入流变量（类型为 `istream` 或 `ifstream`）。从 `istreamVar` 读取直到换行符为止的字符，并存储到 `strVar` 中。（换行符被读取但不存储到 `strVar`。）此函数的返回值通常被忽略。 |
| `strVar.append(str, n)` | 字符数组 `str` 的前 n 个字符被追加到 `strVar`。 |
| `strVar.c_str()` | 与 `strVar` 中字符对应的以空字符结尾的 C 字符串的基地址。 |

