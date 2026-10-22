
```
int main()
{
int a;
clear(a); // ERROR: int doesn't support the unary *
}
```

## 12.3.3 非类型实参

非类型模板实参是替换非类型参数的值。这样的值必须是以下之一：
- 另一个具有正确类型的非类型模板参数。
- 整数（或枚举）类型的编译期常量值。仅当对应参数的类型与该值的类型匹配，或者该值可以隐式转换到该类型且不发生窄化转换时，该值才是可接受的。例如，可以为 int 参数提供 char 值，但 500 不能作为 8 位 char 参数的有效值。
- 一个外部变量或函数的名称，前面加上内置的一元 &（“取地址”）运算符。对于函数和数组变量，可以省略 &。这类模板实参匹配指针类型的非类型参数。C++17 放宽了这一要求，允许任何产生指向函数或变量的指针的常量表达式。
- 前一种实参但不带前导 & 运算符的形式，是引用类型非类型参数的有效实参。同样，C++17 放宽了约束，允许任何针对函数或变量的常量表达式泛左值。
- 成员指针常量；换句话说，形式为 &C::m 的表达式，其中 C 是类类型，m 是非静态成员（数据或函数）。这仅匹配成员指针类型的非类型参数。同样，在 C++17 中，实际语法形式不再受限：任何求值为匹配的成员指针常量的常量表达式都是允许的。
- 空指针常量是指针或成员指针类型的非类型参数的有效实参。

对于整数类型的非类型参数——可能是最常见的一类非类型参数——会考虑对参数类型的隐式转换。随着 C++11 引入 constexpr 转换函数，这意味着转换前的实参可以具有类类型。

在 C++17 之前，当将实参与指针或引用类型的参数匹配时，实参必须是具有外部链接（C++11 起也允许内部链接）的常量表达式（任一链接形式均可）。字符串字面量的一个问题是，两个相同的字面量可能存储在两个不同的地址。要在常量字符串上实例化模板，还有一种（但比较笨拙）的替代方法是引入一个额外变量来保存该字符串：单击此处查看代码图像

```
template<char const* str>
class Message {
...;
};

extern char const hello[] = "Hello World!";
char const hello11[] = "Hello World!";

void foo()
{
static char const hello17[] = "Hello World!";

Message<hello> msg03; // OK in all versions
Message<hello11> msg11; // OK since C++11
Message<hello17> msg17; // OK since C++17
}
```

要求是，声明为引用或指针的非类型模板参数在所有 C++ 版本中都可以是带有外部链接的常量表达式，自 C++11 起可以是内部链接，自 C++17 起可以是任意链接。

关于此领域未来可能的变化，参见第 354 页的 17.2 节。下面是一些其他（不太令人惊讶的）无效示例：单击此处查看代码图像

```
template<typename T, T nontypeParam>
class C;

struct Base {
int i;
} base;

struct Derived : public Base {
} derived;

C<Base*, &derived>* err1; // ERROR: derived-to-base conversions are not considered

C<int&, base.i>* err2; // ERROR: fields of variables aren’t considered to be variables

int a[10];
C<int*, &a[0]>* err3; // ERROR: addresses of array elements aren’t acceptable either
```

## 12.3.4 模板模板实参

模板模板实参通常必须是类模板或别名模板，其参数必须与它所替换的模板模板参数完全匹配。在 C++17 之前，模板模板实参的默认模板实参会被忽略（但如果模板模板参数具有默认实参，则在模板实例化期间会考虑这些默认实参）。C++17 放宽了匹配规则，只要求模板模板参数至少与相应的模板模板实参一样特化（参见第 330 页的 16.2.2 节）。

这使得以下示例在 C++17 之前无效：单击此处查看代码图像

```
#include <list>
// declares in namespace std:
// template<typename T, typename Allocator = allocator<T>>
// class list;

template<typename T1, typename T2,
template<typename> class Cont> // Cont expects one parameter
class Rel {
...
};

Rel<int, double, std::list> rel; // ERROR before C++17: std::list has more than
// one template parameter
```

