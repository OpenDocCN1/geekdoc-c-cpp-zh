
| 原型 | 描述 |
|---|---|
| `unsigned long strtoul( const char *nPtr, char **endPtr, int base )` | 将字符串 nPtr 转换为 unsigned long。endPtr 是指向 unsigned long 之后字符串剩余部分的指针的地址。如果字符串无法转换，则返回 0。base 参数指示要转换的数字的进制（例如，8 表示八进制，10 表示十进制，16 表示十六进制）。默认为十进制。 |

图19.21 | 通用实用程序库中基于指针的字符串转换函数。（第2部分，共2部分。）

函数 atof（图19.22，第12行）将其参数——表示浮点数的字符串——转换为 double 值。该函数返回 double 值。如果字符串无法转换——例如，如果字符串的第一个字符不是数字——函数 atof 返回零。

```
// Fig. 19.22: fig19_21.cpp
// Using atof.
#include <iostream>
using std::cout;
using std::endl;

#include <cstdlib> // atof prototype
using std::atof;

int main()
{
    double d = atof( "99.0" ); // convert string to double

    cout << "The string \"99.0\" converted to double is " << d
        << "\nThe converted value divided by 2 is " << d / 2.0 << endl;
    return 0;
} // end main
```

The string "99.0" converted to double is 99
The converted value divided by 2 is 49.5

图19.22 | 字符串转换函数 atof。

函数 atoi（图19.23，第12行）将其参数——表示整数的数字字符串——转换为 int 值。该函数返回 int 值。如果字符串无法转换，函数 atoi 返回零。

```
// Fig. 19.23: Fig19_23.cpp
// Using atoi.
#include <iostream>
using std::cout;
using std::endl;

#include <cstdlib> // atoi prototype
using std::atoi;

int main()
{
    int i = atoi( "2593" ); // convert string to int

    cout << "The string \"2593\" converted to int is " << i
        << "\nThe converted value minus 593 is " << i - 593 << endl;
    return 0;
} // end main
```

The string "2593" converted to int is 2593
The converted value minus 593 is 2000

图19.23 | 字符串转换函数 atoi。

函数 atol（图19.24，第12行）将其参数——表示长整数的数字字符串——转换为 long 值。该函数返回 long 值。如果字符串无法转换，函数 atol 返回零。如果 int 和 long 都存储为四个字节，则函数 atoi 和函数 atol 的工作方式完全相同。

```
// Fig. 19.24: fig19_24.cpp
// Using atol.
#include <iostream>
using std::cout;
using std::endl;

#include <cstdlib> // atol prototype
using std::atol;

int main()
{
    long x = atol( "1000000" ); // convert string to long

    cout << "The string \"1000000\" converted to long is " << x
        << "\nThe converted value divided by 2 is " << x / 2 << endl;
    return 0;
} // end main
```

The string "1000000" converted to long int is 1000000
The converted value divided by 2 is 500000

图19.24 | 字符串转换函数 atol。

函数 strtod（图19.25）将表示浮点值的字符序列转换为 double。函数 strtod 接收两个参数——一个字符串（char *）和一个 char * 指针的地址（即 char **）。该字符串包含要转换为 double 的字符序列。第二个参数使 strtod 能够修改调用函数中的 char * 指针，使该指针指向字符串中已转换部分之后的第一个字符的位置。第16行表示，d 被赋值为从字符串转换的 double 值，而 stringPtr 被赋值为字符串中转换值（51.2）之后的第一个字符的位置。

```
// Fig. 19.25: fig19_25.cpp
// Using strtod.
#include <iostream>
using std::cout;
using std::endl;

#include <cstdlib> // strtod prototype
using std::strtod;

int main()
{
    double d;
    const char *string1 = "51.2% are admitted";
    char *stringPtr;

    d = strtod( string1, &stringPtr ); // convert characters to double

    cout << "The string \"" << string1
        << "\" is converted to the\ndouble value " << d
        << " and the string \"" << stringPtr << "\"" << endl;
    return 0;
} // end main
```

The string "51.2% are admitted" is converted to the double value 51.2 and the string "% are admitted"

图19.25 | 字符串转换函数 strtod。

