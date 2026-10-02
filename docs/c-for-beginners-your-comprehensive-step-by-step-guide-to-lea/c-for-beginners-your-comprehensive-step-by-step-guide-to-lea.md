# C++ 初学者指南：全面分步学习 C++ 指南







![](img/574a0c5ef35f7474b7a0f010b8a2211a_0_0.png)





## 引言

C++ 是一种高性能编程语言，广泛应用于各种应用中，例如操作系统、网页浏览器和视频游戏。它由 Bjarne Stroustrup 于 1979 年开发，是 C 编程语言的扩展，增加了面向对象特性和其他增强功能。

C++ 是一种静态类型、编译型语言，这意味着它比 Python 或 JavaScript 等动态类型语言更高效。它也是一种非常富有表现力的语言，允许程序员编写既高效又易于阅读的代码。

C++ 的关键特性之一是对面向对象编程（OOP）的支持。在 OOP 中，数据和行为被封装在“对象”中，这些对象可用于建模现实世界概念，并通过方法相互交互。C++ 也支持过程式编程，这是一种更传统的编程风格，专注于编写函数来执行特定任务。

C++ 是一种功能强大且灵活的语言，但对初学者来说也可能复杂且难以学习。它需要对计算机科学概念有良好的理解，以及对变量、数据类型、循环和控制结构等编程概念的坚实基础。然而，一旦你对这些概念有牢固的理解，C++ 将是一种非常有回报的学习和使用语言。

## 第一章
### 基本概念
### C++ 类型系统

在 C++ 中，数据使用各种数据类型进行存储和操作。这些数据类型决定了变量使用的内存大小和布局，以及可以对其执行的操作集合。

C++ 拥有丰富的类型系统，包括内置类型和用户定义类型。

内置类型包括：

- 整数类型：这些表示整数，包括 `char`、`short`、`int`、`long` 和 `long long`。每种类型大小不同，`char` 是最小的，`long long` 是最大的。
- 浮点类型：这些表示带小数部分数字，包括 `float`、`double` 和 `long double`。这些类型也有不同的大小，`float` 是最小的，`long double` 是最大的。
- 布尔类型：这表示真/假值，由 `bool` 类型表示。
- 字符类型：这些表示单个字符，包括 `char` 和 `wchar_t`。`char` 用于 ASCII 字符，`wchar_t` 用于宽字符，可表示各种不同字母表的字符。

C++ 中的用户定义类型包括：

- 类：类是一种用户定义的数据类型，允许你定义自己的数据字段和方法。
- 结构体：结构体与类类似，但数据字段和方法默认是公开的。
- 枚举：枚举是一种用户定义的类型，由一组命名常量组成。
- Typedef：`typedef` 关键字允许你为现有数据类型定义一个新名称。这可用于为复杂类型创建更易读或更具表现力的名称。

C++ 还支持类型转换，允许你将值从一种数据类型转换为另一种数据类型。这在处理需要一起使用不同数据类型时很有用，但使用类型转换时必须谨慎，因为如果使用不当，可能导致精度丢失或其他意外行为。

### 作用域

在 C++ 中，变量的作用域是指变量在程序中可见或可访问的部分。变量的作用域由其在程序中的声明位置决定。

C++ 中主要有两种作用域：局部作用域和全局作用域。

局部变量是在函数或代码块内声明的变量。局部变量仅在声明它的函数或块内可见，并且只能从声明点访问到块结束。当函数或块结束时，局部变量被销毁，不再可访问。

全局变量是在任何函数或代码块之外声明的变量。全局变量在整个程序中都可见，可以从任何函数或代码块访问。然而，通常认为良好的编程实践是尽量减少全局变量的使用，因为它们会使程序更难以理解和维护。

C++ 还支持嵌套作用域，其中一个代码块定义在另一个代码块内。在这种情况下，在内部块中声明的变量仅在该块内可见，但也可能从外部块访问。

变量的作用域是 C++ 中的一个重要概念，因为它决定了变量在程序中的可见性和可访问性。理解变量的作用域对于编写高效且可维护的代码至关重要。

### 头文件

在 C++ 中，头文件是一个包含可在 C++ 程序中使用的函数、变量和其他构造的声明的文件。头文件通常以 .h 后缀表示，并使用 #include 指令包含在 C++ 源文件中。

头文件在 C++ 中用于多种目的。它们可用于声明在另一个源文件中定义并可在多个文件中使用的函数和变量，而无需代码重复。它们也可用于声明在库中实现并可在程序中使用而无需将库链接到程序中的函数和变量。

头文件还可用于定义宏，即由预处理器替换为其对应展开形式的短代码片段。宏常用于定义需要在程序多处使用的常量和其他值。

使用头文件的主要优点之一是它使代码更易于组织和重用。通过将声明与定义分离并将其放在单独的头文件中，可以在多个程序中使用相同的代码，而无需复制粘贴。这使得维护和更新代码变得更容易，因为更改只需在一个位置进行。

标准 C++ 头文件的一些示例包括 <iostream>，它提供用于读取和写入数据的输入输出流，以及 <string>，它提供用于处理字符串的函数和类。C++ 标准库中还有许多其他头文件，以及第三方库中提供的头文件，为各种任务提供广泛的功能。

### 翻译单元和链接

在 C++ 中，翻译单元是一个源文件及其包含的所有头文件，以及这些头文件包含的头文件，等等。将翻译单元转换为可执行程序的过程称为编译。

在编译期间，预处理器处理翻译单元中的 #include 指令，将包含头文件的内容插入到源文件中。然后，将生成的展开源文件传递给编译器，将其翻译成目标代码。

目标代码是计算机可执行的程序的机器可读表示。然而，目标代码并不是操作系统可以直接执行的形式。相反，它必须与其他目标代码文件和库结合起来创建可执行程序。此过程称为链接。

C++ 中有两种链接：内部链接和外部链接。

内部链接是指仅在单个翻译单元内可见的符号（变量和函数）。这些符号通常用于不打算从其他翻译单元访问的实现细节。通过使用 static 关键字声明符号来实现内部链接。

外部链接是指对多个翻译单元可见的符号。这些符号通常用于定义 intended 在多个翻译单元之间共享的函数和变量。外部链接是未使用 static 关键字声明的符号的默认值。

链接是 C++ 中的一个重要概念，因为它决定了符号在程序中的可见性和可访问性。理解链接对于编写高效且可维护的代码至关重要，特别是在处理由多个源文件和库组成的大型程序时。

### main 函数和命令行参数

在 C++ 中，main 函数是程序的入口点。它是操作系统在程序启动时调用的函数，它决定了程序其余部分的控制流。

main 函数具有特定的语法和返回类型。在 C++ 中，它可以以以下方式之一声明：

```
int main()
{
    // code goes here
    return 0;
}

int main(int argc, char* argv[])
{
    // code goes here
    return 0;
}
```

第一个版本的 main 不接受参数并返回 int 值。第二个版本接受两个参数：argc 和 argv。argc 是一个 int 值，表示传递给程序的命令行参数的数量，



and argv 是一个 char* 值的数组，保存实际的参数。

命令行参数是程序从命令行启动时传递给程序的值。它们通常用于向程序传递配置选项或其他输入。

例如，考虑以下打印其接收到的命令行参数的程序：

```
#include <iostream>

int main(int argc, char* argv[])
{
    std::cout << "Number of arguments: " << argc << std::endl;
    for (int i = 0; i < argc; i++)
    {
        std::cout << "Argument " << i << ": " << argv[i] << std::endl;
    }
    return 0;
}
```

要运行此程序并向其传递一些命令行参数，你将使用如下命令：

```
./myprogram arg1 arg2 arg3
```

这将打印以下输出：

```
Number of arguments: 4
Argument 0: ./myprogram
Argument 1: arg1
Argument 2: arg2
Argument 3: arg3
```

正如你所见，第一个参数（ argv[0] ）是程序本身的名称，其余参数是命令行上传递的参数。

命令行参数对于向程序提供输入或配置其行为非常有用。它们是许多命令行程序的常见功能，并且在 C++ 中使用起来很容易。

### 程序终止

在 C++ 中，程序在 main 函数返回或调用 exit 函数时终止。

main 函数是 C++ 程序的入口点，并决定其余程序的控制流。当 main 函数返回时，程序终止。main 的返回值是程序的退出状态，可由操作系统或其他程序用来确定程序的结果。返回值 0 通常表示程序成功运行，而非零值通常表示错误。

例如，以下 main 函数返回 0 以表示程序成功运行：

```
int main()
{
    // code goes here
    return 0;
}
```

exit 函数是 cstdlib 库中定义的一个函数，允许程序立即终止。它接受一个 int 值作为参数，即程序的退出状态。exit 函数可以从程序中的任何位置调用，并将导致程序立即终止，即使还有其他函数或代码块尚未完成。

例如，以下代码调用 exit 函数以退出状态 1 终止程序：

```
#include <cstdlib>

int main()
{
    // code goes here
    exit(1);
}
```

通常认为良好的编程实践是使用 return 终止 main 函数，并将 exit 函数保留用于紧急情况或特殊情况。

了解程序如何终止对于编写高效且可维护的代码很重要，因为它允许你在程序退出前确保所有必要的清理任务都已执行。

### 左值和右值

在 C++ 中，左值（lvalue，意为“左值”）是指向内存位置的表达式，并且可以出现在赋值的左侧。右值（rvalue，意为“右值”）是指不指向内存位置的表达式，并且不能出现在赋值的左侧。

以下是左值和右值的一些示例：

```
int x;        // x 是左值（一个变量）
x = 5;        // x 是左值（出现在赋值的左侧）
*p = 7;       // *p 是左值（解引用左值会产生另一个左值）

5;            // 5 是右值（一个常量）
x + y;        // x + y 是右值（一个算术表达式）
*p + 5;       // *p + 5 是右值（解引用左值并加上一个常量）
```

在 C++ 中，左值具有特定类型，可用于引用存储在内存中的对象。另一方面，右值没有特定类型，不能用于引用存储在内存中的对象。

左值和右值是 C++ 中的一个重要概念，因为它们决定了可以对表达式执行的操作集。例如，可以对左值进行赋值，而不能对右值进行赋值。左值也可以被解引用，而右值不能。理解左值和右值之间的区别对于编写正确且高效的 C++ 代码至关重要。

### 临时对象

在 C++ 中，临时对象是为保存表达式的结果而创建的对象，并在表达式求值后立即销毁。临时对象也称为“右值”，因为它们通常由右值表达式创建（不引用内存位置且不能出现在赋值左侧的表达式）。

在 C++ 的各种情况下会创建临时对象。例如，当右值传递给函数或当右值用作赋值的右操作数时，就会创建临时对象。

以下是 C++ 中创建临时对象的一些示例：

```
int x = 5 + 6;      // 创建一个临时对象来保存 5 + 6 的结果

void foo(int& x)    // x 是对 int 的引用
{
    // code goes here
}

foo(5 + 6);         // 创建一个临时对象来保存 5 + 6 的结果并传递给 foo

int x = 5;
int y = x + 6;      // 创建一个临时对象来保存 x + 6 的结果

struct Point
{
    int x, y;
};

Point p = Point(1, 2); // 创建一个临时对象来保存 Point 构造函数的結果
```

临时对象通常用于避免不必要的拷贝或利用移动语义，这允许对象的內容被“移动”而不是拷贝。

了解 C++ 中的临时对象很重要，因为它们的行为可能与普通对象不同，如果使用不当会导致意外结果。例如，通常不允许将非常量引用绑定到临时对象，因为临时对象会在引用超出作用域后立即被销毁。理解临时对象的行为对于编写正确且高效的 C++ 代码至关重要。

### 对齐

在 C++ 中，对齐是指数据在内存中的排列方式。对齐会影响程序的性能和效率，因为它会影响数据访问的速度和使用的内存量。
C++ 提供了多种语言特性和库函数来控制对齐。

一种控制 C++ 中对齐的方法是通过使用 alignas 和 alignof 关键字。alignas 关键字可用于指定变量或数据类型的对齐方式，而 alignof 关键字可用于确定变量或数据类型的对齐方式。

例如，以下代码定义了一个对齐为 16 字节的变量 x：

```
alignas(16) int x;
```

alignof 关键字可用于确定变量或数据类型的对齐方式，如以下示例所示：

```
int x;
std::cout << "Alignment of x: " << alignof(x) << std::endl;
```

控制 C++ 中对齐的另一种方法是通过使用 <type_traits> 头文件中的 std::aligned_storage 和 std::aligned_union 类型。这些类型提供了一种以可移植且高效的方式以指定对齐方式存储数据的方法。

例如，以下代码定义了一个变量 storage，可用于以 16 字节的对齐方式存储类型 T 的对象：

```
#include <type_traits>

template <typename T>
using aligned_storage_t = std::aligned_storage<sizeof(T), alignof(T)>;

aligned_storage_t<int> storage;
```

理解对齐对于编写高效且高性能的 C++ 代码很重要，尤其是在处理大型数据结构或与低级硬件或系统交互时。适当的对齐可以通过减少内存访问次数来显著提高程序的性能，并且

### 平凡、标准布局和 POD 类型

在 C++ 中，如果类型具有平凡的默认构造函数、平凡的析构函数，并且没有虚函数或虚基类，则该类型被视为平凡的


classes.

如果一个类型满足以下条件，则认为该类型是标准布局类型：

- 它是一个平凡类型。
- 它没有非静态数据成员是非标准布局类类型（或此类类型的数组）。
- 它没有虚函数也没有虚基类。

如果一个类型满足以下条件，则认为该类型是 POD（Plain Old Data，普通旧数据）类型：

- 它是一个标准布局类型。
- 它没有非静态数据成员是非 POD 类类型（或此类类型的数组）。
- 它没有用户定义的拷贝赋值运算符也没有用户定义析构函数。

平凡、标准布局和 POD 类型是 C++ 中的重要概念，因为它们具有程序员可以依赖的特定行为和属性。例如，平凡类型可以用 memset 置零并使用 memcpy 复制，而标准布局类型可以传递给 C 函数并可用于实现联合类型。POD 类型可用于实现 C 风格的结构体，并可以用花括号括起来的初始化列表进行初始化。

理解平凡、标准布局和 POD 类型的行为和属性对于编写高效且正确的 C++ 代码非常重要，尤其是在处理低级硬件或系统时，或在与 C 代码交互时。

### what is Value types

在 C++ 中，值类型是一种保存值且通常存储在栈上的内存中的类型。值类型也被称为“基本类型”，因为它们是语言提供的最基本类型。

标准 C++ 库提供了几种值类型，包括以下：

- bool : 一个布尔类型，表示 true 或 false。
- char : 一个字符类型，表示单个字符。
- int , short , long , 和 long long : 各种大小的整数类型。
- float 和 double : 各种精度的浮点类型。

值类型通常用于保存简单数据，例如数字、字符和布尔值。它们使用高效，因为它们不需要任何额外的内存管理，并且直接存储在栈上的内存中。

以下是 C++ 中使用值类型的示例：

```
int x = 5;      // x is a value of type int
char c = 'a';   // c is a value of type char
bool b = true;  // b is a value of type bool

float f = 3.14; // f is a value of type float
double d = 1.23456789; // d is a value of type double
```

值类型是 C++ 中的一个重要概念，因为它们构成了语言中许多其他类型的基础。理解值类型的工作原理以及如何使用它们对于编写高效且正确的 C++ 代码至关重要。

### Type conversions and type safety

在 C++ 中，类型转换是将值从一种类型转换为另一种类型的过程。在 C++ 中执行类型转换有几种方法，包括显式类型转换、函数重载和类型转换运算符。

显式类型转换是将值从一种类型显式转换为另一种类型，使用 static_cast 运算符的过程。这通常用于将值从基类型转换为派生类型，或从派生类型转换为基类型。

例如，以下代码使用显式类型转换将 double 值转换为 int 值：

```
double x = 3.14;
int y = static_cast<int>(x); // y is now 3
```

函数重载是定义多个同名但参数类型不同的函数的过程。这允许同一个函数根据其参数的类型执行不同的操作。

例如，以下代码定义了一个 abs 函数，可用于计算 int 、 float 或 double 的绝对值：

```
int abs(int x)
{
    return x < 0 ? -x : x;
}

float abs(float x)
{
    return x < 0.0f ? -x : x;
}

double abs(
```

### Standard conversions

在 C++ 中，标准转换是由编译器执行的预定义隐式类型转换。标准转换是一组预定义规则，规定不同类型的值如何相互转换。

C++ 中有三种标准转换：

1. Lvalue-to-rvalue conversion：此转换应用于左值（引用内存位置的表达式）以生成右值（不引用内存位置的表达式）。此转换通常应用于对象以允许它们用作右值，例如当它们作为参数传递给函数或用作赋值运算符的右操作数时。
2. Array-to-pointer conversion：此转换应用于数组以将它们转换为指向其第一个元素的指针。此转换通常在数组传递给函数或在表达式中使用时应用。
3. Function-to-pointer conversion：此转换应用于函数名以将它们转换为指向函数的指针。此转换通常在函数名传递给函数或在表达式中使用时应用。

标准转换由编译器自动应用，程序员无需显式指定它们。它们是 C++ 类型系统的重要组成部分，因为它们允许不同类型的值在许多上下文中互换使用。理解标准转换的工作原理对于编写正确且高效的 C++ 代码至关重要。

## Chapter II

### built-in types

### Built-in types

在 C++ 中，内置类型是一组由语言提供并由编译器直接实现预定义类型。内置类型也被称为“基本类型”或“值类型”，因为它们是语言提供的最基本类型，通常存储在栈上的内存中。

C++ 标准库提供了几种内置类型，包括以下：

- bool : 一个布尔类型，表示 true 或 false。
- char : 一个字符类型，表示单个字符。
- int , short , long , 和 long long : 各种大小的整数类型。
- float 和 double : 各种精度的浮点类型。
- void : 一种特殊类型，表示值的缺失。

内置类型是 C++ 中的一个重要概念，因为它们构成了语言中许多其他类型的基础。理解内置类型的工作原理以及如何使用它们对于编写高效且正确的 C++ 代码至关重要。

以下是 C++ 中使用内置类型的示例：

```
int x = 5;      // x is a value of type int
char c = 'a';   // c is a value of type char
bool b = true;  // b is a value of type bool

float f = 3.14; // f is a value of type float
double d = 1.23456789; // d is a value of type double
```

### Data type ranges

在 C++ 中，数据类型的范围是它可以表示的值的集合。数据类型的范围由其大小和编码方式决定。

C++ 标准库提供了几种内置类型，每种都有其特定的值范围。以下表格显示了 C++ 中一些常见内置类型的范围：

| Type | Size (bytes) | Minimum value | Maximum value |
|---|---|---|---|
| bool | 1 | false | true |
| char | 1 | -128 | 127 |
| wchar_t | 2 or 4 | implementation-defined | implementation-defined |
| char16_t | 2 | 0 | 65535 |
| char32_t | 4 | 0 | 4294967295 |
| short | 2 | -32768 | 32767 |
| int | 4 | -2147483648 | 2147483647 |
| long | 4 or 8 | implementation-defined | implementation-defined |
| long long | 8 | -9223372036854775808 | 9223372036854775807 |
| float | 4 | 1.17549e-38 | 3.40282e+38 |
| double | 8 | 2.22507e-308 | 1.79769e+308 |
| long double | 8 or 10 or 16 | implementation-defined | implementation-defined |

在使用 C++ 时，了解数据类型的范围很重要，因为使用超出其范围的值可能导致未定义行为。了解数据类型的范围对于选择给定任务的适当类型也很重要，因为使用范围更大的类型可能会带来更好的性能或更准确的结果。

### nullptr

在 C++ 中，`nullptr` 是一个表示空指针值的特殊关键字。它在 C++11 中引入，作为使用整数常量 `0` 或宏 `NULL` 表示空指针更安全、更明确的方式。
`nullptr` 的类型为 `std::nullptr_t`，这是一种特殊类型，可以隐式转换为任何指针类型。这允许 `nullptr` 在期望指针的各种上下文中使用，例如初始化指针时或将指针传递给函数时。





以下是使用 `nullptr` 在 C++ 中的示例：

```
int* p = nullptr; // p is a null pointer

void foo(int* p)
{
    // code goes here
}

foo(nullptr); // pass a null pointer to foo
```

使用 `nullptr` 而不是 `0` 或 `NULL` 有几个优点。它更明确且更易读，因为它清楚地表明正在使用空指针。它也更安全，因为它防止了指针和整数之间意外的转换，这可能导致未定义行为。

`nullptr` 是 C++ 中的一个重要概念，特别是在处理指针和可空值时。了解如何使用 `nullptr` 以及它与 `0` 和 `NULL` 的区别对于编写正确且安全的 C++ 代码至关重要。

### nullptr

在 C++ 中，`nullptr` 是一个特殊的关键字，表示空指针值。它是在 C++11 中引入的，比使用整数常量 `0` 或宏 `NULL` 来表示空指针更安全、更明确的方式。

`nullptr` 的类型是 `std::nullptr_t`，这是一种特殊类型，可以隐式转换为任何指针类型。这使得 `nullptr` 可以在期望指针的各种上下文中使用，例如初始化指针时或将指针传递给函数时。

以下是使用 `nullptr` 在 C++ 中的示例：

```
int* p = nullptr; // p is a null pointer

void foo(int* p)
{
    // code goes here
}

foo(nullptr); // pass a null pointer to foo
```

使用 `nullptr` 而不是 `0` 或 `NULL` 有几个优点。它更明确且更易读，因为它清楚地表明正在使用空指针。它也更安全，因为它防止了指针和整数之间意外的转换，这可能导致未定义行为。

nullptr 是 C++ 中的一个重要概念，特别是在处理指针和可空值时。了解如何使用 nullptr 以及它与 0 和 NULL 的区别对于编写正确且安全的 C++ 代码至关重要。

### bool

在 C++ 中，bool 是一个内置数据类型，表示布尔值，可以是 true 或 false。它用于表示条件或表达式的真假。

以下是如何在 C++ 中使用 bool 数据类型的示例：
#include <iostream>

```
#include <iostream>

int main() {
    bool b1 = true;
    bool b2 = false;

    std::cout << "b1: " << b1 << std::endl;
    std::cout << "b2: " << b2 << std::endl;

    return 0;
}
```

此程序的输出将为：

b1: 1
b2: 0

在 C++ 中，true 通常表示为 1，false 表示为 0。然而，你可以直接在代码中使用值 true 和 false 来表示布尔值。

例如，以下代码也是有效的：

```
#include <iostream>

int main() {
    bool b1 = true;
    bool b2 = false;

    std::cout << "b1: " << b1 << std::endl;
    std::cout << "b2: " << b2 << std::endl;

    if (b1) {
        std::cout << "b1 is true" << std::endl;
    } else {
        std::cout << "b1 is false" << std::endl;
    }

    if (b2) {
        std::cout << "b2 is true" << std::endl;
    } else {
        std::cout << "b2 is false" << std::endl;
    }

    return 0;
}
```

此程序的输出将为：

b1: 1
b2: 0
b1 is true
b2 is false

false

在 C++ 中，false 是一个布尔值，表示 true 的相反。它用于表示条件或表达式的真假。

在 C++ 中，false 通常表示为 0。然而，你可以直接在代码中使用值 false 来表示布尔值。

以下是如何在 C++ 中使用 false 值的示例：

```
#include <iostream>

int main() {
    bool b1 = true;
    bool b2 = false;

    std::cout << "b1: " << b1 << std::endl;
    std::cout << "b2: " << b2 << std::endl;

    if (b1) {
        std::cout << "b1 is true" << std::endl;
    } else {
        std::cout << "b1 is false" << std::endl;
    }

    if (b2) {
        std::cout << "b2 is true" << std::endl;
    } else {
        std::cout << "b2 is false" << std::endl;
    }

    return 0;
}
```

此程序的输出将为：

b1: 1
b2: 0
b1 is true
b2 is false

