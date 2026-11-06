
如果第一个字符串小于第二个字符串，则返回负值；如果第一个字符串大于第二个字符串，则返回正值。函数 `strcmp` 等价于 `strncmp`，不同之处在于 `strncmp` 最多比较指定数量的字符。函数 `strncmp` 在其某个字符串参数中遇到空字符后停止比较字符。程序打印每次函数调用返回的整数值。

### 常见编程错误 21.10

![](img/023f159fdd47d944d48e08843cea732d_918_0.png)

> 假定当 `strcmp` 和 `strncmp` 的参数相等时它们返回一（真值），这是一个逻辑错误。两个函数在相等时都返回零（C++ 的假值）。因此，在测试两个字符串是否相等时，应将 `strcmp` 或 `strncmp` 函数的结果与零比较，以确定字符串是否相等。

```cpp
// Fig. 21.24: fig21_24.cpp
// Using strcmp and strncmp.
#include <iostream>
#include <iomanip>
#include <cstring> // prototypes for strcmp and strncmp
using namespace std;

int main()
{
   char *s1 = "Happy New Year";
   char *s2 = "Happy New Year";
   char *s3 = "Happy Holidays";

   cout << "s1 = " << s1 << "\ns2 = " << s2 << "\ns3 = " << s3
      << "\n\nstrcmp(s1, s2) = " << strcmp(s1, s2)
      << "\nstrcmp(s1, s3) = " << strcmp(s1, s3)
      << "\nstrncmp(s1, s3, 6) = " << setw( 2 ) << strncmp(s1, s3, 6)
      << "\nstrncmp(s1, s3, 7) = " << setw( 2 )
      << strncmp(s1, s3, 7) << "\nstrncmp(s3, s1, 7) = " << setw( 2 )
      << strncmp(s3, s1, 7) << endl;
} // end main
```

```text
s1 = Happy New Year
s2 = Happy New Year
s3 = Happy Holidays

strcmp(s1, s2) = 0
strcmp(s1, s3) = 1
strcmp(s3, s1) = -1

strncmp(s1, s3, 6) = 0
strncmp(s1, s3, 7) = 1
strncmp(s3, s1, 7) = -1
```

**图 21.24** | strcmp 与 strncmp。

要理解一个字符串“大于”或“小于”另一个字符串意味着什么，可以考虑按姓氏字母排序的过程。毫无疑问，你会把“Jones”

本节介绍通用工具库 `<cstdlib>` 中基于指针的**字符串转换函数**。这些函数将基于指针的字符字符串转换为整数和浮点值。在新代码开发中，C++ 程序员通常使用第 18 章介绍的字符串流处理能力来执行此类转换。图 21.27 总结了基于指针的字符串转换函数。注意在函数头中使用 `const` 声明变量 `nPtr`（从右向左读作“nPtr 是指向字符常量的指针”）。使用通用工具库中的函数时，请包含 `<cstdlib>` 头文件。

| 原型 | 描述 |
|---|---|
| `double atof( const char *nPtr )` | 将字符串 `nPtr` 转换为 double。如果字符串无法转换，则返回 0。 |
| `int atoi( const char *nPtr )` | 将字符串 `nPtr` 转换为 int。如果字符串无法转换，则返回 0。 |
| `long atol( const char *nPtr )` | 将字符串 `nPtr` 转换为 long int。如果字符串无法转换，则返回 0。 |
| `double strtod( const char *nPtr, char **endPtr )` | 将字符串 `nPtr` 转换为 double。`endPtr` 是指向 double 之后字符串剩余部分的指针的地址。如果字符串无法转换，则返回 0。 |
| `long strtol( const char *nPtr, char **endPtr, int base )` | 将字符串 `nPtr` 转换为 long。`endPtr` 是指向 long 之后字符串剩余部分的指针的地址。如果字符串无法转换，则返回 0。base 参数表示要转换的数字的基数（例如，8 表示八进制，10 表示十进制，16 表示十六进制）。默认值为十进制。 |
| `unsigned long strtoul( const char *nPtr, char **endPtr, int base )` | 将字符串 `nPtr` 转换为 unsigned long。`endPtr` 是指向 unsigned long 之后字符串剩余部分的指针的地址。如果字符串无法转换，则返回 0。base 参数表示要转换的数字的基数（例如，8 表示八进制，10 表示十进制，16 表示十六进制）。默认值为十进制。 |

