
| 牌 | 花色 | 颜色 | 牌 | 花色 | 颜色 |
|---:|---:|---:|---:|---:|---:|
| 12 | 0 | 0 | 12 | 2 | 1 |
| 0 | 0 | 0 | 0 | 3 | 1 |
| 1 | 1 | 0 | 1 | 3 | 1 |
| 2 | 1 | 0 | 2 | 3 | 1 |
| 3 | 1 | 0 | 3 | 3 | 1 |
| 4 | 1 | 0 | 4 | 3 | 1 |
| 5 | 1 | 0 | 5 | 3 | 1 |
| 6 | 1 | 0 | 6 | 3 | 1 |
| 7 | 1 | 0 | 7 | 3 | 1 |
| 8 | 1 | 0 | 8 | 3 | 1 |
| 9 | 1 | 0 | 9 | 3 | 1 |
| 10 | 1 | 0 | 10 | 3 | 1 |
| 11 | 1 | 0 | 11 | 3 | 1 |
| 12 | 1 | 0 | 12 | 3 | 1 |

**图 21.16** | 用于存储一副纸牌的位域。（第2部分，共2部分。）

可以指定一个**未命名位域**，此时该位域在结构中用作**填充**。例如，该结构定义使用一个未命名的三位域作为填充——这三位中不能存储任何内容。成员b存储在另一个存储单元中。

```cpp
struct Example
{
    unsigned a : 13;
    unsigned   : 4; // align to next storage-unit boundary
    unsigned b : 4;
}; // end struct Example
```

**宽度为零的未命名位域**用于将下一个位域对齐到新的存储单元边界。例如，以下结构定义

```cpp
struct Example
{
    unsigned a : 13;
    unsigned   : 0; // align to next storage-unit boundary
    unsigned b : 4;
}; // end struct Example
```

使用一个未命名的0位域来**跳过**存储a的存储单元中剩余的位（有多少跳多少），并将b对齐到*下一个存储单元边界*。

![](img/bfd978e7e9b192bab46ec2a89e481263_842_0.png)

> **可移植性建议 21.5**  
> *位域操作依赖于机器。例如，有些计算机允许位域跨越字边界，而另一些计算机则不允许。*

![](img/bfd978e7e9b192bab46ec2a89e481263_842_1.png)

> **常见编程错误 21.5**  
> *试图用下标访问位域的各个位，就好像它们是数组元素一样，会导致编译错误。位域不是“位数组”。*

![](img/bfd978e7e9b192bab46ec2a89e481263_842_2.png)

> **常见编程错误 21.6**  
> *试图取位域的地址（&运算符不能用于位域，因为指针只能指定内存中的特定字节，而位域可以从字节中间开始）会导致编译错误。*

![](img/bfd978e7e9b192bab46ec2a89e481263_843_0.png)

### 性能提示 21.2

> 尽管位域节省空间，但使用它们可能导致编译器生成执行较慢的机器语言代码。这是因为仅访问可寻址存储单元的一部分需要额外的机器语言操作。这是计算机科学中出现的众多时空权衡示例之一。

## 21.17 字符处理库

大多数数据以字符形式输入计算机——包括字母、数字和各种特殊符号。在本节中，我们讨论C++检查和操作单个字符的能力。在本章剩余部分，我们继续第8章开始的字符串操作讨论。

字符处理库包含若干对字符数据执行有用测试和操作的函数。每个函数接收一个字符——以int表示——或EOF作为参数。字符通常作为整数来操作。记住，EOF通常的值为−1，而且某些硬件体系结构不允许将负值存储在char变量中。因此，字符处理函数将字符作为整数来操作。图21.17总结了字符处理库的函数。使用字符处理库中的函数时，请包含`<cctype>`头文件。

| 原型 | 描述 |
|---|---|
| `int isdigit( int c )` | 如果c是数字则返回1，否则返回0。 |
| `int isalpha( int c )` | 如果c是字母则返回1，否则返回0。 |
| `int isalnum( int c )` | 如果c是数字或字母则返回1，否则返回0。 |
| `int isxdigit( int c )` | 如果c是十六进制数字字符则返回1，否则返回0。（关于二进制、八进制、十进制和十六进制数的详细说明，请参见附录D“数制”。） |
| `int islower( int c )` | 如果c是小写字母则返回1，否则返回0。 |
| `int isupper( int c )` | 如果c是大写字母则返回1；否则返回0。 |
| `int tolower( int c )` | 如果c是大写字母，tolower将c作为小写字母返回。否则，tolower返回未改变的参数。 |
| `int toupper( int c )` | 如果c是小写字母，toupper将c作为大写字母返回。否则，toupper返回未改变的参数。 |
| `int isspace( int c )` | 如果c是空白字符——换行（'\n'）、空格（' '）、换页（'\f'）、回车（'\r'）、水平制表（'\t'）或垂直制表（'\v'）——则返回1，否则返回0。 |
| `int iscntrl( int c )` | 如果c是控制字符，例如换行（'\n'）、换页（'\f'）、回车（'\r'）、水平制表（'\t'）、垂直制表（'\v'）、警报（'\a'）或退格（'\b'）——则返回1，否则返回0。 |
| `int ispunct( int c )` | 如果c是除空格、数字或字母之外的打印字符则返回1，否则返回0。 |
| `int isprint( int c )` | 如果c是包括空格（`' '`）在内的打印字符则返回1，否则返回0。 |
| `int isgraph( int c )` | 如果c是除空格（`' '`）之外的打印字符则返回1，否则返回0。 |