在此示例中，变量 b2 被赋值为 false，表示为 0。当在 if 语句中测试 b2 的值时，它被认为是 false，并且 else 块中的代码被执行。

true

在 C++ 中，true 是一个布尔值，表示 false 的相反。它用于表示条件或表达式的真假。

在 C++ 中，true 通常表示为 1。然而，你可以直接在代码中使用值 true 来表示布尔值。

以下是如何在 C++ 中使用 true 值的示例：

```
#include <iostream>

int main() {
    bool b1 = true;
    bool b2 = false;

    std::cout << "b1: " << b1 << std::endl;
    std::cout << "b2: " << b2 << std::endl;

    if (b1) {
        std::cout << "b1 is true" << std::endl;
    } else {
        std::cout << "b1 is false" << std::endl;
    }

    if (b2) {
        std::cout << "b2 is true" << std::endl;
    } else {
        std::cout << "b2 is false" << std::endl;
    }

    return 0;
}
```

此程序的输出将为：

b1: 1
b2: 0
b1 is true
b2 is false

在此示例中，变量 b1 被赋值为 true，表示为 1。当在 if 语句中测试 b1 的值时，它被认为是 true，并且 if 块中的代码被执行。

### __m64

__m64 是 C++ 编程语言中的一个类型定义，表示 64 位整数值。它是 Intel C++ 编译器提供的内置数据类型，用于 Intel Streaming SIMD Extensions (SSE) 指令。

__m64 类型可用于以针对 SSE 指令优化的方式存储和操作 64 位整数值。它 intended 用于高性能、多媒体和科学应用中，需要并行处理数据。

以下是如何在 C++ 中使用 __m64 数据类型的示例：

```
#include <iostream>
#include <emmintrin.h> // Required for __m64

int main() {
    __m64 m1 = _mm_set_pi32(1, 2); // Initialize m1 with two 32-bit integers
    __m64 m2 = _mm_set1_pi32(3); // Initialize m2 with a single 32-bit integer

    std::cout << "m1: " << m1 << std::endl;
    std::cout << "m2: " << m2 << std::endl;

    return 0;
}
```

此程序的输出将为：

m1: [1, 2]

m2: [3, 3]

请注意，__m64 数据类型只有在使用 Intel C++ 编译器并且包含 emmintrin.h 头文件时才可用。它不是标准 C++ 数据类型，也不被其他编译器支持。

### __m128

__m128 是 C++ 编程语言中的一个类型定义，表示 128 位浮点值。它是 Intel C++ 编译器提供的内置数据类型，用于 Intel Streaming SIMD Extensions (SSE) 指令。

__m128 类型可用于以针对 SSE 指令优化的方式存储和操作 128 位浮点值。它 intended 用于高性能、多媒体和科学应用中，需要并行处理数据。

以下是如何在 C++ 中使用 __m128 数据类型的示例：

```
#include <iostream>
#include <emmintrin.h> // Required for __m128

int main() {
    __m128 m1 = _mm_set_ps(1.0f, 2.0f, 3.0f, 4.0f); // Initialize m1 with four 32-bit floats
    __m128 m2 = _mm_set1_ps(5.0f); // Initialize m2 with a single 32-bit float

    std::cout << "m1: " << m1 << std::endl;
    std::cout << "m2: " << m2 << std::endl;

    return 0;
}
```

此程序的输出将为：

m1: [1.0, 2.0, 3.0, 4.0]
m2: [5.0, 5.0, 5.0, 5.0]

请注意，__m128 数据类型只有在使用 Intel C++ 编译器并且包含 emmintrin.h 头文件时才可用。它不是标准 C++ 数据类型，也不被其他编译器支持。

### __m128d

__m128d 是 C++ 编程语言中的一个类型定义，表示 128 位浮点值。它是 Intel C++ 编译器提供的内置数据类型，用于 Intel Streaming SIMD Extensions (SSE) 指令。

__m128d 类型可用于以针对 SSE 指令优化的方式存储和操作 128 位浮点值。它 intended 用于高性能、多媒体和科学应用中，需要并行处理数据。

以下是如何在 C++ 中使用 __m128d 数据类型的示例：


```cpp
#include <iostream>
#include <emmintrin.h> // Required for __m128d

int main() {
    __m128d m1 = _mm_set_pd(1.0, 2.0); // Initialize m1 with two 64-bit floats
    __m128d m2 = _mm_set1_pd(3.0); // Initialize m2 with a single 64-bit float

    std::cout << "m1: " << m1 << std::endl;
    std::cout << "m2: " << m2 << std::endl;

    return 0;
}
```

该程序的输出为：

m1: [1.0, 2.0]
m2: [3.0, 3.0]

请注意，__m128d 数据类型仅在使用 Intel C++ 编译器并且包含 emmintrin.h 头文件时可用。它不是标准 C++ 数据类型，也不被其他编译器支持。

### __m128i

__m128i 是 C++ 编程语言中的一种类型定义，表示 128 位整数值。它是 Intel C++ 编译器提供的内置数据类型，用于 Intel 流式 SIMD 扩展指令。

__m128i 类型可用于以针对 SSE 指令优化的方式存储和操作 128 位整数值。它适用于高性能、多媒体和科学应用，在这些应用中数据需要在并行环境下处理。

以下是如何在 C++ 中使用 __m128i 数据类型的示例：

```cpp
#include <iostream>
#include <emmintrin.h> // Required for __m128i

int main() {
    __m128i m1 = _mm_set_epi32(1, 2, 3, 4); // Initialize m1 with four 32-bit integers
    __m128i m2 = _mm_set1_epi32(5); // Initialize m2 with a single 32-bit integer

    std::cout << "m1: " << m1 << std::endl;
    std::cout << "m2: " << m2 << std::endl;

    return 0;
}
```

该程序的输出为：

m1: [1, 2, 3, 4]
m2: [5, 5, 5, 5]

请注意，__m128i 数据类型仅在使用 Intel C++ 编译器并且包含 emmintrin.h 头文件时可用。它不是标准 C++ 数据类型，也不被其他编译器支持。

### __ptr32, __ptr64

__ptr32 和 __ptr64 是 C++ 编程语言中的类型说明符，用于声明具有特定大小的指针。它们由 Microsoft Visual C++ 编译器提供，分别用于 32 位和 64 位应用程序。

__ptr32 说明符声明一个 32 位指针，即占用 4 字节内存的内存地址。这种指针用于 32 位应用程序，通常只能寻址 4 GB 内存。

__ptr64 说明符声明一个 64 位指针，即占用 8 字节内存的内存地址。这种指针用于 64 位应用程序，可以寻址超过 4 GB 内存。

以下是如何在 C++ 中使用 __ptr32 和 __ptr64 类型说明符的示例：

```cpp
#include <iostream>

int main() {
    int x = 10;
    __ptr32 int* p1 = &x; // Declare a 32-bit pointer to an int
    __ptr64 int* p2 = &x; // Declare a 64-bit pointer to an int

    std::cout << "p1: " << p1 << std::endl;
    std::cout << "p2: " << p2 << std::endl;

    return 0;
}
```

该程序的输出取决于系统上指针的大小。在 32 位系统上，输出将为：

p1: 0x0012FF74
p2: 0x0012FF74

在 64 位系统上，输出将为：

p1: 0x00007FF75F4BFF74
p2: 0x00007FF75F4BFF74

请注意，__ptr32 和 __ptr64 类型说明符仅在使用 Microsoft Visual C++ 编译器时可用。它们不是标准 C++ 类型说明符，也不被其他编译器支持。

## Chapter III

### NUMERICAL LIMITS

### Numerical limits

在 C++ 中，<limits> 头文件定义了一组模板和常量，提供有关基本数据类型的范围和精度的信息。这些模板和常量称为数值限制。

数值限制可用于确定给定数据类型可以表示的最小值和最大值，以及数据类型的精度。它们可用于确保程序中使用的值在数据类型可以表示的值范围内。

以下是如何在 C++ 中使用数值限制的示例：

```cpp
int main() {
    std::cout << "Minimum value of int: " << std::numeric_limits<int>::min() << std::endl;
    std::cout << "Maximum value of int: " << std::numeric_limits<int>::max() << std::endl;
    std::cout << "Precision of float: " << std::numeric_limits<float>::digits10 << " decimal digits" << std::endl;
    return 0;
}
```

该程序的输出取决于系统上 C++ 标准库的实现。它可能看起来像这样：

Minimum value of int: -2147483648
Maximum value of int: 2147483647
Precision of float: 6 decimal digits

<limits> 头文件为所有基本数据类型定义了数值限制模板和常量，包括 char、short、int、long、long long、float、double 和 long double。你可以使用这些模板和常量来确定这些数据类型的范围和精度。

### Integer limits

在 C++ 中，<limits> 头文件定义了一组模板和常量，提供有关整数数据类型的范围和精度的信息。这些模板和常量称为整数限制。

整数限制可用于确定整数数据类型，如 char、short、int、long 和 long long，可以表示的最小值和最大值。它们可用于确保程序中使用的值在数据类型可以表示的值范围内。

以下是如何在 C++ 中使用整数限制的示例：

```cpp
#include <iostream>
#include <limits>

int main() {
    std::cout << "Minimum value of char: " <<
(int)std::numeric_limits<char>::min() << std::endl;
    std::cout << "Maximum value of char: " <<
(int)std::numeric_limits<char>::max() << std::endl;
    std::cout << "Minimum value of short: " <<
std::numeric_limits<short>::min() << std::endl;
    std::cout << "Maximum value of short: " <<
std::numeric_limits<short>::max() << std::endl;
    std::cout << "Minimum value of int: " << std::numeric_limits<int>::min() <<
std::endl;
    std::cout << "Maximum value of int: " << std::numeric_limits<int>::max() <<
std::endl;
    std::cout << "Minimum value of long: " << std::numeric_limits<long>::min()
<< std::endl;
    std::cout << "Maximum value of long: " << std::numeric_limits<long>::max()
<< std::endl;
    std::cout << "Minimum value of long long: " << std::numeric_limits<long long>::min() << std::endl;
    std::cout << "Maximum value of long long: " << std::numeric_limits<long long>::max() << std::endl;

    return 0;
}
```

该程序的输出取决于系统上 C++ 标准库的实现。它可能看起来像这样：

```
Minimum value of char: -128
Maximum value of char: 127
Minimum value of short: -32768
Maximum value of short: 32767
Minimum value of int: -2147483648
Maximum value of int: 2147483647
Minimum value of long: -2147483648
Maximum value of long: 2147483647
Minimum value of long long: -9223372036854775808
Maximum value of long
```

### Floating limits

在 C++ 中，<limits> 头文件定义了一组模板和常量，提供有关浮点数据类型的范围和精度的信息。这些模板和常量称为浮点限制。浮点限制可用于确定浮点数据类型，如 float、double 和 long double，可以表示的最小值和最大值。它们还可用于确定这些数据类型的精度，即它们可以表示的小数位数。

以下是如何在 C++ 中使用浮点限制的示例：

```cpp
#include <iostream>
#include <limits>

int main() {
    std::cout << "Minimum value of float: " <<
std::numeric_limits<float>::min() << std::endl;
    std::cout << "Maximum value of float: " <<
std::numeric_limits<float>::max() << std::endl;
    std::cout << "Precision of float: " << std::numeric_limits<float>::digits10
<< " decimal digits" << std::endl;
    std::cout << "Minimum value of double: " <<
std::numeric_limits<double>::min() << std::endl;
    std::cout << "Maximum value of double: " <<
std::numeric_limits<double>::max() << std::endl;
    std::cout << "Precision of double: " <<
std::numeric_limits<double>::digits10 << " decimal digits" <<
```




## 第四章

### 声明和定义

在 C++ 中，声明和定义是两个不同的概念，它们指的是变量、函数和其他实体在程序中被引入和使用的方式。

声明是一个语句，它引入一个实体并指定其类型、名称和其他属性。它不会分配任何内存或执行任何代码。声明可以使用 extern 关键字进行，该关键字表示实体在另一个翻译单元中定义。

定义是一个语句，它通过分配内存和执行代码来创建实体。它必须包含声明，并且还可以包含其他详细信息，例如初始值或函数体。定义必须在仅一个翻译单元中进行，但它可以使用 extern 关键字在多个翻译单元中声明。

以下是 C++ 中声明和定义的示例：

// Declare a global variable
extern int x;

int main() {
    // Define a local variable
    int y = 10;

    // Declare and define a function
    int sum(int a, int b) {
        return a + b;
    }

    // Use the global and local variables
    std::cout << x << std::endl;
    std::cout << y << std::endl;

    // Call the function
    std::cout << sum(x, y) << std::endl;

    return 0;
}

// Define the global variable
int x = 5;
```

在此示例中，全局变量 x 使用 extern 关键字声明，这意味着它在另一个翻译单元中定义。局部

### 存储类

在 C++ 中，存储类是指定变量和函数生命周期和可见性的关键字。它们决定变量和函数如何在内存中存储以及如何从程序的不同部分访问。

C++ 中有四种存储类：

- 1. auto : 这是局部变量的默认存储类。它指定变量在超出作用域时自动创建和销毁。
- 2. static : 此存储类指定变量或函数具有固定的内存位置，其生命周期贯穿整个程序的持续时间。它通常用于创建在函数调用之间保留其值的变量。
- 3. register : 此存储类指定变量应存储在寄存器中而不是主内存中。这可以通过减少对变量的访问时间来提高程序的性能。然而，不能保证变量实际上会被存储在寄存器中，并且可用的寄存器数量通常有限。
- 4. extern : 此存储类指定变量或函数在另一个翻译单元中定义，并且在当前翻译单元中声明。它通常用于在多个源文件之间共享变量和函数。

以下是如何在 C++ 中使用存储类的示例：

```
#include <iostream>

// Declare and define a global variable with static storage
static int x = 10;

