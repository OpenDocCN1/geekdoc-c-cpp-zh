

```text
outputString contains:
Output of several data types to an ostringstream object:
    double: 123.457
    int: 22
address of int: 0012F540

after additional stream insertions,
outputString contains:
Output of several data types to an ostringstream object:
    double: 123.457
    int: 22
address of int: 0012F540
more characters added
```

图 18.11 | 使用动态分配的 `ostringstream` 对象。（第 2 部分，共 2 部分。）

`istringstream` 对象从内存中的字符串向程序变量输入数据。数据以字符形式存储在 `istringstream` 对象中。从 `istringstream` 对象输入的方式与从任何文件输入完全相同。字符串的结尾被 `istringstream` 对象解释为文件结尾。

图 18.12 演示了从 `istringstream` 对象的输入。第 15–16 行创建了包含数据的字符串 `input` 和构造为包含字符串 `input` 中数据的 `istringstream` 对象 `inputString`。字符串 `input` 包含数据

```text
Input test 123 4.7 A
```

当作为程序输入读取时，它包含两个字符串（“Input”和“test”）、一个 int（123）、一个 double（4.7）和一个 char（‘A’）。这些字符在第 23 行被提取到变量 `string1`、`string2`、`integer`、`double1` 和 `character` 中。

图 18.12 | 演示从 `istringstream` 对象输入。（第 1 部分，共 2 部分。）