**图 21.17** | 字符处理库函数。（第1—2部分，共2部分。）

图21.18演示了函数**isdigit**、**isalpha**、**isalnum**和**isxdigit**。函数**isdigit**判断其参数是否为数字（0—9）。函数**isalpha**判断其参数是否为大写字母（A—Z）或小写字母（a—z）。函数**isalnum**判断其参数是否为大写字母、小写字母或数字。函数**isxdigit**判断其参数是否为十六进制数字（A—F、a—f、0—9）。

```cpp
1  // Fig. 21.18: fig21_18.cpp
2  // Character-handling functions isdigit, isalpha, isalnum and isxdigit.
3  #include <iostream>
4  #include <cctype> // character-handling function prototypes
5  using namespace std;
6
7  int main()
8  {
9     cout << "\nAccording to isdigit:\n"
10       << ( isdigit( '8' ) ? "8 is a " : "8 is not a" ) << " digit\n"
11       << ( isdigit( '#' ) ? "# is a " : "# is not a" ) << " digit\n";
12
13    cout << "\nAccording to isalpha:\n"
14       << ( isalpha( 'A' ) ? "A is a " : "A is not a" ) << " letter\n"
15       << ( isalpha( 'b' ) ? "b is a " : "b is not a" ) << " letter\n"
16       << ( isalpha( '&' ) ? "& is a " : "& is not a" ) << " letter\n"
17       << ( isalpha( '4' ) ? "4 is a " : "4 is not a" ) << " letter\n";
18
19    cout << "\nAccording to isalnum:\n"
20       << ( isalnum( 'A' ) ? "A is a " : "A is not a" )
21       << " digit or a letter\n"
22       << ( isalnum( '8' ) ? "8 is a " : "8 is not a" )
23       << " digit or a letter\n"
24       << ( isalnum( '#' ) ? "# is a " : "# is not a" )
25       << " digit or a letter\n";
26
27    cout << "\nAccording to isxdigit:\n"
28       << ( isxdigit( 'F' ) ? "F is a " : "F is not a" )
29       << " hexadecimal digit\n"
30       << ( isxdigit( 'J' ) ? "J is a " : "J is not a" )
31       << " hexadecimal digit\n"
32       << ( isxdigit( '7' ) ? "7 is a " : "7 is not a" )
33       << " hexadecimal digit\n"
34       << ( isxdigit( '$' ) ? "$ is a " : "$ is not a" )
35       << " hexadecimal digit\n"
36       << ( isxdigit( 'f' ) ? "f is a " : "f is not a" )
37       << " hexadecimal digit" << endl;
38 } // end main
```

```text
According to isdigit:
8 is a digit
# is not a digit

According to isalpha:
A is a letter
b is a letter
& is not a letter
4 is not a letter

According to isalnum:
A is a digit or a letter
8 is a digit or a letter
# is not a digit or a letter

According to isxdigit:
F is a hexadecimal digit
J is not a hexadecimal digit
7 is a hexadecimal digit
$ is not a hexadecimal digit
f is a hexadecimal digit
```

**图 21.18** | 字符处理函数`isdigit`、`isalpha`、`isalnum`和`isxdigit`。（第1—2部分，共2部分。）

图21.18对每个函数使用条件运算符（`?:`），以确定对于所测试的每个字符，应在输出中打印字符串"is a"还是字符串"is not a"。例如，第10行表明'8'是数字——即，如果`isdigit`返回真（非零）值——则打印字符串"8 is a"。如果'8'不是数字（即，如果`isdigit`返回0），则打印字符串"8 is not a"。

图21.19演示了函数`islower`、`isupper`、`tolower`和`toupper`。函数`islower`判断其参数是否为*小写字母*（a—z）。函数`isupper`判断其参数是否为*大写字母*（A—Z）。函数`tolower`将大写字母转换为小写，并返回该小写字母——如果参数不是大写字母，则`tolower`返回未改变的参数值。函数`toupper`将小写字母转换为大写，并返回该大写字母——如果参数不是小写字母，则`toupper`返回未改变的参数值。

```cpp
1  // Fig. 21.19: fig21_19.cpp
2  // Character-handling functions islower, isupper, tolower and toupper.
3  #include <iostream>
4  #include <cctype> // character-handling function prototypes
5  using namespace std;
```

**图 21.19** | 字符处理函数`islower`、`isupper`、`tolower`和`toupper`。（第1部分，共2部分。）

