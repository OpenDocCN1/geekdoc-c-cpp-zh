
注意使用`typename`和`::type`提取成员类型时，`Obj_holder`（以及`Int`）的实现细节会显现出来。这是语言规范和使用方式的结果，这是过去 15 年来模板元编程代码的编写方式，也是 C++11 标准中的写法。我认为这令人难以忍受。它让我想起了 C 的坏老日子，那时每个用户定义类型的出现都必须以`struct`关键字为前缀。通过引入模板别名 (§23.6)，我们可以隐藏`::type`实现细节，并使类型函数看起来更像返回类型的函数（或像类型）。例如：

```cpp
template<typename T>
using Holder = typename Obj_holder<T>::type;

void f2() {
    Holder<double> v1;
    // the double goes on the stack
    Holder<array<double,200>> v2; // the array goes on the free store
    //
    *v1 = 7.7; // Scoped provides pointer-like access (* and [])
    v2[77] = 9.9; // On_heap provides pointer-like access (* and [])
    // ...
}
```

除了解释实现或标准具体提供的功能外，我系统地使用此类类型别名。当标准提供一个类型函数（称为“类型属性谓词”或“复合类型类别谓词”），例如`conditional`时，我定义一个对应的类型别名 (§35.4.1)：

```cpp
template<typename C, typename T, typename F>
using Conditional = typename std::conditional<C,T,F>::type;
```

请注意，这些别名不幸的是不是标准的一部分。

### 28.2.1.1 何时不使用别名

有一种情况，直接使用`::type`而不是别名是有意义的。如果只有一种备选方案 supposed to be 有效类型，我们不应使用别名。首先考虑一个简单的类比：

#### Section 28.2.1.1 When Not to Use an Alias 785

```cpp
if (p) {
    p->f(7);
    // ...
}
```

重要的是，如果`p`是`nullptr`，我们不要进入该块。我们正在使用测试来查看`p`是否有效。类似地，我们可能想测试一个类型是否有效。例如：

```cpp
conditional<
    is_integral<T>::value,
    make_unsigned<T>,
    Error<T>
>::type
```

在这里，我们测试`T`是否为整型（使用`std::is_integral`类型谓词），如果是，则生成该类型的无符号变体（使用`std::make_unsigned`类型函数）。如果

在这种情况下，我们得到一个无符号类型；否则，我们就必须处理`Error`指示器。

假如我们将`Make_unsigned<T>`写作

```cpp
typename make_unsigned<T>::type
```

并试图将其用于非整数类型，比如`std::string`，那么我们就会试图创建一个不存在的类型（`make_unsigned<std::string>::type`）。结果将是一个编译期错误。

在少数情况下，我们无法始终一致地使用别名来隐藏`::type`，此时我们可以退回到更显式、面向实现的`::type`风格。另一种方式是，我们可以引入一个`Delay`类型函数，将类型函数的求值延迟到其使用之时：

```cpp
Conditional<
    is_integral<T>::value ,
    Delay<Make_unsigned,T>,
    Error<T>
>
```

一个完美的`Delay`函数的实现并非易事，但对许多用途而言，下面这种写法就足够了：

```cpp
template<template<typename...> class F, typename ... Args>
using Delay = F<Args...>; 
```

这里使用了模板模板参数（§25.2.4）和变参模板（§28.6）。无论我们选择哪种方案来避免不期望的实例化，这都属于专家级领域，我只有在心怀忐忑时才会进入。

## 28.2.2 类型谓词

谓词是返回布尔值的函数。如果你想编写以类型为参数的函数，那么显然你会希望询问关于这些参数类型的问题。例如：这是一个有符号类型吗？这个类型是多态的吗（即它是否至少有一个虚函数）？这个类型是从那个类型派生出来的吗？

许多此类问题的答案编译器已知，并通过一组标准库类型谓词（§35.4.1）暴露给程序员。例如：

