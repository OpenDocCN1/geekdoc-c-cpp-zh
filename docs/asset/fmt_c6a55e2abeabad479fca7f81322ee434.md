
### `static_cast` 运算符与 `dynamic_cast` 运算符有什么不同？

# 编程练习

- 1. 按照所示修改 `Tv` 和 `Remote` 类：
    a. 使它们成为相互友元。
    b. 为 `Remote` 类添加一个静态成员。
    c. 为 `Remote` 类添加一个显示内容的方法。
    d. 让 `Tv` 类使用友元。
    编写一个短程序来测试这些功能。

- 2. 修改 `15.10`，使其使用派生自基异常类的异常类。使用 `<exception>` 头文件中的异常方法。

- 3. 这项练习与编程练习 2 相同，不同之处在于使用异常类来报告。C++11 引入了该特性。

- 4. 修改程序，使其支持 `initializer_list` 语法。`Listing 16.1` 使用了这些构造函数。

# string 类与标准模板库

在本章中，你将学习以下内容：
- 标准 C++ 类
- `auto_ptr`、`unique_ptr` 和 `shared_ptr`
- 标准模板库 `STL`
- 容器类
- 迭代器
- 函数对象 `functors`
- STL 算法
- `initializer_list` 模板

# string 类

许多应用程序需要处理字符串。C++ 通过 `string.h` 提供支持。第 4 章，“复合类型”引入了 ANSI/ISO `string` 类。第 12 章，“类与动态内存”介绍了最简单的 `string` 类。

接下来，章节将介绍标准模板库 `STL`，它体现了泛型编程范式。最后，章节将介绍 `initializer_list` 模板，这是 C++11 的新增。

# 构造字符串

让我们看看字符串构造函数。毕竟，创建类对象时最重要的事情之一就是关于该类。`Listing 16.1` 使用了几个构造函数（标记为 `ctor`，这是构造函数的传统缩写）。

`string` 类由 `string` 文件支持。（注意 `string.h` 和 `cstr` 头文件支持 C 库函数）。`size_type` 类型是定义在头文件中由实现定义的整数类型。该类定义了 `string::npos` 为字符串的最大长度。通常，这将等于无符号整数的最大值。该表使用常用缩写 NBS 表示空终止字符串——即传统的 C 字符串，它以空字符结束。

表 16.1 简要描述了构造函数。表格从 16.1 使用的七个构造函数开始，然后列出了两个 C++11 的新增。构造函数的表示是简化的，它们隐藏了 `string` 实际上是 `basic_string<char>` 模板特化的事实，并且省略了与内存管理相关的可选参数（这部分将在本章稍后部分和附录 E，“字符串模板”中讨论）。

# 表 16.1 string 类构造函数

| 构造函数 | 描述 |
| --- | --- |
| `string(const char * s)` | 初始化字符串对象为 `s` 指向的 NBS |
| `string(size_type n, char c)` | 创建一个包含 `n` 个元素的字符串对象，每个元素都初始化为字符 `c` |
| `string(const string & str)` | 初始化字符串对象 `str`（拷贝构造函数） |

# string 类

表 16.1 string 类构造函数

| 构造函数 | 描述 |
| --- | --- |
| `string()` | 创建一个大小为 O 的默认字符串对象（默认构造函数）。 |
| `string (const char * s, size_type n)` | 将字符串对象初始化为 `s` 指向的 NBTS（空空字符串），并继续读取 `n` 个字符，即使这超过了 NBTS 的大小。 |
| `template<class Iter> string(Iter begin, Iter end)` | 将字符串对象初始化为范围 `[begin, end)` 内的值值，其中 `begin` 和 `end` 像指针一样用于指定位置；该范围包含 `begin`但不包含 `end`。 |
| `string(const string &str, size_type pos, size_type n = npos)` | 将字符串对象初始化为 `str`，从 `str` 中的位置 `pos` 开始，到 `str` 的末尾或使用 `n` 个字符，以先到为准。 |
| `string(&& str) noexcept (C++11)` | 将字符串对象初始化为字符串对象 `str`；`str` 可能会被（移动构造函数）。 |
| `string(initializer_list<char> il) (C++11)` | 将字符串对象初始化为初始化列表 `il` 中的字符。 |

列表 16.1 `str.cpp`

```cpp
// str.cpp -- 引入 string 类
#include <iostream>
#include <string>
// 使用 string 构造函数
int main()
{
    using namespace std;
    string one("Lottery Winner!"); // ctor #1
    cout << one << endl; // 重载的 <<
    string two(20, '$'); // ctor #2
    cout << two << endl;
    string three(one); // ctor #3
    cout << three << endl;
    one += " Oops!"; // 重载的 +=
    cout << one << endl;
    two = "Sorry! That was ";
    three[0] = 'p';
    string four; // ctor #4
}
```

