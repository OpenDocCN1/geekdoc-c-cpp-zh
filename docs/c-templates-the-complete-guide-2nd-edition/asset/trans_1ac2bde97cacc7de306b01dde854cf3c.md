
程序输出如下：

```text
iStack.top(): 2
fStack.top(): 3.3
fStack.top(): 4.4
vStack.top(): 6.6
vStack: 4.4 2 1
```

关于模板模板参数的进一步讨论和示例，请参阅第 187 页的 12.2.3 节、第 197 页的 12.3.4 节以及第 398 页的 19.2.2 节。

### 5.8 小结

- 要访问依赖于模板参数的类型名，必须使用前置的 `typename` 限定该名称。
- 要访问依赖于模板参数的基类成员，必须通过 `this->` 或它们的类名来限定访问。
- 嵌套类和成员函数也可以是模板。其中一个应用是能够实现带有内部类型转换的泛型操作。
- 构造函数或赋值运算符的模板版本不会取代预定义的构造函数或赋值运算符。
- 通过使用花括号初始化或显式调用默认构造函数，可以确保模板的变量和成员在使用内置类型实例化时也会被默认值初始化。
- 可以为原始数组提供特定模板，这些模板也适用于字符串字面量。
- 传递原始数组或字符串字面量时，当且仅当参数不是引用，实参才会在实参推导期间退化（执行数组到指针的转换）。
- 可以定义*变量模板*（自 C++14 起）。
- 也可以将类模板用作模板参数，即*模板模板参数*。
- 模板模板实参通常必须与其参数完全匹配。

1. 也就是说，对于某个类型 X，构造函数带有一个类型为 `std::initializer_list<X>` 的参数。

2. 对于某个任意类型 X，类型为 X (&)[] 的参数只有在 C++17 中才有效，这是通过解决 Core issue 393 实现的。然而，许多编译器在早期版本的语言中已接受此类参数。

3. 这是一个用于演示模板特性的基本实现。当然缺少了诸如正确异常处理之类的问题。

4. 是的，我们使用非常相似的术语来表示截然不同的事物：变量模板（variable template）是一个作为模板的变量（这里的 variable 是名词）。可变参数模板（variadic template）是用于可变数量模板参数的模板（这里的 variadic 是形容词）。

5. 在 C++17 之前，这个版本存在一个问题，我们稍后会解释。然而，这仅影响默认值 `std::deque`。因此，在讨论如何在 C++17 之前处理它之前，我们可以用这个默认值来演示模板模板参数的一般特性。

## 第 6 章：移动语义与 enable_if<>

C++11 引入的最显著特性之一是*移动语义*。你可以使用它来优化拷贝和赋值，通过从源对象移动（“窃取”）内部资源到目标对象，而不是拷贝这些内容。只要源对象不再需要其内部值或状态（因为它即将被丢弃），就可以这样做。

移动语义对模板的设计有重大影响，并且引入了特殊规则来在泛型代码中支持移动语义。本章介绍这些特性。

### 6.1 完美转发

假设你想编写泛型代码来转发所传实参的基本属性：

- 可修改对象应被转发，以便它们仍然可以被修改。
- 常量对象应作为只读对象被转发。
- 可移动对象（我们可以“窃取”其内容的对象，因为它们即将过期）应作为可移动对象被转发。

要在不使用模板的情况下实现此功能，我们必须对所有三种情况进行编程。例如，将对 f() 的调用转发给相应的函数 g()：

```cpp
// basics/move1.cpp
#include <utility>
#include <iostream>

class X {
    ...
};

void g (X&) {
    std::cout << "g() for variable\n";
}
void g (X const&) {
    std::cout << "g() for constant\n";
}
void g (X&&) {
    std::cout << "g() for movable object\n";
}

// let f() forward argument val to g():
void f (X& val) {
    g(val); // val is non-const lvalue => calls g(X&)
}
void f (X const& val) {
    g(val); // val is const lvalue => calls g(X const&)
}
void f (X&& val) {
    g(std::move(val)); // val is non-const lvalue => needs std::move() to call g(X&&)
}

int main()
{
    X v; // create variable
    X const c; // create constant

    f(v); // f() for nonconstant object calls f(X&) => calls g(X&)
    f(c); // f() for constant object calls f(X const&) => calls g(X const&)
    f(X()); // f() for temporary calls f(X&&) => calls g(X&&)
    f(std::move(v)); // f() for movable variable calls f(X&&) => calls g(X&&)
}
```

