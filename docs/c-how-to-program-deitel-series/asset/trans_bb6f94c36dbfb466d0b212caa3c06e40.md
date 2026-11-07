

```cpp
// Fig. 23.1: fig23_01.cpp
// Demonstrating const_cast.
#include <iostream>
#include <cstring> // contains prototypes for functions strcmp and strlen
#include <cctype> // contains prototype for function toupper
using namespace std;

// returns the larger of two C strings
const char *maximum( const char *first, const char *second )
{
   return ( strcmp( first, second ) >= 0 ? first : second );
} // end function maximum

int main()
{
   char s1[] = "hello"; // modifiable array of characters
   char s2[] = "goodbye"; // modifiable array of characters

   // const_cast required to allow the const char * returned by maximum
   // to be assigned to the char * variable maxPtr
   char *maxPtr = const_cast<char *>( maximum( s1, s2 ) );

   cout << "The larger string is: " << maxPtr << endl;

   for ( size_t i = 0; i < strlen( maxPtr ); ++i )
      maxPtr[ i ] = toupper( maxPtr[ i ] );

   cout << "The larger string capitalized is: " << maxPtr << endl;
} // end main
```

```text
The larger string is: hello
The larger string capitalized is: HELLO
```

**图 23.1 |** 演示运算符 `const_cast`。

在此程序中，函数 maximum（第 9–12 行）接收两个 C 字符串作为 const char * 参数，并返回一个指向两个字符串中较大者的 const char *。函数 main 将这两个 C 字符串声明为非 const 的 char 数组（第 16–17 行）；因此，这些数组是可修改的。在 main 中，我们希望输出两个 C 字符串中较大的一个，然后通过将其转换为大写字母来修改该 C 字符串。

函数 maximum 的两个参数类型为 const char *，因此函数的返回类型也必须声明为 const char *。如果返回类型仅指定为 char *，编译器会发出错误消息，指出返回的值无法从 const char * 转换为 char *——这是一种危险的转换，因为它试图将函数认为是 const 的数据当作非 const 数据来处理。

尽管函数 maximum 认为数据是 const，但我们知道 main 中的原始数组并不包含常量数据。因此，main 应该能够按需修改这些数组的内容。由于我们知道这些数组是可修改的，所以我们使用 const_cast（第 21 行）去掉 maximum 返回的指针的 const 性质，以便在 for 语句（第 25–26 行）中将该指针用作字符数组名，将较大字符串的内容转换为大写字母。如果没有第 21 行的 const_cast，该程序将*无法*编译，因为*不允许*将类型为 const char * 的指针赋值给类型为 char * 的指针。

> **错误预防提示 23.1**
> 
> *通常，只有在预先知道原始数据不是常量时，才应使用 const_cast。否则，可能会发生意外结果。*

## 23.3 mutable 类成员

在第 23.2 节中，我们介绍了 const_cast 运算符，它允许我们移除类型的“const 性”。const_cast 操作也可以从 const 对象的 const 成员函数体内应用于该对象类的数据成员。这使得 const 成员函数能够修改该数据成员，即使在该函数体内该对象被视为 const。当对象的大部分数据成员都应被视为 const，但某个特定数据成员仍然需要修改时，可能会执行这样的操作。

举个例子，考虑一个按排序顺序维护其内容的链表。在链表中搜索不需要修改链表的数据，因此搜索函数可以是链表类的 const 成员函数。然而，可以想象，链表对象为了将来搜索更高效，可能会记录上次成功匹配的位置。如果下一次搜索操作试图定位列表中较晚出现的项，搜索可以从上次成功匹配的位置开始，而不是从列表开头开始。要做到这一点，执行搜索的 const 成员函数必须能够修改记录上次成功搜索位置的数据成员。

如果上述这样的数据成员应该*始终*是可修改的，C++ 提供了存储类说明符 **mutable** 作为 const_cast 的替代方案。mutable 数据成员始终是可修改的，即使在 const 成员函数或 const 对象中也是如此。

> **可移植性提示 23.1**
> 
> *试图修改定义为常量的对象的效果，无论该修改是通过 const_cast 还是 C 风格强制转换实现的，都会因编译器而异。*

