
```cpp
6  int main()
7  {
8     char x[] = "Home Sweet Home";
9
10    cout << "The string in array x before memmove is: " << x;
11    cout << "\nThe string in array x after memmove is: "
12       << static_cast< char * >( memmove( x, &x[ 5 ], 10 ) ) << endl;
13
14 } // end main
```

```text
The string in array x before memmove is: Home Sweet Home
The string in array x after memmove is: Sweet Home Home
```

图 21.43 | 内存处理函数 memmove。（第 2 部分，共 2 部分）

函数 `memcmp`（图 21.44，第 14–16 行）将其第一个参数中指定数量的字符与第二个参数中的对应字符进行比较。如果第一个参数大于第二个参数，函数返回大于零的值；如果参数相等，返回零；如果第一个参数小于第二个参数，返回小于零的值。[注：在某些编译器中，函数 `memcmp` 返回 –1、0 或 1，如图 21.44 的示例输出所示。在其他编译器中，该函数返回 0，或返回被比较字符串中第一个不同字符的数字编码之差。例如，当比较 `s1` 和 `s2` 时，它们之间第一个不同的字符是各自字符串的第五个字符——`s1` 的 e（数字编码 69）和 `s2` 的 X（数字编码 72）。在这种情况下，返回值将是 19（当 `s2` 与 `s1` 比较时为 –19）。]

```cpp
1  // Fig. 21.44: fig21_38.cpp
2  // Using memcmp
3  #include <iostream>
4  #include <iomanip>
5  #include <cstring> // memcmp prototype
6  using namespace std;
7
8  int main()
9  {
10    char s1[] = "ABCDEFG";
11    char s2[] = "ABCDXYZ";
12
13    cout << "s1 = " << s1 << "\ns2 = " << s2
14       << "\n\nmemcmp(s1, s2, 4) = " << setw( 3 ) << memcmp( s1, s2, 4 )
15       << "\nmemcmp(s1, s2, 7) = " << setw( 3 ) << memcmp( s1, s2, 7 )
16       << "\nmemcmp(s2, s1, 7) = " << setw( 3 ) << memcmp( s2, s1, 7 )
17       << endl;
18 } // end main
```

```text
s1 = ABCDEFG
s2 = ABCDXYZ
```

图 21.44 | 内存处理函数 `memcmp`。（第 1 部分，共 2 部分）

```text
memcmp(s1, s2, 4) = 0
memcmp(s1, s2, 7) = -1
memcmp(s2, s1, 7) = 1
```

图 21.44 | 内存处理函数 `memcmp`。（第 2 部分，共 2 部分）

函数 **memchr** 在对象的指定字节数中搜索一个字节（表示为 unsigned char）的首次出现。如果在对象中找到该字节，则返回指向它的指针；否则，函数返回空指针。图 21.45 的第 13 行在字符串 "This is a string" 中搜索字符（字节）'r'。

```cpp
1  // Fig. 21.45: fig21_39.cpp
2  // Using memchr.
3  #include <iostream>
4  #include <cstring> // memchr prototype
5  using namespace std;
6
7  int main()
8  {
9      char s[] = "This is a string";
10
11     cout << "s = " << s << "\n" << endl;
12     cout << "The remainder of s after character 'r' is found is \""
13         << static_cast< char * >( memchr( s, 'r', 16 ) ) << '\"' << endl;
14 } // end main
```

```text
s = This is a string
The remainder of s after character 'r' is found is "ring"
```

图 21.45 | 内存处理函数 `memchr`。

函数 **memset** 将其第二个参数中的字节值复制到其第一个参数所指向对象的指定字节数中。图 21.46 的第 13 行使用 `memset` 将 'b' 复制到 `string1` 的前 7 个字节中。

```cpp
1  // Fig. 21.46: fig21_40.cpp
2  // Using memset.
3  #include <iostream>
4  #include <cstring> // memset prototype
5  using namespace std;
6
7  int main()
8  {
9      char string1[ 15 ] = "BBBBBBBBBBBBBBB";
10
11     cout << "string1 = " << string1 << endl;
12     cout << "string1 after memset = "
13         << static_cast< char * >( memset( string1, 'b', 7 ) ) << endl;
14  } // end main
```

图 21.46 | 内存处理函数 `memset`。（第 1 部分，共 2 部分）

```text
string1 = BBBBBBBBBBBBBB
string1 after memset = bbbbbbbbbbbbbb
```

图 21.46 | 内存处理函数 `memset`。（第 2 部分，共 2 部分）

## 21.14 本章小结