```cpp
four = two + three; // 重载的 += =
cout << four << endl;
char all[20] = "All's well that ends well";
string five(alls,20); // ctor #5
cout << five << "!\n";
string six(alls+6, all + 10); // ctor #6
cout << six << " ";
string seven(&five[6], &five[10]); // ctor #6
cout << seven << "...\n";
string eight(four, 16); // ctor #7
cout << eight << " in motion!" << endl;
return 0;
```

列表 16.1 中的程序使用了重载的 `+=` 运算符，将一个字符串附加到另一个字符串；重载的 `=` 运算符用于将一个字符串赋值给另一个；重载的 `[]` 运算符用于访问字符串中的单个字符。

以下是列表 16.1 程序的输出：

Lottery Winner!
$$$$$$$$$$$$$$$$$
Lottery Winner!
Lottery Winner! Oops!
Sorry! That was Pottery Winner!
All's well that ends!
well,...
That was Pottery in motion!

## 程序说明

列表 16.1 中的 C 风格字符串开头说明了你可以使用重载的 `<<` 运算符将字符串初始化为普通字符串并显示它：

```cpp
string one("Lottery Winner!"); // ctor #1
cout << one << endl; // 重载的 <<
```

下一个构造函数将字符串对象 `two` 初始化为一个由 20 个字符组成的字符串：

```cpp
string two(20, '$'); // ctor #2
```

拷贝构造函数将字符串对象 `three` 初始化为字符串对象 `one`：

```cpp
string three(one); // ctor #3
```

重载的 `+=` 运算符将字符串 " Oops!" 附加到字符串 `one`：

```cpp
one += " Oops!"; // 重载的 +=
```

此示例将 C 风格字符串添加到字符串对象。然而，`+=` 运算符被多次重载，因此你也可以附加字符串对象和单个字符：

```cpp
one = two; // 附加字符串对象（程序中未）
one += '!'; // 追加 char 类型值（程序中未）
```

同样，`=` 运算符被重载，因此可以将字符串对象赋值给字符串，将 C 风格字符串赋值给字符串对象，或将简单的 char 值赋值给字符串对象：

```cpp
two = "Sorry! That was "; // 赋值C风格字符串
two = one; // 赋值字符串对象（程序中未）
two = '?'; // 赋值 char 值（程序中未）
```

重载 `[]` 运算符（如第12章String示例所示）允许通过数组符号访问字符串对象中的单个字符：

```cpp
three[0] = 'P';
```

默认构造函数创建一个空字符串，稍后赋予值：

```cpp
string four; // ctor #4
four = two + three; // 重载的 += =
```

第二行使用重载的 `+` 创建一个临时字符串对象，然后通过重载的 `=` 运算符将其赋值给 `four` 对象。正如你预期的那样，`+` 运算符将其两个操作数连接成单个字符串对象。该运算符被多次重载，因此第二个操作数可以是字符串对象、C风格字符串或 char。

第五个构造函数接收一个 C 风格字符串和一个整数参数，该整数表示要拷贝多少字符：

```cpp
char als[] = "All's well that ends well";
string five(als,20); // ctor #5
```

在这里，如表 16.1 所示，仅取第一个字符。`five(als,20)` 构造函数显示了如何初始化。20 个字符。

正如表 16.1 所示，第六个构造函数接收 `begin` 和 `end`：

```cpp
template<class Iter> string(Iter begin, Iter end)
```

`begin` 和 `end` 像指针一样用于指定位置；该范围 `[begin, end)` 包含 `begin` 但不包含 `end`。这里的 `six` 构造函数是第 6 的：

```cpp
string six(alls+6, all + 10); // ctor #6
```

`alls+6` 和 `all + 10` 是指针。这里的 `six` 构造函数是第 6 个构造函数：

```cpp
string six(alls+6, all + 10); // ctor #6
```

`seven(&five[6], &five[10])` 构造函数也是第 6 个构造函数：

```cpp
string seven(&five[6], &five[10]); // ctor #6
```

`eight(four, 16)` 构造函数是第 7 个构造函数：

```cpp
string eight(four, 16); // ctor #7
```

`string(const string &str, size_type pos, size_type n = npos)` 将字符串对象初始化为 `str`，从 `str` 中的位置 `pos` 开始，到 `str` 的末尾或使用 `n` 个字符，以先到为准。

`string(&& str) noexcept (C++11)` 将字符串对象初始化为字符串对象 `str`；`str` 可能会被（移动构造函数）。

`string(initializer_list<char> il) (C++11)` 将字符串对象初始化为初始化列表 `il` 中的字符。

`five(als,20)` 构造函数是第 5 个构造函数：

```cpp
char als[] = "All's well that ends well";
string five(als,20); // ctor #5
```