函数 strtol（图19.26）将表示整数的字符序列转换为 long。该函数接收三个参数——一个字符串（char *）、一个 char * 指针的地址和一个整数。字符串包含要转换的字符序列。第二个参数被赋值为字符串中已转换部分之后的第一个字符的位置。整数指定要转换的值的进制。第16行表示，x 被赋值为从字符串转换的 long 值，而 remainderPtr 被赋值为 string1 中转换值（-1234567）之后的第一个字符的位置。对第二个参数使用空指针会导致忽略字符串的其余部分。第三个参数 0 表示要转换的值可以是八进制（基数为8）、十进制（基数为10）或十六进制（基数为16）。这由字符串中的起始字符决定——0 表示八进制数，0x 表示十六进制数，1–9 的数字表示十进制数。

在调用函数 strtol 时，基数可以指定为零或 2 到 36 之间的任何值。从基数 11 到基数 36 的整数的数字表示使用字符 A–Z 来表示值 10 到 35。例如，十六进制值可以由数字 0–9 和字符 A–F 组成。基数 11 的整数可以由数字 0–9 和字符 A 组成。基数 24 的整数可以由数字 0–9 和字符 A–N 组成。基数 36 的整数可以由数字 0–9 和字符 A–Z 组成。[注意：所使用的字母的大小写被忽略。]

```
// Fig. 19.26: fig19_26.cpp
// Using strtol.
#include <iostream>
using std::cout;
using std::endl;

#include <cstdlib> // strtol prototype
using std::strtol;

int main()
{
    long x;
    const char *string1 = "-1234567abc";
    char *remainderPtr;

    x = strtol( string1, &remainderPtr, 0 ); // convert characters to long

    cout << "The original string is \"" << string1
        << "\"\nThe converted value is " << x
        << "\nThe remainder of the original string is \"" << remainderPtr
        << "\"\nThe converted value plus 567 is " << x + 567 << endl;
    return 0;
} // end main
```

The original string is "-1234567abc"
The converted value is -1234567
The remainder of the original string is "abc"
The converted value plus 567 is -1234000

图19.26 | 字符串转换函数 strtol。

函数 strtoul（图19.27）将表示 unsigned long 整数的字符序列转换为 unsigned long。该函数的工作方式与 strtol 完全相同。第17行表示，x 被赋值为从字符串转换的 unsigned long 值，而 remainderPtr 被赋值为 string1 中转换值（1234567）之后的第一个字符的位置。第三个参数 0 表示要转换的值可以是八进制、十进制或十六进制格式，具体取决于起始字符。

// Fig. 19.27: fig19_27.cpp
// Using strtoul.
#include <iostream>
using std::cout;
using std::endl;

#include <cstdlib> // strtoul prototype
using std::strtoul;

图19.27 | 字符串转换函数 strtoul。（第1部分，共2部分。）

```
10  int main()
11  {
12      unsigned long x;
13      const char *string1 = "1234567abc";
14      char *remainderPtr;
15
16      // convert a sequence of characters to unsigned long
17      x = strtoul( string1, &remainderPtr, 0 );
18
19      cout << "The original string is \"" << string1
20          << "\"\nThe converted value is " << x
21          << "\nThe remainder of the original string is \"" << remainderPtr
22          << "\"\nThe converted value minus 567 is " << x - 567 << endl;
23      return 0;
24  } // end main
```

The original string is "1234567abc"
The converted value is 1234567
The remainder of the original string is "abc"
The converted value minus 567 is 1234000

图19.27 | 字符串转换函数 strtoul。（第2部分，共2部分。）

## 19.11 基于指针的字符串处理库的搜索函数

本节介绍字符串处理库中用于在字符串中搜索字符和其他字符串的函数。这些函数汇总于图19.28。请注意，函数-

| 原型 | 描述 |
|---|---|
| `char *strchr( const char *s, int c )` | 在字符串 s 中定位字符 c 的首次出现。如果找到 c，则返回指向 s 中 c 的指针。否则，返回空指针。 |
| `char *strrchr( const char *s, int c )` | 从字符串 s 的末尾开始搜索，定位字符串 s 中字符 c 的最后一次出现。如果找到 c，则返回指向字符串 s 中 c 的指针。否则，返回空指针。 |
| `size_t strspn( const char *s1, const char *s2 )` | 确定并返回字符串 s1 中仅由字符串 s2 中包含的字符组成的初始段的长度。 |
| `char *strpbrk( const char *s1, const char *s2 )` | 在字符串 s1 中定位字符串 s2 中任意字符的首次出现。如果找到来自字符串 s2 的字符，则返回指向字符串 s1 中该字符的指针。否则，返回空指针。 |

图19.28 | 基于指针的字符串处理库的搜索函数。（第1部分，共2部分。）
