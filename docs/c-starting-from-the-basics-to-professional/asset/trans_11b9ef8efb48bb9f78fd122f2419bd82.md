
**注意** 并非所有编译器都（完全）实现两阶段查找，并且会将更多（如果不是大多数）检查推迟到模板实例化时。因此，你的编译器可能直到你实际使用该模板时，才会注意到我们先前示例中未声明的 `kfzT3e7l` 名称。如果是这样，你可能也不需要我们在接下来两个小节中讨论的部分或任何变通方法。

当然，编译器是在早期还是在实例化时才拒绝无效模板，通常并不重要。然而，我们在这里要处理的问题是，编译器有时也会在实例化之前拒绝看似有效的模板——这些模板在用实际类型文本替换所有类型参数名后会产生完全有效的代码。这是 C++ 最令人烦恼的怪癖之一：你的模板在你看来完全正确，但编译器却吐出一大堆令人困惑的错误消息。

这种情况有时发生的原因总是归结为同一件事：编译器试图理解未实例化的模板，并以某种方式误解了依赖名。要纠正这一点，你需要了解一些简单——但远非显而易见——的语法变通方法。我们现在概述两种相当常见的情况，你的编译器可能会像那样困惑，然后展示你可以使用哪些变通方法让它正确解析你的模板。

### 依赖类型名

假设你有一个如下形式的类模板（类似于之前的 Stack<> 模板）。

```cpp
template <typename T>
class Outer
{
public:
    class Nested { /* ... */ }; // Or a type alias of form "using Nested = ...;"
    // ...
};
```

**注意** 嵌套类型和类型别名成员在标准库中实际上相当常见。示例包括 `vector<>::iterator`、`optional<>::value_type` 和 `shared_ptr<>::weak_type`。

现在尝试定义以下函数模板（见 Ex17_05A.cpp）：

```cpp
template <typename T>
void someFunction() { Outer<T>::Nested* nested; /* ... */ }
```

在我们的一个编译器中，这会产生以下错误（没有任何进一步信息）：

```text
error: 'nested' was not declared in this scope
   17 | void someFunction() { Outer<T>::Nested* nested; /* ... */ }
      |                                       ^~~~~~
```

愚蠢的编译器……当然，nested 在那里还没有被声明：你正在拒绝的语句正是 nested 的声明！那么发生了什么？为什么我们的编译器在这里搞糊涂了？

问题在于，在模板体内，编译器通常不会将诸如 `T::name` 或 `MyClass<T>::name` 这样的依赖名解释为类型名。因此，在我们的示例中，编译器将函数体的起始语句读作两个变量 `Outer<T>::Nested` 和 `nested` 的乘法。因此，在编译器看来，`nested` 必须是一个非依赖名，就像我们先前示例中的[名称]一样。当然，编译器随后在周围作用域中找不到 `nested` 的声明——于是就有了那条令人困惑的错误消息。

要让编译器将诸如 `Nested` 这样的依赖名解释为类型名，你必须使用 `typename` 关键字显式地将其标记为类型名。例如，Ex17_05A 中的模板可以按如下方式修复：

```cpp
template <typename T>
void someFunction() { typename Outer<T>::Nested* nested; /* ... */ }
```

现在编译器会按预期解析其起始语句：将其解析为变量 `nested` 的声明，其类型为指向 `Outer<T>::Nested` 的指针。

这是否意味着你总是必须在依赖类型名前添加 `typename`？不完全如此。有时你的编译器确实会默认将依赖名识别为类型名。例如，当依赖名与 `new` 一起使用或位于强制转换表达式中时，你的编译器显然已经知道该名称只能指代类型。下面是一个示例（另见 Ex17_05B）：

```cpp
template <typename T> // assumed to define Nested Base and Derived types / aliases
void someOtherFunction()
{
    typename T::Base* b = new T::Derived();        // Or: auto* b = ...
    const typename T::Derived& d = static_cast<T::Derived&>(*b); // Or: const auto& d = ...
    /* ... */
}
```

在这里，你仍然需要 `typename` 来消除赋值左侧名称的歧义。不过，如所示，诸如 `auto`、`auto*` 或 `auto&` 这样的占位类型通常可以成为更紧凑的替代方案。

遗憾的是，在函数模板体之外，依赖类型名的规则甚至更加不稳定。例如，在 C++20 中，你不再需要在类模板的成员声明中消除依赖类型名的歧义（另见 Ex17_05C）：

```cpp
template <typename T>
class MyClass
{
public:
    Outer<T>::Nested memberFunction(const Outer<T>::Nested& nested);
private:
    T::Nested m_member_variable;
};
```