int main() {
    // Declare and define a local variable with auto storage
    auto int y = 20;

    // Declare a local variable with register storage
    register int z = 30;

    // Declare and define a function
```

### auto

在 C++ 中，auto 是一个存储类，指定变量在超出作用域时自动创建和销毁。它是局部变量的默认存储类，局部变量是在函数或块内部声明的变量。

auto 存储类用于创建具有有限生命周期且仅在声明它们的块内可访问的变量。当块结束时，变量会自动销毁，其占用的内存会被释放供其他用途使用。

以下是如何在 C++ 中使用 auto 存储类的示例：

```
#include <iostream>

int main() {
    // Declare and define a local variable with auto storage
    auto int x = 10;

    std::cout << "x: " << x << std::endl;

    // The variable x is only accessible within this block
    {
        auto int y = 20;
        std::cout << "y: " << y << std::endl;
    }

    // The variable y is no longer accessible here
    std::cout << "y: " << y << std::endl; // This line will cause a compile error

    return 0;
}
```

此程序的输出将为：

x: 10
y: 20

请注意，auto 存储类与 auto 类型说明符不同，后者用于从其初始值设定项推导出变量的类型。例如：

```
#include <iostream>

int main() {
    // Declare and define a local variable with auto type specifier
    auto x = 10;

    std::cout << "x: " << x << std::endl;

    return 0;

```

### const

在 C++ 中，const 是一个类型限定符，指定对象不可被修改。它可以应用于变量、函数和其他类型的对象，以表示其值或行为不能被更改。

const 限定符可用于防止对变量进行非预期的修改，并确保函数不会修改其参数或全局状态。它还可用于提高程序的可读性和可维护性，通过使变量和函数的预期行为明确化。

以下是如何在 C++ 中使用 const 限定符的示例：

```
#include <iostream>

// Declare a global constant
const int x = 10;

int main() {
    // Declare and define a local constant
    const int y = 20;

    std::cout << "x: " << x << std::endl;
    std::cout << "y: " << y << std::endl;

    // Attempt to modify a constant
    x = 30; // This line will cause a compile error
    y = 30; // This line will cause a compile error

    return 0;
}
```

const 限定符也可以应用于指针和引用，以表示被指向或引用的对象不可被修改。例如：

```
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // Declare and define a constant pointer to x
    const int* p1 = &x;

    std::cout << "*p1: " << *p1 << std::endl;

    // Attempt to modify x through a constant pointer
    *p1
```

### constexpr

在 C++ 中，constexpr 是一个关键字，指定函数或变量是编译时常量。它表示函数或变量的值可以在编译时确定，而不是在运行时。

constexpr 关键字可用于通过允许编译器对使用编译时常量的表达式执行常量折叠和其他优化技术来提高程序的性能。它还可用于确保常量的值在编译时已知，这在某些上下文中是必需的，例如使用常量表达式初始化数组时。

以下是如何在 C++ 中使用 constexpr 关键字的示例：

```
#include <iostream>

// Declare a global constant
constexpr int x = 10;

// Declare a constant expression function
constexpr int square(int n) {
    return n * n;
}

int main() {
    // Declare and define a local constant
    constexpr int y = 20;

    std::cout << "x: " << x << std::endl;
    std::cout << "y: " << y << std::endl;
    std::cout << "square(x): " << square(x) << std::endl;
    std::cout << "square(y): " << square(y) << std::endl;

    // Attempt to modify a constant
    x = 30; // This line will cause a compile error
    y = 30; // This line will cause a compile error

    return 0;
}
```

此程序的输出将为：

x: 10
y: 20
square

### extern

在 C++ 中，extern 是一个存储类，指定变量或函数在另一个翻译单元中定义，并且在当前翻译单元中声明。它通常用于在多个源文件之间共享变量和函数。

extern 存储类用于声明在另一个翻译单元中定义的变量和函数。它不会分配任何内存或执行任何代码。相反，它告诉编译器变量或函数在其他地方定义，并且可以从当前翻译单元访问。

以下是如何在 C++ 中使用 extern 存储类的示例：


// File 1: declarations.h
#pragma once

// Declare a global variable with extern storage
extern int x;

// Declare a function with extern storage
extern int sum(int a, int b);

// File 2: definitions.cpp
#include "declarations.h"

// Define the global variable
int x = 10;

// Define the function
int sum(int a, int b) {
    return a + b;
}

// File 3: main.cpp
#include "declarations.h"
#include <iostream>

int main() {
    std::cout << "x: " << x << std::endl;
    std::cout << "sum(x, 10): " << sum(x, 10) << std::endl;

    return 0;
}

在此示例中，全局变量 x 和函数 sum() 使用 extern 存储类在头文件 declarations.h 中声明。它们在源文件 definitions.cpp 中定义，该文件包含了头文件。主源文件 main.cpp 也包含了头文件，这使得它可以访问该变量和函数。

请注意，extern 存储类与 extern 关键字不同，后者用于指示变量或函数是定义

### Initializers

在 C++ 中，初始化器是用于在声明变量时初始化变量的值或表达式。它指定了在创建变量时变量应被初始化为的值。

初始化器可用于在声明时为变量赋予特定值，而不是稍后对其赋值。这对于将变量的初始值设置为常量或为函数参数提供默认值非常有用。

在 C++ 中指定初始化器有几种方法：

- 1. 使用赋值表达式：这是初始化变量最常见的方法。它使用赋值运算符 = 来指定变量的初始值。例如：

int x = 10;
double y = 3.14;
char c = 'A';

- 2. 使用初始化列表：此方法用于初始化具有复合数据类型的变量，例如数组和结构体。它使用用大括号括起来的值列表来指定变量的初始值。例如：

int a[3] = {1, 2, 3};
struct Point { int x, y; } p = {1, 2};

- 3. 使用构造函数：此方法用于初始化具有用户定义类型的变量，例如类和枚举。它使用构造函数函数来创建并初始化所需类型对象。例如：

```
class Vector {
public:
    Vector(int x, int y) : x_(x), y_(y) {}
private:
    int x_, y_;
};
Vector v(1, 2);
```

以下是如何使用初始化器的示例

### Aliases and typedefs

在 C++ 中，別名是为现有类型或对象引入的新名称。它允许你使用不同的名称引用相同的类型或对象，这可以提高程序的可读性和可维护性。

在 C++ 中创建别名有两种方法：

- 1. 使用 using 关键字：此方法允许你为任何类型或对象创建别名，包括内置类型、用户定义类型和模板。它使用以下语法：

```
using alias_name = type_name;
```

例如：

```
using Int = int;
using Str = std::string;
```

- 2. 使用 typedef：此方法允许你为任何类型创建别名，包括内置类型、用户定义类型和模板。它使用以下语法：

```
typedef type_name alias_name;
```

例如：

```
typedef int Int;
typedef std::string Str;
```

以下是如何在 C++ 中使用别名和 typedef 的示例：

```
#include <iostream>
#include <string>

// Create an alias using the 'using' keyword
using Int = int;

// Create an alias using 'typedef'
typedef std::string Str;

int main() {
    // Declare and define variables using the aliases
    Int x = 10;
    Str s = "Hello";

    std::cout << "x: " << x << std::endl;
    std::cout << "s: " << s << std::endl;

    return 0;
}
```

此程序的输出将为：

x: 10
s: Hello

请注意，typedef 关键字在 using 关键字引入之前在 C++ 中被广泛使用，但 using 关键字现在被认为是在 C++ 中创建别名的首选方式。它更灵活，允许更简洁和更具表现力的代码。

### using declaration

在 C++ 中，using 声明是将命名空间中的名称引入当前作用域的语句。它允许你使用该名称而无需指定其定义的命名空间。

using 声明通常用于避免每次使用命名空间中的名称时都输入完整的命名空间名称。它也可以用于

将多个名称从相同或不同的命名空间引入同一作用域，这可以提高程序的可读性和可维护性。以下是如何在 C++ 中使用 using 声明的示例：

```
#include <iostream>

// Declare a namespace
namespace foo {
    int x = 10;
    int y = 20;
}

int main() {
    // Introduce the name 'x' into the current scope
    using foo::x;

    std::cout << "x: " << x << std::endl;

    // The name 'y' is not in the current scope, so it must be qualified
    std::cout << "foo::y: " << foo::y << std::endl;

    return 0;
}
```

此程序的输出将为：

x: 10
foo::y: 20

你也可以使用 using 声明将多个名称从相同或不同的命名空间引入同一作用域，如下所示：

```
#include <iostream>

// Declare two namespaces
namespace foo {
    int x = 10;
    int y = 20;
}
namespace bar {
    int x = 30;
    int y = 40;
}

int main() {
    // Introduce the names 'x' and 'y' from both namespaces
    using foo::x;
    using foo::y;
    using bar::x;
    using bar::y;

    std::cout << "foo::x: " << foo::x << std::endl;
    std::cout << "foo::y: " << foo::y << std::endl;
    std::cout << "bar::
```

### volatile

在 C++ 中，volatile 是一个类型限定符，指定变量可能由外部进程或硬件修改。它表示变量的值可能意外更改，即使在程序中似乎未被修改。

volatile 限定符用于防止编译器对变量执行某些优化，例如将其值缓存到寄存器中或优化对其的访问。它通常用于与硬件或与其他进程共享的变量，例如内存映射 I/O 寄存器或由多个线程访问的全局变量。

以下是如何在 C++ 中使用 volatile 限定符的示例：

```
#include <iostream>

// Declare a global volatile variable
volatile int x = 10;

int main() {
    std::cout << "x: " << x << std::endl;

    // Modify the value of x
    x = 20;

    std::cout << "x: " << x << std::endl;

    return 0;
}
```

此程序的输出将为：
x: 10
x: 20

请注意，volatile 限定符与 volatile 关键字不同，后者用于指示变量或函数可能由外部进程或硬件修改。volatile 限定符用于指示变量可能由外部进程或硬件修改，而 volatile 关键字用于声明变量或函数

### decltype

在 C++ 中，decltype 是一个关键字，允许你确定表达式的类型。它通常用于从其初始化器或返回类型推导出变量或函数的类型。

decltype 关键字用于通过计算表达式或 type-id 来指定变量或函数的类型。它通常与 auto 关键字结合使用，以从其初始化器推导出变量的类型。

以下是如何在 C++ 中使用 decltype 关键字的示例：

```
#include <iostream>

int main() {
    int x = 10;
    double y = 3.14;

    // Determine the type of x using decltype
    decltype(x) a;
    // Determine the type of y using decltype
    decltype(y) b;

    std::cout << "Type of a: " << typeid(a).name() << std::endl;
    std::cout << "Type of b: " << typeid(b).name() << std::endl;

    return 0;
}
```

此程序的输出将为：

Type of a: int
Type of b: double

你也可以使用 decltype 关键字通过将函数名指定为表达式来确定函数的返回类型。例如：

```
#include <iostream>

int add(int x, int y) {
```

### Attributes

在 C++ 中，属性是可以与函数、变量、类型或其他语言构造关联的额外元数据。它们允许你为构造提供额外信息或指定某些行为，例如其对齐、可见性或目标平台。

属性使用 [[attribute]] 语法指定，后跟属性名称和任何额外参数。它们可以应用于函数、变量、类型和其他构造的声明和定义。

C++ 有许多在 <attributes> 头文件中指定的预定义属性。一些预定义属性的示例是：

- [[noreturn]] : 表示函数不会返回给其调用者。
- [[carries_dependency]] : 表示函数可能将其参数之一的依赖关系传递给其返回值。
- [[deprecated]] : 表示函数或类型已弃用，不应



not be used.

- [[nodiscard]] : Indicates that the return value of a function should not be discarded.

Here is an example of how to use attributes in C++:

```
#include <iostream>
#include <attributes>

// Declare a function with the 'noreturn' attribute
[[noreturn]] void exit() {
    std::exit(0);
}

int main() {
    // Call the 'exit' function
    exit();

    // This line will never be reached
    std::cout << "Hello, world!" << std::endl;

    return 0;
}
```

In this example, the exit() function is declared with the [[noreturn]] attribute, which indicates that it

## Chapter V

### Built-in operators, precedence, and association

In C++, operators are special symbols that perform specific operations on one, two, or three operands, and produce a result. Operators can be classified as unary, binary, or ternary based on the number of operands they require.

C++ has a set of built-in operators that are predefined by the language and are available for use in any program. These operators can be grouped into the following categories:

- 1. Arithmetic operators: These operators perform arithmetic calculations on operands, such as addition, subtraction, multiplication, and division.
- 2. Comparison operators: These operators compare two operands and return a Boolean value indicating whether the comparison is true or false.
- 3. Logical operators: These operators perform logical operations on operands, such as AND, OR, and NOT.
- 4. Bitwise operators: These operators perform bitwise operations on operands, such as AND, OR, XOR, and NOT.
- 5. Assignment operators: These operators assign a value to a variable.
- 6. Increment and decrement operators: These operators increase or decrease the value of a variable by 1.
- 7. Conditional operator: This operator selects one of two operands based on a Boolean condition.

Operators have a precedence, which determines the order in which they are evaluated in an expression. Operators with higher precedence are evaluated before operators with lower precedence.

Operators also have an associativity, which determines the order in which they are evaluated when they have the same precedence. Operators with left-to-right associativity are evaluated from left to right, whereas operators with right-to-left associativity are evaluated from right to left.

### alignof operator

In C++, the alignof operator is a keyword that determines the alignment requirement of a type or expression. It returns the minimum alignment required for an object of the specified type, in bytes.

The alignof operator is used to determine the alignment requirement of a type or expression in order to allocate memory for an object of that type. It is often used in conjunction with the alignas specifier to specify the alignment of a variable or type.

Here is an example of how to use the alignof operator in C++:

```
#include <iostream>
#include <cstdint>

// Declare a struct with a 4-byte alignment requirement
struct alignas(4) S {
    std::int32_t x;
};

int main() {
    // Determine the alignment requirement of the 'S' struct
    std::cout << "alignof(S): " << alignof(S) << " bytes" << std::endl;

    // Determine the alignment requirement of the 'int' type
    std::cout << "alignof(int): " << alignof(int) << " bytes" << std::endl;

    return 0;
}
```

The output of this program will be:

alignof(S): 4 bytes
alignof(int): 4 bytes

Note that the alignof operator is not the same as the alignas specifier, which is used to specify the alignment of a variable or type. The alignof operator is used to determine the alignment requirement of a type or expression

### __uuidof operator

In C++, the __uuidof operator is a Microsoft-specific operator that returns the universally unique identifier (UUID) of a type. It is used to identify a type, interface, or component in a COM (Component Object Model) program.

The __uuidof operator is used to retrieve the UUID of a type or interface in order to create an instance of the object or to query for the object's type information. It is often used in conjunction with the CoCreateInstance function to create an instance of a COM object.

Here is an example of how to use the __uuidof operator in C++:

```
#include <iostream>
#include <objbase.h>

int main() {
    // Retrieve the UUID of the 'IUnknown' interface
    IID iid = __uuidof(IUnknown);

    // Create an instance of the 'IUnknown' interface
    IUnknown* pUnknown;
    HRESULT hr = CoCreateInstance(iid, nullptr, CLSCTX_ALL,
    IID_PPV_ARGS(&pUnknown));
    if (SUCCEEDED(hr)) {
        std::cout << "Instance of IUnknown created successfully" << std::endl;
    } else {
        std::cout << "Failed to create instance of IUnknown" << std::endl;
    }

    return 0;
}
```

In this example, the __uuidof operator is used to retrieve the UUID of the IUnknown interface, which is a fundamental interface in COM programming. The UUID is then passed to the CoCreateInstance function to create an instance of the IUnknown interface.

Note that the __uuidof operator is a Microsoft-specific operator and is not part of the standard C++ language. It is only available on platforms that support COM programming.

### Additive operators: + and -

In C++, the + and - operators are additive operators that perform addition and subtraction, respectively. They can be used to add or subtract two operands of the same or compatible types, and produce a result of the same type as the operands.

The + operator is a binary operator that adds two operands and returns their sum. It can be used with operands of any arithmetic type, including integers, floating-point numbers, and complex numbers.

The - operator is also a binary operator that subtracts one operand from another and returns the difference. It can be used with operands of any arithmetic type, including integers, floating-point numbers, and complex numbers.

Here is an example of how to use the + and - operators in C++:

```
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // Add x and y
    int z = x + y;
    std::cout << "x + y = " << z << std::endl;

    // Subtract y from x
    z = x - y;
    std::cout << "x - y = " << z << std::endl;

    return 0;
}
```

The output of this program will be:

x + y = 30
x - y = -10

Note that the + and - operators can also be used as unary operators, in which case they operate on a single operand. The + operator returns the operand unchanged, whereas the - operator returns the neg

### Address-of operator: &

In C++, the & operator is the address-of operator, which returns the memory address of a variable or object. It is a unary operator that takes a single operand and returns a pointer to the operand.

The & operator is used to obtain the memory address of a variable or object in order to access it directly or to pass it as an argument to a function. It is often used in conjunction with pointer variables to manipulate the value of the pointed-to object.

Here is an example of how to use the & operator in C++:

```
#include <iostream>

int main() {
    int x = 10;

    // Obtain the memory address of x
    int* px = &x;

    std::cout << "x: " << x << std::endl;
    std::cout << "&x: " << &x << std::endl;
    std::cout << "px: " << px << std::endl;

    return 0;
}
```

The output of this program will be:

x: 10
&x: 0x7ffdc91a6884
px: 0x7ffdc91a6884

In this example, the & operator is used to obtain the memory address of the x variable, which is stored in the px pointer. The value of x can then be accessed directly through the pointer using the * operator, like this:

```
*px = 20;
std::cout << "x: " << x << std::endl;
```

The output of this code will be:

x: 20

Note that the & operator has a higher precedence than the * operator, so it is evaluated before the * operator. For example, the expression *&x is equivalent to x, whereas the expression &*x is equivalent to x if x is a pointer,

### Assignment operators

In C++, assignment operators are used to assign a value to a variable. The most basic assignment operator is the = operator, which assigns the value of the right-hand operand to the left-hand operand.

C++ also has a number of compound assignment operators, which perform an operation on the left-hand operand and assign the result to the left-hand operand. These operators include:

- += : Add the right-hand operand to the left-hand operand and assign the result to the left-hand operand.





- -= : 从左操作数中减去右操作数，并将结果赋给左操作数。
- *= : 将左操作数乘以右操作数，并将结果赋给左操作数。
- /= : 将左操作数除以右操作数，并将结果赋给左操作数。
- %= : 计算左操作数除以右操作数的余数，并将结果赋给左操作数。

以下是 C++ 中使用赋值运算符的示例：

```
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // Basic assignment
    x = y;
    std::cout << "x = " << x << std::endl;

    // Compound assignment
    x += y;
    std::cout << "x += y = " << x << std::endl;
    x -= y;
    std::cout << "x -= y = " << x << std::endl;
    x *= y;
    std::cout << "x *= y = " << x << std::endl;
    x /= y;
    std::cout << "x /= y = " << x << std::endl;
    x %= y;
    std::cout << "
```

按位与运算符：&

在 C++ 中，& 运算符是按位与运算符，它对两个操作数执行按位与操作并返回结果。它是一个二元运算符，接受两个整数类型的操作数并返回与操作数相同类型的结果。

按位与运算符将第一个操作数的每一位与第二个操作数的对应位进行比较，如果两个位都是 1，则对应的结果位设为 1。否则，结果位设为 0。
以下是 C++ 中使用按位与运算符的示例：

```
#include <iostream>

int main() {
    int x = 0b1010; // 10 in binary
    int y = 0b0101; // 5 in binary

    int z = x & y; // 0b0000 (0 in decimal)

    std::cout << "x & y = " << z << std::endl;

    return 0;
}
```

此程序的输出为：
x & y = 0

在此示例中，按位与运算符用于对 x 和 y 变量执行按位与操作。结果存储在 z 变量中，其十进制值为 0。

请注意，按位与运算符的优先级高于 = 运算符，因此先求值。例如，表达式 x = y & z 等价于 x = (y & z)，而表达式 x &= y 等价于 x = x & y。

### 按位异或运算符：^

在 C++ 中，^ 运算符是按位异或 XOR 运算符，它对两个操作数执行按位 XOR 操作并返回结果。它是一个二元运算符，接受两个整数类型的操作数并返回与操作数相同类型的结果。

按位异或运算符将第一个操作数的每一位与第二个操作数的对应位进行比较，如果其中一个位为 1 而另一个为 0，则对应的结果位设为 1。否则，结果位设为 0。

以下是 C++ 中使用按位异或运算符的示例：

```
#include <iostream>

int main() {
    int x = 0b1010; // 10 in binary
    int y = 0b0101; // 5 in binary

    int z = x ^ y; // 0b1111 (15 in decimal)

    std::cout << "x ^ y = " << z << std::endl;

    return 0;
}
```

此程序的输出为：

x ^ y = 15

在此示例中，按位异或运算符用于对 x 和 y 变量执行按位异或操作。结果存储在 z 变量中，其十进制值为 15。

请注意，按位异或运算符的优先级高于 = 运算符，因此先求值。例如，表达式 x = y ^ z 等价于 x = (y ^ z)，而表达式 x ^= y 等价于 x = x ^ y。

### 按位包含或运算符：|

在 C++ 中，| 运算符是按位包含或 OR 运算符，它对两个操作数执行按位或操作并返回结果。它是一个二元运算符，接受两个整数类型的操作数并返回与操作数相同类型的结果。

按位或运算符将第一个操作数的每一位与第二个操作数的对应位进行比较，如果任一位为 1，则对应的结果位设为 1。否则，结果位设为 0。

以下是 C++ 中使用按位或运算符的示例：

```
#include <iostream>

int main() {
    int x = 0b1010; // 10 in binary
    int y = 0b0101; // 5 in binary

    int z = x | y; // 0b1111 (15 in decimal)

    std::cout << "x | y = " << z << std::endl;

    return 0;
}
```

此程序的输出为：

x | y = 15

在此示例中，按位或运算符用于对 x 和 y 变量执行按位或操作。结果存储在 z 变量中，其十进制值为 15。

请注意，按位或运算符的优先级高于 = 运算符，因此先求值。例如，表达式 x = y | z 等价于 x = (y | z)，而表达式 x |= y 等价于 x = x | y。

### 强制转换运算符：()

在 C++ 中，() 运算符是强制转换运算符，用于显式地将一个值从一种类型转换为另一种类型。它是一个一元运算符，接受一个操作数和一个类型作为其操作数，并返回指定类型的值。

强制转换运算符用于在隐式转换不可行或不期望时将值从一种类型转换为另一种类型。它通常用于在基本类型之间转换值，例如整数和浮点数，或在不同类型之间转换指针。

以下是 C++ 中使用强制转换运算符的示例：

```
#include <iostream>

int main() {
    double x = 3.14;

    // Cast x to an int
    int y = (int)x;

    std::cout << "y = " << y << std::endl;

    return 0;
}
```

此程序的输出为：

y = 3

在此示例中，强制转换运算符用于将类型为 double 的 x 变量转换为 int 并将结果存储在 y 变量中。x 的值在转换为 int 时被截断。

请注意，强制转换运算符的优先级高于 = 运算符，因此先求值。例如，表达式 x = (int)y 等价于 x = (int)(y)，而表达式 x = int(y) 也等价于 x = (int)(y)。

C++ 还提供了多种类型安全的强制转换运算符，例如 dynamic_cast、static_cast、const_cast 和 reinterpret_cast，它们执行更专门的类型转换。这些运算符通常与继承和多态结合使用，以在相关类型之间进行转换。

### 逗号运算符：,

在 C++ 中，, 运算符是逗号运算符，它分隔两个或多个操作数并从左到右求值它们。它是一个二元运算符，接受两个或多个操作数并返回右操作数的值。

逗号运算符通常用于在一个语句中包含多个表达式，每个表达式由逗号分隔。只有右操作数的值用于最终结果，而其他操作数的值被丢弃。

以下是 C++ 中使用逗号运算符的示例：

```
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // Evaluate x and y, but only use the value of y
    int z = (x++, y++, x + y);

    std::cout << "z = " << z << std::endl;

    return 0;
}
```

此程序的输出为：

z = 32

在此示例中，逗号运算符用于求值 x++ 和 y++ 表达式，分别递增 x 和 y 的值。然后计算 x + y 的值并赋给 z 变量。

请注意，逗号运算符的优先级低于大多数其他运算符，因此通常在其他运算符之后求值。例如，表达式 x = y, z 等价于 (x = y), z，而表达式 x = y + z 等价于 x = (y + z)。

### 条件运算符：? :

在 C++ 中，?: 运算符是条件运算符，也称为三元运算符，用于求值条件表达式。它是一个三元运算符，接受三个操作数并根据条件表达式的结果返回一个值。

条件运算符通常用作 if 语句的简写形式，其中第一个操作数是布尔条件，第二个操作数是在条件为真时返回的值，第三个操作数是在条件为假时返回的值。

以下是 C++ 中使用条件运算符的示例：



```cpp
#include <iostream>

int main() {
    int x = 10;
    int y = 20;

    // Evaluate the condition x < y and return the appropriate value
    int z = (x < y) ? x : y;

    std::cout << "z = " << z << std::endl;

    return 0;
}
```

The output of this program will be:

z = 10

In this example, the conditional operator is used to evaluate the x < y condition. If the condition is true, the value of x is returned; otherwise, the value of y is returned. The result is stored in the z variable.

Note that the conditional operator has a lower precedence than the assignment operator, so it is usually evaluated after the assignment. For example, the expression x = y ? z : w is equivalent to x = (y ? z : w), whereas the expression x ? y = z : w = t is equivalent to (x ? (y = z) : (w = t)).

### delete operator

In C++, the delete operator is used to deallocate memory that was previously allocated by the new operator. It is a unary operator that takes a pointer as its operand and frees the memory pointed to by the pointer.

The delete operator is used to release the memory occupied by an object or array that was created using the new operator. It is important to use the delete operator to deallocate memory when it is no longer needed, to avoid memory leaks and other memory-related issues.

Here is an example of how to use the delete operator in C++:

```cpp
#include <iostream>

int main() {
    int *p = new int;
    *p = 10;

    std::cout << "*p = " << *p << std::endl;

    // Deallocate the memory pointed to by p
    delete p;

    return 0;
}
```

In this example, the new operator is used to dynamically allocate memory for an int object and assign the address of the object to the p pointer. The value of the object is then initialized to 10. The delete operator is then used to deallocate the memory pointed to by p.

Note that the delete operator should only be used to deallocate memory that was previously allocated using the new operator. It should not be used to deallocate memory that was allocated on the stack or using other memory management techniques, such as malloc() and free().

### Equality operators: == and !=

In C++, the == and != operators are the equality and inequality operators, respectively, which are used to compare two values for equality or inequality. They are binary operators that take two operands and return a boolean value indicating whether the operands are equal or unequal.

The equality operator == compares the values of its operands and returns true if they are equal, and false if they are not equal. The inequality operator != compares the values of its operands and returns true if they are not equal, and false if they are equal.

Here is an example of how to use the equality and inequality operators in C++:

```cpp
#include <iostream>

int main() {
    int x = 10;
    int y = 20;
    int z = 10;

    std::cout << "x == y: " << (x == y) << std::endl;
    std::cout << "x != y: " << (x != y) << std::endl;
    std::cout << "x == z: " << (x == z) << std::endl;
    std::cout << "x != z: " << (x != z) << std::endl;

    return 0;
}
```

The output of this program will be:

x == y: 0
x != y: 1
x == z: 1
x != z: 0

In this example, the equality and inequality operators are used to compare the values of the x, y, and z variables. The results of the comparisons are printed to the console.

Note that the equality and inequality operators have a lower precedence than most other operators, so they are usually evaluated after the other operators. For example, the expression x = y == z is equivalent to x = (y == z), whereas the expression x == y = z is equivalent to (x == (y = z)).

### Explicit type conversion operator: ()

In C++, the () operator is the explicit type conversion operator, which is used to explicitly convert a value from one type to another. It is a unary operator that takes a single operand and a type as its operands, and returns a value of the specified type.

The explicit type conversion operator is used to convert a value from one type to another when an implicit conversion is not possible or desired. It is often used to convert values between basic types, such as integers and floating-point numbers, or to convert pointers between different types.

Here is an example of how to use the explicit type conversion operator in C++:

```cpp
#include <iostream>

int main() {
    double x = 3.14;

    // Convert x to an int using the explicit type conversion operator
    int y = int(x);

    std::cout << "y = " << y << std::endl;

    return 0;
}
```

The output of this program will be:

y = 3

In this example, the explicit type conversion operator is used to convert the x variable, which has a type of double, to an int and store the result in the y variable. The value of x is truncated to an integer when it is converted to int.

Note that the explicit type conversion operator has a higher precedence than the = operator, so it is evaluated before the assignment. For example, the expression x = int(y) is equivalent to x = (int)(y), whereas the expression x = y + int(z) is equivalent to x = (y + (int)(z)).

C++ also provides a number of type-safe cast operators, such as dynamic_cast, static_cast, const_cast, and reinterpret_cast, which perform more specialized types of conversions. These operators are often used in conjunction with inheritance and polymorphism to convert between related types.

### Function call operator: ()

In C++, the () operator is the function call operator, which is used to call a function and execute its code. It is a unary operator that takes a function name and a list of arguments as its operands, and returns a value of the function's return type.

The function call operator is used to invoke a function and pass arguments to it. The arguments are specified within the parentheses, and are separated by commas. The function call operator can also be used to invoke a function through a function pointer or a member function of a class.

Here is an example of how to use the function call operator in C++:

```cpp
#include <iostream>

int add(int x, int y) {
    return x + y;
}

int main() {
    int x = 10;
    int y = 20;
    int z = 0;

    // Call the add function and pass x and y as arguments
    z = add(x, y);

    std::cout << "z = " << z << std::endl;

    return 0;
}
```

The output of this program will be:

z = 30

In this example, the add() function is defined to take two int arguments and return their sum. The function call operator is then used to invoke the add() function and pass the values of x and y as arguments. The result of the function call is stored in the z variable.

Note that the function call operator has a higher precedence than the assignment operator, so it is evaluated before the assignment. For example, the expression x = add(y, z) is equivalent to x = (add(y, z)), whereas the expression x = y + add(z, w) is equivalent to x = (y + (add(z, w))).

### Indirection operator: *

In C++, the * operator is the indirection operator, also known as the dereference operator, which is used to access the value stored at a memory address. It is a unary operator that takes a pointer as its operand and returns the value pointed to by the pointer.

The indirection operator is often used in conjunction with pointers to access the value stored at the memory address pointed to by the pointer. It is also used to declare pointers, where it is placed in front of the variable name to indicate that the variable is a pointer.

Here is an example of how to use the indirection operator in C++:

```cpp
#include <iostream>

int main() {
    int x = 10;
    int *p = &x;

    std::cout << "x = " << x << std::endl;
    std::cout << "*p = " << *p << std::endl;

    return 0;
}
```

The output of this program will be:

x = 10
*p = 10

In this example, the p pointer is declared and initialized to the address of the x variable. The indirection operator is then used to access the value stored at the memory address pointed to by p, which is the value of the x variable.

Note that the indirection operator has a higher precedence than the assignment operator, so it is evaluated before the assignment. For example, the expression x = *p is equivalent to x = (*p), whereas the expression x = *p + y is equivalent to x = (*p) + y.

### Left shift and right shift operators (>> and <<)

In C++, the << and >> operators are the left shift and right shift operators, respectively, which are used to perform bit shifting on integer values. They are binary operators that take two operands, an integer value and a shift count, and return a value that is the original value shifted left or right by the specified number of bits.

The left shift operator << shifts the bits of its first operand to the left by the number of positions specified in the second operand. The right shift operator >> shifts the bits of its first operand to the right by the number of positions specified in the second operand.

Here is an example of how to use the left shift and right shift operators in C++:



```cpp
#include <iostream>

int main() {
    int x = 10;
    int y = 3;

    std::cout << "x << y = " << (x << y) << std::endl;
    std::cout << "x >> y = " << (x >> y) << std::endl;

    return 0;
}
```

The output of this program will be:

x << y = 80

x >> y = 1

In this example, the left shift operator << is used to shift the bits of the x variable to the left by 3 positions, and the right shift operator >> is used to shift the bits of the x variable to the right by 3 positions. The results of the shift operations are printed to the console.

Note that the left shift and right shift operators have a higher precedence than the addition and subtraction operators, so they are usually evaluated before these operators. For example, the expression x << y + z is equivalent to x << (y + z), whereas the expression x + y << z is equivalent to (x + y) << z.

### Logical AND operator: &&

In C++, the && operator is the logical AND operator, which is used to perform a logical AND operation on two boolean values. It is a binary operator that takes two boolean operands and returns a boolean value indicating the result of the logical AND operation.

The logical AND operator && performs a short-circuit evaluation of its operands, meaning that it only evaluates the second operand if the first operand is true. If the first operand is false, the second operand is not evaluated and the result of the && operator is false. This can be useful for optimizing code and avoiding unnecessary computations.

Here is an example of how to use the logical AND operator in C++:

```cpp
#include <iostream>

int main() {
    bool x = true;
    bool y = false;
    bool z = true;

    std::cout << "x && y: " << (x && y) << std::endl;
    std::cout << "x && z: " << (x && z) << std::endl;
    std::cout << "y && z: " << (y && z) << std::endl;

    return 0;
}
```

The output of this program will be:

x && y: 0
x && z: 1
y && z: 0

In this example, the logical AND operator && is used to perform logical AND operations on the x, y, and z variables. The results of the && operations are printed to the console.

Note that the logical AND operator has a higher precedence than the logical OR operator ||, so it is usually evaluated before the || operator. For example, the expression x && y || z is equivalent to (x && y) || z, whereas the expression x || y && z is equivalent to x || (y && z)

### Logical negation operator: !

In C++, the ! operator is the logical negation operator, which is used to negate a boolean value. It is a unary operator that takes a boolean operand and returns the negated value.

The logical negation operator ! negates the value of its operand by reversing its truth value. If the operand is true, the ! operator returns false, and if the operand is false, the ! operator returns true.

Here is an example of how to use the logical negation operator in C++:

```cpp
#include <iostream>

int main() {
    bool x = true;
    bool y = false;

    std::cout << "!x: " << !x << std::endl;
    std::cout << "!y: " << !y << std::endl;

    return 0;
}
```

The output of this program will be:

!x: 0
!y: 1

In this example, the logical negation operator ! is used to negate the values of the x and y variables. The results of the ! operations are printed to the console.

Note that the logical negation operator has a higher precedence than the logical AND and OR operators && and ||, so it is usually evaluated before these operators. For example, the expression !x && y is equivalent to (!x) && y, whereas the expression x || !y is equivalent to x || (!y).

### Logical OR operator: ||

In C++, the || operator is the logical OR operator, which is used to perform a logical OR operation on two boolean values. It is a binary operator that takes two boolean operands and returns a boolean value indicating the result of the logical OR operation.

The logical OR operator || performs a short-circuit evaluation of its operands, meaning that it only evaluates the second operand if the first operand is false. If the first operand is true, the second operand is not evaluated and the result of the || operator is true. This can be useful for optimizing code and avoiding unnecessary computations.

Here is an example of how to use the logical OR operator in C++:

```cpp
#include <iostream>

int main() {
    bool x = true;
    bool y = false;
    bool z = true;

    std::cout << "x || y: " << (x || y) << std::endl;
    std::cout << "x || z: " << (x || z) << std::endl;
    std::cout << "y || z: " << (y || z) << std::endl;

    return 0;
}
```

The output of this program will be:

x || y: 1
x || z: 1
y || z: 1

In this example, the logical OR operator || is used to perform logical OR operations on the x, y, and z variables. The results of the || operations are printed to the console.

Note that the logical OR operator has a lower precedence than the logical AND operator &&, so it is usually evaluated after the && operator. For example, the expression x || y && z is equivalent to x || (y && z), whereas the expression x && y || z is equivalent to (x && y) || z.

### Member access operators: . and ->

In C++, the . and -> operators are the member access operators, which are used to access data members and member functions of a class or struct. They are binary operators that take an object or a pointer to an object as their left operand and the name of a data member or member function as their right operand.

The . operator is used to access data members and member functions of an object, whereas the -> operator is used to access data members and member functions of a pointer to an object. The -> operator is equivalent to using the * operator to dereference the pointer and the . operator to access the data member or member function.

Here is an example of how to use the member access operators in C++:

```cpp
#include <iostream>

class Point {
public:
    int x;
    int y;

    void set(int x, int y) {
        this->x = x;
        this->y = y;
    }

    void print() const {
        std::cout << "(" << x << ", " << y << ")" << std::endl;
    }
};

int main() {
    Point p;

    // Use the . operator to access data members and member functions
    p.x = 10;
    p.y = 20;
    p.set(30, 40);
    p.print();

    Point *q = &p;

    // Use the -> operator to access data members and member functions of a pointer
    q->x = 50;
    q->y = 60;
    q->set(70, 80);
    q->print();

    return 0;
}
```

The output of this program will be:
(30, 40)
(70, 80)

In this example, the Point class is defined with two data members x and y, and two member functions set() and print(). The main() function creates a Point object p and a pointer to a Point object q. The member access operators . and -> are used to access the data members and member functions of the p and q objects.

Note that the member access operators have a higher precedence than the assignment operator =, so they are usually evaluated before the assignment. For example, the expression p.x = y is equivalent to (p.x) = y, whereas the expression x = p.y is equivalent to x = (p.y).

### Multiplicative operators and the modulus operator

In C++, the *, /, and % operators are the multiplicative operators and the modulus operator, respectively, which are used to perform multiplication, division, and modulus operations on integer and floating-point values. They are binary operators that take two operands and return a value that is the result of the multiplication, division, or modulus operation.

The * operator is the multiplication operator, which multiplies its operands and returns the product. The / operator is the division operator, which divides its first operand by its second operand and returns the quotient. The % operator is the modulus operator, which returns the remainder of the division of its first operand by its second operand.

Here is an example of how to use the multiplicative operators and the modulus operator in C++:

```cpp
#include <iostream>

int main() {
    int x = 10;
    int y = 3;
    double z = 5.5;

    std::cout << "x * y = " << (x * y) << std::endl;
    std::cout << "x / y = " << (x / y) << std::endl;
    std::cout << "x % y = " << (x % y) << std::endl;
    std::cout << "x * z = " << (x * z) << std::endl;
    std::cout << "x / z = " << (x / z) << std::endl;
    std::cout << "z / x = " << (z / x) << std::endl;

    return 0;
}
```

The output of this program will be:

x * y = 30
x / y = 3
x % y = 1
x * z = 55
x / z = 1.81818
z / x = 0.55

In this example, the multiplicative operators *, /, and % are used to perform multiplication, division, and modulus operations on the x, y, and z variables. The results of the operations are printed to the console.

Note that the multiplicative operators and the modulus operator have a higher


优先级高于加法运算符 + 和 -，因此它们通常在这些运算符之前求值。例如，表达式 x * y + z 等价于 (x * y) + z，而表达式 x + y * z 等价于 x + (y * z)。

### new 运算符

在 C++ 中，new 运算符用于从堆中为对象或对象数组动态分配内存。它是一个一元运算符，接受一个类型和一个可选的初始化表达式作为操作数，并返回指向新分配内存的指针。

new 运算符通常用于创建生命周期长于局部变量的对象，或创建大于可用栈内存的对象。它通常与 delete 运算符配对使用，以便在不再需要时释放内存。

以下是如何在 C++ 中使用 new 运算符的示例：

```
#include <iostream>

class Point {
public:
    int x;
    int y;

    Point(int x, int y) : x(x), y(y) { }
};

int main() {
    // Allocate a single object
    Point *p = new Point(10, 20);
    std::cout << "p: (" << p->x << ", " << p->y << ")" << std::endl;
    delete p;

    // Allocate an array of objects
    Point *q = new Point[5]{ {1, 2}, {3, 4}, {5, 6}, {7, 8}, {9, 10} };
    std::cout << "q[0]: (" << q[0].x << ", " << q[0].y << ")" << std::endl;
    std::cout << "q[4]: (" << q[4].x << ", " << q[4].y << ")" << std::endl;
    delete[] q;

    return 0;
}
```

该程序的输出为：

p: (10, 20)
q[0]: (1, 2)
q[4]: (9, 10)

在此示例中，new 运算符用于为单个 Point 对象和一个 Point 对象数组动态分配内存。delete 运算符用于在不再需要时释放内存。成员访问运算符 -> 和 [] 用于访问对象的数据成员。

请注意，如果 new 运算符无法分配请求的内存，它会抛出 std::bad_alloc 异常，因此它通常在 try-catch 块中使用来处理异常。最好一致地使用 new 和 delete 运算符，因为将它们与 C 标准库中的 malloc() 和 free() 函数混合使用可能导致未定义行为。

### 按位取反运算符：~

在 C++ 中，~ 运算符是按位取反运算符，用于对整数值执行按位 NOT 操作。它是一个一元运算符，接受一个整数操作数并返回一个整数值，该值是按位 NOT 操作的结果。

按位取反运算符 ~ 通过翻转其操作数的所有位来否定操作数的值。如果操作数是一个 n 位整数，~ 运算符返回一个 n 位整数，其所有位都被翻转。例如，0000 1100（十进制 12）的按位取反是 1111 0011（十进制 243）。

以下是如何在 C++ 中使用按位取反运算符的示例：

```
#include <iostream>

int main() {
    int x = 12;
    int y = ~x;

    std::cout << "x: " << x << std::endl;
    std::cout << "y: " << y << std::endl;

    return 0;
}
```

该程序的输出为：

x: 12
y: -13

在此示例中，按位取反运算符 ~ 用于否定 x 变量的值。~ 操作的结果存储在 y 变量中并打印到控制台。

请注意，按位取反运算符的优先级高于按位与、或和异或运算符 &、| 和 ^，因此它通常在这些运算符之前求值。例如，表达式 ~x & y 等价于 (~x) & y，而表达式 x | ~y 等价于 x | (~y)。

### 指向成员的运算符：.* 和 ->*

在 C++ 中，.* 运算符和 ->* 运算符用于通过指向对象的指针访问类或结构体的成员。

.* 运算符用于对象本身是指针时，而 ->* 运算符用于对象是实际对象且你想通过指向对象的指针访问成员时。

以下是这些运算符如何使用的示例：

```
#include <iostream>

struct S
{
    int x;
    double y;
};

int main()
{
    S s{10, 3.14};
    S* p = &s;
    int S::*px = &S::x;
    double S::*py = &S::y;

    std::cout << "s.x = " << s.x << std::endl;
    std::cout << "s.y = " << s.y << std::endl;

    std::cout << "(p->*px) = " << (p->*px) << std::endl;
    std::cout << "(p->*py) = " << (p->*py) << std::endl;

    std::cout << "(s.*px) = " << (s.*px) << std::endl;
    std::cout << "(s.*py) = " << (s.*py) << std::endl;

    return 0;
}
```

该程序的输出将为：

s.x = 10
s.y = 3.14
(p->*px) = 10
(p->*py) = 3.14
(s.*px) = 10
(s.*py) = 3.14

在此示例中，我们有一个结构体 s 包含两个成员：x 和 y。我们创建了一个类型为 s 的对象 s 和指向 s 的指针 p。我们还定义了 s 的两个指向成员的指针 px 和 py，它们分别指向成员 x 和 y。

我们可以使用点运算符 . 直接访问 s 的成员 x 和 y，也可以使用 ->* 运算符通过指针 p 访问它们。我们还可以使用 .* 运算符通过指向对象本身的指针访问 s 的成员 x 和 y。

### 后缀增量和减量运算符：++ 和 --

在 C++ 中，后缀增量运算符（ ++ ）和后缀减量运算符（ -- ）用于将变量的值增加或减少 1。这些运算符称为“后缀”，因为它们出现在操作数之后（即其值被增量或减量的变量之后）。

以下是这些运算符如何使用的示例：

```
#include <iostream>

int main()
{
    int x = 10;
    int y = 10;

    std::cout << "x = " << x << std::endl;
    std::cout << "y = " << y << std::endl;

    std::cout << "x++ = " << x++ << std::endl;
    std::cout << "y-- = " << y-- << std::endl;

    std::cout << "x = " << x << std::endl;
    std::cout << "y = " << y << std::endl;

    return 0;
}
```

该程序的输出将为：

x = 10
y = 10
x++ = 10
y-- = 10
x = 11
y = 9

在此示例中，我们有两个变量 x 和 y，均初始化为 10。我们使用后缀增量运算符 x++ 将 x 的值增加 1，并使用后缀减量运算符 y-- 将 y 的值减少 1。

后缀增量和减量运算符返回操作数在被增量或减量之前的值。这就是为什么 x++ 和 y-- 的输出为 10，即使 x 和 y 的值分别被增量和减量。

需要注意的是，后缀增量和减量运算符的优先级低于大多数其他运算符，因此它们通常与其他运算符组合使用。例如：

```
int a = 10;
int b = 20;
int c = a++ + b;  // c = 30, a = 11
int d = a-- - b;  // d = -1, a = 10
```

在此示例中，c 的值计算为 10 + 20 = 30，并在计算完成后将 a 的值递增到 11。同样，d 的值计算为 11 - 20 = -1，并在计算完成后将 a 的值递减到 10。

### 前缀增量和减量运算符：++ 和 --

在 C++ 中，前缀增量运算符（ ++ ）和前缀减量运算符（ -- ）用于将变量的值增加或减少 1。这些运算符称为“前缀”，因为它们出现在操作数之前（即其值被增量或减量的变量之前）。

以下是这些运算符如何使用的示例：

```
#include <iostream>

int main()
{
    int x = 10;
    int y = 10;

    std::cout << "x = " << x << std::endl;
    std::cout << "y = " << y << std::endl;

    std::cout << "++x = " << ++x << std::endl;
    std::cout << "--y = " << --y << std::endl;

    std::cout << "x = " << x << std::endl;
    std::cout << "y = " << y << std::endl;

    return 0;
}
```

该程序的输出将为：

x = 10
y = 10
++x = 11
--y = 9
x = 11
y = 9

在此示例中，我们有两个变量 x 和 y，均初始化为 10。我们使用前缀增量运算符 ++x 将 x 的值增加 1，并使用前缀减量运算符 --y 将 y 的值减少 1。
前缀增量和减量运算符返回操作数在被增量或减量之后的值。这就是为什么 ++x 和 --y 的输出分别为 11 和 9，即使 x 和 y 的值在输出产生之前就已被增量和减量。

需要注意的是，前缀增量和减量运算符的优先级高于大多数其他运算符，因此它们通常与其他运算符组合使用。例如：

```
int a = 10;
int b = 20;
int c = ++a + b;  // c = 31, a = 11
int d = --a - b;  // d = -9, a = 10
```

在此示例中，a 的值在 c 的值被计算之前被递增到 11


calculated as 11 + 20 = 31 . Similarly, the value of a is decremented to 10 before the value of d is calculated as 10 - 20 = -10 .

### Relational operators: <, >, <=, and >=

In C++, the relational operators < , > , <= , and >= are used to compare the values of two operands. These operators return a boolean value indicating whether the comparison is true or false.

Here is an example of how these operators can be used:

```
#include <iostream>

int main()
{
    int x = 10;
    int y = 20;
    int z = 10;

    std::cout << "(x < y) = " << (x < y) << std::endl;
    std::cout << "(x > y) = " << (x > y) << std::endl;
    std::cout << "(x <= y) = " << (x <= y) << std::endl;
    std::cout << "(x >= y) = " << (x >= y) << std::endl;
    std::cout << "(x == z) = " << (x == z) << std::endl;
    std::cout << "(x != z) = " << (x != z) << std::endl;

    return 0;
}
```

The output of this program would be:

```
(x < y) = 1
(x > y) = 0
(x <= y) = 1
(x >= y) = 0
(x == z) = 1
(x != z) = 0
```

In this example, we have three variables: x , y , and z . We use the relational operators to compare the values of x and y , as well as the values of x and z .

The relational operator < returns true if the value of the left operand is less than the value of the right operand, and false otherwise. The relational operator > returns true if the value of the left operand is greater than the value of the right operand, and false otherwise.

The relational operator <= returns true if the value of the left operand is less than or equal to the value of the right operand, and false otherwise. The relational operator >= returns true if the value of the left operand is greater than or equal to the value of the right operand, and false otherwise.

The relational operator == returns true if the value of the left operand is equal to the value of the right operand, and false otherwise. The relational operator != returns true if the value of the left operand is not equal to the value of the right operand, and false otherwise.

It's important to note that the relational operators have a lower precedence than most other operators, so they are often used in combination with other operators. For example:

```
int a = 10;
int b = 20;
```

```
if (a < b && b > a)
{
    std::cout << "a is less than b and b is greater than a" << std::endl;
}
```

```
if (a == b || a != b)
{
    std::cout << "a is either equal to b or not equal to b" << std::endl;
}
```

In this example, the first if statement will be true because both conditions

### Scope resolution operator: ::

In C++, the scope resolution operator ( :: ) is used to specify the scope in which a name is defined. It is used to qualify the name of a class, function, or variable, and is often used to access a name that is defined in a different scope.

Here is an example of how the scope resolution operator can be used:

```
#include <iostream>

int x = 10;

int main()
{
    int x = 20;

    std::cout << "x = " << x << std::endl;
    std::cout << "::x = " << ::x << std::endl;

    return 0;
}
```

The output of this program would be:

x = 20
::x = 10

In this example, we have a global variable x and a local variable x in the main function. The local variable x is defined within the scope of the main function, while the global variable x is defined outside of any function and is therefore in the global scope.

We use the scope resolution operator :: to specify the global scope when accessing the global variable x. Without the scope resolution operator, the local variable x would be accessed instead.

The scope resolution operator can also be used to access a name that is defined in a different namespace:

```
#include <iostream>

namespace NS1
{
    int x = 10;
}

namespace NS2
{
    int x = 20;

    int main()
    {
        std::cout << "x = " << x << std::endl;
        std::cout << "NS1::x = " << NS1::x << std::endl;
        std::cout << "NS2::x = " << NS2::x << std::endl;

        return 0;
    }
}
```

The output of this program would be:

```
x = 20
NS1::x = 10
NS2::x = 20
```

In this example, we have two namespaces, NS1 and NS2, each with a variable x. The variable x in NS2 is defined within the scope of the main function, while the variable x in NS1 is defined outside of any function and is therefore in the global scope.

We use the scope resolution operator :: to specify the namespace when accessing the variables x in NS1 and NS2. Without the scope resolution operator, the local variable x in NS2 would be accessed instead.

### sizeof operator

In C++, the sizeof operator is used to determine the size, in bytes, of a data type or an expression. It is often used to allocate memory dynamically or to determine the size of an array.

Here is an example of how the sizeof operator can be used:

```
#include <iostream>
#include <array>

int main()
{
std::cout << "sizeof(int) = " << sizeof(int) << " bytes" << std::endl;
std::cout << "sizeof(double) = " << sizeof(double) << " bytes" << std::endl;

std::array<int, 10> arr;
std::cout << "sizeof(arr) = " << sizeof(arr) << " bytes" << std::endl;

int* p = new int[10];
std::cout << "sizeof(p) = " << sizeof(p) << " bytes" << std::endl;
delete [] p;

return 0;
}
```

The output of this program will depend on the machine and compiler being used, but it might look something like this:

```
sizeof(int) = 4 bytes
sizeof(double) = 8 bytes
sizeof(arr) = 40 bytes
sizeof(p) = 8 bytes
```

In this example, we use the sizeof operator to determine the size of various data types and expressions. We use it to determine the size of an int and a double, as well as the size of an std::array of ints and a dynamically-allocated array of ints.

It's important to note that the sizeof operator does not evaluate the expression that it is applied to. It simply determines the size of the data type or expression, regardless of its value.

For example:

```
int x = 10;
std::cout << "sizeof(x + 20) = " << sizeof(x + 20) << " bytes" << std::endl;
```

The output of this program would be:
sizeof(x + 20) = 4 bytes

In this example, the expression x + 20 is not evaluated. The sizeof operator simply determines the size of an int, which is 4 bytes.

### Subscript operator:

In C++, the subscript operator ( [] ) is used to access an element of an array or a container class. It is used to specify the index of the element that is being accessed.

Here is an example of how the subscript operator can be used with an array:

```
#include <iostream>

int main()
{
    int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    std::cout << "arr[0] = " << arr[0] << std::endl;
    std::cout << "arr[1] = " << arr[1] << std::endl;
    std::cout << "arr[2] = " << arr[2] << std::endl;
    std::cout << "arr[9] = " << arr[9] << std::endl;

    return 0;
}
```

The output of this program would be:
arr[0] = 1
arr[1] = 2
arr[2] = 3
arr[9] = 10

In this example, we have an array of ints called arr, with 10 elements. We use the subscript operator [] to access the elements of the array, specifying the index of the element that we want to access. The first element of the array has an index of 0, the second element has an index of 1, and so on.

The subscript operator can also be used with container classes that provide subscript operator overloads, such as std::vector and std::map. For example:

```
#include <iostream>
#include <vector>
#include <map>

int main()
{
    std::vector<int> vec = {1, 2, 3, 4, 5};
    std::map<std::string, int> m = {{"one", 1}, {"two", 2}, {"three", 3}};

    std::cout << "vec[0] = " << vec[0] << std::endl;
    std::cout << "vec[1] = " << vec[1] << std::endl;
    std::cout << "m[\"one\"] = " << m["one"] << std::endl;
    std::cout << "m[\"two\"] = " << m["two"] << std::endl;

    return 0;
}
```

The output of this program would be:

vec[0] = 1
vec[1] = 2
m["one"] = 1
m["two"] = 2

In this example, we have a std::vector of int s called vec and a std::map of int s called m. We use the subscript operator [] to access the elements of the vector and map, specifying the index of the element that we want to access. The indices for a vector are integer values starting from 0, while the indices for a map are keys of the appropriate type (in this case, std::string).

It's important to note that the subscript operator can be used to both read from and write to the elements of an array or container. For example:

arr[0]





### typeid operator in

在 C++ 中，`typeid` 运算符用于在运行时确定表达式的类型。它返回一个 `std::type_info` 对象，该对象描述表达式的类型。

以下是 `typeid` 运算符用法的示例：

```
#include <iostream>
#include <typeinfo>

int main()
{
    int x = 10;
    double y = 3.14;
    std::string z = "hello";

    std::cout << "typeid(x).name() = " << typeid(x).name() << std::endl;
    std::cout << "typeid(y).name() = " << typeid(y).name() << std::endl;
    std::cout << "typeid(z).name() = " << typeid(z).name() << std::endl;

    return 0;
}
```

此程序的输出取决于实现，但可能看起来像这样：

typeid(x).name() = i
typeid(y).name() = d
typeid(z).name() = NSt3__112basic_stringIcNS_11char_traitsIcEENS_9allocatorIcEEEE

在此示例中，我们有三个变量：x 的类型为 `int`，y 的类型为 `double`，z 的类型为 `std::string`。我们使用 `typeid` 运算符在运行时确定每个变量的类型，并使用返回的 `std::type_info` 对象的 `name` 成员函数获取类型的名称。

需要注意的是，`typeid` 运算符只能与具有已定义类型的表达式一起使用。它不能与具有未定义或不完整类型的表达式一起使用，例如未初始化的变量或具有不完整类类型的变量。

例如：

```
int x;
std::cout << "typeid(x).name() = " << typeid(x).name() << std::endl; // error: x has an undefined type
```

在此示例中，变量 x 的类型未定义，因为它未初始化。对 x 使用 typeid 运算符将导致编译时错误。

### Unary plus and negation operators: + and -

在 C++ 中，一元加法和取反运算符（ + 和 - ）用于对单个操作数执行算术运算。一元加法运算符返回操作数的值，而一元取反运算符返回操作数值的取反。

以下是这些运算符用法的示例：

```
#include <iostream>

int main()
{
    int x = 10;
    int y = -20;

    std::cout << "+x = " << +x << std::endl;
    std::cout << "-x = " << -x << std::endl;
    std::cout << "+y = " << +y << std::endl;
    std::cout << "-y = " << -y << std::endl;

    return 0;
}
```

此程序的输出将为：

+x = 10
-x = -10
+y = -20
-y = 20

在此示例中，我们有两个变量：x 和 y。x 的值为 10，而 y 的值为 -20。

我们使用一元加法运算符 + 返回 x 的值，即 10。我们使用一元取反运算符 - 返回 x 值的取反，即 -10。

我们使用一元加法运算符 + 返回 y 的值，即 -20。我们使用一元取反运算符 - 返回 y 值的取反，

即 20。

需要注意的是，一元加法运算符实际上并没有执行任何算术运算，它只是返回操作数的值。它通常用于明确指出一个值为正值，尤其是在该值被其他算术运算符包围时。

例如：

```
int a = 10;
int b = 20;
int c = -30;
```

```
std::cout << a + b - c << std::endl; // output: 40
std::cout << a + +b - c << std::endl; // output: 50
```

在第一个示例中，表达式 a + b - c 被计算为 10 + 20 - (-30)，结果为 40。

在第二个示例中，表达式 a + +b - c 被计算为 10 + (+20) - (-30)，结果为 50。一元加法运算符用于明确指出 b 的值为正值，即使它已经是正值。

### Expressions

在 C++ 中，表达式是由一个或多个操作数和运算符组合而成，可以求值为单个值的组合。表达式可以很简单，例如常量值或变量，也可以很复杂，涉及多个操作和函数调用。

以下是 C++ 中表达式的一些示例：

```
1 + 2 // simple expression, evaluates to 3
x + y // simple expression, evaluates to the sum of x and y
f(x) // function call expression, evaluates to the return value of the function f
x + y * z // complex expression, evaluates to the sum of x and the product of y and z
```

表达式可以在 C++ 的多种上下文中使用，包括作为赋值语句的右手边、作为函数的参数，或作为更大表达式的一部分。

例如：

```
int x = 1 + 2; // assignment statement, x is assigned the value 3
int y = f(x + 3); // function call, y is assigned the return value of f(x + 3)
if (x > 0 && y < 10) // conditional statement, tests whether x is greater than 0 and y is less than 10
    std::cout << "x is positive and y is less than 10" << std::endl;
```

需要注意的是，表达式可能具有副作用，例如修改变量的值或执行其他操作。例如：

```
int x = 1;
int y = x++; // y is assigned the value of x before x is incremented
std::cout << "x = " << x << " y = " << y << std::endl; // output: x = 2 y = 1
```

在此示例中，表达式 x++ 在用于为 y 赋值后递增 x 的值。程序的输出为 x = 2 y = 1，表明 x 在用于赋值后被递增。

## Chapter six

### Types of expressions

在 C++ 中，有几种不同类型的表达式，每种都有自己的语法和求值规则。一些常见的表达式类型包括：

- Arithmetic expressions: 这些表达式涉及算术运算，例如加法、减法、乘法和除法。它们可以包含常量、变量和其他算术表达式作为操作数。例如：`1 + 2`，`x + y`，`x * y / z`。
- Relational expressions: 这些表达式涉及比较运算符，例如 `<`、`>`、`<=` 和 `>=`，并求值为布尔值，表示比较为真或假。它们可以包含常量、变量和其他算术表达式作为操作数。例如：`x < y`，`a <= b`，`c > d`。
- Logical expressions: 这些表达式涉及逻辑运算符，例如 `&&`（与）、`||`（或）和 `!`（非），并求值为布尔值，表示逻辑运算为真或假。它们可以包含常量、变量和其他逻辑表达式作为操作数。例如：`x && y`，`a || b`，`!c`。
- Assignment expressions: 这些表达式涉及赋值运算符 `=` 并用于为变量赋值。它们可以包含常量、变量，

### Primary expressions

在 C++ 中，一元表达式是可独立存在且无需任何额外运算符即可求值的简单表达式。初级表达式包括字面量、变量、函数调用以及对象或成员访问表达式。

以下是 C++ 中初级表达式的一些示例：

- Literals: 诸如整数字面量（`42`）、浮点字面量（`3.14`）、字符字面量（`'a'`）和字符串字面量（`"hello"`）等常量都是初级表达式。
- Variables: 诸如 `x`、`y` 和 `z` 的变量都是初级表达式。
- Function calls: 诸如 f(x, y, z) 的函数调用都是初级表达式。
- Object or member access expressions: 访问对象或对象成员的表达式，例如 obj.x、ptr->y 和 arr[i]，都是初级表达式。

初级表达式通常用作较大表达式中的操作数，但也可以单独使用。

例如：

```
int x = 10;
double y = 3.14;
std::string z = "hello";
```

```
std::cout << x << std::endl; // primary expression: variable x
std::cout << y << std::endl; // primary expression: variable y
std::cout << z << std::endl; // primary expression: variable z
std::cout << f(x, y) << std::endl; // primary expression: function call f(x, y)
```

在此示例中，我们有三个变量：x 的类型为 int，y 的类型为 double，z 的类型为 std::string。我们在单独的 std::cout 语句中使用每个变量作为初级表达式。我们还使用函数调用 f(x, y) 作为初级表达式。

需要注意的是，初级表达式不包括需要额外运算符求值的表达式，例如算术表达式或逻辑表达式。例如，x + y 和 x && y 不是初级表达式。





### 省略号和可变参数模板

在 C++ 中，省略号（ ... ）用于表示可变参数函数，即可以接受可变数量参数的函数。省略号用于函数参数列表中以表示可变数量的参数。

以下是 C++ 中可变参数函数的示例：

```
#include <iostream>
#include <string>

void print_all(const char* fmt, ...)
{
    va_list args;
    va_start(args, fmt);

    while (*fmt) {
        if (*fmt == '%') {
            ++fmt;
            if (*fmt == 'd') {
                std::cout << va_arg(args, int);
            } else if (*fmt == 's') {
                std::cout << va_arg(args, const char*);
            } else if (*fmt == 'f') {
                std::cout << va_arg(args, double);
            }
        } else {
            std::cout << *fmt;
        }
        ++fmt;
    }

    va_end(args);
}

int main()
{
    print_all("%d %s %f", 10, "hello", 3.14);
    return 0;
}
```

在此示例中，我们有一个名为 print_all 的函数，它接受可变数量的参数。第一个参数是 const char* 类型的 fmt ，它指定了剩余参数的格式。参数列表中的省略号（ ... ）表示可以有任意数量的额外参数。在函数内部，我们使用 va_list 、 va_start 、 va_arg 和 va_end 宏来访问可变参数。 va_list 类型用于保存参数列表， va_start 宏用于将 va_list 初始化为 fmt 之后第一个参数。 va_arg 宏用于从列表中检索下一个参数， va_end 宏用于在我们完成使用后清理 va_list 。

在此示例中，我们使用循环遍历 fmt 字符串中的字符。如果我们遇到 % 字符，我们将 fmt 字符串的指针递增并检查下一个字符以确定下一个参数的类型。如果下一个字符是 d，我们将下一个参数作为 int 打印，如果是 s，我们将下一个参数作为 const char* 打印，如果是 f，我们将下一个参数作为 double 打印。

此程序的输出为：

10 hello 3.14

### 后缀表达式

在计算机科学中，后缀表达式是一种表达式，其中每个运算符都跟在其操作数之后。这与中缀表达式形成对比，在中缀表达式中，运算符放置在其操作数之间。

例如，中缀表达式 "2 + 3 * 4" 将在后缀记法中写成 "2 3 4 * +"。

### 包含一元运算符的表达式

一元运算符是作用于单个操作数的运算符。在 C++ 中，有多个一元运算符，包括：

- ++ （递增运算符）
- -- （递减运算符）
- + （一元加）
- - （一元减）
- ! （逻辑非）
- ~ （按位非）
- * （解引用运算符）
- & （引用运算符）

以下是如何在 C++ 中使用一元递增运算符（ ++ ）的示例：

```
#include <iostream>

using namespace std;

int main()
{
    int x = 10;

    // Prefix increment: value is incremented, then used
    cout << ++x << endl; // Outputs 11

    // Postfix increment: value is used, then incremented
    cout << x++ << endl; // Outputs 11
    cout << x << endl; // Outputs 12

    return 0;
}
```

一元递减运算符（ -- ）的工作方式类似。

你可以使用一元加和减运算符来改变值的符号：

```
int x = 10;
cout << +x << endl; // Outputs 10
cout << -x << endl; // Outputs -10
```

逻辑非运算符（ ! ）可用于反转布尔表达式的真值：

```
bool x = true;
cout << !x << endl; // Outputs false
```

按位非运算符（ ~ ）可用于反转整数值的位：

```
int x = 10; // Binary representation: 00000000000000000000000000001010
cout << ~x << endl; // Outputs -11 (11111111111111111111111111110101)
```

解引用运算符（ * ）用于访问存储在内存地址中的值：

```
int x = 10;
int *ptr = &x; // ptr holds the memory address of x
cout << *ptr << endl; // Outputs 10 (the value stored at the memory address held by ptr)
```

引用运算符（ & ）用于获取变量的内存地址：

```
int x = 10;
int *ptr = &x; // ptr holds the memory address of x
cout << ptr << endl; // Outputs the memory address of x
```

### 包含二元运算符的表达式

二元运算符是作用于两个操作数的运算符。在 C++ 中，有多个二元运算符，包括：

- + （加法）
- - （减法）
- * （乘法）
- / （除法）
- % （取模）
- = （赋值）
- += （加法赋值）
- -= （减法赋值）
- *= （乘法赋值）
- /= （除法赋值）
- %= （取模赋值）
- == （等于）
- != （不等于）
- > （大于）
- < （小于）
- >= （大于或等于）
- <= （小于或等于）
- && （逻辑与）
- || （逻辑或）
- & （按位与）
- | （按位或）
- ^ （按位异或）
- << （左移）
- >> （右移）

以下是如何在 C++ 中使用其中一些运算符的示例：

```
#include <iostream>

using namespace std;

int main()
{
    int x = 10, y = 5;

    // Arithmetic operators
    cout << x + y << endl; // Outputs 15
    cout << x - y << endl; // Outputs 5
    cout << x * y << endl; // Outputs 50
    cout << x / y << endl; // Outputs 2

    // Assignment operator
    int z = x;
    cout << z << endl; // Outputs 10

    // Comparison operators
    cout << (x == y) << endl; // Outputs false
    cout << (x != y) << endl; // Outputs true
    cout << (x > y) << endl; // Outputs true
    cout << (x < y) << endl; // Outputs false

    // Logical operators
    cout << (x > 0 && y < 10) << endl; // Outputs true
    cout << (x > 0 || y > 10) << endl; // Outputs true

    // Bitwise operators
    cout << (x & y) << endl; // Outputs 0 (binary:
00000000000000000000000000001010 & 00000000000000000000000000000101 =
00000000000000000000000000000000)
    cout << (x | y) << endl; // Outputs 15 (binary:
00000000000000000000000000001010 | 00000000000000000000000000000101 =
00000000000000000000000000001111)
    cout << (x ^ y) << endl; // Outputs 15 (binary:
00000000000000000000000000001010 ^ 00000000000000000000000000000101 =
00000000000000000000000000001111)

    return 0;
}
```

### 常量表达式

在 C++ 中，常量表达式是在编译时而不是在运行时可以求值的表达式。常量表达式通常用于用固定值初始化变量或指定数组大小。
在 C++ 中创建常量表达式有几种方法：

- 1. 使用常量：任何字面值（例如 42、3.14 或 'A'）都是常量表达式。
- 2. 使用 const 变量：使用 const 关键字声明的变量是常量表达式。例如：
- 3. 使用 constexpr 变量：使用 constexpr 关键字声明的变量是常量表达式。例如：
- 4. 使用枚举：枚举常量在 C++ 中被视为常量。例如：
- 5. 使用 constexpr 函数：使用 constexpr 关键字声明并满足某些条件（例如具有单个 return 语句）的函数可用于常量表达式。例如：

```
const int x = 42;
const double pi = 3.14;
const char c = 'A';
```

```
constexpr int x = 42;
constexpr double pi = 3.14;
constexpr char c = 'A';
```

```
enum Colors { Red, Green, Blue };

