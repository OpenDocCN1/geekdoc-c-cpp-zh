

isupper 判断其参数是否为大写字母（A-Z）。函数 tolower 将大写字母转换为小写并返回小写字母——如果参数不是大写字母，tolower 返回参数值不变。函数 toupper 将小写字母转换为大写并返回大写字母——如果参数不是小写字母，toupper 返回参数值不变。

```cpp
// Fig. 19.19: fig19_19.cpp
// Using functions islower, isupper, tolower and toupper.
#include <iostream>
using std::cout;
using std::endl;

#include <cctype> // character-handling function prototypes
using std::islower;
using std::isupper;
using std::tolower;
using std::toupper;

int main()
{
    cout << "According to islower:\n"
         << ( islower( 'p' ) ? "p is a" : "p is not a" )
         << " lowercase letter\n"
         << ( islower( 'P' ) ? "P is a" : "P is not a" )
         << " lowercase letter\n"
         << ( islower( '5' ) ? "5 is a" : "5 is not a" )
         << " lowercase letter\n"
         << ( islower( '!' ) ? "! is a" : "! is not a" )
         << " lowercase letter\n";

    cout << "\nAccording to isupper:\n"
         << ( isupper( 'D' ) ? "D is an" : "D is not an" )
         << " uppercase letter\n"
         << ( isupper( 'd' ) ? "d is an" : "d is not an" )
         << " uppercase letter\n"
         << ( isupper( '8' ) ? "8 is an" : "8 is not an" )
         << " uppercase letter\n"
         << ( isupper( '$' ) ? "$ is an" : "$ is not an" )
         << " uppercase letter\n";

    cout << "\nu converted to uppercase is "
         << static_cast< char >( toupper( 'u' ) )
         << "\n7 converted to uppercase is "
         << static_cast< char >( toupper( '7' ) )
         << "\n$ converted to uppercase is "
         << static_cast< char >( toupper( '$' ) )
         << "\nL converted to lowercase is "
         << static_cast< char >( tolower( 'L' ) ) << endl;
    return 0;
} // end main
```

*Fig. 19.19 | Character-handling functions islower, isupper, tolower and toupper. (Part 1 of 2.)*

```
According to islower:
p is a lowercase letter
P is not a lowercase letter
5 is not a lowercase letter
! is not a lowercase letter

According to isupper:
D is an uppercase letter
d is not an uppercase letter
8 is not an uppercase letter
$ is not an uppercase letter

u converted to uppercase is U
7 converted to uppercase is 7
$ converted to uppercase is $
L converted to lowercase is l
```

*Fig. 19.19 | Character-handling functions islower, isupper, tolower and toupper. (Part 2 of 2.)*

Figure 19.20 demonstrates functions isspace, iscntrl, ispunct, isprint and isgraph. Function isspace determines whether its argument is a white-space character, such as space (' '), form feed ('\f'), newline ('\n'), carriage return ('\r'), horizontal tab ('\t') or vertical tab ('\v'). Function iscntrl determines whether its argument is a control character such as horizontal tab ('\t'), vertical tab ('\v'), form feed ('\f'), alert ('\a'), backspace ('\b'), carriage return ('\r') or newline ('\n'). Function ispunct determines whether its argument is a printing character other than a space, digit or letter, such as $, #, (, ), [, ], {, }, ;, : or %. Function isprint determines whether its argument is a character that can be displayed on the screen (including the space character). Function isgraph tests for the same characters as isprint, but the space character is not included.