这里，我们看到 f() 将其实参转发给 g() 的三种不同实现：

```cpp
void f (X& val) {
    g(val); // val is non-const lvalue => calls g(X&)
}
void f (X const& val) {
    g(val); // val is const lvalue => calls g(X const&)
}
void f (X&& val) {
    g(std::move(val)); // val is non-const lvalue => needs std::move() to call g(X&&)
}
```

注意，可移动对象（通过*右值引用*）的代码与其他代码不同：它需要 `std::move()`，因为根据语言规则，移动语义不会被传递。¹ 尽管第三个 f() 中的 `val` 被声明为右值引用，但它在作为表达式使用时，其值类别是非常量左值（见附录 B），其行为与第一个 f() 中的 val 相同。如果没有 move()，将调用针对非常量左值的 g(X&)，而不是 g(X&&)。

如果要在泛型代码中组合所有三种情况，我们会遇到一个问题：

```cpp
template<typename T>
void f (T val) {
    g(val);
}
```

这适用于前两种情况，但不适用于（第三种）传递可移动对象的情况。

C++11 为此引入了用于完美转发参数的特殊规则。实现这一点的惯用代码模式如下：

```cpp
template<typename T>
void f (T&& val) {
    g(std::forward<T>(val)); // perfect forward val to g()
}
```

注意，std::move() 没有模板参数，并且会“触发”所传实参的移动语义，而 std::forward<>() 则根据所传模板实参“转发”潜在的移动语义。

不要认为模板参数 T 的 T&& 与特定类型 X 的 X&& 行为相同。适用的规则不同！然而，它们在语法上看起来相同：

- 对于特定类型 X，`X&&` 声明参数为右值引用。它只能绑定到可移动对象（纯右值，如临时对象，以及将亡值，如使用 std::move() 传递的对象；详见附录 B）。它总是可变的，你总是可以“窃取”它的值。²
- 对于模板参数 T，`T&&` 声明一个转发引用（也称为通用引用）。³ 它可以绑定到可变的、不可变的（即 const）或可移动的对象。在函数定义内部，参数可以是可变的、不可变的，或者引用一个你可以“窃取”其内部内容的值。

注意，T 必须确实是模板参数的名称。仅仅依赖于模板参数是不够的。对于模板参数 T，像 `typename T::iterator&&` 这样的声明只是右值引用，而不是转发引用。

因此，用于完美转发实参的完整程序如下所示：

```cpp
// basics/move2.cpp
#include <utility>
#include <iostream>

class X {
    ...
};

void g (X&) {
    std::cout << "g() for variable\n";
}
void g (X const&) {
    std::cout << "g() for constant\n";
}
void g (X&&) {
    std::cout << "g() for movable object\n";
}

// let f() perfect forward argument val to g():
template<typename T>
void f (T&& val) {
    g(std::forward<T>(val)); // call the right g() for any passed argument
}

int main()
{
    X v; // create variable
    X const c; // create constant

    f(v); // f() for variable calls f(X&) => calls g(X&)
    f(c); // f() for constant calls f(X const&) => calls g(X const&)
    f(X()); // f() for temporary calls f(X&&) => calls g(X&&)
    f(std::move(v)); // f() for move-enabled variable calls f(X&&) => calls g(X&&)
}
```

当然，完美转发也可以与可变参数模板一起使用（一些示例见第 60 页的 4.3 节）。完美转发的详细信息见第 280 页的 15.6.3 节。

### 6.2 特殊成员函数模板

成员函数模板也可以用作特殊成员函数，包括用作构造函数，然而这可能会导致令人惊讶的行为。考虑以下示例：