constexpr Colors favoriteColor = Green;
```

```
constexpr int square(int x)
{
    return x * x;
}

constexpr int x = square(5); // x is 25
```

以下是如何在 C++ 中使用常量表达式初始化数组的示例：

```
#include <iostream>

using namespace std;

constexpr int N = 5; // N is a constant expression

int main()
{
    int arr[N]; // arr has 5 elements

    for (int i = 0; i < N; i++)
        arr[i] = i * i;

    for (int i = 0; i < N; i++)
        cout << arr[i] << " "; // Outputs 0 1 4 9 16

    return 0;
}
```

### 表达式的语义

在 C++ 中，表达式的语义是指表达式在求值时的含义和行为。C++ 中求值表达式的规则由运算符优先级和结合性规则以及操作数的类型和值决定。

以下是 C++ 中求值表达式的一些通用规则：

- 1. 可以使用括号来覆盖默认的优先级和结合性规则。括号内的表达式总是首先求值。
- 2. 一元运算符在二元运算符之前求值。例如，在表达式 !x + y 中，逻辑非运算符（!）在加法运算符（+）应用于 x 和 y 之前应用于 x。
- 3. 二元运算符按优先级从高到低的顺序求值。例如，在表达式 x + y * z 中，乘法运算符（*）的优先级高于加法运算符（+），因此 y 和 z 先相乘。
- 4. 具有相同优先级的运算符从左到右求值（对于左结合运算符）或从右到左求值（对于右结合运算符）。例如，在表达式 x = y = z 中，赋值运算符（=）是右结合的，因此 z 先赋给 y，然后该赋值的結果再赋给 x。





Here is an example of how these rules can be applied in a C++ expression:

```
#include <iostream>

