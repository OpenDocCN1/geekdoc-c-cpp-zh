
C++ 库，后来成为 C++ 标准库的一部分（参见 [Josuttis03]）。

- 3. Josuttis 在核心语言特性的开发中也发挥了重要作用。

## 第28章 调试模板

模板在调试时会带来两类挑战。其中一类挑战对于复杂软件的编写者来说无疑是问题：我们如何确保所编写的模板能够对任何满足我们记录条件的模板参数正常工作？另一类问题则几乎正好相反：模板的用户如何找出问题涉及哪些模板参数？

在深入探讨这些问题之前，有必要思考可能施加于模板参数的各种约束。在本章中，我们主要处理那些违反时会导致编译错误的约束，并将这些约束称为语法约束。语法约束可以包括需要存在某种构造函数、特定的函数调用必须无歧义等等。另一种约束我们称为语义约束。这些约束更难机械化验证。在一般情况下，甚至可能不切实际。例如，我们可能要求模板类型参数具有某种定义（这是语法约束），但通常我们还要求该运算符在其定义域上实际定义了某种排序（这是语义约束）。

“概念”一词常用于表示模板库中反复要求的一组约束。例如，C++ 标准库依赖于随机访问迭代器和可默认构造等概念。有了这个术语，我们可以说调试模板代码需要大量识别概念在模板实现及其使用中是如何被违反的。本章深入探讨了使模板更易于使用的设计和调试技术，无论是对模板作者还是模板用户而言。

### 28.1 浅实例化

当模板错误发生时，问题往往是在一连串漫长的实例化之后才被发现的，从而产生如第 143 页 9.4 节所讨论的那样冗长的错误信息。为了说明这一点，请考虑下面这段有些刻意构造的代码：

```cpp
template<typename T>
void f(T p)
{
    p = 0; // assumes T is pointer-like type
}

template<typename T>
void code(T p)
{
    clear(p);
}

template<typename T>
void shell(T const& p)
{
    code(p);
}

template<typename T>
void shell(T const& env)
{
    typename T::index i;
    middle(env);
}
```

这个例子说明了软件开发中典型的层次结构：像 `shell()` 这样的高层定义模板依赖于较低层的组件；而较低层组件本身又使用像 `code()` 这样的基本设施。当我们实例化 `shell()` 时，其下方所有层次也被迫实例化。在这个例子中，问题在最低层暴露：`code()` 以 `int` 类型实例化（源于 `shell()` 中 `T::index` 的使用），并试图解引用该类型的值，这是一个错误。

该错误仅在实例化时才能被检测到。例如：

```cpp
class Client
{
public:
    using Index = std::int32_t;

private:
    Client mClient;
    std::uint64_t mId;
};
```

一个好的泛型诊断应包含导致问题的所有层次的轨迹，但我们也需要看到哪些信息能够自然地出现。

围绕这个问题的核心问题的精彩讨论可以在 [Fairbanks02] 中找到。Bryce Adelstein Lelbach 在那篇文章中确定了两类判断类模板参数是否有效的方法：一类是语法方法，尝试识别表达式的有效性（例如 `std::is_constructible`）；另一类是语义方法，检查给定类型是否为给定模板参数的合法匹配。他还提到，生成的代码并不总是与原始代码一样高效。

在我们之前的例子中，我们可以添加一个小检查，尝试确定一个值是否是一种类型。

```cpp
template<typename T>
void f(T t) {
    if constexpr (is_valid<T>) {
        ...
    }
    else {
        ...
    }
}
```

```cpp
template<typename T>
void f(T t) {
    if constexpr (std::is_class<T>::value) {
        ...
    }
    else {
        ...
    }
}
```

如果我们传入的类型没有默认构造函数，错误现在会在调用 `std::is_class` 的那一行被诊断出来。这并非因为该类实际上不为真，而是因为编译器尝试为一个没有默认构造函数的类型实例化该模板。不幸的是，许多编译器对 `std::is_class` 的实现仍然不够好（或者至少不正确），因此这种方法仍然行不通。我们可以定义一个类型用作模板参数，并使用 `std::is_class` 来检查该类型是否是一个类。由于第一个问题，这种方法仍然行不通。

