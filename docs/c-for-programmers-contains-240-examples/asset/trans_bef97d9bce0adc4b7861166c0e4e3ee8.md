

### 扩展 `sizeof`

`sizeof` 运算符返回存储对象所需的字节数。C++0x 允许在不通过其所属类的实例访问的情况下对数据成员调用 `sizeof`。`sizeof` 也可以更自然地与 `static` 数据成员一起使用。

### 序列点的替代方案

C++ 标准使用术语“序列点”来描述程序中操作发生的顺序。许多 C++ 专家认为该措辞未能清楚地描述程序执行中所需事件的顺序。本提案更改了标准中的措辞，以更精确地定义排序要求。此问题对 C++ 很重要，因为任何未来尝试添加并发性（即多线程）都需要对程序中事件的顺序有充分的理解。

### 21.12 总结

在本章中，我们讨论了 C++ 未来的各个方面。我们介绍了 Boost C++ 库并描述了包含在 TR1 中的 Boost 库——对 C++ 标准库的补充。

我们讨论了 `Boost.Regex` 库以及用于形成正则表达式的符号。我们提供了如何使用 `Boost.Regex` 类的示例，包括 `regex`、`match_results` 和 `regex_token_iterator`。你学习了如何使用 `Boost.Regex` 算法 `regex_search` 和 `regex_match` 在字符串中查找模式并将整个字符串与模式匹配。我们演示了如何使用 `regex_replace` 替换字符串中的字符，以及如何使用 `regex_token_iterator` 将字符串拆分为标记。

我们提供了如何使用 `Boost.Smart_ptr` 库的示例。我们讨论了包含在 TR1 中的智能指针，即 `shared_ptr` 和 `weak_ptr`。我们向你展示了如何使用这些类在使用动态分配内存时避免内存泄漏。我们演示了如何使用自定义删除器函数使 `shared_ptr` 管理需要特殊销毁过程的资源。我们还解释了如何使用 `weak_ptr` 来防止循环引用数据中的内存泄漏。

我们概述了即将修订的标准 C++0x，讨论了 TR1 以及对核心语言的更改。我们介绍了被接受到 TR1 中的每个库。我们描述了新的核心语言特性，包括 `auto` 关键字、*rvalue* 引用、与 C99 兼容性的改进、额外的整数类型以及有条件支持行为的新概念。请记住 Boost、TR1 和 C++0x  constantly 变化——访问我们的资源中心以了解最新信息。

在下一章中，我们将讨论更多高级 C++ 特性，包括强制转换运算符、命名空间、运算符关键字、指向类成员的指针运算符、多重继承和虚基类。

- 33. Jens Maurer，“Extending sizeof to Apply to Non-Static Data Members Without an Object”，文件编号 N2150=07-0010，2007 年 1 月 7 日，www.open-std.org/jtc1/sc22/wg21/docs/papers/2007/n2150.html。
- 34. Clark Nelson，“A Finer-Grained Alternative to Sequence Points”，文件编号 N1944=06-0014，2006 年 2 月 17 日，www.open-std.org/jtc1/sc22/wg21/docs/papers/2006/n1944.htm。

## 其他主题

> *What’s in a name? that*  
> *which we call a rose*  
> *By any other name would*  
> *smell as sweet.*  
>  
> —William Shakespeare  
>  
> *O Diamond! Diamond!*  
> *thou little knowest the*  
> *mischief done!*  
>  
> —Sir Isaac Newton

### OBJECTIVES

在本章你将学习：

- 使用 `const_cast` 暂时将 `const` 对象视为非 const 对象。
- 使用命名空间。
- 使用运算符关键字。
- 在 const 对象中使用 mutable 成员。
- 使用类成员指针运算符 `.*` 和 `->*`。
- 使用多重继承。
- 虚基类在多重继承中的作用。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_911_0.png)

- 22.1 Introduction
- 22.2 const_cast Operator
- 22.3 namespaces
- 22.4 Operator Keywords
- 22.5 mutable Class Members
- 22.6 Pointers to Class Members ( .* and ->* )
- 22.7 Multiple Inheritance
- 22.8 Multiple Inheritance and virtual Base Classes
- 22.9 Wrap-Up

### 22.1 Introduction

我们现在考虑几个高级 C++ 特性。首先，你将学习 const_cast 运算符，它允许程序员添加或删除变量的 const 限定。接下来，我们讨论命名空间，可用于确保程序中每个标识符都有唯一名称，并可帮助解决因使用具有相同变量、函数或类名称的库而导致命名冲突的问题。然后，我们介绍了一些运算符关键字，对那些键盘不支持运算符符号中某些字符（如 !、&、^、~ 和 |）的程序员很有用。我们继续讨论 mutable 存储类说明符，它使程序员能够指示数据成员应始终可修改，即使它出现在程序当前将其视为 const 对象的对象中。接下来，我们介绍两个特殊运算符，可与指向类成员的指针一起使用，以在不知道其名称的情况下访问数据成员或成员函数。最后，我们介绍多重继承，它使派生类能够继承多个基类的成员。作为介绍的一部分，我们讨论了多重继承的潜在问题以及如何使用虚继承来解决这些问题。

### 22.2 const_cast Operator

C++ 提供了 const_cast 运算符用于转换掉 const 或 volatile 限定。当你期望变量被硬件或其他编译器不知道的程序修改时，你声明变量具有 volatile 限定符。声明变量为 volatile 表示编译器不应优化该变量的使用，因为这样做可能会影响那些其他程序访问和修改 volatile 变量的能力。

通常，使用 const_cast 运算符很危险，因为它允许程序修改声明为 const 的变量，而该变量本不应该被修改。有时，取消 const 属性是可取的，甚至是必要的。例如，较旧的 C 和 C++ 库可能提供具有非 const 参数且不修改其参数的函数。如果你希望将 const 数据传递给此类函数，你需要取消数据的 const 属性；否则，编译器会报告错误消息。

同样，你可以将非 const 数据传递给将数据视为常量然后将其作为常量返回的函数。在这种情况下，你可能需要取消返回数据的 const 属性，正如我们在图 22.1 中演示的那样。

在此程序中，函数 maximum（第 11–14 行）接收两个 C 风格字符串作为 const char * 参数，并返回指向两个字符串中较大者的 const char *。函数 main 将两个 C 风格字符串声明为非 const char 数组（第 18–19 行）；因此，这些数组是可修改的。在 main 中，我们希望输出两个 C 风格字符串中较大的一个，然后通过将其转换为大写字母来修改该 C 风格字符串。

函数 maximum 的两个参数的类型为 const char *，因此函数的返回类型也必须声明为 const char *。如果返回类型仅指定为 char *，编译器会发出错误消息，指出无法将值从 const char * 转换为 char *——这是危险的转换，因为它试图将函数认为 const 的数据当作非 const 数据处理。

```
// Fig. 22.1: fig22_01.cpp
// Demonstrating const_cast.
#include <iostream>
using std::cout;
using std::endl;

#include <cstring> // contains prototypes for functions strcmp and strlen
#include <cctype> // contains prototype for function toupper

// returns the larger of two C-style strings
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
    char *maxPtr = const_cast< char * >( maximum( s1, s2 ) );

    cout << "The larger string is: " << maxPtr << endl;

    for ( size_t i = 0; i < strlen( maxPtr ); i++ )
        maxPtr[ i ] = toupper( maxPtr[ i ] );

    cout << "The larger string capitalized is: " << maxPtr << endl;
    return 0;
} // end main
```

The larger string is: hello  
The larger string capitalized is: HELLO