这个示例的问题在于，标准库的 std::list 模板有多个参数。第二个参数（描述分配器）有一个默认值，但在 C++17 之前，将 std::list 与 Container 参数匹配时不会考虑该默认值。

可变参数模板模板参数是上述 C++17 之前“精确匹配”规则的一个例外，为这个限制提供了解决方案：它们允许与模板模板实参进行更通用的匹配。模板模板参数包可以匹配模板模板实参中任意数量（零个或多个）的同类模板参数：单击此处查看代码图像

```
#include <list>

template<typename T1, typename T2,
template<typename...> class Cont> // Cont expects any number of
class Rel { // type parameters
...
};
```

```
Rel<int, double, std::list> rel; // OK: std::list has two template parameters
// but can be used with one argument
```

模板参数包只能匹配同一种类的模板实参。例如，下面的类模板可以用任何只具有模板类型参数的类模板或别名模板来实例化，因为这里作为 TT 传递的模板类型参数包可以匹配零个或多个模板类型参数：单击此处查看代码图像

```
#include <list>
#include <map>
// declares in namespace std:
// template<typename Key, typename T,
// typename Compare = less<Key>,
// typename Allocator = allocator<pair<Key const, T>>>
// class map;
#include <array>
// declares in namespace std:
// template<typename T, size_t N>
// class array;
```

```
template<template<typename... > class TT>
class AlmostAnyTmpl {
};
```

```
AlmostAnyTmpl<std::vector> withVector; //two type parameters
AlmostAnyTmpl<std::map> withMap; // four type parameters
AlmostAnyTmpl<std::array> withArray; // ERROR: a template type parameter pack
// doesn’t match a nontype template parameter
```

在 C++17 之前，只有关键字 class 可以用于声明模板模板参数，但这并不意味着只有用关键字 class 声明的类模板才能作为替换实参。事实上，struct、union 和别名模板都是模板模板参数的有效实参（别名模板自 C++11 引入时起即可）。这与任何类型都可以用作以关键字 class 声明的模板类型参数的实参这一事实类似。

## 12.3.5 等价性

当两组模板实参的值逐项相同时，它们是等价的。对于类型实参，类型别名无关紧要：比较的是最终位于类型别名声明底层的类型。对于整数非类型实参，比较的是实参的值；该值的表达方式并不重要。下面的示例说明了这个概念：单击此处查看代码图像

```
template<typename T, int I>
class Mix;

using Int = int;

Mix<int, 3*3>* p1;
Mix<Int, 4+5>* p2; // p2 has the same type as p1
```

（从这个示例可以清楚地看到，不需要模板定义就能确定模板实参列表的等价性。）然而，在依赖于模板的上下文中，模板实参的“值”并不总能明确确定，等价性规则因此会变得稍微复杂一些。考虑以下示例：单击此处查看代码图像

```
template<int N> struct I {};

template<int M, int N> void f(I<M+N>); // #1
template<int N, int M> void f(I<N+M>); // #2

template<int M, int N> void f(I<N+M>); // #3 ERROR
```

仔细研究声明 #1 和 #2，你会注意到，只需将 M 和 N 分别重命名为 N 和 M，就能得到相同的声明：因此这两个声明是*等价的*，声明了相同的函数模板 f。这两个声明中的表达式 M+N 和 N+M 被称为*等价*的。

然而，声明 #3 有一个微妙的区别：操作数的顺序颠倒了。这使得 #3 中的表达式 N+M 与其他两个表达式中的任意一个都*不*等价。但是，由于该表达式对所涉及的模板参数的任意值都会产生相同的结果，因此这些表达式被称为*功能等价*的。如果模板的声明方式仅仅因为包含实际上不等价但功能等价的表达式而不同，那是错误的。不过，这种错误不一定需要编译器诊断出来。这是因为某些编译器可能会在内部以与 N+2 完全相同的方式表示 N+1+1，而其他编译器可能不会。标准并没有强制规定具体的实现方式，而是允许任一种情况，并要求程序员在这一领域小心谨慎。

从函数模板生成的函数与普通函数永远不等价，即使它们可能具有相同的类型和相同的名称。这对类成员有两个重要后果：1. 生成的函数