```cpp
template<typename T>
void copy(T* p, const T* q, int n) {
    if (std::is_pod<T>::value)
        memcpy(p,q,n); // 使用优化的内存拷贝
    else
        for (int i=0; i!=n; ++i)
            p[i] = q[i]; // 逐个拷贝值
}
```

在这里，当我们能把对象视为“普通旧数据”（POD；§8.2.6）时，我们尝试使用（据称最优的）标准库函数`memcpy()`来优化拷贝。否则，我们就逐个拷贝对象，（潜在地）使用它们的拷贝构造函数。我们通过标准库类型谓词`is_pod`来确定模板参数类型是否为 POD。结果通过成员`value`呈现。这个标准库约定类似于类型函数以成员类型呈现其结果的方式。

`std::is_pod`谓词是标准库提供的众多谓词之一（§35.4.1）。由于成为 POD 的规则很复杂，`is_pod`很可能是编译器内建功能，而不是作为 C++ 代码在库中实现的。

与`::type`约定一样，`::value`会造成冗长，并且偏离传统表示法，使得实现细节过于醒目：一个返回`bool`的函数应该使用`()`调用：

```cpp
template<typename T>
void copy(T* p, const T* q, int n)
{
    if (is_pod<T>())
    // ...
}
```

幸运的是，标准对所有标准库类型谓词都支持这种写法。不幸的是，由于语言技术上的原因，在模板参数上下文中无法使用这种解析方式。例如：

```cpp
template<typename T>
void do_something()
{
    Conditional<is_pod<T>(),On_heap<T>,Scoped<Y>> x; // 错误：is_pod<T>() 是一个类型
    // ..
}
```

具体来说，`is_pod<T>`被解释为一个函数的类型，该函数不接受参数并返回一个`is_pod<T>`（§iso.14.3[2]）。

我的解决方案是添加函数，以便在所有上下文中提供传统表示法：

```cpp
template<typename T>
constexpr bool Is_pod()
{
    return std::is_pod<T>::value; }
```

### 28.2.2 节 类型谓词 787

我将这些类型函数的名字大写，以避免与标准库版本混淆。此外，我将它们放在一个单独的命名空间（`Estd`）中。

我们可以定义自己的类型谓词。例如：

```cpp
template<typename T>
constexpr bool Is_big()
{
    return 100<sizeof(T);
}
```

我们可以这样使用这种（相当粗糙的）“大”的概念：

```cpp
template<typename T>
using Obj_holder = Conditional<(Is_big<T>()), Scoped<T>, On_heap<T>>;
```

很少有必要定义直接反映类型基本属性的谓词，因为标准库已经提供了许多此类谓词。例如`is_integral`、`is_pointer`、`is_empty`、`is_polymorphic`和`is_move_assignable`（§35.4.1）。当我们必须定义这样的谓词时，我们有相当强大的技术可用。例如，我们可以定义一个类型函数，以确定一个类是否具有给定名称且类型合适的成员（§28.4.4）。

自然地，具有多个参数的类型的谓词也可能很有用。特别是，我们这样来表示两个类型之间的关系，例如`is_same`、`is_base_of`和`is_convertible`。这些也来自标准库。

我使用`Is_*` constexpr 函数来为所有这些`is_*`函数支持通常的`()`调用语法。

## 28.2.3 选择一个函数

函数对象是某个类型的对象，因此用于选择类型和值的技术也可以用于选择函数。例如：

```cpp
struct X { // 写 X
    void operator()(int x) { cout <<"X" << x << "!"; }
    // ...
};
struct Y { // 写 Y
    void operator()(int y) { cout <<"Y" << y << "!"; } // ...
};
void f() {
    Conditional<(sizeof(int)>4),X,Y>{}(7); // 生成一个 X 或 Y
    using Z = Conditional<(Is_polymorphic<X>()),X,Y>;
    Z zz; // 生成一个 X 或 Y
    zz(7); // 调用一个 X 或 Y
}
```

如图所示，选定的函数对象类型可以立即使用，也可以“记住”以备后用。具有计算某个值的成员函数的类，是模板元编程中进行计算的最通用、最灵活的机制。

