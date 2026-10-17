
```
typedef float dollars;
using money = float;
```

在之前的声明中，新类型 `dollars` 可以与类型 `float` 互换。同样，新的别名 `money` 也可以与类型 `float` 互换。演示 `typedef` 与 `struct` 的过时用法并无意义，因此让我们转向 C++ 中最常用的用户定义类型：`class`。

### class

最简单形式的 `class` 几乎可以像 `struct` 一样用于将相关数据封装到一个数据类型中。在第 5 章“深入探索类”中，我们将看到 `class` 通常用于将相关函数与新数据类型结合在一起。将数据和该数据的行为结合是封装的基础。现在，让我们看看最简单形式的 `class`，就像 `struct` 一样：

`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter01/Chp1-Ex9.cpp`

```cpp
#include <iostream>
using namespace std; // 我们很快会限制命名空间
class Student {
public:
    string name;
    float semesterGrades[5];
    float gpa;
};
int main() {
    Student s1;
    s1.name = "George Katz";
    s1.semesterGrades[0] = 3.0;
    s1.semesterGrades[1] = 4.0;
    s1.gpa = 3.5;
    cout << s1.name << " has GPA: " << s1.gpa << endl;
    return 0;
}
```

注意，之前的代码与 `struct` 中使用的非常相似。主要区别是使用了 `class` 关键字而不是 `struct`，并且在类定义的开头添加了访问标识符 `public:`（更多内容请见第 5 章“深入探索类”）。在风格上，数据类型首字母大写（如 `Student`）是类的典型做法。我们将在后续介绍特性。

### enum 和强类型枚举

传统的枚举类型可用于以具记忆点的方式表示整数列表。除非另初始化，枚举中的整数值从零开始，并在整个列表中递增 1。两个枚举类型不能使用相同的枚举符名称。

强类型枚举改进了传统的枚举。强类型枚举默认表示整数列表，但也可以用于表示整数类型，如 `int`、`short int`、`long int`、`char` 或 `bool`。枚举符不会导出到周围作用域，枚举符可以在类型之间复用。强类型枚举允许对其进行前声明（允许在枚举符声明之前作为函数参数）。

让我们来看传统枚举和强类型枚举的示例：

`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter01/Chp1-Ex10.cpp`

```cpp
#include <iostream>
using namespace std; // 我们很快会限制命名空间
// 传统的枚举
enum day {Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday};
enum workDay {Mon = 1, Tues, Wed, Thurs, Fri};
// 强类型枚举可以是 struct 或 class
enum struct Holiday {Diwali, Hanukkah, ThreeKings,
WinterSolstice, StLucia, StNicholas, Christmas, Kwanzaa};
enum class Holiday : short int {NewYear = 1, MLK, Memorial,
Independence, Labor, Thanksgiving};
int main() {
    day birthday = Monday;
    workDay payday = Fri;
    Holiday myTradition = Holiday::StNicholas;
    Holiday favorite = Holiday::NewYear;
    cout << "Birthday is " << birthday << endl;
    cout << "Payday is " << payday << endl;
    cout << "Traditional Winter holiday is " <<
          static_cast<int>(myTradition) << endl;
    cout << "Favorite holiday is " <<
          static_cast<short int>(favorite) << endl;
    return 0;
}
```

在在上一个示例中，传统的枚举类型 `day` 的值为 0 到 6，从周日开始。传统的枚举类型 `workDay` 的值为 1 到 5，从周一开始。请注意，这里显式地使用 `Mon = 1` 作为枚举类型中的第一个项，这被覆盖了默认的起始值 0。有趣的是，我们可能在两个枚举类型之间重复使用枚举成员。因此，你会发现 `Mon` 在 `workDay` 中被用枚举成员，因为 `Monday` 已经在枚举类型 `day` 中用过了。现在，当我们创建如 `birthday` 或 `payday` 等变量时，可以使用具有意义的枚举类型来初始化或赋值，例如 `Monday` 或 `Fri`。尽管这些枚举成员在代码中很有意义，但请注意，当对其进行操作或打印时，它们将是其对应的整数值。

继续考虑上一个示例中的强类型枚举，`WinterHoliday` 的枚举是使用结构体（struct）定义的。枚举成员的默认值是整数，从值 0 开始（与传统枚举相同）。然而，注意 `Holiday` 的枚举指定了成员类型为 `short int`。此外，我们选择让枚举类型中的第一个项从值 1 开始而不是 0。注意，当我们打印强类型枚举成员时，我们必须使用 `static_cast` 将类型转换为枚举成员的类型。这是因为插入运算符（insertion operator）知道如何处理选定的类型，但这些类型不包括强类型枚举；因此，我们将枚举类型强制转换为插入运算符可以理解的类型。