**图 21.27** | 通用工具库中基于指针的字符串转换函数。

函数 `atof`（图 21.28 第 9 行）将其参数——表示浮点数的字符串——转换为 double 值。该函数返回 double 值。如果字符串无法转换——例如，字符串的第一个字符不是数字——函数 `atof` 返回零。

函数 `atoi`（图 21.29 第 9 行）将其参数——表示整数的数字字符串——转换为 `int` 值。该函数返回 `int` 值。如果字符串无法转换，函数 `atoi` 返回零。

```cpp
// Fig. 21.28: fig21_28.cpp
// Using atof.
#include <iostream>
#include <cstdlib> // atof prototype
using namespace std;

int main()
{
   double d = atof( "99.0" ); // convert string to double

   cout << "The string \"99.0\" converted to double is " << d
      << "\nThe converted value divided by 2 is " << d / 2.0 << endl;
} // end main
```

```text
The string "99.0" converted to double is 99
The converted value divided by 2 is 49.5
```

**图 21.28** | 字符串转换函数 atof。

```cpp
// Fig. 21.29: fig21_29.cpp
// Using atoi.
#include <iostream>
#include <cstdlib> // atoi prototype
using namespace std;

int main()
{
   int i = atoi( "2593" ); // convert string to int

   cout << "The string \"2593\" converted to int is " << i
      << "\nThe converted value minus 593 is " << i - 593 << endl;
} // end main
```

```text
The string "2593" converted to int is 2593
The converted value minus 593 is 2000
```

**图 21.29** | 字符串转换函数 atoi。

函数 **atol**（图 21.30 第 9 行）将其参数——表示长整数的数字字符串——转换为 long 值。该函数返回 long 值。如果字符串无法转换，函数 **atol** 返回零。如果 **int** 和 **long** 都存储为四个字节，则函数 **atoi** 和函数 **atol** 的工作方式完全相同。

```cpp
// Fig. 21.30: fig21_30.cpp
// Using atol.
#include <iostream>
#include <cstdlib> // atol prototype
using namespace std;
```

**图 21.30** | 字符串转换函数 atol。（第 1 部分，共 2 部分。）

将字符串中已转换部分之后第一个字符的位置赋给。该整数指定要转换的值的基数。第 13 行表明，`x` 被赋值为从 `string` 转换而来的 long 值，并且 `remainderPtr` 被赋值为 `string1` 中已转换值（-1234567）之后第一个字符的位置。为第二个参数使用空指针会导致字符串的剩余部分被忽略。第三个参数 0 表示要转换的值可以是八进制（基 8）、十进制（基 10）或十六进制（基 16）。这由字符串中的初始字符决定——0 表示八进制数，0x 表示十六进制，1–9 的数字表示十进制。

```cpp
// Fig. 21.32: fig21_32.cpp
// Using strtol.
#include <iostream>
#include <cstdlib> // strtol prototype
using namespace std;

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
} // end main
```

```text
The original string is "-1234567abc"
The converted value is -1234567
The remainder of the original string is "abc"
The converted value plus 567 is -1234000
```

**图 21.32** | 字符串转换函数 `strtol`。

在调用函数 `strtol` 时，基数可以指定为零，也可以指定为 2 到 36 之间的任何值。（有关八进制、十进制、十六进制和二进制数制的详细说明，请参见附录 D。）从基 11 到基 36 的整数数字表示使用字符 A–Z 表示值 10 到 35。例如，十六进制值可以由数字 0–9 和字符 A–F 组成。基 11 的整数可以由数字 0–9 和字符 A 组成。基 24 的整数可以由数字 0–9 和字符 A–N 组成。基 36 的整数可以由数字 0–9 和字符 A–Z 组成。[注：所用字母的大小写忽略。]

函数 `strtoul`（图 21.33）将表示无符号长整数的字符序列转换为 unsigned long。该函数的工作方式与 `strtol` 完全相同。第 14 行表明，`x` 被赋值为从 *string* 转换而来的 unsigned long 值，并且 `remainderPtr` 被赋值为 `string1` 中已转换值（1234567）之后第一个字符的位置。第三个参数 0 表示要转换的值可以是八进制、十进制或十六进制格式，具体取决于初始字符。