using namespace std;

int main()
{
    int x = 1, y = 2, z = 3;

    // The expression is evaluated as ((x + y) * (z + 1))
    int result = (x + y) * (z + 1);
    cout << result << endl; // Outputs 9

    return 0;
}
```

In this example, the addition operator ( + ) has a lower precedence than the multiplication operator ( * ), so the expressions within the parentheses are evaluated first. The addition operator ( + ) is left-associative, so x and y are added first, then z and 1 are added. The result of these additions is then multiplied to produce the final result.

### what is Casting

In C++, casting is the process of converting a value of one type to a value of another type. There are several ways to perform casting in C++:

- 1. Static cast: The static_cast operator is used to perform a safe, explicit type conversion. It can be used to convert a value from one type to another, as long as the target type is explicitly specified. For example:

```
double x = 3.14;
int y = static_cast<int>(x); // y is 3
```

- 2. Dynamic cast: The dynamic_cast operator is used to perform a type conversion at runtime. It is used to convert a pointer or reference from a base class type to a derived class type. For example:

```
class Base { };
class Derived : public Base { };
```

```
Base *b = new Base();
Derived *d = dynamic_cast<Derived*>(b); // d is nullptr
```

- 3. Reinterpret cast: The reinterpret_cast operator is used to interpret the bits

of a value as a value of a different type. It is used to convert a pointer to an integer type, or vice versa. For example:

```
int x = 42;
char *ptr = reinterpret_cast<char*>(&x); // ptr points to the first byte of x
```

- 4. Const cast: The `const_cast` operator is used to remove the `const` qualifier from a value. It is used to modify a `const` value, or to pass a `const` value to a function that expects a non-`const` parameter. For example:

```
const int x = 42;
int *ptr = const_cast<int*>(&x); // ptr points to x, but x can be modified through ptr
```

It is important to note that casting can sometimes result in loss of information or undefined behavior if the target type is not capable of representing the value being converted. Therefore, it is important to use casting cautiously and only when necessary.

## seventh chapter

### Casting operators

In C++, casting refers to the process of converting a value of one data type to another data type. This can be done using a variety of casting operators, including:

- 1. `static_cast` : This operator is used to perform a safe, explicit type conversion. It can be used to convert values between compatible types, such as converting an `int` to a `float` .
- 2. `dynamic_cast` : This operator is used to perform a safe, downcast conversion from a base class to a derived class. It is used when the type of the object being converted is not known at compile-time, and is typically used in conjunction with polymorphism.
- 3. `const_cast` : This operator is used to remove the `const` or `volatile` attribute from a variable. It can be used to cast away the `const` or `volatile` qualifier from a pointer or reference, allowing the value to be modified.
- 4. `reinterpret_cast` : This operator is used to perform a low-level, implementation-defined type conversion. It can be used to convert a value of one type to a value of a different type, regardless of whether the two types are related. This operator is generally used to cast pointers to and from integer types, or to cast one pointer type to another.

It's important to note that these casting operators can often result in undefined behavior if used improperly, so they should be used with caution.

### dynamic_cast operator

The `dynamic_cast` operator in C++ is used to perform a safe, downcast conversion from a base class to a derived class. It is typically used in conjunction with polymorphism, where a pointer or reference to a base class is used to refer to objects of derived classes.

The syntax for using `dynamic_cast` is as follows:

```
derived_type *ptr = dynamic_cast<derived_type*>(base_ptr);
```

Where derived_type is the type of the derived class and base_ptr is a pointer to the base class. If the conversion is successful, dynamic_cast will return a pointer to the derived class. If the conversion is not possible (for example, if base_ptr does not actually point to an object of the derived class), dynamic_cast will return a null pointer.

Here is an example of using dynamic_cast to downcast a pointer to a base class:

```
#include <iostream>

class Shape {
public:
    virtual ~Shape() {}
};

class Circle : public Shape {
public:
    void Draw() { std::cout << "Drawing a circle" << std::endl; }
};

int main() {
    Shape *shape = new Circle;
    Circle *circle = dynamic_cast<Circle*>(shape);
    if (circle != nullptr) {
        circle->Draw();
    } else {
        std::cout << "Error: shape is not a circle" << std::endl;
    }
    return 0;
}
```

In this example, the dynamic_cast operator is used to downcast a pointer to a Shape object to a pointer to a Circle object. If the Shape object is actually a Circle, the conversion will succeed and the Draw method will be called on the Circle object. If the Shape object is not a Circle, the dynamic_cast operator will return a null pointer and the Draw method will not be called.

### bad_cast exception

The bad_cast exception is a type of exception that is thrown by the dynamic_cast operator in C++ when it fails to perform a downcast conversion from a base class to a derived class.

The bad_cast exception is defined in the stdexcept header and is derived from the exception class. It can be caught using a try - catch block, like any other exception:

```
#include <iostream>
#include <stdexcept>

int main() {
    try {
        Shape *shape = new Shape;
        Circle *circle = dynamic_cast<Circle*>(shape);
    } catch (std::bad_cast& e) {
        std::cout << "Error: " << e.what() << std::endl;
    }
    return 0;
}
```

In this example, the dynamic_cast operator will fail to convert the Shape object to a Circle object, and will throw a bad_cast exception. The exception will be caught in the catch block, and the error message will be printed to the console.

It's important to note that the bad_cast exception will only be thrown if the dynamic_cast operator fails to perform the conversion. If the conversion is successful, the bad_cast exception will not be thrown.

### static_cast operator

The static_cast operator in C++ is used to perform a safe, explicit type conversion. It can be used to convert values between compatible types, such as converting an int to a float, or to convert a pointer to a base class to a pointer to a derived class.

The syntax for using static_cast is as follows:

```
destination_type value = static_cast<destination_type>(expression);
```

Where destination_type is the type to which the value of expression will be converted, and expression is the value to be converted.

Here is an example of using static_cast to convert an int to a float :

```
#include <iostream>

int main() {
    int x = 5;
    float y = static_cast<float>(x);
    std::cout << "y = " << y << std::endl;
    return 0;
}
```

In this example, the value of x is converted from an int to a float using the static_cast operator, and the result is stored in the float variable y. The output of this program will be "y = 5.0".

It's important to note that static_cast does not perform any runtime checks to ensure that the conversion is valid. It is the responsibility of the programmer to ensure that the conversion is safe and will not result in undefined behavior.

### const_cast operator

The const_cast operator in C++ is used to remove the const or volatile attribute from a variable. It can be used to cast away the const or volatile qualifier from a pointer or reference, allowing the value to be modified.

The syntax for using const_cast is as follows:

```
destination_type value = const_cast<destination_type>(expression);
```

Where destination_type is the type to which the value of expression will be converted, and expression is the value to be converted.

Here is an example of using const_cast to remove the const attribute from a const int :

```
#include <iostream>

int main() {
    const int x = 5;
    int *y = const_cast<int*>( &x );
    *y = 10;
    std::cout << "x = " << x << std::endl;
    return 0;
}
```

In this example, the const_cast operator is used to remove the const attribute from a pointer to x. This allows the value of x to be modified through the pointer y. The output of this program will be "x = 10", even though x is declared as a const int.





需要注意的是，使用 const_cast 修改 const 或 volatile 变量可能会导致未定义行为，如果该变量实际上是 intended to be const 或 volatile。const_cast 应谨慎使用。

### reinterpret_cast 运算符

C++ 中的 reinterpret_cast 运算符用于执行低级、实现定义的类型的转换。它可用于将一种类型的值转换为另一种类型的值，而不管这两种类型是否相关。该运算符通常用于在指针和整数类型之间进行转换，或将一种指针类型转换为另一种指针类型。

使用 reinterpret_cast 的语法如下：

```
destination_type value = reinterpret_cast<destination_type>(expression);
```

其中 destination_type 是 expression 的值将被转换成的类型，而 expression 是要转换的值。

以下是使用 reinterpret_cast 将指针转换为 int 的示例：

```
#include <iostream>

int main() {
    int x = 5;
    int *ptr = &x;
    std::cout << "ptr = " << ptr << std::endl;
    int y = reinterpret_cast<int>(ptr);
    std::cout << "y = " << y << std::endl;
    return 0;
}
```

在此示例中，reinterpret_cast 运算符用于将指针转换为 int。该程序的输出将是 x 的地址作为整数值。需要注意的是，reinterpret_cast 不会对正在转换的值执行任何类型检查或转换。它只是将值视为一系列位，并将这些位重新解释为目标类型的值。如果正在转换的类型不兼容，这可能会导致未定义行为。

reinterpret_cast 应谨慎使用。

## 第八章

### 运行时类型信息（RTTI）

运行时类型信息（RTTI）是 C++ 编程语言的一项功能，允许程序员在运行时确定对象的类型。RTTI 使用一组特殊函数和 typeid 表达式实现，通常与多态结合使用，以确定当使用指向基类的指针或引用来引用派生类对象时对象的实际类型。

要使用 RTTI，您必须首先通过包含 <typeinfo> 头文件并使用 -frtti 标志编译代码来启用它。

以下是使用 RTTI 确定对象类型的示例：

```
#include <iostream>
#include <typeinfo>

class Shape {
public:
    virtual ~Shape() {}
};

class Circle : public Shape {
public:
    void Draw() { std::cout << "Drawing a circle" << std::endl; }
};

int main() {
    Shape *shape = new Circle;
    std::cout << "Type of shape: " << typeid(*shape).name() << std::endl;
    return 0;
}
```

在此示例中，typeid 运算符用于确定 shape 指向的对象的类型。该程序的输出将是 "Type of shape: class Circle"，表明该对象实际上是一个 Circle 对象，即使它是通过指向 Shape 对象的指针引用的。

需要注意的是，RTTI 可能会对代码的性能产生影响，因为它需要在运行时进行额外的检查来确定对象的类型。它应谨慎使用，仅在必要时使用。

### bad_typeid 异常

bad_typeid 异常是 C++ 中 typeid 运算符在对具有已删除或不完整类型的对象使用时抛出的异常类型。

bad_typeid 异常在 stdexcept 头文件中定义，并派生自 exception 类。它可以使用 try-catch 块捕获，就像其他任何异常一样：

```
#include <iostream>
#include <stdexcept>

int main() {
    try {
        Shape *shape = nullptr;
        std::cout << "Type of shape: " << typeid(*shape).name() << std::endl;
    } catch (std::bad_typeid& e) {
        std::cout << "Error: " << e.what() << std::endl;
    }
    return 0;
}
```

在此示例中，typeid 运算符用于空指针，该指针具有已删除的类型。这将导致抛出 bad_typeid 异常，该异常将在 catch 块中捕获，并将错误消息打印到控制台。

需要注意的是，只有当 typeid 运算符用于具有已删除或不完整类型的对象时，才会抛出 bad_typeid 异常。如果对象具有完整且有效的类型，则不会抛出 bad_typeid 异常。

### type_info 类

C++ 中的 type_info 类是表示运行时类型信息的类。它与 typeid 运算符结合使用，以检索有关对象的类型信息。

type_info 类在 <typeinfo> 头文件中定义，并提供多个成员函数用于访问类型信息：

- name() : 返回包含类型名称的以空字符结尾的字符数组。
- hash_code() : 返回类型的唯一哈希码。
- before(const type_info& rhs) : 如果此 type_info 对象表示的类型在字典上小于 rhs type_info 对象表示的类型，则返回 true。
- operator==(const type_info& rhs) : 如果此 type_info 对象表示的类型与 rhs type_info 对象表示的类型相同，则返回 true。
- operator!=(const type_info& rhs) : 如果此 type_info 对象表示的类型与 rhs type_info 对象表示的类型不同，则返回 true。

以下是使用 type_info 类比较两个对象的类型的示例：

```
#include <iostream>
#include <typeinfo>

class Shape {
public:
    virtual ~Shape() {}
};

class Circle : public Shape {
public:
    void Draw() { std::cout << "Drawing a circle" << std::endl; }
};