mutable 和 const_cast 用于不同的上下文。对于没有 mutable 数据成员的 const 对象，每次要修改成员时都必须使用运算符 const_cast。这大大降低了成员被意外修改的可能性，因为该成员并非永久可修改。涉及 const_cast 的操作通常*隐藏*在成员函数的实现中。类的用户可能不会意识到成员正在被修改。

> **软件工程观察 23.1**
> 
> *mutable 成员在具有“秘密”实现细节的类中非常有用，这些实现细节与客户对类对象的使用无关。*

## 23.4 命名空间

一个程序可能包含许多在不同作用域中定义的标识符。有时，一个作用域中的变量会与另一个作用域中*同名*的变量“重叠”（即冲突），从而可能产生*命名冲突*。这种重叠可能发生在许多级别。在恰好对全局标识符（如函数）使用相同名称的第三方库中，标识符重叠经常发生。这可能导致编译错误。

C++ 通过**命名空间**解决了这个问题。每个命名空间定义一个作用域，在其中放置标识符和变量。要使用**命名空间成员**，成员的名称必须用命名空间名称和*作用域解析运算符*（`::`）限定，如下所示：

```cpp
MyNameSpace::member
```

或者必须在程序中使用该名称之前出现 using 指令。通常，这样的 using 语句放置在文件开头，该文件使用了命名空间的成员。例如，在源代码文件开头放置以下 using 指令：

```cpp
using namespace MyNameSpace;
```

表示命名空间 *MyNameSpace* 的成员可以在文件中使用，而无需在每个成员前加上 *MyNameSpace* 和作用域解析运算符（`::`）。

以下形式的 using 指令

```cpp
using std::cout;
```

将*一个名称*带入该指令所在的作用域。以下形式的 using 指令

```cpp
using namespace std;
```

将指定命名空间（`std`）中的*所有*名称带入该指令所在的作用域。

> **错误预防提示 23.2**
> 
> *如果存在命名冲突的可能性，请在成员前加上其命名空间名称和作用域解析运算符（`::`）。*

并非所有命名空间都能保证是唯一的。两个第三方供应商可能无意中为他们的命名空间名称使用了相同的标识符。图 23.3 演示了命名空间的使用。

```cpp
// Fig. 23.3: fig23_03.cpp
// Demonstrating namespaces.
#include <iostream>
using namespace std;

int integer1 = 98; // global variable

// create namespace Example
namespace Example
{
// declare two constants and one variable
const double PI = 3.14159;
const double E = 2.71828;
int integer1 = 8;

void printValues(); // prototype

// nested namespace
namespace Inner
{
    // define enumeration
    enum Years { FISCAL1 = 1990, FISCAL2, FISCAL3 };
} // end Inner namespace
} // end Example namespace

// create unnamed namespace
namespace
{
    double doubleInUnnamed = 88.22; // declare variable
} // end unnamed namespace

int main()
{
    // output value doubleInUnnamed of unnamed namespace
    cout << "doubleInUnnamed = " << doubleInUnnamed;

    // output global variable
    cout << "\n(global) integer1 = " << integer1;

    // output values of Example namespace
    cout << "\nPI = " << Example::PI << "\nE = " << Example::E
         << "\ninteger1 = " << Example::integer1 << "\nFISCAL3 = "
         << Example::Inner::FISCAL3 << endl;

    Example::printValues(); // invoke printValues function
} // end main

// display variable and constant values
void Example::printValues()
{
    cout << "\nPI in printValues:\ninteger1 = " << integer1 << "\nPI = "
         << PI << "\nE = " << E << "\ndoubleInUnnamed = "
         << doubleInUnnamed << "\n(global) integer1 = " << ::integer1
         << "\nFISCAL3 = " << Inner::FISCAL3 << endl;
} // end printValues
```

```text
doubleInUnnamed = 88.22
(global) integer1 = 98
PI = 3.14159
E = 2.71828
integer1 = 8
FISCAL3 = 1992
```

**图 23.3** | 演示命名空间的使用。