现在我们已经回顾了 C++ 中的简单用户自定义类型，包括 `struct`、`typedef`（以及使用别名）、`class` 和 `enum`，我们准备好继续回顾下一个语言基础要素：命名空间（namespace）。

## 回顾命名空间基础

C++ 引入命名空间工具是为了为应用程序添加一个全局作用域之外的作用域级。此功能可以允许使用两个或多个库，而不必担心它们可能包含重复的数据类型、函数或标识符。程序员需要在应用程序的每个相关部分使用 `using` 关键字来激活所需的命名空间。程序员也可以创建自己的命名空间（通常用于用于创建可重用的库代码），并根据情况激活每个命名空间。在之前的示例中，我们看到了对 `std` 命名空间的简单用法，以包含 `cin` 和 `cout`，它们是 `istream` 和 `ostream` 的实例（其定义在 `<iostream>` 中）。让我们回顾一下我们如何自己创建命名空间：

`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter01/Ch1-Ex11.cpp`

```cpp
#include <iostream>
// using namespace std; // 不要打开整个 std 命名空间
using std::cout; // 取反，激活单个元素
using std::endl; // 根据需在命名空间内
namespace DataTypes
{
    int total;
    class LinkList
    { // 完整的类定义 ...
    };
    class Stack
    { // 完整的类定义 ...
    };
}
namespace AbstractDataTypes
{
    class Stack
{ // 完整的类定义 ...
};
class Queue
{ // 完整的类描述 ...
};
// 向 AbstractDataTypes 命名空间添加条目
namespace AbstractDataTypes
{
  int total;
  class Tree
  { // 完整的类定义 ...
  };
}
int main()
{
  using namespace AbstractDataTypes; // 激活命名空间
  using DataTypes::LinkedList; // 仅激活 LinkedList
  LinkedList listl; // LinkedList 在 DataTypes 中找到
  Stack stackl;
  total = 5; // 来自激活的 AbstractDataTypes 的 total
  DataTypes::total = 8;// 指定非激活成员，total
  cout << "total" << total << "\n";
  cout << "DataTypes::total" << DataTypes::total;
  cout << endl;
  return 0;
}
```

在上述代码的第二行（被注释掉的行）中，我们注意到使用 `using` 关键字表示我们想要使用或激活 `std` 命名空间。理想情况下，在接下来的两行代码中，我们可以只激活标准命名空间中我们需要的元素，例如 `std::cout` 或 `std::endl`。我们可以利用 `using` 打开现有的库（或这些库中的单个元素），这些库可能包含用的类；该关键字用于激活给定库可能所属的命名空间。代码的后续部分，使用 `namespace` 关键字调用了一个用户指定的命名空间 `DataTypes`。在这个可见的命名空间内存在一个变量 `total` 和两个类定义：`LinkList` 和 `Stack`。紧接着这个命名空间，创建了第二个命名空间 `AbstractDataTypes`，它包含了两个类定义：`Stack` 和 `Queue`。此外，通过第二次命名空间定义增加了 `AbstractDataTypes` 命名空间，其中添加了一个变量 `total` 和一个 `Tree` 类定义。

在 `main()` 函数中，首先用 `using` 关键字打开 `AbstractDataTypes` 命名空间。这激活了该命名空间中的所有名称。接下来，`using` 关键字与作用域解析运算符 (`::`) 结合，仅激活 `DataTypes` 命名空间中的 `LinkList` 类定义。如果 `AbstractDataType` 命名空间中也有 `LinkList` 类，那么初始可见的 `LinkList` 将被 `DataTypes::LinkList` 的激活隐藏。

接着声明了一个 `LinkList` 类型的变量，其定义来自 `DataTypes` 命名空间。接着声明一个 `Stack` 类型的变量；虽然两个命名空间都有 `Stack` 类定义，但并没有歧义，因为只激活了一个 `Stack`。接下来，我们可以使用 `cin` 读取到 `total` 中，它来自 `AbstractDataTypes` 命名空间。最后，我们使用作用域解析运算符显式读取到 `DataTypes::total`，这是一个会被隐藏的变量。需要注意的一点：如果两个或多个命名空间包含该标识符，最后一个打开的将占据主导。

只激活我们希望使用的命名空间的元素被认为是良好的做法。从上述示例中，我们可以看到否则可能出现的潜在歧义。

## 总结

在本章中，我们回顾了核心 C++ 语法和非面向对象语言特性，以刷新你现有的技能集。这些特性包括基础语言语法、带有 `<iostream>` 的基础 I/O、控制结构/语句/循环、运算符基础、函数基础、简单用户自定义类型以及命名空间。最重要的是，你现在准备好进入下一章了，在其中我们将通过额外的语言基础要素来扩展其中的一些思想，例如 `const` 修饰的变量、理解和使用原型声明（包括默认值）以及函数重载。