int main() {
    Shape *shape1 = new Shape;
    Shape *shape2 = new Circle;
    if (typeid(*shape1) == typeid(*shape2)) {
        std::cout << "shape1 and shape2 are the same type" << std::endl;
    } else {
        std::cout << "shape1 and shape2 are different types" << std::endl;
    }
    return 0;
}
```

在此示例中，typeid 运算符用于检索 shape1 和 shape2 指向的对象的 type_info 对象。然后使用 type_info 类的 operator== 成员函数比较这两种类型。该程序的输出将是 "shape1 and shape2 are different types"，表明这两个对象是不同类型的。

### 语句

在 C++ 中，语句是一段执行操作或修改程序状态的代码。C++ 中有几种类型的语句，包括：

1. 表达式语句：表达式语句由单个表达式后跟分号组成。表达式语句用于计算表达式并丢弃结果。
2. 声明语句：声明语句将新名称引入程序并指定命名实体的类型和初始值。声明语句用于定义变量、函数和其他命名实体。
3. 选择语句：选择语句用于根据条件的值执行不同的代码块。C++ 中的两种选择语句是 if 和 switch。
4. 迭代语句：迭代语句，也称为循环，用于多次执行代码块。C++ 中的三种迭代语句是 for、while 和 do-while。
5. 跳转语句：跳转语句用于将控制转移到程序的另一部分。C++ 中的三种跳转语句是 break、continue 和 goto。

语句是 C++ 的重要组成部分，用于控制执行流程并在程序中执行操作。

### C++ 语句概述

在 C++ 中，语句用于执行操作或修改程序的状态。C++ 中有几种类型的语句，包括：

1. 表达式语句：表达式语句用于计算表达式并丢弃结果。它们通常用于调用函数、执行赋值以及递增或递减变量。
2. 声明语句：声明语句用于将新名称引入程序并指定命名实体的类型和初始值。声明语句可用于定义变量、函数和其他命名实体。
3. 选择语句：选择语句用于根据条件的值执行不同的代码块。if 语句用于在条件为真时执行代码块，而 switch 语句用于根据值的



variable.

- 4. 迭代语句：迭代语句，也称为循环，用于多次执行一段代码。`for` 循环用于执行一段代码特定次数，`while` 循环用于在条件为真时执行一段代码，而 `do-while` 循环则在评估条件之前至少执行一次代码。

- 5. 跳转语句：跳转语句用于将控制转移到程序的另一部分。`break` 语句用于退出循环或 switch 语句，`continue` 语句用于跳过当前循环迭代的剩余部分，而 `goto` 语句用于将控制转移到带标签的语句。

语句是 C++ 的重要组成部分，用于控制执行流程并在其中执行操作

### 标签语句

在 C++ 中，标签语句用于在代码块内创建命名位置。标签语句通常与 `goto` 语句结合使用，以将控制转移到程序中的特定位置。

要创建标签语句，可以使用任何有效标识符后跟冒号：

```
label: statement
```

以下是 C++ 中使用标签语句的示例：

```
#include <iostream>

int main() {
    int x = 0;
    start:
    std::cout << "x = " << x << std::endl;
    x++;
    if (x < 10) {
        goto start;
    }
    return 0;
}
```

在此示例中，标签语句 start: 在代码块内创建了一个命名位置。然后使用 goto start 语句将控制转移到 start 标签并执行标签后的语句。这将导致代码块执行 10 次，x 的值每次增加 1。该程序的输出将是 0 到 9 的数字，每行一个。

需要注意的是，goto 语句通常被认为是一种不太理想的控制流机制，应谨慎使用。它会使代码难以阅读和理解，并可能导致结构不良且难以维护的代码。在大多数情况下，使用 goto 语句通常有更易读且更易维护的替代方案。

### 表达式语句

在 C++ 中，表达式语句是由单个表达式后跟分号组成的语句。表达式语句用于计算表达式并丢弃结果。

以下是 C++ 中表达式语句的示例：

```
#include <iostream>

int main() {
    int x = 5;
    x++;  // expression statement
    std::cout << "x = " << x << std::endl;
    return 0;
}
```

在此示例中，表达式 x++ 是一个表达式语句，将 x 的值递增 1。表达式的结果被丢弃，x 的值被修改。该程序的输出将是 "x = 6"。

表达式语句通常用于执行赋值、递增或递减变量以及调用函数。它们是 C++ 的重要组成部分，用于修改程序的状态。

### 空语句

在 C++ 中，空语句是由单个分号组成的语句。空语句用于在程序中创建占位符，在此处需要语句但不需要操作。

以下是 C++ 中空语句的示例：

```
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        ;  // null statement
    }
    return 0;
}
```

在此示例中，空语句 ; 用作 for 循环的主体。这创建了一个将执行 10 次的循环，但在每次迭代时不会采取任何操作。

空语句通常用作占位符，在需要语句但不需要采取操作的情况下使用。它们是创建更易读和更易理解的代码的有用工具。

### 复合语句（块）

在 C++ 中，复合语句，也称为块，是作为一个单元一起执行的一组语句。复合语句通常用于将语句分组并为变量创建新的作用域。

复合语句用花括号 {} 括起来，可以包含任意数量的语句。以下是 C++ 中复合语句的示例：

```
#include <iostream>

int main() {
    int x = 5;
    { // start of compound statement
        int y = 10;
        std::cout << "x + y = " << x + y << std::endl;
    } // end of compound statement
    return 0;
}
```

在此示例中，复合语句 { int y = 10; std::cout << "x + y = " << x + y << std::endl; } 为变量 y 创建了一个新的作用域，该变量只能在复合语句内访问。该程序的输出将是 "x + y = 15"。

复合语句是 C++ 的重要组成部分，用于将语句分组并为变量创建新的作用域。它们通常与选择和迭代语句结合使用，以创建作为一个单元执行的代码块。

## 第九章

### 选择语句

在 C++ 中，选择语句用于根据条件的值执行不同的代码块。C++ 中有两种选择语句：if 语句和 switch 语句。

if 语句用于在条件为真时执行代码块。if 语句的语法如下：

```
if (condition) {
    // code to be executed if condition is true
} else {
    // code to be executed if condition is false
}
```

以下是 C++ 中使用 if 语句的示例：

```
#include <iostream>

int main() {
    int x = 5;
    if (x > 0) {
        std::cout << "x is positive" << std::endl;
    } else {
        std::cout << "x is not positive" << std::endl;
    }
    return 0;
}
```

在此示例中，if 语句用于根据 x 的值执行不同的代码块。如果 x 大于 0，则将执行第一个代码块，并将消息 "x is positive" 打印到控制台。如果 x 不大于 0，则将执行第二个代码块，并将消息 "x is not positive" 打印到控制台。

switch 语句是 C++ 中的另一种选择语句，用于根据变量的值执行代码块。switch 语句的语法如下：

```
switch (expression) {
    case value1:
    // code to be
```

### if-else 语句

在 C++ 中，if-else 语句是一种选择语句，用于根据条件的值执行不同的代码块。if-else 语句由 if 子句和 else 子句组成，语法如下：

```
if (condition) {
    // code to be executed if condition is true
} else {
    // code to be executed if condition is false
}
```

if 子句用于指定条件，如果条件为真，则执行 if 子句后花括号内的代码。else 子句用于指定在条件为假时执行的备用代码块。

以下是 C++ 中使用 if-else 语句的示例：

```
#include <iostream>

int main() {
    int x = 5;
    if (x > 0) {
        std::cout << "x is positive" << std::endl;
    } else {
        std::cout << "x is not positive" << std::endl;
    }
    return 0;
}
```

在此示例中，if 子句指定条件 x > 0，如果此条件为真，则执行 if 子句后花括号内的代码。else 子句指定在条件为假时执行的备用代码块。如果 x 大于 0，则将消息 "x is positive" 打印到控制台。如果 x 不大于 0，则将消息 "x is not positive" 打印到控制台。

The `if

### __if_exists 语句

在 C++ 中，__if_exists 语句是一种预处理器指令，用于在指定符号存在时包含代码块。__if_exists 语句通常用于包含特定于特定编译器或平台的代码，语法如下：

```
#if __has_include(<symbol>)
```




```
#include <symbol>
#endif
```

Here is an example of using the __if_exists statement in C++:

```
#include <iostream>

#if __has_include(<windows.h>)
    #include <windows.h>
#endif

int main() {
    std::cout << "Hello, world!" << std::endl;
    return 0;
}
```

In this example, the __if_exists statement is used to include the windows.h header file if it exists. If the header file is not available, the block of code within the #if and #endif directives will be skipped and the windows.h header file will not be included.

The __if_exists statement is a useful tool for including code that is specific to a particular compiler or platform, and is often used to create code that is portable across different systems.

### __if_not_exists statement

In C++, the __if_not_exists statement is a preprocessor directive that is used to include a block of code if a specified symbol does not exist. The __if_not_exists statement is typically used to include code that is specific to a particular compiler or platform, and the syntax is as follows:

```
#if !__has_include(<symbol>)
    #include <symbol>
#endif
```

Here is an example of using the __if_not_exists statement in C++:

```
#include <iostream>

#if !__has_include(<windows.h>)
    #include "windows.h"
#endif

int main() {
    std::cout << "Hello, world!" << std::endl;
    return 0;
}
```

In this example, the __if_not_exists statement is used to include the windows.h header file if it does not exist. If the header file is available, the block of code within the #if and #endif directives will be skipped and the windows.h header file will not be included.

The __if_not_exists statement is a useful tool for including code that is specific to a particular compiler or platform, and is often used to create code that is portable across different systems.

### switch statement

In C++, the switch statement is a selection statement that is used to execute a block of code based on the value of a variable. The switch statement consists of a switch clause, a series of case clauses, and an optional default clause. The syntax for the switch statement is as follows:

```
switch (expression) {
    case value1:
        // code to be executed if expression == value1
        break;
    case value2:
        // code to be executed if expression == value2
        break;
    ...
    default:
        // code to be executed if expression does not match any of the case values
}
```

Here is an example of using the switch statement in C++:

```
#include <iostream>

int main() {
    int x = 3;
    switch (x) {
        case 1:
            std::cout << "x is 1" << std::endl;
            break;
        case 2:
            std::cout << "x is 2" << std::endl;
            break;
        case 3:
            std::cout << "x is 3" << std::endl;
            break;
        default:
            std::cout << "x is not 1, 2, or 3" << std::endl;
    }
    return 0;
}
```

In this example, the switch statement is used to execute different blocks of code based on the value of x. If x is 1, the message "x is 1" will be printed to the console. If x is 2, the message "x is 2" will be printed to the console. If x is 3, the message "x is 3" will be printed to the console. If x is none of these values, the message "x is not 1, 2, or 3" will be printed to the console.

The switch statement is a useful tool for executing code based on the value of a variable, and can be more efficient than using multiple if-else statements in certain situations. It is important to include the break statement at the end of each case clause to prevent the code from falling through to the next case.

The default clause is optional, but is generally included to specify a block of code to be executed if the expression does not match any of the case values.

### Iteration statements

In C++, iteration statements, also known as loops, are used to execute a block of code multiple times. There are three types of iteration statements in C++: the for loop, the while loop, and the do-while loop.

The for loop is used to execute a block of code a specific number of times.

The syntax for the for loop is as follows:

```
for (initialization; condition; increment) {
  // code to be executed
}
```

The initialization clause is used to initialize a loop variable, the condition clause is used to specify a condition that is checked before each iteration of the loop, and the increment clause is used to modify the loop variable at the end of each iteration.

Here is an example of using the for loop in C++:

```
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        std::cout << i << std::endl;
    }
    return 0;
}
```

In this example, the for loop is used to execute the block of code 10 times. The loop variable i is initialized to 0, and the condition i < 10 is checked before each iteration of the loop. If the condition is true, the block of code is executed and the loop variable is incremented by 1. This will cause the loop to execute 10 times, with the value of i increasing by

### while statement

In C++, the while loop is a type of iteration statement that is used to execute a block of code repeatedly while a condition is true. The syntax for the while loop is as follows:

```
while (condition) {
    // code to be executed
}
```

The condition clause is used to specify a condition that is checked before each iteration of the loop. If the condition is true, the block of code is executed. If the condition is false, the loop is terminated and control is transferred to the next statement following the loop.

Here is an example of using the while loop in C++:

```
#include <iostream>

int main() {
    int x = 0;
    while (x < 10) {
        std::cout << x << std::endl;
        x++;
    }
    return 0;
}
```

In this example, the while loop is used to execute the block of code 10 times. The condition x < 10 is checked before each iteration of the loop. If the condition is true, the block of code is executed and the value of x is incremented by 1. This will cause the loop to execute 10 times, with the value of x increasing by 1 each time. The output of this program will be the numbers 0 through 9, each on a separate line.

The while loop is a useful tool for executing a block of code repeatedly while a condition is true. It is important to include a statement within the loop that will eventually cause the condition to become

### do-while statement

In C++, the do-while loop is a type of iteration statement that is used to execute a block of code repeatedly while a condition is true. The syntax for the do-while loop is as follows:

```
do {
    // code to be executed
} while (condition);
```

The block of code is executed once before the condition is checked. If the condition is true, the block of code is executed again. If the condition is false, the loop is terminated and control is transferred to the next statement following the loop.

Here is an example of using the do-while loop in C++:

```
#include <iostream>

int main() {
    int x = 0;
    do {
        std::cout << x << std::endl;
        x++;
    } while (x < 10);
    return 0;
}
```

In this example, the do-while loop is used to execute the block of code 10 times. The block of code is executed once before the condition x < 10 is checked. If the condition is true, the block of code is executed again and the value of x is incremented by 1. This will cause the loop to execute 10 times, with the value of x increasing by 1 each time. The output of this program will be the numbers 0 through 9, each on a separate line.

The do-while loop

### for statement

In C++, the for loop is a type of iteration statement that is used to execute a block of code a specific number of times. The syntax for the for loop is as follows:

```
for (initialization; condition; increment) {
    // code to be executed
}
```

The initialization clause is used to initialize a loop variable, the condition clause is used to specify a condition that is checked before each iteration of the loop, and the increment clause is used to modify the loop variable at the end of each



iteration.

以下是 C++ 中使用 for 循环的示例：

```
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，for 循环用于执行代码块 10 次。循环变量 i 初始化为 0，并在每次迭代前检查条件 i < 10。如果条件为真，则执行代码块并将循环变量递增 1。这将导致循环执行 10 次，i 的值每次增加 1。该程序的输出将是 0 到 9 的数字，每行一个。

for 循环是执行特定次数的代码块的有用工具，常在迭代次数已知时使用。重要的是在循环中包含一个最终会使条件变为假的语句，否则循环将成为无限循环。

### 基于范围的 for 语句

在 C++ 中，基于范围的 for 循环是一种用于遍历范围内元素的迭代语句。基于范围的 for 循环的语法如下：

```
for (range_declaration : range_expression) {
    // code to be executed
}
```

range_declaration 是为范围中的每个元素声明的变量，而 range_expression 是指定要遍历范围的表达式。

以下是 C++ 中使用基于范围的 for 循环的示例：

```
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    for (int number : numbers) {
        std::cout << number << std::endl;
    }
    return 0;
}
```

在此示例中，基于范围的 for 循环用于遍历 numbers 向量中的元素。循环变量 number 为范围中的每个元素声明，而范围表达式 numbers 指定要遍历的范围。这将导致循环执行 5 次，number 的值依次设置为 numbers 向量中的每个元素。该程序的输出将是 1 到 5 的数字，每行一个。

基于范围的 for 循环是遍历范围内元素的有用工具，常用于简化使用传统 for 循环的代码。重要的是确保范围表达式指定的范围在循环期间未被修改，否则可能导致未定义行为。

## 第十章

### 跳转语句

在 C++ 中，跳转语句用于将控制转移到程序中的不同位置。C++ 中有四种跳转语句：break 语句、continue 语句、goto 语句和 return 语句。

break 语句用于终止循环或 switch 语句并将控制转移到循环或 switch 之后下一个语句。break 语句的语法如下：

```
break;
```

以下是 C++ 中使用 break 语句的示例：

```
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        if (i == 5) {
            break;
        }
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，break 语句用于在 i 的值为 5 时终止 for 循环。循环将执行 5 次，i 的值每次增加 1。当 i 的值变为 5 时，break 语句将被执行，循环将被终止。该程序的输出将是 0 到 4 的数字，每行一个。

continue 语句用于跳过当前循环迭代的剩余部分并将控制转移到下一次迭代。continue 语句的语法如下：

```
continue;
```

以下是 C++ 中使用 continue 语句的示例：

```
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 0) {
            continue;
        }
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，continue 语句用于在 i 的值为偶数时跳过 for 循环当前迭代的剩余部分。循环将执行 10 次，i 的值每次增加 1。如果 i 的值为偶数，则执行 continue 语句并跳过当前迭代的剩余部分。该程序的输出将是 1 到 9 的奇数，每行一个。

goto 语句用于将控制转移到同一函数中的带标签语句。goto 语句的语法如下：

```
goto label;
...
label:
// code to be executed
```

return 语句用于终止函数并返回一个值

### break 语句

在 C++ 中，break 语句是一种跳转语句，用于终止循环或 switch 语句并将控制转移到循环或 switch 之后下一个语句。break 语句的语法如下：

```
break;
```

以下是 C++ 中使用 break 语句的示例：

```
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        if (i == 5) {
            break;
        }
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，break 语句用于在 i 的值为 5 时终止 for 循环。循环将执行 5 次，i 的值每次增加 1。当 i 的值变为 5 时，break 语句将被执行，循环将被终止。该程序的输出将是 0 到 4 的数字，每行一个。

break 语句常用于在满足特定条件时提前终止循环或 switch 语句。重要的是仅在循环或 switch 语句的主体中使用 break 语句，因为在这些上下文之外使用它将导致编译时错误。

### continue 语句

在 C++ 中，continue 语句是一种跳转语句，用于跳过当前循环迭代的剩余部分并将控制转移到下一次迭代。continue 语句的语法如下：

```
continue;
```

以下是 C++ 中使用 continue 语句的示例：

```
#include <iostream>

int main() {
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 0) {
            continue;
        }
        std::cout << i << std::endl;
    }
    return 0;
}
```

在此示例中，continue 语句用于在 i 的值为偶数时跳过 for 循环当前迭代的剩余部分。循环将执行 10 次，i 的值每次增加 1。如果 i 的值为偶数，则执行 continue 语句并跳过当前迭代的剩余部分。该程序的输出将是 1 到 9 的奇数，每行一个。

continue 语句常用于在满足特定条件时跳过循环的某些迭代。重要的是仅在循环的主体中使用 continue 语句，因为在循环之外使用它将导致编译时错误。

### return 语句

在 C++ 中，return 语句是一种跳转语句，用于终止函数并将值返回给调用函数。return 语句的语法如下：

```
return expression;
```

expression 是一个可选表达式，指定要返回给调用函数的值。如果省略 expression，则函数返回函数返回类型的默认值。

以下是 C++ 中使用 return 语句的示例：

```
#include <iostream>

int add(int x, int y) {
    return x + y;
}

int main() {
    int result = add(2, 3);
    std::cout << result << std::endl;
    return 0;
}
```

在此示例中，return 语句用于将 add 函数的结果返回给调用函数。add 函数接受两个参数 x 和 y，并返回它们的和。return 语句在调用 add 函数时执行，x + y 的值被返回给调用函数。在



this case, the value 5 is returned and printed to the screen.

The return statement is used to terminate a function and return a value to the calling function. It is important to ensure that the return type of the function is compatible with the value being returned, as attempting to return a value of the wrong type will result in a compile-time error.

### goto statement

In C++, the goto statement is a jump statement that is used to transfer control to a labeled statement in the same function. The syntax for the goto statement is as follows:

```
goto label;
...
label:
  // code to be executed
```

The label is a user-defined identifier that is used to mark a point in the code to which control can be transferred.

Here is an example of using the goto statement in C++:

```
#include <iostream>

int main() {
    int x = 0;
    while (true) {
        x++;
        if (x % 2 == 0) {
            goto even;
        }
        std::cout << x << std::endl;
    }
    even:
        std::cout << "Even number: " << x << std::endl;
    return 0;
}
```

In this example, the goto statement is used to transfer control to the even label when the value of x is even. The while loop will execute indefinitely, with the value of x increasing by 1 each time. If the value of x is even, the goto statement will be executed and control will be transferred to the even label. At the even label, a message is printed to the screen indicating that an even number has been encountered.

The goto statement is generally considered to be a less desirable control flow construct than other options such as if statements, for loops, and while loops. It is generally recommended to use goto sparingly, if at all, as it can make code more difficult to understand and maintain.

### Transfers of control

In C++, transfers of control are used to change the flow of execution in a program. There are several types of transfers of control in C++, including:

- **Conditional statements**: Conditional statements are used to execute a block of code conditionally based on the value of a boolean expression. The if statement is used to execute a block of code if a condition is true, and the if-else statement is used to execute one block of code if a condition is true and another block of code if the condition is false.
- **Iteration statements**: Iteration statements are used to execute a block of code repeatedly. The while loop is used to execute a block of code while a condition is true, the do-while loop is used to execute a block of code at least once and then repeatedly while a condition is true, and the for loop is used to execute a block of code a specific number of times.
- **Jump statements**: Jump statements are used to transfer control to a different point in the program. The break statement is used to terminate a loop or switch statement and transfer control to the next statement following the loop or switch, the continue statement is used to skip the remainder of the current iteration of a loop and transfer control to the next iteration, the goto statement is used to transfer control to a labeled statement in the same function, and the return statement is used to terminate a function and return a value to the calling function.
- **Exception handling**: Exception handling is used to handle errors or exceptional circumstances that may occur during the execution of a program. The try statement is used to enclose a block of code that may throw an exception, the throw statement is used to throw an exception, and the catch statement is used to handle an exception that has been thrown.

### Namespaces

In C++, a namespace is a container for a set of identifiers (such as functions, variables, and classes). Namespaces are used to organize and manage the identifiers in a program, and to prevent name collisions between identifiers with the same name but different meanings.

The syntax for defining a namespace in C++ is as follows:

```
namespace namespace_name {
    // declarations
}
```

The namespace_name is the name of the namespace, and the declarations within the namespace are the identifiers that are contained within the namespace.

Here is an example of defining and using a namespace in C++:

```
#include <iostream>

namespace my_namespace {
    int x = 10;
    int y = 20;
    int add(int a, int b) {
        return a + b;
    }
}

int main() {
    std::cout << my_namespace::x << std::endl;
    std::cout << my_namespace::y << std::endl;
    std::cout << my_namespace::add(my_namespace::x, my_namespace::y) << std::endl;
    return 0;
}
```

In this example, the my_namespace namespace contains the variables x and y and the function add. The identifiers within the namespace can be accessed using the namespace_name::identifier syntax. In this case, the variables x and y are accessed using the my_namespace::x and my_namespace::y syntax, and the function `add` is accessed using the `my_namespace::add` syntax.

Namespaces are useful for organizing and managing the identifiers in a program, and for preventing name collisions between identifiers with the same name but different meanings. It is important to choose descriptive and unique names for namespaces to avoid conflicts with other namespaces in the same program.

### Enumerations

An enumeration (or enum) in C++ is a way to define a set of named integer constants. It is often used to assign meaningful names to a set of integral values, making it easier to understand and maintain the code.

Here's an example of how to define an enumeration:

```
enum Color {
    RED,    // RED is assigned the value 0
    GREEN,  // GREEN is assigned the value 1
    BLUE,   // BLUE is assigned the value 2
    YELLOW  // YELLOW is assigned the value 3
};
```

In this example, we have defined an enumeration called `Color` with four members: `RED`, `GREEN`, `BLUE`, and `YELLOW`. By default, the first member of an enumeration is assigned the value 0, and each subsequent member is assigned a value that is one greater than the previous member. So, in this case, `RED` is 0, `GREEN` is 1, `BLUE` is 2, and `YELLOW` is 3.

You can also specify the values for each member of the enumeration explicitly, like this:

