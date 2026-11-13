

## 图 4.13 字符串构造函数和运算符的实现

### 构造函数和运算符的实现

```
string::string(const char str[])
// Library facilities used: cstring
{
    current_length = strlen(str);
    allocated = current_length + 1;
    characters = new char[allocated];
    strcpy(characters, str);
}
```

```
bool operator ==(const string& s1, const string& s2)
// Postcondition: The return value is true if s1 is identical to s2.
// Library facilities used: cstring
{
    return (strcmp(s1.characters, s2.characters) == 0);
}
```

预留函数。我们的设计包含一个名为 reserve 的成员函数，类似于动态袋的 reserve 函数。以下是前置条件/后置条件契约：

```
void reserve(size_t n);
// Postcondition: All functions will now work efficiently (without allocating
// new memory) until n characters are in the string.
```

使用我们字符串类的程序员永远不需要激活 reserve，但为了更高效率，他们可能希望这样做。

当需要更大的数组时，我们对其他成员函数的实现也可以激活 reserve。当成员函数激活 reserve 时，激活应在对字符串进行任何其他更改之前发生。这遵循我们通常的编程准则：在更改对象之前分配新内存。（参见第 191 页“如何在成员函数中分配内存”。）

输出运算符 >>。我们的输入运算符首先跳过输入流中的任何空白。（C++ 中的所有标准 >> 运算符都从跳过空白开始。）跳过初始空白后，我们的字符串输入运算符读取一个字符串——读取直到但不包括下一个空白字符（或直到输入流失败，这可能由多种原因引起，例如到达文件末尾）。来自 <cctype> 库设施的函数 isspace 可以提供帮助。该函数有一个参数（一个字符）；如果其参数是空白字符之一，则返回 true。考虑到这一点，我们可以使用这个循环跳过任何初始空白：

```
while (ins && !isspace(ins.peek()))
    ins.ignore();
```

- ins, peek, ignore 该循环还使用了三个 iostream 特性：
  1. 在布尔表达式中，istream 的名称（即 ins）充当测试输入流是否出错的条件。如果 ins 结果为 true，则流正常；false 值表示输入流出错。
  2. peek 成员函数返回下一个要读取的字符（而不实际读取它）。
  3. ignore 成员函数读取并丢弃下一个字符。

跳过初始空白后，你的实现应将字符串设置为空字符串，然后逐个读取输入字符，将每个字符添加到字符串末尾。读取在遇到更多空白（或文件末尾）时停止。

一旦目标字符串达到其当前容量，我们的方法仍能正确工作，尽管效率低下，因为每次添加另一个字符时，target 可能都会由 += 运算符调整大小。你的文档应警告程序员注意这种低效率，以便程序员在调用输入运算符之前可以显式调整 target 的大小。

getline 函数提供了一种读取输入的替代方法。

## 字符串类的演示程序

图 4.14 显示了一个针对字符串类的简短演示程序。该程序询问用户的名和姓，然后打印一些消息。示例对话大致如下：

```
What is your first name? Timothy
My first name is Demo.
What is your last name? Program
That is the same as my last name!
I am happy to meet you, Timothy Program.
```

该程序使用了几个 C++ 对象特性，例如从普通字符串到我们新类的自动转换。我们将在第 210 页讨论这些特性，你可以使用自己的字符串类来尝试它们。

## 图 4.14 字符串类的演示程序

### 一个程序

```
// FILE: str_demo.cxx (a small demonstration program showing how the string class is used)
#include <iostream> // Provides cout and cin
#include <cstdlib> // Provides EXIT_SUCCESS
#include "mystring.h" // Provides our new string class
using namespace std;

// PROTOTYPES for functions used by this demonstration program:
void match(const main_savitch_4::string& variety,
           const main_savitch_4::string& mine,
           const main_savitch_4::string& yours);
// The two strings, mine and yours, are compared. If they are the same, then a
// message is printed saying they are the same; otherwise mine is printed
// in a message. In either case, the string variety is part of the message.

int main( )
{
    const main_savitch_4::string BLANK(" ");
    const main_savitch_4::string me_first("Demo");
    main_savitch_4::string me_last("Program");
    main_savitch_4::string your_first, your_last, you;
    cout << "What is your first name? ";
    cin >> your_first;
    match("first name", me_first, your_first);
    cout << "What is your last name? ";
    cin >> your_last;
    match("last name", me_last, your_last);
    you = your_first + BLANK + your_last;
    cout << "I am happy to meet you, " << you << "." << endl;
    return EXIT_SUCCESS;
}

void match(const main_savitch_4::string& variety,
           const main_savitch_4::string& mine,
           const main_savitch_4::string& yours)
{
    if (mine == yours)
        cout << "That is the same as my " << variety << '!' << endl;
    else
        cout << "My " << variety << " is " << mine << '.' << endl;
}
```