本章介绍了 struct 定义、初始化结构体以及在函数中使用结构体。我们讨论了 `typedef`，使用它创建别名以帮助提高可移植性。我们还介绍了用于操作数据的位运算符，以及用于紧凑存储数据的位域。你还学习了 `<cstdlib>` 中的字符串转换函数和 `<cstring>` 中的字符串处理函数。下一章，我们将通过讨论容器——C++ 标准模板库中定义的数据结构——继续讨论数据结构。我们还会介绍 STL 中定义的许多算法。

## 总结

### 第 21.2 节 结构体定义

- 结构体是在一个名称下的一组相关变量（或聚合体）的集合。
- 结构体可以包含不同数据类型的变量。
- 关键字 `struct` 开始每个结构体定义。结构体定义的花括号之间是结构体成员声明。
- 同一结构体的成员必须具有唯一的名称。
- 结构体定义创建一种新的数据类型，可用于声明变量。

### 第 21.3 节 初始化结构体

- 可以通过在声明中的变量后跟一个等号和一个用花括号括起来的逗号分隔的初始化器列表，来使用初始化器列表初始化结构体。如果列表中的初始化器少于结构体中的成员，则其余成员被初始化为零（对于指针成员则为空指针）。
- 整个结构体变量可以赋值给相同类型的结构体变量。
- 结构体变量可以用相同类型的结构体变量初始化。

### 第 21.4 节 在函数中使用结构体

- 结构体变量和单个结构体成员按值传递给函数。
- 要按引用传递结构体，可传递结构体变量的地址或结构体变量的引用。结构体数组按引用传递。要按值传递数组，可创建一个以该数组为成员的结构体。

### 第 21.5 节 typedef

- 用 `typedef` 创建新类型名并不会创建新类型；它创建一个与先前定义的类型同义的名称。

### 第 21.7 节 位运算符

- 按位与运算符（`&`）接受两个整型操作数。如果两个操作数中的对应位都为 1，则结果中的该位被置为 1。
- 掩码与按位与一起使用，以隐藏某些位而保留其他位。
- 按位包含或运算符（`|`）接受两个操作数。如果任一操作数中的对应位被置为 1，则结果中的该位被置为 1。
- 每个位运算符（按位取反运算符除外）都有一个对应的赋值运算符。
- 按位异或运算符（`^`）接受两个操作数。如果两个操作数中的对应位中恰好有一个被置为 1，则结果中的该位被置为 1。
- 左移运算符（`<<`）将其左操作数的位向左移动其右操作数指定的位数。右侧空出的位用零填充。
- 右移运算符（`>>`）将其左操作数的位向右移动其右操作数指定的位数。右移无符号整数时，左侧空出的位用零填充。有符号整数中空出的位可以用零或一填充。
- 按位取反运算符（`~`）接受一个操作数并反转其各位——这会生成操作数的反码。

### 第 21.8 节 位域

- 位域通过以所需的最少位数存储数据来减少存储空间的使用。位域成员必须声明为 `int` 或 `unsigned`。
- 位域的声明方式是在 unsigned 或 int 成员名后跟一个冒号和位域的宽度。
- 位域宽度必须是整型常量。
- 如果指定位域时没有名称，则该字段用作结构体中的填充。
- 宽度为 0 的未命名位域将下一个位域对齐到新的机器字边界。

### 第 21.9 节 字符处理库

- 函数 `islower` 判断其参数是否为小写字母（a-z）。函数 `isupper` 判断其参数是否为大写字母（A-Z）。
- 函数 `isdigit` 判断其参数是否为数字（0-9）。
- 函数 `isalpha` 判断其参数是否为大写字母（A-Z）或小写字母（a-z）。
- 函数 `isalnum` 判断其参数是否为大写字母（A-Z）、小写字母（a-z）或数字（0-9）。
- 函数 `isxdigit` 判断其参数是否为十六进制数字（A-F、a-f、0-9）。
- 函数 `toupper` 将小写字母转换为大写字母。函数 `tolower` 将大写字母转换为小写字母。
- 函数 `isspace` 判断其参数是否为以下空白字符之一：' '（空格）、'\f'、'\n'、'\r'、'\t' 或 '\v'。
- 函数 `iscntrl` 判断其参数是否为控制字符，例如 '\t'、'\v'、'\f'、'\a'、'\b'、'\r' 或 '\n'。
- 函数 `ispunct` 判断其参数是否为除空格、数字或字母之外的打印字符。
- 函数 `isprint` 判断其参数是否为任何打印字符，包括空格。
- 函数 `isgraph` 判断其参数是否为除空格之外的打印字符。

### 第 21.10 节 基于指针的字符串操作函数

- 函数 `strcpy` 将其第二个参数复制到第一个参数中。必须确保目标数组足够大，以存储该字符串及其终止空字符。