```cpp
// Fig. 18.12: Fig18_12.cpp
// Demonstrating input from an istringstream object.
#include <iostream>
using std::cout;
using std::endl;

#include <string>
using std::string;

#include <sstream>
using std::istringstream;

int main()
{
    string input( "Input test 123 4.7 A" );
    istringstream inputString( input );
    string string1;
    string string2;
    int integer;
    double double1;
    char character;

    inputString >> string1 >> string2 >> integer >> double1 >> character;

    cout << "The following items were extracted\n"
         << "from the istringstream object:" << "\nstring: " << string1
         << "\nstring: " << string2 << "\n  int: " << integer
         << "\ndouble: " << double1 << "\n  char: " << character;

    // attempt to read from empty stream
    long value;
    inputString >> value;

    // test stream results
    if ( inputString.good() )
       cout << "\n\nlong value is: " << value << endl;
    else
       cout << "\ninputString is empty" << endl;

    return 0;
} // end main
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_752_0.png)

*图 18.12* — 演示从 `istringstream` 对象输入。（第 2 部分，共 2 部分。）

然后在第 25–28 行输出数据。程序在第 32 行再次尝试从 `inputString` 读取。第 35 行的 `if` 条件使用函数 `good`（第 15.8 节）测试是否还有剩余数据。因为没有剩余数据，该函数返回 `false`，因此执行 `if...else` 语句的 `else` 部分。

## 18.13 小结

本章介绍了 C++ 标准库中的 `string` 类，它允许程序将字符串视为功能完整的对象。我们讨论了字符串的赋值、连接、比较、查找和交换。我们还介绍了一些方法，用于确定字符串特征、在字符串中查找、替换和插入字符，以及在 C 风格字符串与字符串对象之间进行转换。你还学习了字符串迭代器，以及在内存中对字符串执行输入和输出。在下一章中，我们将介绍与类相似的结构体（`struct`），并讨论位、字符和 C 风格字符串的操作。

## 第 19 章 位、字符、C 风格字符串和结构体

> 同样的善意谎言  
> 随着岁月流逝不断重复  
> 总是能引起共鸣——“你一点都没变！”  
> ——玛格丽特·菲什巴克

> 亨利·金的主要缺点  
> 是咀嚼细小的绳子。  
> ——希莱尔·贝洛克

> 有力的写作是简洁的。  
> 一个句子不应包含不必要的词语，一个段落不应包含不必要的句子。  
> ——小威廉·斯特伦克

### 目标

在本章中，你将学习：

- 创建和使用结构体（`struct`）。
- 按值和按引用将结构体传递给函数。
- 使用 `typedef` 为先前定义的数据类型和结构体创建别名。
- 使用位运算符操作数据，并创建位域以紧凑地存储数据。
- 使用字符处理库 `<cctype>` 中的函数。
- 使用通用工具库 `<cstdlib>` 中的字符串转换函数。
- 使用字符串处理库 `<cstring>` 中的字符串处理函数。

- 19.1 引言
- 19.2 结构体定义
- 19.3 结构体的初始化
- 19.4 在函数中使用结构体
- 19.5 typedef
- 19.6 示例：高性能洗牌和发牌模拟
- 19.7 位运算符
- 19.8 位域
- 19.9 字符处理库
- 19.10 基于指针的字符串转换函数
- 19.11 基于指针的字符串处理库的搜索函数
- 19.12 基于指针的字符串处理库的内存函数
- 19.13 小结

### 19.1 引言

我们现在讨论结构体以及位、字符和 C 风格字符串的操作。我们在此介绍的许多技术都是为了帮助那些需要处理遗留 C 和 C++ 代码的 C++ 程序员。

C++ 的设计者将结构体演化为类的概念。与类一样，C++ 结构体可以包含访问说明符、成员函数、构造函数和析构函数。事实上，在 C++ 中，结构体与类之间的唯一区别是：当未使用访问说明符时，结构体成员默认为 `public` 访问，而类成员默认为 `private` 访问；此外，结构体默认为公有继承，而类默认为私有继承。本书已经详细介绍了类，因此我们确实没有必要再详细讨论结构体。本章对结构体的介绍侧重于它们在 C 语言中的使用，在 C 语言中结构体只包含公有数据成员。这种结构体的使用方式正是你在工业界会遇到的遗留 C 代码和早期 C++ 代码的典型特征。

我们讨论如何声明结构体、初始化结构体以及将结构体传递给函数。然后，我们介绍一个高性能的洗牌和发牌模拟，其中使用结构体对象和 C 风格字符串来表示牌。我们讨论允许程序员访问和操作数据字节中各个位的位运算符。我们还介绍了位域——一种特殊结构，可用于指定变量在内存中占用的精确位数。这些位操作技术在直接与内存有限的硬件设备交互的 C 和 C++ 程序中很常见。本章最后以许多字符和 C 风格字符串操作函数的示例结束——其中一些函数旨在将内存块作为字节数组处理。

### 19.2 结构体定义

结构体是*聚合数据类型*——也就是说，它们可以由多种类型的元素构建，包括其他结构体。考虑以下结构体定义：

```c
struct Card
{
    char *face;
    char *suit;
}; // end struct Card
```

关键字 **struct** 引入了结构体 Card 的定义。标识符 Card 是 *结构体名称*，在 C++ 中用于声明该 *结构体类型* 的变量（在 C 中，上述结构体的类型名是 `struct Card`）。在此示例中，结构体类型是 Card。在结构体定义的花括号内声明的数据（以及可能的函数——与类一样）是结构体的*成员*。同一结构体的成员必须具有唯一名称，但两个不同的结构体可以包含相同名称的成员而不会冲突。每个结构体定义都必须以分号结尾。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_755_0.png)

**常见编程错误 19.1**

> 忘记结构体定义末尾的分号是语法错误。

Card 的定义包含两个 `char *` 类型的成员——face 和 suit。结构体成员可以是基本数据类型（如 int、double 等）的变量，也可以是聚合类型，如数组、其他结构体或类。单个结构体定义中的数据成员可以是多种数据类型。例如，Employee 结构体可能包含用于名字和姓氏的字符串成员、用于员工年龄的 int 成员、包含 'M' 或 'F' 表示员工性别的 char 成员、用于员工小时工资的 double 成员等等。

结构体不能包含自身的实例。例如，不能在结构体 Card 的定义中声明 Card 类型的结构体变量。但是，可以包含指向 Card 结构体的指针。包含指向同一结构体类型的指针成员的结构体称为*自引用结构体*。

Card 结构体定义不会在内存中预留任何空间；相反，它创建了一个用于声明结构体变量的新数据类型。结构体变量的声明方式与其他类型的变量类似。以下声明

```c
Card oneCard;
Card deck[ 52 ];
Card *cardPtr;
```

声明 `oneCard` 为 Card 类型的结构体变量，`deck` 为具有 52 个 Card 类型元素的数组，`cardPtr` 为指向 Card 结构体的指针。也可以通过在结构体定义的右花括号和结束结构体定义的分号之间放置逗号分隔的变量名列表来声明给定结构体类型的变量。例如，上述声明可以合并到 Card 结构体定义中，如下所示：

```c
struct Card
{
    char *face;
    char *suit;
} oneCard, deck[ 52 ], *cardPtr;
```