```cpp
// Fig. 19.20: fig19_20.cpp
// Using functions isspace, iscntrl, ispunct, isprint, isgraph.
#include <iostream>
using std::cout;
using std::endl;

#include <cctype> // character-handling function prototypes
using std::iscntrl;
using std::isgraph;
using std::isprint;
using std::ispunct;
using std::isspace;

int main()
{
    cout << "According to isspace:\nNewline "
        << ( isspace( '\n' ) ? "is a" : "is not a" )
        << " whitespace character\nHorizontal tab "
        << ( isspace( '\t' ) ? "is a" : "is not a" )
        << " whitespace character\n"
        << ( isspace( '%' ) ? "% is a" : "% is not a" )
        << " whitespace character\n";

    cout << "\nAccording to iscntrl:\nNewline "
        << ( iscntrl( '\n' ) ? "is a" : "is not a" )
        << " control character\n"
        << ( iscntrl( '$' ) ? "$ is a" : "$ is not a" )
        << " control character\n";

    cout << "\nAccording to ispunct:\n"
        << ( ispunct( ';' ) ? "; is a" : "; is not a" )
        << " punctuation character\n"
        << ( ispunct( 'Y' ) ? "Y is a" : "Y is not a" )
        << " punctuation character\n"
        << ( ispunct( '#' ) ? "# is a" : "# is not a" )
        << " punctuation character\n";

    cout << "\nAccording to isprint:\n"
        << ( isprint( '$' ) ? "$ is a" : "$ is not a" )
        << " printing character\nAlert "
        << ( isprint( '\a' ) ? "is a" : "is not a" )
        << " printing character\nSpace "
        << ( isprint( ' ' ) ? "is a" : "is not a" )
        << " printing character\n";

    cout << "\nAccording to isgraph:\n"
        << ( isgraph( 'Q' ) ? "Q is a" : "Q is not a" )
        << " printing character other than a space\nSpace "
        << ( isgraph( ' ' ) ? "is a" : "is not a" )
        << " printing character other than a space" << endl;
    return 0;
} // end main
```

*Fig. 19.20 | Character-handling functions isspace, iscntrl, ispunct, isprint and isgraph. (Part 1 of 2.)*

```
According to isspace:
Newline is a whitespace character
Horizontal tab is a whitespace character
% is not a whitespace character

According to iscntrl:
Newline is a control character
$ is not a control character

According to ispunct:
; is a punctuation character
Y is not a punctuation character
# is a punctuation character

According to isprint:
$ is a printing character
Alert is not a printing character
Space is a printing character

According to isgraph:
Q is a printing character other than a space
Space is not a printing character other than a space
```

*Fig. 19.20 | Character-handling functions isspace, iscntrl, ispunct, isprint and isgraph. (Part 2 of 2.)*

## 19.10 基于指针的字符串转换函数

在第 8 章中，我们讨论了 C++ 中最流行的基于指针的字符串操作函数。在接下来的几个小节中，我们将介绍剩余的函数，包括用于将字符串转换为数值值的函数、用于搜索字符串的函数以及用于操作、比较和搜索内存块的函数。

本节介绍来自 *通用实用库* `<cstdlib>` 的基于指针的 *字符串转换函数*。这些函数将字符指针字符串转换为整数和浮点值。图 19.21 总结了基于指针的字符串转换函数。请注意函数头中对变量 nPtr 使用 const 的声明（从右到左读作“nPtr 是指向字符常量的指针”）。使用通用实用库中的函数时，请包含 `<cstdlib>` 头文件。

| Prototype | Description |
|---|---|
| `double atof(const char *nPtr)` | Converts the string nPtr to double. If the string cannot be converted, 0 is returned. |
| `int atoi(const char *nPtr)` | Converts the string nPtr to int. If the string cannot be converted, 0 is returned. |
| `long atol(const char *nPtr)` | Converts the string nPtr to long int. If the string cannot be converted, 0 is returned. |
| `double strtod(const char *nPtr, char **endPtr)` | Converts the string nPtr to double. endPtr is the address of a pointer to the rest of the string after the double. If the string cannot be converted, 0 is returned. |
| `long strtol(const char *nPtr, char **endPtr, int base)` | Converts the string nPtr to long. endPtr is the address of a pointer to the rest of the string after the long. If the string cannot be converted, 0 is returned. The base parameter indicates the base of the number to convert (e.g., 8 for octal, 10 for decimal or 16 for hexadecimal). The default is decimal. |

*Fig. 19.21 | Pointer-based string-conversion functions of the general-utilities library. (Part 1 of 2.)*