```
enum Color {
    RED = 10,   // RED is assigned the value 10
    GREEN = 20,  // GREEN is assigned the value 20
    BLUE = 30,   // BLUE is assigned the value 30
    YELLOW = 40  // YELLOW is assigned the value 40
};
```

Once you have defined an enumeration, you can use its members like variables:

```
Color favoriteColor = RED;
```

```
if (favoriteColor == RED) {
    std::cout << "Your favorite color is red." << std::endl;
}
```

Enumerations are often used in conjunction with a switch statement to handle a fixed set of values:

```
switch (favoriteColor) {
    case RED:
        std::cout << "Your favorite color is red." << std::endl;
        break;
    case GREEN:
        std::cout << "Your favorite color is green." << std::endl;
        break;
    case BLUE:
        std::cout << "Your favorite color is blue." << std::endl;
        break;
    case YELLOW:
        std::cout << "Your favorite color is yellow." << std::endl;
        break;
    default:
        std::cout << "Your favorite color is unknown." << std::endl;
        break;
}
```

I hope this helps! Let me know if you have any questions.

### Unions

In C++, a union is a data type that allows you to store different data types in the same memory location. It is similar to a structure, but only one member can be accessed at a time.

Here is an example of how to define a union in C++:

```
union MyUnion
{
    int x;
    float y;
    char z;
};
```

In this example, the union MyUnion has three members: x, y, and z.

However, because a union only allows you to access one member at a time, you can only use one of these members at any given time.

To access the members of a union, you can use the . operator, just like you would with a structure:

```
MyUnion u;

u.x = 10;
std::cout << u.x << std::endl;  // Outputs 10

u.y = 3.14;
std::cout << u.y << std::endl;  // Outputs 3.14

u.z = 'a';
std::cout << u.z << std::endl;  // Outputs 'a'
```

Unions are often used when you want to store different data types in the same memory location, but you only need to access one of them at a time. This can be useful for saving memory in certain situations. However, you should be careful when using unions, as it is easy to accidentally overwrite the values of one member with another.

### Functions

In C++, a function is a block of code that performs a specific task and may return a value. Functions allow you to reuse code and divide a large program into smaller, more manageable pieces.

Here is an example of a simple function in C++:

```
int add(int x, int y)
{
    return x + y;
}
```

This function, called add, takes two integer arguments, x and y, and returns their sum as an integer.

To call this function and use its return value, you would do something like this:

```
int a = 3;
int b = 4;
int c = add(a, b);  // c is now equal to 7
```

In C++, functions can have different types of parameters and return values. For example, a function could return a floating-point value, or it could have no return value at all (in which case it would have a return type of void). Functions can also have default values for their parameters. This allows you to


要使用更少的参数调用函数，在这种情况下，缺失参数将使用默认值。以下是示例：

```
int add(int x, int y = 1)
{
    return x + y;
}

int a = 3;
int b = add(a);  // b is now equal to 4
```

函数是 C++ 的重要组成部分，在大多数程序中被广泛使用。它们可以帮助你编写更模块化、可重用的代码，从而使程序更易于理解和维护。

### 具有可变参数列表的函数

在 C++ 中，你可以使用 ... 记法定义一个具有可变数量参数的函数。这被称为“可变参数”函数。

以下是 C++ 中简单可变参数函数的示例：

```
void print(const char* format, ...)
{
    va_list args;
    va_start(args, format);

    while (*format != '\0')
    {
        if (*format == 'd')
        {
            int i = va_arg(args, int);
            std::cout << i << " ";
        }
        else if (*format == 'f')
        {
            double d = va_arg(args, double);
            std::cout << d << " ";
        }
        else if (*format == 'c')
        {
            int c = va_arg(args, int);
            std::cout << static_cast<char>(c) << " ";
        }
        else if (*format == 's')
        {
            char* s = va_arg(args, char*);
            std::cout << s << " ";
        }

        ++format;
    }

    va_end(args);
}
```

这个函数名为 print，以格式字符串作为第一个参数，并接受可变数量的额外参数。格式字符串指定额外参数的类型。例如，如果格式字符串是 "dff s"，这表示接下来的三个参数是整数，第四个参数是字符串。

要调用此函数，可以使用 ... 记法传入额外参数。以下是示例：
print("dff s", 10, 3.14, 5.67, "hello"); // Outputs "10 3.14 5.67 hello"

可变参数函数在需要向函数传递可变数量参数时很有用，但它们也可能比具有固定参数的函数更难使用和维护。通常建议尽可能使用固定参数函数，仅在必要时使用可变参数函数。

### 函数重载

在 C++ 中，函数重载是一种允许你使用相同名称定义多个函数但参数集不同的特性。C++ 编译器将根据传递给函数的参数数量和类型自动选择要调用的正确函数。

以下是 C++ 中函数重载的示例：

```
int add(int x, int y)
{
    return x + y;
}

double add(double x, double y)
{
    return x + y;
}

std::string add(const std::string& x, const std::string& y)
{
    return x + y;
}
```

在此示例中，函数 add 被重载了三次。第一个版本接受两个整数参数并返回整数。第二个版本接受两个 double 参数并返回 double。第三个版本接受两个字符串参数并返回字符串。

要调用这些函数中的一个，可以使用正常的函数调用语法，C++ 编译器将根据你传递的参数类型自动选择函数的正确版本。例如：

```
int a = add(1, 2); // Calls the first version of add
double b = add(3.14, 2.72); // Calls the second version of add
std::string c = add("hello", " world"); // Calls the third version of add
```

函数重载在你想要对不同数据类型执行类似操作时很有用，或者当你想要提供具有不同参数数量的函数的多个版本时很有用。然而，在重载函数时应谨慎，因为如果函数具有相同名称但根据参数表现不同，使用你代码的用户可能会感到困惑。通常最好选择能够清楚描述其目的和预期参数类型的函数名称。

### 显式默认和删除的函数

在 C++ 中，你可以使用 = default 和 = delete 语法来指定类中某些函数的默认行为。

= default 语法可用于显式指定函数应具有其默认行为，该行为由 C++ 语言定义。这通常用于具有默认实现的函数，例如拷贝构造函数或赋值运算符。

以下是使用 = default 显式指定拷贝构造函数默认行为的示例：

```
class MyClass
{
public:
    MyClass(const MyClass& other) = default;
    // ...
};
```

= delete 语法可用于显式指定函数不应被使用。这通常用于防止编译器生成你不想要的某些函数，例如拷贝构造函数或赋值运算符。

以下是使用 = delete 显式指定不应使用拷贝构造函数的示例：

```
class MyClass
{
public:
    MyClass(const MyClass& other) = delete;
    // ...
};
```

在某些情况下，使用 = default 和 = delete 可以是有用的，因为你想要显式控制类中某些函数的行为。然而，在使用这些语法时应谨慎，因为如果使用不当，使用你代码的用户可能会感到困惑。通常最好尽可能使用函数的默认行为，仅在必要时使用 = default 或 = delete。

### 基于参数的依赖名称查找 Koenig 查找

在 C++ 中，基于参数的依赖名称查找 也称为 “Koenig 查找” 是一种允许编译器在函数参数类型的命名空间中搜索函数的特性。这在你想要调用定义在函数参数之一相同命名空间中的函数时很有用。

以下是基于参数的依赖名称查找在 C++ 中如何工作的示例：

```
namespace A
{
    class X {};
    void f(X x)
    {
        g(x);  // Calls A::g(X)
    }
}
```

```
namespace B
{
    class Y {};
    void g(Y y)
    {
        // ...
    }
}
```

在此示例中，函数 f 定义在 A 命名空间中，并接受类型为 X 的参数，X 也定义在 A 命名空间中。函数 f 调用函数 g，g 未定义在 A 命名空间中。然而，因为 g 是使用类型为 Y 的参数调用的，而 Y 定义在 B 命名空间中，编译器将使用基于参数的依赖名称查找在 B 命名空间中搜索 g。这允许编译器找到 g 的正确定义并正确调用它。

基于参数的依赖名称查找在你想要调用定义在函数参数之一相同命名空间中的函数时很有用。然而，如果不小心，它也可能导致混淆，因为编译器可能在不同命名空间中找到同一函数的多个定义。通常最好使用完全限定名称调用函数以避免任何潜在的混淆。

### c++ 中的函数

在 C++ 中，函数是一段执行特定任务并且可能返回值代码块。函数允许你重用代码并将大型程序划分为更小、更易管理的部分。

以下是 C++ 中简单函数的示例：

```
int add(int x, int y)
{
    return x + y;
}
```

这个函数名为 add，接受两个整数参数 x 和 y，并返回它们的和作为整数。

要调用此函数并使用其返回值，你可以这样做：

```
int a = 3;
int b = 4;
int c = add(a, b);  // c is now equal to 7
```

在 C++ 中，函数可以具有不同类型的参数和返回值。例如，函数可以返回浮点值，或者它可以根本没有返回值 在这种情况下，其返回类型为 void。

函数还可以为其参数提供默认值。这允许你使用更少的参数调用函数，在这种情况下，缺失参数将使用默认值。以下是示例：

```
int add(int x, int y = 1)
{
    return x + y;
}
```

```
int a = 3;
int b = add(a);  // b is now equal to 4
```

函数是 C++ 的重要组成部分，在大多数程序中被广泛使用。它们可以帮助你编写更模块化、可重用的代码，从而使程序更易于理解和维护。

### 默认参数

在 C++ 中，你可以为函数参数指定默认值。这允许你使用更少的参数调用函数，在这种情况下，缺失参数将使用默认值。

以下是 C++ 中具有默认参数的函数的示例：



```
int add(int x, int y = 1)
{
    return x + y;
}
```

在此示例中，函数 add 接受两个整数参数，x 和 y。y 参数具有默认值 1，这意味着它是可选的。你可以用一个或两个参数调用此函数：

```
int a = add(3); // a is now equal to 4
int b = add(3, 5); // b is now equal to 8
```

默认参数在你想要为可选函数参数提供默认值时很有用。然而，在使用默认参数时应谨慎，因为如果使用过度，会使代码更难理解。一般来说，最好仅对具有明确且明显的默认值的可选参数使用默认参数。

### 内联函数

在 C++ 中，内联函数是编译器在每次调用时就地展开的函数，而不是通过正常的函数调用机制进行调用。内联函数可以通过减少函数调用的开销来提高程序性能。
以下是 C++ 中内联函数的示例：

```
inline int add(int x, int y)
{
    return x + y;
}
```

要使用此内联函数，你可以像使用任何其他函数一样调用它：

```
int a = 3;
int b = 4;
int c = add(a, b); // c is now equal to 7
```

inline 关键字是向编译器请求内联展开函数的请求，但编译器并不必须遵守此请求。如果编译器判定这样做没有益处，它可能会选择不内联该函数。

内联函数可以通过减少函数调用的开销来提高程序性能。然而，在使用内联函数时应谨慎，因为如果使用过度，会增加程序的大小。一般来说，最好仅对小型、简单且被频繁调用的函数使用内联函数

仅用于小型、简单且被频繁调用的函数。

## 第十一章

### 运算符重载

在 C++ 中，运算符重载是一种允许你为用户定义类型重新定义运算符行为的特性。这对于使你的代码更易读和直观很有用，因为它允许你使用 +、-、* 和 / 等运算符来操作自己的类型。

以下是 C++ 中运算符重载的示例：

```
class Vector2
{
public:
    Vector2(float x, float y) : x_(x), y_(y) {}

    Vector2 operator+(const Vector2& other) const
    {
        return Vector2(x_ + other.x_, y_ + other.y_);
    }

    Vector2 operator-(const Vector2& other) const
    {
        return Vector2(x_ - other.x_, y_ - other.y_);
    }

    Vector2 operator*(float scalar) const
    {
        return Vector2(x_ * scalar, y_ * scalar);
    }

private:
    float x_;
    float y_;
};
```

在此示例中，Vector2 类重载了三个运算符：+、- 和 *。这些运算符允许你使用熟悉的 +、- 和 * 运算符来对 Vector2 对象进行加法、减法和乘法。

要使用这些重载的运算符，你可以使用正常的运算符语法：

```
Vector2 v1(1, 2);
Vector2 v2(3, 4);

Vector2 v3 = v1 + v2;  // v3 is now (4, 6)
Vector2 v4 = v1 - v2;  // v4 is now (-2, -2)
Vector2 v5 = v1 * 2;  // v5 is now (2, 4)
```

运算符重载对于使代码更易读和直观很有用。然而，在重载运算符时应谨慎，因为如果运算符行为出乎意料，会让代码使用者感到困惑。一般来说，最好以与标准行为一致的方式重载运算符。

### 运算符重载的一般规则

在 C++ 中，重载运算符时应遵循以下几个一般规则：

- 1. 仅为有意义的类型重载运算符。例如，为表示数据库连接的类型重载 + 运算符是没有意义的。
- 2. 以与标准行为一致的方式重载运算符。例如，如果为表示复数的类型重载 + 运算符，它应将数的实部和虚部相加。
- 3. 避免重载改变运算符基本行为的运算符。例如，通常不建议重载 = 运算符以执行其他操作，因为这会让代码使用者感到困惑。
- 4. 在重载运算符时适当使用 const 关键字。这将允许你在 const 对象上使用重载的运算符并防止用户意外修改对象。
- 5. 注意你所重载的运算符的优先级和结合性。这将确保你的重载运算符在使用与其他运算符的表达式中时按预期行为。

通过遵循这些一般规则，你可以确保运算符重载清晰、直观且与运算符的标准行为一致。这将使你的代码更易于理解和维护。

### 重载一元运算符

在 C++ 中，你可以通过定义具有适当名称的成员函数或非成员函数来重载一元运算符（一元运算符接受单个操作数）。

以下是将一元 - 运算符重载为成员函数的示例：

```
class Vector2
{
public:
    Vector2(float x, float y) : x_(x), y_(y) {}

    Vector2 operator-() const
    {
        return Vector2(-x_, -y_);
    }

private:
    float x_;
    float y_;
};
```

在此示例中，Vector2 类有一个重载的 - 运算符，它取反 Vector2 对象的 x 和 y 分量。

要使用此重载运算符，你可以使用正常的运算符语法：

```
Vector2 v1(1, 2);
Vector2 v2 = -v1;  // v2 is now (-1, -2)
```

以下是将一元 ! 运算符重载为非成员函数的示例：

```
class MyClass
{
public:
    MyClass(bool b) : b_(b) {}

    bool getValue() const { return b_; }

private:
    bool b_;
};

MyClass operator!(const MyClass& obj)
{
    return MyClass(!obj.getValue());
}
```

在此示例中，MyClass 类有一个名为 getValue 的成员函数，它返回私有成员变量的值。! 运算符被重载为一个非成员函数，它取反 getValue 返回的值。

要使用此重载运算符，你可以使用正常的运算符语法：

```
MyClass obj(true);
MyClass obj2 = !obj;  // obj2 is now false
```

一元运算符重载对于使代码更易读和直观很有用。然而，在重载一元运算符时应谨慎，因为如果运算符行为出乎意料，会让代码使用者感到困惑。一般来说，最好以与标准行为一致的方式重载一元运算符。

### 自增和自减运算符重载

在 C++ 中，你可以为用户定义类型重载自增（ ++ ）和自减（ -- ）运算符。这对于使你的代码更易读和直观很有用，因为它允许你使用这些运算符来操作自己的

类型。

以下是将自增和自减运算符重载为成员函数的示例：

```
class Counter
{
public:
    Counter() : value_(0) {}

    Counter& operator++()
    {
        ++value_;
        return *this;
    }

    Counter operator++(int)
    {
        Counter tmp(*this);
        ++value_;
        return tmp;
    }

    Counter& operator--()
    {
        --value_;
        return *this;
    }

    Counter operator--(int)
    {
        Counter tmp(*this);
        --value_;
        return tmp;
    }

private:
    int value_;
};
```

在此示例中，Counter 类重载了 ++ 和 -- 运算符，它们递增和递减一个名为 value_ 的私有成员变量。++ 运算符以前缀（ ++x ）和后缀（ x++ ）形式重载，-- 运算符以前缀（ --x ）和后缀（ x-- ）形式重载。

要使用这些重载运算符，你可以使用正常的运算符语法：

```
Counter c;
++c;  // c is now 1
c++;  // c is now 2
--c;  // c is now 1
c--;  // c is now 0
```




递增和递减运算符重载对于使你的代码更具可读性和直观性是有用的。然而，在重载这些运算符时应格外小心，因为如果运算符行为异常，会让使用你代码的用户感到困惑。一般来说，以与标准行为一致的方式重载这些运算符是一个好主意。

### 二元运算符

在 C++ 中，二元运算符是接受两个操作数的运算符。一些常见的二元运算符示例包括 +、-、*、/ 和 % 。

以下是 C++ 中使用二元运算符的示例：

```
int a = 3;
int b = 4;
int c = a + b;  // c is now 7
int d = a - b;  // d is now -1
int e = a * b;  // e is now 12
int f = b / a;  // f is now 1
int g = b % a;  // g is now 1
```

在 C++ 中，你也可以为用户定义的类型重载二元运算符。这允许你在将它们与自己的类型一起使用时为运算符定义自定义行为。

以下是将 + 运算符作为成员函数重载的示例：

```
class Vector2
{
public:
    Vector2(float x, float y) : x_(x), y_(y) {}

    Vector2 operator+(const Vector2& other) const
    {
        return Vector2(x_ + other.x_, y_ + other.y_);
    }

private:
    float x_;
    float y_;
};
```

在这个示例中，Vector2 类有一个重载的 + 运算符，它将两个 Vector2 对象的 x 和 y 分量相加。

要使用此重载运算符，可以使用正常的运算符语法：

```
Vector2 v1(1, 2);
Vector2 v2(3, 4);
Vector2 v3 = v1 + v2;  // v3 is now (4, 6)
```

二元运算符重载对于使你的代码更具可读性和直观性是有用的。然而，在重载二元运算符时应格外小心，因为如果运算符行为异常，会让使用你代码的用户感到困惑。一般来说，以与标准行为一致的方式重载二元运算符是一个好主意。

### 赋值

在 C++ 中，赋值运算符（ = ）用于将值赋给变量。

以下是 C++ 中使用赋值运算符的示例：

```
int a = 3;  // Initialize a to 3
a = 4;  // Assign a new value to a
```

在第一行，= 运算符用于将变量 a 初始化为值 3。在第二行，= 运算符用于为 a 分配一个新值，覆盖之前的值。

你也可以使用赋值运算符来链式赋值，像这样：

```
int a, b, c;
a = b = c = 0;  // Assign 0 to a, b, and c
```

在这个示例中，赋值运算符用于在一行代码中将值 0 分配给全部三个变量。

你也可以使用赋值运算符将表达式的值赋给变量，像这样：

```
int a = 3;
int b = 4;
int c = a + b;  // c is now 7
```

在这个示例中，= 运算符用于将表达式 a + b 的结果（即 7）赋给变量 c。

赋值运算符是 C++ 的重要组成部分，在大多数程序中被广泛使用。它允许你为变量赋值并根据需要修改它们的值。

### 函数调用

在 C++ 中，函数调用是一个表达式，它调用一个函数并可选地向函数传递参数。函数调用的语法是函数名后跟括号中的参数列表。

以下是 C++ 中函数调用的示例：

```
int add(int x, int y)
{
    return x + y;
}

int a = 3;
int b = 4;
int c = add(a, b);  // c is now 7
```

在这个示例中，函数 add 接受两个整数参数 x 和 y，并返回它们的和作为整数。函数通过使用其名称后跟括号中的参数来调用。函数的返回值被赋给变量 c。

你也可以将函数调用作为表达式的一部分使用，像这样：

```
int a = 3;
int b = 4;
int c = add(a, b) * 2;  // c is now 14
```

在这个示例中，函数调用 add(a, b) 被用作乘以返回值的表达式的一部分。表达式的结果随后被赋给变量 c。

函数调用是 C++ 的重要组成部分，在大多数程序中被广泛使用。它们允许你重用代码并将大型程序划分为更小、更易管理的部分。

### 下标

在 C++ 中，下标（也称为索引）是一种使用 [] 运算符访问数组或容器中单个元素的方式。

以下是使用下标访问 C++ 中数组元素的示例：

```
int arr[5] = {1, 2, 3, 4, 5};

int a = arr[0];  // a is now 1
int b = arr[2];  // b is now 3
int c = arr[4];  // c is now 5
```

在这个示例中，[] 运算符用于访问 arr 数组的元素。数组的第一个元素的索引为 0，第二个元素的索引为 1，以此类推。

你也可以使用下标来修改数组的元素：

```
int arr[5] = {1, 2, 3, 4, 5};

arr[0] = 10;  // arr is now {10, 2, 3, 4, 5}
arr[2] = 20;  // arr is now {10, 2, 20, 4, 5}
arr[4] = 30;  // arr is now {10, 2, 20, 4, 30}
```

下标是访问和修改 C++ 中数组或容器元素的强大且方便的方式。它在许多程序中被广泛用于操作存储在数组和容器中的数据。

### 成员访问

在 C++ 中，成员访问是一种使用 . 或 -> 运算符访问类或结构的数据成员和成员函数的方式。

以下是使用成员访问访问 C++ 中类的数据成员的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};

Point p(1, 2);

int a = p.x_;  // a is now 1
int b = p.y_;  // b is now 2
```

在这个示例中，Point 类有两个数据成员 x_ 和 y_，以及两个成员函数 getX 和 getY，它们返回这些数据成员的值。数据成员使用 . 运算符访问，成员函数使用 . 运算符和括号调用。

你也可以使用成员访问来调用类的成员函数：

```
Point p(1, 2);

int a = p.getX();  // a is now 1
int b = p.getY();  // b
```

### 类和结构体

在 C++ 中，类和结构体是用户定义的类型，允许你定义自己的自定义数据类型。

类是用户定义的类型，可以包含数据成员（变量）和成员函数（属于类的函数）。类使用 class 关键字定义，像这样：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};
```

在这个示例中，Point 类有两个数据成员 x_ 和 y_，以及两个成员函数 getX 和 getY，它们返回这些数据成员的值。

结构体类似于类，但默认情况下所有成员都是公开的。结构体使用 struct 关键字定义，像这样：

```
struct Point
{
    int x;
    int y;
};
```

在这个示例中，Point 结构体有两个数据成员 x 和 y，它们都是公开的。

你可以使用 new 运算符或通过声明类或结构体类型的变量来创建类或结构体的实例，像这样：

```
Point p1(1, 2); // Create an instance of Point using constructor

Point *p2 = new Point(3, 4); // Create an instance of Point using new

Point p3; // Create an instance of Point with default constructor
```

类和结构体是 C++ 的重要组成部分，在许多程序中被广泛用于定义自定义数据类型并封装数据和功能。

### what is class

在 C++ 中，类是用户定义的类型，可以包含数据成员（变量）和成员函数（属于类的函数）。类使用 class 关键字定义，像这样：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};
```

在这个示例中，Point 类有两个数据成员 x_ 和 y_，以及两个成员函数 getX 和 getY，它们返回这些数据成员的值。

你可以使用 new 运算符或通过声明类类型的变量来创建类的实例，像这样：

```
Point p1(1, 2); // Create an instance of Point using constructor
```

```
Point *p2 = new Point(3, 4); // Create an instance of Point using new
```

```
Point p3; // Create an instance of Point with default constructor
```

类是 C++ 的重要组成部分，在许多程序中被广泛用于定义自定义数据类型并封装数据和功能。

### what struct

在 C++ 中，结构体是用户定义的类型，类似于类，但所有成员默认都是公开的。结构体使用 struct 关键字定义，像这样：

```
struct Point
{
    int x;
    int y;
};
```

在这个示例中，Point 结构体有两个数据成员 x 和 y，它们都是公开的。

你可以通过声明结构体类型的变量来创建结构体的实例，像这样：

```
Point p1 = {1, 2};  // Create an instance of Point using initializer list
```

```
Point p2;  // Create an instance of Point with default values
```





结构体通常用于定义不需要类提供的封装和保护的简单数据结构。然而，结构体也可以包含成员函数，并且在许多情况下可以像类一样使用。

结构体是 C++ 的重要组成部分，在许多程序中被广泛用于定义自定义数据类型并将相关数据组合在一起。

### 类成员概述

在 C++ 中，类是一种用户定义的类型，可以包含数据成员（变量）和成员函数（属于类的函数）。类使用 class 关键字定义，如下所示：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};
```