`five(als,20)` 构造函数是第 5 个构造函数：

```cpp
char als[] = "All's well that ends well";
string five(als,20); // ctor #5
```

# 第 16 章 string 类与标准模板库

```cpp
cin.operator>>(fname); // istream 类方法
operator>>(cin, lname); // 普通函数
```

让我们更仔细地检查一下字符串输入函数。如前提到的，这两个函数都会寻找要输入的目标字符串。但它们有局限性。第一个限制因素是字符串允许的最大尺寸，由常量 `string::npos` 表示。这通常是无符号 `int` 的最大值，因此对于普通的交互式输入来说，不会产生实际限制。然而，如果你尝试将整个文件的内容读取到单个字符串对象中，这可能会成为一个因素。第二个限制因素是程序可用的内存量。

`string` 类的 `getline` 函数从输入内容并存储在字符串对象中，直到发生以下三种情况之一：
- 遇到文件末尾 `EOF`，此时输入流的 `eof` 标志被设置，意味着 `fail()` 和 `eof()` 方法返回 `true`。
- 遇到定界符（默认是 `\n`），此时该字符将从输入流中移除，但不会被存储。
- 达到最大可能的字符数（`string::npos` 与可用内存分配字节数之间的较小值），此时输入流的 `failbit` 被设置，意味着 `fail()` 方法将返回 `true`。

（输入流拥有一套计数系统来跟踪流错误状态。其中，设置 `eof` 寄存器检测文件末尾；设置 `failbit` 寄存器检测输入错误；设置 `badbit` 寄存器检测某些未知的故障，如硬件故障；设置 `goodbit` 表示一切正常。第 17 章“输入、输出与文件”将讨论这一点。）

`string` 的 `operator>>` 函数行为类似，不同之处在于它不是读取并丢弃定界符，而是读取到空白字符为止，并将其留在输入队列中。空白字符是换行符、制表符，或者更通俗地说，任何 `isspace()` 返回 `true` 的字符。

因此，在本书中，你已经看到了几个控制台字符串输入的示例。由于输入函数与字符串对象配合并能识别文件末尾，你也可以将它们用于文件输入。列表 16.2 显示了一个从文件读取字符串的简短示例。它假设文件包含由冒号字符分隔的字符串，并使用 `getline()` 方法指定定界符来显示字符串。然后它将字符串输出到输出端。

## 列表 16.2 strfile.cpp

```cpp
// strfile.cpp -- 从文件读取字符串
#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>
int main()
using namespace std;
ifstream fin;
fin.open("tobuy.txt");
if (fin.is_open() == false)
{
    cerr << "Can't open file. Bye.\n";
    exit(EXIT_FAILURE);
}
string item;
int count = 0;
getline(fin, item, ':');
while (fin) // 当输入正常时
{
    ++count;
    cout << count << " :" << " " << item << endl;
    getline(fin, item, ':');
}
cout << "Done\n";
fin.close();
return 0;
```

这是一个示例的 `tobuy.txt` 文件：
sardines:chocolate ice cream corn:leeks
cottage cheese:olive oil:butter:tofu

通常，为了让程序找到文本文件，该文本文件应与可执行程序处于同一目录，有时与项目文件处于同一目录。或者你可以提供完整的路径名。在 Windows 系统上，请记住在 C 风格字符串中序列 `\\` 代表单个反斜杠：
`fin.open("C:\\CPP\\Progs\\tobuy.txt"); // file = C:\CPP\Progs\tobuy.txt`

这是列表 16.2 中程序的输出：

1: sardines
2: chocolate ice cream
3: pop corn
4: leeks
5:
cottage cheese
6: olive oil
7: butter
8: tofu
9:

Done

## 第 16 章 string 类与标准模板库

注意当指定 `:` 为定界符时，换行符变成了另一个普通字符。因此，文件第一行末尾的换行符变成了后续字符串“cottage cheese”的首个字符；同样，如果第二个输入行末尾存在换行符，它将成为第九个输入字符串的内容。

## 操作字符串

到为止，你已经学习了如何以多种方式创建字符串对象、显示字符串对象的内容、将数据读入字符串对象、向字符串对象追加内容、为字符串对象赋值以及拼接两个字符串。你还能做什么？

你可以比较字符串。所有六个关系运算符都对字符串对象进行了重载，如果一个对象在排序序列中出现得较早，则认为它小于另一个对象。如果机器的排序序列是 ASCII 码，则意味着数字小于大写字母，而大写字母小于小写字母。每个关系运算符都重载了三种方式，以便你可以将字符串与其他字符串对象比较，将字符串对象与 C 风格字符串进行比较，以及将 C 风格字符串与字符串对象进行比较：

```cpp
string snake1("cobra")
string snake2("coral")
char snake3[20] = "anaconda";
```