### 概念检查

显然，在例子中编写占位代码可能会变得繁琐。我们需要一种更好的方法来检查给定的模板参数是否满足模板的语法要求。为了应对这种复杂性，在语言中引入概念（concept）来检查类型对模板是否有效是自然的做法。概念是一个编译期谓词，可用于检查模板参数是否有效。这种方法比之前的方法更高效，并且是标准库目前使用的方法。最流行的此类库是 Boost（参见 [Boost]）。

不幸的是，该技术并不是特别可移植（错误诊断的方式在不同编译器之间差异很大），并且有时会掩盖无法在更高层次表达的问题。

一旦我们在 C++ 中有了概念（参见附录 A），我们就会有其他方式来表示要求和预期行为。

### 28.2 静态断言

`static_assert` 宏在 C++ 代码中经常用于检查某个特定条件在程序执行的某个点是否成立。如果条件不成立，程序（大部分情况下）会被编译器中止，并输出一条错误信息。

```cpp
static_assert(sizeof(void*) >= 8, "64-bit code generation required for this library.");
```

静态断言可用于在模板参数不满足模板约束时提供有用的错误信息。例如，使用第 19.6 节中描述的技术，我们可以创建一个类型特征（type trait）来确定给定类型是否可解引用。

```cpp
template<typename T>
struct is_dereferenceable
{
    static constexpr bool value = ...;
};
```

```cpp
template<typename T>
class HasDereference {
private:
  template<typename U> struct Identity;

  template<typename U>
  static auto test(int) -> decltype(std::declval<U>());

  template<typename>
  static std::false_type test(...);

public:
  static constexpr bool value = decltype(test<T>(nullptr))::value;
};
```

现在，我们可以在 `shell()` 中引入一个静态断言，如果上一节中的 `shell()` 模板以不可解引用的类型实例化，它可以提供更好的诊断：

```cpp
template<typename T>
void shell() {
  static_assert(HasDereference<T>::value, "T is not dereferenceable");

  typename T::index i;
  middle(i);
}
```

通过这一改动，编译器会生成显著更简洁的诊断信息，指出类型 `T` 不可解引用。

静态断言可以使错误信息更简短、更直接，从而极大地改善使用模板库时的用户体验。

请注意，你也可以将它们应用于类模板，并使用附录 D 中讨论的所有类型特征。

```cpp
template<typename T>
class C {
  static_assert(HasDereference<T>::value, "T is not dereferenceable");
  static_assert(std::is_default_constructible<T>::value,
                "T is not default constructible");
};
```

### 28.3 原型

在编写模板时，要确保模板定义能够针对任何满足该模板指定约束的模板参数编译通过，是一项很有挑战性的工作。考虑一个简单的 `find()` 算法，它在一个数组中查找某个值，并附带其文档化的约束：

```cpp
// T must be EqualityComparable, meaning
// objects of type T can be compared with == and
// the result converted to bool
template<typename T>
int find(T const* array, int n, T const& value);
```

我们可以想象下面这个函数模板的直接实现：

```cpp
template<typename T>
int find(T const* array, int n, T const& value) {
  int i = 0;
  while (i < n && array[i] != value)
    ++i;
  return i;
}
```

这个模板定义存在两个问题。当给定某些模板参数时，这两个问题都会表现为编译错误——这些参数在技术上满足模板要求，但其行为与模板作者的预期略有不同。我们将使用原型（archetypes）的概念，根据 `find()` 模板所指定的要求来测试我们实现对其模板参数的使用。

原型是用户自定义的类，可以用作模板参数来测试模板定义是否遵守其对相应模板参数施加的约束。原型经过特别设计，以尽可能最简化的方式满足模板的要求，不提供任何额外的操作。如果使用原型对模板定义的实例化能够编译通过，那么就说明模板定义满足了模板的要求。