## 输出运算符的链式调用

查看图 4.14 底部的 match 函数。该函数有三个常量字符串参数。其中两个参数（mine 和 yours）使用字符串的 == 运算符进行比较。如果字符串相等，则将第三个参数（variety）作为消息的一部分打印：

```
cout << "That is the same as my " << variety << '!' << endl;
```

例如，如果 variety 是字符串 "first name"，则输出语句打印 "That is the same as my first name"。实际输出涉及四个输出运算符 << 的序列，或称为“链式调用”。

- 1. 第一个 << 打印字符串常量："That is the same as my "。这是一个普通的 C++ 字符串常量，而不是字符串对象。
- 2. 第二个 << 打印字符串对象 variety，使用新字符串类的 << 运算符。
- 3. 第三个 << 将感叹号作为普通字符打印。
- 4. 最后一个 << 打印换行符。

关键点是字符串类的 << 运算符可以与其他对象链式组合，以打印一系列对象——有些是字符串对象，有些不是。

## 声明常量对象

图 4.14 中主程序的顶部声明了几个字符串。第一个声明是：

```
const string BLANK(" ");
```

这声明了一个名为 BLANK 的常量字符串，它被初始化为仅包含一个空格的序列。以这种方式使用名称 BLANK 使得使用空格的语句更易于阅读。使用关键字 const 禁止程序实际将 BLANK 更改为不同的字符串。作为我们文档标准（附录 J）的一部分，我们为声明常量的名称使用全大写字母。

## 构造函数生成的转换

在图 4.14 的主程序中，我们有两次对 match 函数的调用。例如：

```
match("first name", me_first, your_first);
```

查看第一个参数 "first name"，它是一个普通字符串常量。

但是 match 的第一个参数不是普通字符串；它是我们新字符串类的一个字符串对象：

```
void match(const string& variety, ...
```

这是怎么回事？难道这不是一个错误，因为参数的类型与形式参数不同吗？答案是否定的，因为 C++ 自动应用了一种特殊的转换操作。转换的工作原理如下：当检测到类型不匹配时，编译器会尝试将给定值转换为所需类型的值。在我们的示例中，编译器尝试将字符串常量 "first name" 转换为字符串对象。转换机制之一是为所需类型查找一个带有单个参数的构造函数。在我们的示例中，编译器使用这个构造函数：

```
string(const char str[]);
```

将普通字符串常量转换为字符串对象。构造的字符串对象随后用作 match 的第一个参数。

## 在表达式中使用重载运算

字符串类重载了二元 + 运算符以执行字符串连接。图 4.14 主程序中 + 的用法可能看起来不寻常：

```
you = your_first + BLANK + your_last;
```

编译器使用表达式中 + 运算符的常规结合性规则来处理该表达式。与一系列 + 操作通常一样，最左边的 + 首先应用，等效于这个带括号的表达式，其中高亮部分首先求值：

```
you = (your_first + BLANK) + your_last;
```

## 我们的字符串类与 C++ 库字符串类的对比

新字符串类由你编写的头文件（mystring.h）和实现文件（mystring.cxx）实现。该类只有少数几个操作——足够我们编写一些示例程序。使用这些示例程序以及你编写的程序时，可以使用 mystring.h。但是，如果你有一个提供标准库字符串类的较新编译器，则可能希望使用库的类而不是我们的简单类。库字符串类具有我们所有的操作以及更多。

## 第 4.5 节自测练习

- 26. 编写 C++ 代码，声明一个可容纳最多 20 个字符的常规 C++ 空终止字符串，将用户输入读入字符串，在字符串末尾追加一个感叹号，并打印结果。