`Conditional` 是一种编译期编程机制。特别是，这意味着条件必须是常量表达式。注意`sizeof(int)>4`周围的括号；如果没有这些括号，我们就会遇到语法错误，因为编译器会将`>`解释为模板参数列表的结尾。出于这个原因（以及其他原因），我更喜欢使用`<`（小于）而不是`>`（大于）。此外，为了可读性，我有时也会在条件周围加上括号。

## 28.2.4 Traits

标准库严重依赖于*traits*。trait 用于将属性与类型关联起来。例如，迭代器的属性由其`iterator_traits`（§33.1.3）定义：

```cpp
template<typename Iterator>
struct iterator_traits {
    using difference_type = typename Iterator::difference_type;
    using value_type = typename Iterator::value_type;
    using pointer = typename Iterator::pointer;
    using reference = typename Iterator::reference;
    using iterator_category = typename Iterator::iterator_category;
};
```

你可以将 trait 视为具有多个结果的类型函数，或视为一组类型函数。

标准库提供了`allocator_traits`（§34.4.2）、`char_traits`（§36.2.2）、`iterator_traits`（§33.1.3）、`regex_traits`（§37.5）、`pointer_traits`（§34.4.3）。此外，它还提供了`time_traits`（§35.2.4）和`type_traits`（§35.4.1），而令人困惑的是，后者只是简单的类型函数。

给定一个针对指针的`iterator_traits`，即使指针没有成员，我们也可以谈论指针的`value_type`和`difference_type`：

```cpp
template<typename Iter>
Iter search(Iter p, Iter q, typename iterator_traits<Iter>::value_type val)
{
    typename iterator_traits<Iter>::difference_type m = q-p;
    // …
}
```

这是一种非常有用且强大的技术，但是：

- 它很冗长。
- 它经常将本来关联性较弱的类型函数捆绑在一起。
- 它向用户暴露了实现细节。

此外，人们有时会“以防万一”添加类型别名，导致不必要的复杂性。因此，我更喜欢使用简单的类型函数：

```cpp
template<typename T>
using Value_type = typename std::iterator_traits<T>::value_type;
template<typename T>
using Difference_type = typename std::iterator_traits<T>::difference_type;
template<typename T>
using Iterator_category = typename std::iterator_traits<T>::iterator_category;
```

The example cleans up nicely：

```cpp
template<typename Iter>
Iter search(Iter p, iter q, Value_type<Iter> val)
{
    Difference_type<Iter> m = q-p;
    // ...
}
```

I suspect that traits are currently overused. Consider how to write the previous example without any mention of traits or other type functions：

```cpp
template<typename Iter, typename Val>
Iter search(Iter p, iter q, Val val)
{
    auto x = *p; // if we don’t need to name *p’s type
    auto m = q-p; // if we don’t need to name q-p’s type
    using value_type = decltype(*p); // if we want to name *p’s type
    using difference_type = decltype(q-p); // if we want to name q-p’s type
    // ...
}
```

Of course, `decltype()` is a type function, so all I did was to eliminate user-defined and standard library type functions. Also, `auto` and `decltype` are new in C++11, so older code could not have been written this way.

We need a trait (or equivalent, such as `decltype()`) to associate a type with another type, such as a `value_type` with a `T*`. For that, a trait (or an equivalent) is indispensable for non-intrusively adding type names needed for generic programming or metaprogramming. When a trait is used simply to provide a name for something that already has a perfectly good name, such as `pointer` for `value_type*` and `reference` for `value_type&`, the utility is less clear and the potential for confusion greater. Don’t blindly define traits for everything “just in case.”

# 28.3 Control Structures

To do general computation at compile time, we need selection and recursion.

## 28.3.1 Selection

In addition to what is trivially done using ordinary constant expressions (§10.4), I use:

- `Conditional`: a way of choosing between two types (an alias for `std::conditional`)
- `Select`: a way of choosing among several types (defined in §28.3.1.3)
