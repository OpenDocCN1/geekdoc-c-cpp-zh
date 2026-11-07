
## 24 其他主题

> 名字有什么关系？我们称为玫瑰的那朵花
> 换个名字，依然芬芳。
> ——威廉·莎士比亚
>
> 啊，钻石！钻石！你根本不知道闯下的祸端！
> ——艾萨克·牛顿爵士

### 学习目标

在本章中，你将学习：

- 使用 `const` 将 `const` 对象临时当作非 const 对象处理。
- 使用命名空间。
- 使用运算符关键字。
- 在 `const` 对象中使用可变成员。
- 使用类成员指针运算符 `.*` 和 `->*`。
- 使用多重继承。
- `virtual` 基类在多重继承中的作用。

![](img/bfd978e7e9b192bab46ec2a89e481263_1007_0.png)

![](img/bfd978e7e9b192bab46ec2a89e481263_1008_0.png)

- 24.1 引言
- 24.2 `const_cast` 运算符
- 24.3 `mutable` 类成员
- 24.4 `namespaces`
- 24.5 运算符关键字
- 24.6 指向类成员的指针（`.*` 和 `->*`）
- 24.7 多重继承
- 24.8 多重继承与 `virtual` 基类
- 24.9 收尾
- 总结 | 自测练习 | 自测练习答案 | 练习

### 24.1 引言

现在我们来考虑 C++ 的其他特性。首先讨论 const_cast 运算符，它允许你添加或移除变量的 const 限定。接下来讨论命名空间，命名空间可用于确保程序中的每个标识符都具有唯一名称，并有助于解决因使用含有相同变量名、函数名或类名的库而导致的命名冲突。然后介绍几个运算符关键字，这些关键字对键盘不支持运算符符号（如 !、&、^、~ 和 |）中某些字符的程序员很有用。接着讨论 mutable 存储类说明符，它使你能够指明某个数据成员应始终可修改，即使它出现在程序当前视为 const 对象的对象中。接下来介绍两个特殊运算符，它们可与指向类成员的指针一起使用，从而无需事先知道数据成员或成员函数的名称即可访问它。最后介绍多重继承，它使派生类能够继承多个基类的成员。作为这一介绍的一部分，我们讨论多重继承可能带来的问题，以及如何使用虚继承来解决这些问题。

### 24.2 `const_cast` 运算符

C++ 提供 const_cast 运算符，用于去除 const 或 volatile 限定。当你预期变量会被硬件或编译器未知的其他程序修改时，就用 volatile 限定符声明该变量。将变量声明为 volatile 表示编译器不应优化对该变量的使用，因为这样做可能影响那些其他程序访问和修改该 volatile 变量的能力。

一般来说，使用 const_cast 运算符是危险的，因为它允许程序修改声明为 const 的变量。有些情况下，去除 const 限定是合适的，甚至是必要的。例如，较旧的 C 和 C++ 库提供的函数具有非 const 参数，并且不会修改其参数——如果你希望将 const 数据传递给这样的函数，就需要去除数据的 const 限定；否则，编译器会报告错误消息。

类似地，你可以将非 const 数据传递给一个函数，该函数把这些数据当作常量处理，然后以常量形式返回这些数据。在这种情况下，你可能需要去除返回数据的 const 限定，如图 24.1 所示。

```cpp
// Fig. 24.1: fig24_01.cpp
// Demonstrating const_cast.
#include <iostream>
#include <cstring> // contains prototypes for functions strcmp and strlen
#include <cctype> // contains prototype for function toupper
using namespace std;

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

    for ( size_t i = 0; i < strlen( maxPtr ); ++i )
        maxPtr[ i ] = toupper( maxPtr[ i ] );

    cout << "The larger string capitalized is: " << maxPtr << endl;
} // end main
```

```
The larger string is: hello
The larger string capitalized is: HELLO
```

**图 24.1** | 演示运算符 `const_cast`。

在这个程序中，函数 maximum（第 9—12 行）接收两个 C 风格字符串作为 const char * 参数，并返回一个指向两个字符串中较大者的 const char *。函数 main 将这两个 C 风格字符串声明为非 const char 数组（第 16—17 行）；因此，这些数组是可修改的。在 main 中，我们希望输出两个 C 风格字符串中较大的那个，然后通过将其转换为大写字母来修改该 C 风格字符串。

函数 maximum 的两个参数类型为 const char *，因此该函数的返回类型也必须声明为 const char *。如果返回类型仅指定为 char *，编译器会发出错误消息，指出正在返回的值无法从 const char * 转换为 char *——这是一种危险的转换，因为它试图把函数认为是 const 的数据当作非 const 数据处理。

尽管函数 maximum 认为数据是常量，但我们知道 main 中的原始数组并不包含常量数据。因此，main 应该能够在必要时修改这些数组的内容。既然我们知道这些数组是可修改的，就使用 const_cast（第 21 行）去除 maximum 返回的指针的 const 限定，这样之后就能修改表示两个 C 风格字符串中较大者的数组中的数据。然后，我们可以在 for 语句（第 25—26 行）中将该指针用作字符数组的名称，以将较大字符串的内容转换为大写字母。如果没有第 21 行中的 `const_cast`，该程序将无法编译，因为不允许将 `const char *` 类型的指针赋给 `char *` 类型的指针。

> **错误预防提示 24.1**
>
> *通常，只有在事先知道原始数据不是常量时，才应使用 `const_cast`。否则，可能会发生意外结果。*

### 24.3 mutable 类成员

在 24.2 节中，我们介绍了 `const_cast` 运算符，它允许我们移除某个类型的“const 限定”。`const_cast` 操作也可以在该对象所属类的 const 成员函数体内，应用于 const 对象的数据成员。这使得 const 成员函数能够修改该数据成员，即使在该函数体内该对象被视为 const。当对象的多数数据成员应被视为 const，但某个特定数据成员仍需要修改时，就可以执行这样的操作。

例如，考虑一个按排序顺序维护其内容的链表。在链表中搜索不需要修改链表的数据，因此搜索函数可以是链表类的 const 成员函数。然而，可以设想，链表对象为了提高将来搜索的效率，可能会记录上一次成功匹配的位置。如果下一次搜索操作试图定位列表中更靠后的项，搜索可以从上一次成功匹配的位置开始，而不是从列表开头开始。为此，执行搜索的 const 成员函数必须能够修改记录上一次成功搜索的数据成员。

如果像上面描述的那样的数据成员应当*始终*可修改，C++ 提供了存储类说明符 `mutable` 作为 `const_cast` 的替代方案。mutable 数据成员始终可修改，即使在 const 成员函数或 const 对象中也是如此。

> **可移植性提示 24.1**
>
> *尝试修改定义为 const 的对象的效果，无论该修改是通过 `const_cast` 还是 C 风格强制转换实现的，都因编译器而异。*

`mutable` 和 `const_cast` 用于不同的上下文。对于没有 mutable 数据成员的 const 对象，每次要修改成员时都必须使用 `const_cast` 运算符。这大大降低了成员被意外修改的可能性，因为该成员并非永久可修改。涉及 `const_cast` 的操作通常*隐藏*在成员函数的实现中。类的使用者可能并不知道某个成员正在被修改。

> **软件工程观察 24.1**
>
> *`mutable` 成员在具有“秘密”实现细节的类中很有用，这些细节不参与客户端对该类对象的使用。*