在此示例中，Point 类有两个数据成员 x_ 和 y_，以及两个成员函数 getX 和 getY，用于返回这些数据成员的值。

类定义中的 public 关键字指定其后的成员可以从类外部访问。这意味着你可以使用 . 运算符从类外部访问 Point 类实例的成员函数和数据成员。

类定义中的 private 关键字指定其后的成员只能从类内部访问。这意味着你不能直接从类外部访问数据成员，但可以通过成员函数访问它们。

你可以使用 new 运算符或声明类类型的变量来创建类的实例，如下所示：

```
Point p1(1, 2);  // Create an instance of Point using constructor

Point *p2 = new Point(3, 4);  // Create an instance of Point using new

Point p3;  // Create an instance of Point with default constructor
```

类是 C++ 的重要组成部分，在许多程序中被广泛用于定义自定义数据类型并封装数据和功能。

### 成员访问控制

在 C++ 中，你可以使用 public、private 和 protected 关键字来指定类成员的访问控制。

public 关键字指定其后的成员可以从类外部访问。这意味着你可以使用 . 运算符从类外部访问类的实例的成员函数和数据成员。

private 关键字指定其后的成员只能从类内部访问。这意味着你不能直接从类外部访问数据成员，但可以通过成员函数访问它们。

protected 关键字指定其后的成员只能从类内部及其派生类访问。这意味着你不能直接从类外部访问数据成员，但可以在类及其派生类中的成员函数中访问它们。

以下是类定义中使用访问控制的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};
```

在此示例中，Point 类有两个公共成员函数 getX 和 getY，可以使用 . 运算符从类外部调用。x_ 和 y_ 数据成员是私有的，这意味着它们只能从类内部访问。

访问控制是 C++ 的重要组成部分，用于指定类的哪些成员可以从类外部访问。它允许你封装数据和功能并控制其使用方式。

### 什么是友元

在 C++ 中，友元函数是可以访问类的私有和受保护成员的函数。友元函数不是类的成员函数，但它可以访问类的内部实现细节。

你可以在类定义中使用 friend 关键字将函数声明为类的友元，如下所示：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    friend int distance(const Point &p1, const Point &p2);

private:
    int x_;
    int y_;
};

int distance(const Point &p1, const Point &p2)
{
    int dx = p1.x_ - p2.x_;
    int dy = p1.y_ - p2.y_;
    return sqrt(dx * dx + dy * dy);
}
```

在此示例中，Point 类有一个私有数据成员 x_，以及一个友元函数 distance，可以访问 x_ 数据成员。distance 函数不是 Point 类的成员函数，但它可以像成员函数一样访问 Point 类的私有数据成员。

当你希望允许函数访问类的私有数据成员，但又不想将该函数设为类的成员函数时，友元函数很有用。它们还用于在 C++ 中实现运算符重载。

友元函数是 C++ 的重要组成部分，在许多程序中被广泛用于实现高级编程技术和运算符重载。

### private

在 C++ 中，private 关键字用于指定类成员的访问控制。声明为 private 的类成员只能从类内部访问，不能直接从类外部访问。

以下是类定义中使用 private 关键字的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};
```

在此示例中，Point 类有两个公共成员函数 getX 和 getY，可以使用 . 运算符从类外部调用。x_ 和 y_ 数据成员是私有的，这意味着它们只能从类内部访问。

private 访问控制用于封装数据和功能并控制其使用方式。它允许你将类的实现细节隐藏在外部代码之外并保护数据的完整性。

private 关键字是 C++ 的重要组成部分，在许多程序中被广泛用于指定类成员的访问控制。

### protected

在 C++ 中，protected 关键字用于指定类成员的访问控制。声明为 protected 的类成员只能从类内部及其派生类访问，不能直接从类外部访问。

以下是类定义中使用 protected 关键字的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

protected:
    int x_;
    int y_;
};
```

```
class ColorPoint : public Point
{
public:
    ColorPoint(int x, int y, int color) : Point(x, y), color_(color) {}

    int getColor() const { return color_; }

private:
    int color_;
};
```

在此示例中，Point 类有两个公共成员函数 getX 和 getY，可以使用 . 运算符从类外部调用。x_ 和 y_ 数据成员是受保护的，这意味着它们只能从 Point 类及其派生类内部访问。

ColorPoint 类派生自 Point 类，可以访问 x_ 和 y_ 数据成员。然而，这些数据成员不能从 ColorPoint 类外部访问。

protected 访问控制用于允许派生类访问其基类的数据和功能，同时仍然将实现细节隐藏在外部代码之外。它是 C++ 中继承机制的重要组成部分，在许多程序中被广泛用于指定类成员的访问控制。

### public

在 C++ 中，public 关键字用于指定类成员的访问控制。声明为 public 的类成员可以从类外部访问，可以直接使用 . 运算符访问。

以下是类定义中使用 public 关键字的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};
```

在此示例中，Point 类有两个公共成员函数 getX 和 getY，可以使用 . 运算符从类外部调用。x_ 和 y_ 数据成员是私有的，这意味着它们只能从类内部访问。

public 访问控制用于指定类的哪些成员可以从类外部访问。它允许你向外部代码公开类的数据和功能并控制其使用方式。

public 关键字是 C++ 的重要组成部分，在许多程序中被广泛用于指定类成员的访问控制。

### 大括号初始化

在 C++ 中，大括号初始化是使用花括号 {} 初始化变量和对象的一种方式。它允许你在创建变量或对象时指定变量的值或对象构造函数的参数。





以下是使用大括号初始化的一些示例：

```
int x{1};  // Initialize x to 1

int y = {2};  // Initialize y to 2

int z{};  // Initialize z to 0

std::vector<int> v{1, 2, 3};  // Initialize v with elements 1, 2, 3

std::map<std::string, int> m{{"key1", 1}, {"key2", 2}};  // Initialize m with elements {"key1", 1} and {"key2", 2}

Point p{1, 2};  // Initialize p using constructor
```

与 C++ 中其他形式的初始化相比，大括号初始化更受青睐，因为它更具表达性且不易出错。它也更灵活，允许你使用更广泛的值和类型来初始化变量和对象。

大括号初始化是 C++ 的重要组成部分，在许多程序中被广泛用于初始化变量和对象。当你想要指定非默认值或对象的构造函数的参数时，它尤其有用。

### 对象生命周期和资源管理（RAII）

在 C++ 中，对象的生命周期是指对象存在于内存中并且可从代码中访问的时间段。正确管理对象的生命周期很重要，因为它决定了资源何时分配和释放，以及资源对程序可用多长时间。

在 C++ 中管理对象和资源生命周期的一种常见方式是通过使用资源获取即初始化（RAII）技术。RAII 是一种设计模式，它利用对象生命周期以安全、高效且异常安全的方式管理资源。

RAII 的基本思想是将资源获取与对象的创建关联起来，并将资源的释放与对象的销毁关联起来。这确保了当对象超出作用域或被销毁时，资源会自动释放，即使抛出异常也是如此。

以下是使用 RAII 管理对象和资源生命周期的示例：

```
class File
{
public:
    File(const std::string &filename) : handle_(fopen(filename.c_str(), "r"))
    {
        if (!handle_)
        {
            throw std::runtime_error("Error opening file");
        }
    }

    ~File()
    {
        if (handle_)
        {
            fclose(handle_);
        }
    }

    // Other member functions...

private:
    FILE *handle_;
};

int main()
{
    try
    {
        File file("data.txt");
        // Use the file...
    }
    catch (const std::exception &e)
    {
        std::cerr << e.what() << std::endl;
        return 1;
    }

    return 0;
}
```

在此示例中，File 类管理文件句柄的生命周期。文件句柄在 File 对象的构造函数中获取，并在析构函数中释放。这确保了即使在使用文件时抛出异常，文件句柄也始终被正确关闭。

RAII 是 C++ 的重要组成部分，在许多程序中被广泛用于以安全高效的方式管理对象和资源的生命周期。它有助于防止资源泄漏并提高代码的可靠性和异常安全性。

### 用于编译时封装的 Pimpl 惯用法

在 C++ 中，指向实现（Pimpl）惯用法是一种设计模式，用于实现对实现细节的编译时封装。它用于将类的实现细节从公共接口中隐藏，同时仍允许以类型安全的方式使用该类。

Pimpl 惯用法的核心思想是在头文件中定义类的公共接口，并在单独的源文件中定义实现细节。实现细节通过指向在实现文件中定义的向前声明类的指针来访问。

### ABI 边界的移植性

在 C++ 中，应用程序二进制接口（ABI）定义了不同软件组件在二进制级别交互的约定和规则。它指定了数据在内存中的布局方式、函数调用和返回如何进行，以及不同软件组件互操作所需的其他低级细节。

在编写可移植的 C++ 代码时，在不同软件组件之间的边界处考虑 ABI 很重要，例如库、可执行文件和共享对象。不同的编译器和平台可能具有不同的 ABI，必须确保你的代码与目标平台的 ABI 兼容。

在 C++ 中确保 ABI 边界移植性的几种方法有：

- 1. 使用稳定的 ABI：某些平台，例如 Linux 和 Windows，具有由多个编译器支持的稳定 ABI。通过使用稳定 ABI，你可以确保代码与不同的编译器和平台兼容。
- 2. 使用跨平台 ABI：有几种跨平台 ABI 可用，例如 Itanium C++ ABI，由不同平台上的多个编译器支持。通过使用跨平台 ABI，你可以确保代码在不同平台之间可移植。
- 3. 使用版本控制系统：某些系统，例如 Linux 上的 ELF 版本控制系统，允许你为不同的 ABI 指定代码的不同版本。通过使用版本控制系统，你可以确保代码与不同的 ABI 和平台兼容。
- 4. 使用兼容性层：某些系统，例如 Microsoft Windows 可移植可执行文件（PE）格式，允许你在二进制中指定兼容性信息。通过使用兼容性层，你可以确保代码兼容

## 第十二章

### 构造函数

在 C++ 中，构造函数是类的特殊成员函数，在创建类的对象时被调用。构造函数用于初始化对象的数据成员并执行设置对象以供使用的任何其他任务。

构造函数与类同名，没有返回类型，甚至不是 void。它们在对象创建时由编译器自动调用，不能直接从代码中调用。

以下是带构造函数的类的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};

int main()
{
    Point p(1, 2);
    std::cout << "x = " << p.getX() << ", y = " << p.getY() << std::endl;
    return 0;
}
```

在此示例中，Point 类有一个构造函数，接受两个参数 x 和 y，并使用这些值初始化 x_ 和 y_ 数据成员。构造函数没有返回类型，并在创建 Point 类对象时由编译器自动调用。

构造函数是 C++ 的重要组成部分，在许多程序中被广泛用于初始化对象并在创建时执行其他任务。你可以在类中定义多个构造函数以提供创建对象的不同方式，或支持

### 拷贝构造函数和拷贝赋值运算符

在 C++ 中，拷贝构造函数是类的特殊成员函数，在将类的对象作为另一个对象的副本创建时被调用。拷贝赋值运算符是当一个对象被赋给另一个对象时被调用的特殊成员函数。

拷贝构造函数和拷贝赋值运算符用于执行对象的深度拷贝，这意味着它们创建具有原始对象数据成员的单独副本的新对象。这对于确保新对象独立于原始对象并且可以被修改而不影响原始对象是必要的。

以下是带拷贝构造函数和拷贝赋值运算符的类的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}
    Point(const Point &other) : x_(other.x_), y_(other.y_) {}
    Point &operator=(const Point &other)
    {
        if (this != &other)
        {
            x_ = other.x_;
            y_ = other.y_;
        }
        return *this;
    }

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};
```

在此示例中，Point 类有一个拷贝构造函数，它接受另一个 Point 对象的 const 引用，并使用原始对象的值初始化新对象的数据成员。拷贝赋值运算符被定义为重载的赋值运算符，它执行原始对象数据成员的深度拷贝。

拷贝构造函数和拷贝赋值运算符是 C++ 的重要组成部分，在许多程序中被广泛用于支持对象的创建和



对象赋值。它们是必要的，以确保对象在复制和修改时不会影响原始对象。

### 移动构造函数和移动赋值运算符

在 C++ 中，移动构造函数是类的特殊成员函数，当通过移动另一个对象的内容来创建该类的对象时会被调用。移动赋值运算符是特殊成员函数，当通过移动原始对象的内容将一个对象赋给另一个对象时会被调用。

移动构造函数和移动赋值运算符用于执行对象的移动，这意味着它们将原始对象的内容转移到新对象，而不进行复制。这比复制更高效，因为它避免了复制对象数据成员的开销。

下面是一个带有移动构造函数和移动赋值运算符的类的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}
    Point(Point &&other) noexcept : x_(other.x_), y_(other.y_)
    {
        other.x_ = 0;
        other.y_ = 0;
    }
    Point &operator=(Point &&other) noexcept
    {
        if (this != &other)
        {
            x_ = other.x_;
            y_ = other.y_;
            other.x_ = 0;
            other.y_ = 0;
        }
        return *this;
    }

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};
```

在此示例中，Point 类有一个移动构造函数，它接受另一个 Point 对象的右值引用，并使用原始对象的值初始化新对象的数据成员。移动赋值运算符被定义为重载的赋值运算符，它执行原始对象数据成员的移动。

移动构造函数和移动赋值运算符是 C++ 的重要组成部分，并在许多程序中被广泛使用，以支持对象的有效创建和赋值。它们在处理大型对象或复制操作昂贵的对象时尤其有用，因为它们可以提高代码的性能。

### 委托构造函数

在 C++ 中，委托构造函数是一种特性，允许类的一个构造函数在其初始化过程中调用同一类的另一个构造函数。这在你想要提供多种构造对象的方式，或在另一个构造函数中重用一个构造函数的初始化代码时很有用。

要使用委托构造函数，可以使用 : 语法，后跟要调用的构造函数的名称以及要传递给它的参数。被调用的构造函数在调用构造函数的函数体执行之前执行，并且可以初始化数据成员并根据需要执行其他任务。

下面是一个带有委托构造函数的类的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}
    Point() : Point(0, 0) {}
    Point(int x) : Point(x, 0) {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};
```

在此示例中，Point 类有三个构造函数：默认构造函数、单参数构造函数和双参数构造函数。默认构造函数和单参数构造函数使用委托构造函数通过使用适当的 arguments 调用双参数构造函数来初始化对象的数据成员。

委托构造函数是 C++ 的重要组成部分，并在许多程序中被广泛使用，以提供多种构造对象的方式并重用初始化代码。它们可以通过减少重复并允许你将常见的初始化任务集中到单个构造函数中来提高代码的可读性和可维护性。

### 析构函数

在 C++ 中，析构函数是类的特殊成员函数，当该类的对象被销毁时会被调用。析构函数用于执行清理对象和释放其持有的任何资源所需的任何任务。

析构函数具有与类相同的名称，后跟波浪号（ ~ ），并且没有参数或返回类型。它们由编译器在对象超出作用域或被删除时自动调用，并且不能直接从代码中调用。

下面是一个带有析构函数的类的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}
    ~Point() {}

    int getX() const { return x_; }
    int getY() const { return y_; }

private:
    int x_;
    int y_;
};

int main()
{
    Point p(1, 2);
    std::cout << "x = " << p.getX() << ", y = " << p.getY() << std::endl;
    return 0;
}
```

在此示例中，Point 类有一个析构函数，它没有参数或返回类型并且不执行任何任务。析构函数由编译器在 main 结束时 p 对象超出作用域时自动调用。

析构函数是 C++ 的重要组成部分，并在许多程序中被广泛使用，以在对象被销毁时释放资源并执行其他任务。你可以在类中定义析构函数，以在对象被销毁之前执行清理对象所需的任何任务。

### 成员函数概述

在 C++ 中，成员函数是在类内定义并操作类的数据成员的函数。它们是类接口的重要组成部分，用于提供类的行为和功能。

成员函数具有以下几个区别于其他类型函数的特征：

- 1. 成员函数在类定义内部定义，并且可以访问类的私有数据成员。这使它们能够操作对象的内部状态并提供所需的行为和功能。
- 2. 成员函数使用 . 或 -> 运算符调用，具体取决于对象是引用还是指针。这使你能够在对象上调用成员函数并访问其数据成员。
- 3. 成员函数可以声明为 const，这意味着它们不会修改对象的数据成员，并且可以在 const 对象上调用。这使你能够定义不修改对象状态并且可以在 const 上下文中调用的函数。

下面是一个带有一些成员函数的类的示例：

```
class Point
{
public:
    Point(int x, int y) : x_(x), y_(y) {}
    ~Point() {}

    int getX() const { return x_; }
    int getY() const { return y_; }
    void setX(int x) { x_ = x; }
    void setY(int y) { y_ = y; }

private:
    int x_;
    int y_;
};

int main()
{
    Point p(1, 2);
    std::cout << "x = " << p.getX() << ", y = " << p.getY() << std::endl;
    p.setX(3);
    p.setY(4);
    std::cout << "x = " << p.getX() << ", y = " << p.getY() << std::endl;
    return 0;
}
```

### virtual 说明符

在 C++ 中，virtual 说明符用于在类中声明虚成员函数。虚成员函数是可以被派生类重写的成员函数，从而允许它们提供自己的函数实现。

virtual 说明符用于在基类中成员函数的声明中，并且在派生类中函数被标记为 override 以指示它正在重写基类实现。

下面是一个带有虚成员函数的类的示例：

```
class Shape
{
public:
    virtual void draw() = 0;
};

class Circle : public Shape
{
public:
    void draw() override { std::cout << "Drawing a circle" << std::endl; }
};

class Square : public Shape
{
public:
    void draw() override { std::cout << "Drawing a square" << std::endl; }
};

int main()
{
    Shape *s1 = new Circle();
    s1->draw();

    Shape *s2 = new Square();
    s2->draw();

    delete s1;
    delete s2;
    return 0;
}
```

在此示例中，Shape 类有一个纯虚成员函数 draw，它使用 virtual 说明符声明并且没有实现。Circle 和 Square 类派生自 Shape 并通过将其标记为 override 来提供自己的 draw 函数实现。
虚成员函数是 C++ 的重要组成部分，并在许多程序中被广泛使用以支持多态性和运行时多态性。它们允许你为一组相关类定义通用接口，并为每个类提供不同的实现，具体取决于其特定的行为和功能。

### override 说明符





在 C++ 中，override 说明符用于指示派生类中的成员函数重写了基类中的虚成员函数。override 说明符确保派生类函数与基类函数具有相同的签名和返回类型，并有助于防止错误并提高代码的可读性。

override 说明符用于派生类中成员函数的声明中，并且必须在基类函数声明中前面加上 virtual 说明符。

下面是一个具有虚成员函数和被重写函数的类的示例：

```
class Shape
{
public:
    virtual void draw() = 0;
};

class Circle : public Shape
{
public:
    void draw() override { std::cout << "Drawing a circle" << std::endl; }
};

int main()
{
    Shape *s = new Circle();
    s->draw();
    delete s;
    return 0;
}
```

在此示例中，Shape 类具有一个纯虚成员函数 draw，该函数使用 virtual 说明符声明并且没有实现。

Circle 类派生自 Shape 并通过将其标记为 override 来提供 draw 函数的自己的实现。

override 说明符是 C++ 的重要组成部分，并在许多程序中广泛使用，以指示派生类中的成员函数重写了基类中的虚成员函数。它有助于确保派生类函数具有正确的签名和返回类型，并防止在派生类的实现中出现错误。

## 目录

学习有关 C++ 的一切内容的全面分步指南

介绍

第一章

基本概念

C++ 类型系统

作用域

头文件

翻译单元和链接

main 函数和命令行参数

程序终止

左值和右值

临时对象

对齐

平凡、标准布局和 POD 类型

什么是值类型

类型转换和类型安全

标准转换

第二章

内置类型

内置类型

数据类型范围

nullptr

nullptr

bool

false

true

__m64

__m128

__m128d

__m128i

__ptr32, __ptr64

第三章

数值限制

数值限制

整数限制

```
Minimum value of char: -128
Maximum value of char: 127
Minimum value of short: -32768
Maximum value of short: 32767
Minimum value of int: -2147483648
Maximum value of int: 2147483647
Minimum value of long: -2147483648
Maximum value of long: 2147483647
Minimum value of long long: -9223372036854775808
Maximum value of long
```

[浮点限制]()

[第四章]()

[声明和定义]()

[存储类]()

[auto]()

[const]()

[constexpr]()

[extern]()

[初始化器]()

[别名和 typedef]()

[using 声明]()

[volatile]()

[decltype]()

[属性]()

[第五章]()

[内置运算符、优先级和结合性]()

[alignof 运算符]()

[uuidof 运算符]()

[加法运算符：+ 和 -]()

[取地址运算符：&]()

[赋值运算符]()

[按位与运算符：&]()

[按位异或运算符：^]()

[按位或运算符：|]()

[强制转换运算符：()]()

[逗号运算符：,]()

[条件运算符：? :]()

[delete 运算符]()

[相等运算符：== 和 !=]()

[显式类型转换运算符：()]()

函数调用运算符：()

间接运算符：*

左移和右移运算符（>> 和 <<）

逻辑与运算符：&&

逻辑非运算符：!

逻辑或运算符：||

成员访问运算符：. 和 ->

乘法运算符和取模运算符

new 运算符

按位取反运算符：~

指向成员运算符：.* 和 ->*

后缀增量和减量运算符：++ 和 --

前缀增量和减量运算符：++ 和 --

关系运算符：<, >, <= 和 >=

作用域解析运算符：::

sizeof 运算符

下标运算符：

typeid 运算符 in

一元加法和取反运算符：+ 和 -

表达式

第六章

表达式的类型

主表达式

省略号和可变参数模板

后缀表达式

带一元运算符的表达式

带二元运算符的表达式

常量表达式

表达式的语义

什么是强制转换

第七章

强制转换运算符

dynamic_cast 运算符

bad_cast 异常

static_cast 运算符

const_cast 运算符

reinterpret_cast 运算符

第八章

+   - 运行时类型信息（RTTI）
  - bad_typeid 异常
  - type_info 类
  - 语句
  - C++ 语句概述
  - 标签语句
  - 表达式语句
  - 空语句
  - 复合语句（块）
- 第九章
  - 选择语句
    - if-else 语句
    - if exists 语句
    - if not exists 语句
    - switch 语句
  - 迭代语句
    - while 语句
    - do-while 语句
    - for 语句
    - 基于范围的 for 语句
- 第十章
  - 跳转语句
    - break 语句
    - continue 语句
    - return 语句
    - goto 语句
  - 控制转移
  - 命名空间
  - 枚举
  - 联合体
  - 函数
  - 具有可变参数列表的函数
  - 函数重载
  - 显式默认和删除的函数
  - 参数相关名称查找（Koenig）on
  - 默认参数
  - 内联函数
- 第十一章

+   - 运算符重载
- 运算符重载的一般规则
- 重载一元运算符
- 增量和减量运算符重载
- 二元运算符
- 赋值
- 函数调用
- 下标
- 成员访问
- 类和结构体
- 什么是类
- 什么是结构体
- 类成员概述
- 成员访问控制
- 什么是友元
- private
- protected
- public
- 大括号初始化
- 对象生命周期和资源管理（RAII）
- 用于编译时封装的 Pimpl 惯用法
- ABI 边界的移植性
- 第十二章
- 构造函数
- 拷贝构造函数和拷贝赋值运算符
- 移动构造函数和移动赋值运算符
- 委托构造函数
- 析构函数
- 成员函数概述
- virtual 说明符
- override 说明符