事实上，对于函数模板的返回类型，你再也不必使用 `typename`。但出于某种原因，在函数模板和成员函数模板的参数列表中，你仍然需要在依赖名前添加 `typename`。

```cpp
template<class T>
T::Nested nonMemberFunction(const typename T::Nested* nested);
```

```cpp
template<typename T>
Outer<T>::Nested MyClass<T>::memberFunction(const typename Outer<T>::Nested& nested)
{
    return nested;
}
```

准确知道 `typename` 在依赖类型名前何时可选或何时必需，并没有那么重要。老实说，我们也不知道完整的规则集。本节的主要收获应该是：你学会识别由被误解的依赖类型名引起的错误，并且知道如何通过添加 `typename` 来规避它们。在实践中，这意味着你基本上有以下选择：你可以稳妥起见，在所有（或大多数）依赖类型名前添加 `typename`，或者尽可能少地添加，并依靠编译器告诉你何时漏掉了一个。既然你理解了这个问题，这两种务实的方法都可以很好地工作。

### 依赖基类

当你将模板与继承结合时，依赖名带来的麻烦也会出现。更具体地说，当你使用依赖类型作为基类时，它们就会出现。其最常见的形式是，当你定义如下所示的类模板时（可在 Ex17_06.cpp 中找到）：

```cpp
template <typename T>
class Base
{
public:
    void baseFun() { /* ... */ }
protected:
    int m_base_var;
};

template <typename T>
class Derived : public Base<T>
{
public:
    void derivedFun();
};
```

这个设置根本没有什么特别之处：`Derived<T>` 类继承自 `Base<T>` 类，并且它们都有一些基本的、非常现实的成员。

现在假设你按如下方式为派生类的成员函数定义模板：

```cpp
template <typename T>
void Derived<T>::derivedFun()
{
    baseFun();
    std::cout << m_base_var << std::endl;
}
```

## 练习

以下练习让你尝试本章学到的内容。如果遇到困难，请回顾本章以寻求帮助。如果之后仍然卡住，你可以从 Apress 网站（www.apress.com/source-code/）下载解决方案，但这确实应该是最后的手段。

- **练习 17-1.** Ex17_01 中的 Array<> 模板在许多方面与 std::vector<> 相似。一个明显的缺点是，Array<> 的大小需要在构造时固定。我们来弥补这一点，并添加一个 push_back() 成员函数，用于在所有现有元素之后插入一个类型为 T 的单个元素。为了保持简单，你的 push_back() 版本可以在每次调用时分配一个新的、更大的数组来容纳 size + 1 个元素。另外，确保一个（空的）Array<> 可以被默认构造。编写一个小程序来练习这个新功能。

  额外要求：让 push_back() 具有强异常安全性应该不难。也就是说，如果 push_back() 期间的任何操作出错并抛出异常，请确保没有内存泄漏，并且原始 Array<> 保持原样，丢弃新元素。

- **练习 17-2.** 为表示可能不同类型的值对的类定义一个模板。这些值可以通过公有的 first 和 second 成员变量访问。然后可以创建并使用一个 int 和一个 std::string 组成的值对，如下所示：

```cpp
auto my_pair = Pair<int, std::string>(122, "abc");
++my_pair.first;
std::cout << "my_pair equals (" << my_pair.first
          << ", " << my_pair.second << ")" << std::endl;
```

虽然通常我们会建议不要使用公有成员变量，但在本练习中我们睁一只眼闭一只眼，因为 std::pair 的标准模板也使用这些相同的公有成员。

还要定义一个默认构造函数，并确保值对可以基于所谓的字典序比较，使用 ==、<、>、<=、>= 等运算符进行比较。也就是说，值对应该使用与排序由两个字母组成的单词时相同的逻辑来排序，只不过现在单词不是由两个字母组成，而是由两个不同的值组成。假设你有以下三个值对：

```cpp
auto pair1 = Pair<int, std::string>(0, "def");
auto pair2 = Pair<int, std::string>(123, "abc");
auto pair3 = Pair<int, std::string>(123, "def");
```

那么表达式 pair1 < pair2 和 pair2 < pair3 都应该求值为 true。第一个是因为 0 < 123；第二个是因为 "abc" < "def"。仅当第一个值使用 == 比较相等时，才会查看 Pair 的第二个值。

编写一个小程序来确保你的 Pair<> 模板符合要求地工作。例如，你可以使用我们在本练习任务中提供的代码片段。

类模板实参推导（CTAD）适用于 Pair<> 模板吗？

- **练习 17-3.** 创建一个 << 运算符模板，将练习 17-2 的 Pair 流式输出到输出流。同时调整测试程序以使用该运算符。