下一章的思想开始更接近我们面向对象（OO）编程的目标，因为随着我们深入学习语言，这些许多聚合技能经常被使用且非常重要。记住，在 C++ 中，你可以做任何事情，无论你是否是有意为之。语言具有巨大的力量，为其许多细微差别和特性建立坚实的基础至关重要。在接下来的几章中，将用一系列非面向对象的 C++ 技能奠定基础，以便我们以高水平的理解和成功地参与 C++ 中的面向对象编程。

## 问题

- 1. 描述在使用 `flush` 而不是 `endl` 对于清除 `cout` 相关缓冲区有用的情况。
- 2. 一元运算符 `++` 可以作为前增或后增运算符，例如 `i++` 或 `++i`。你能描述在什么情况下，对 `++` 选择前增或后增会有不同的结果吗？
- 3. 使用 `struct` 或 `class` 创建一个简单的程序为 `Book` 创建用户自定义类型。添加标题、作者和页数的数据成员。创建两个 `Book` 类型的变量并使用点运算符 `.` 填充每个实例的数据成员。使用 `iostreams` 提示用户输入值，并在完成后打印每个 `Book` 实例。仅使用本章涵盖的功能。

# 2

## 添加语言必要特性

本章将介绍 C++ 中必要的非面向对象（OO）特性，这些特性是 C++ 面向对象特性的关键构建模块。本章介绍的功能代表了从本书此处开始，你将看到它们是如何平实地被使用的。C++ 是一门充满“灰色地带”的语言；从本章开始，你不仅将精通语言特性，还将掌握语言的细微差别。本章的目标是开始将你的技能从一名普通的 C++ 程序员提升为能够在成功处理语言细微之处的同时创建可维护代码的程序员。

在本章中，我们将涵盖以下主要主题：

- `const` 限定符
- 函数原型
- 函数重载

在本章结束时，你将理解非面向对象的特性，例如 const 限定符、函数原型（包括使用默认值）以及函数重载（包括标准类型转换如何影响重载函数的选择，并可能产生潜在的歧义）。这些看似简单的主题中，许多包含各种有趣的细节和细微差别。这些技能对于顺利进行书中后续章节至关重要。

## 技术要求

可以在以下 GitHub Hub 地址找到找到完整程序示例的在线代码：`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/tree/main/Chapter02`。每个完整程序示例都可以在 GitHub 相应的章节标题（子目录）下找到，文件名与章节号对应，后面紧跟一个破折号，然后是当前章节中的示例编号。例如，第 2 章“添加语言必要特性”中的第一个完整程序可以在上述 GitHub 目录下的 `chapter02` 子目录中名为 `chap2-Ex1.cpp` 的文件中。

本章的 CiA 视频可以在此处查看：`https://bit.ly/3CM65dF`。

## 使用 const 和 constexpr 限定符

在本节中，我们将为变量添加 `const` 和 `constexpr` 限定符，并讨论如何将它们作为输入参数和返回值添加到函数中。随着对 C++ 语言的深入学习，这些限定符将被频繁使用。`const` 和 `constexpr` 的使用允许值被初始化，但不再被修改。通过使用 `const` 或 `constexpr`，函数可以声明它们不会修改输入参数，或者其返回值仅可以被捕获（但不能修改）。这些限定符有助于使 C++ 成为一种更安全的语言。让我们来看看 `const` 和 `constexpr` 的实际应用。

### const 和 constexpr 变量

带有 `const` 限定符的变量是必须初始化且不能赋予新值的变量。将 `const` 与变量结合使用似乎是一个悖论——`const` 意味着不改变，而变量的概念本质上是不同的值。尽管如此，拥有一个强类型检查且其唯一值可以在运行时确定的变量是有用的。`const` 关键字被添加到变量声明中。

同样，使用 `constexpr` 声明的变量是带有常量限定符的变量——即一个可以初始化且从不被赋予新值的变量。只要可以使用，使用 `constexpr` 正变得越来越首选。

在某些情况下，常量的值在编译时是不可知的。例如，使用用户输入或函数的返回值来初始化常量。`const` 变量很容易在运行时初始化。`constexpr` 通常经常（但并非总是）可以在运行时初始化。我们将在示例中考虑各种场景。

让我们考虑以下程序中的几个示例。为了更具针对性地解释，我们将该程序分为两个部分，但完整的程序示例可以在以下链接完整找到：

`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/blob/main/Chapter02/Chp2-Ex1.cpp`

```cpp
#include <iostream>
#include <iomanip>
#include <string>; // 虽然我们更倾向于使用 std::string;
// char [ ] 在下面的用例中可以演示 const 限定符
using std::cout; // 优于：using namespace std;
```
