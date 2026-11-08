
你已经在复合要求的 -> 箭头之后遇到过类型约束，因此，形如 concept<args...> T 的模板参数等价于常规类型参数 typename T，并将约束 concept<T, args...> 添加到模板的 requires 子句中，这应该不会令人意外。对于诸如 std::totally_ordered<> 这样的一元概念，空尖括号 <> 通常会在类型约束中省略。

> **提示** 对具有单个约束的类型参数使用简写记法。这会使模板头部更紧凑、更易读。如果要求由多个约束的合取组成，有时你也可以以清晰且有意义的方式将其中一个合取项提升为类型约束（稍后 §21.4 有一个示例），但并非总是如此——有时将所有约束都归组在 requires 子句中反而更清晰。

对于带多个参数的概念，当然也可以使用简写记法。能很好地运用这种记法的概念包括 std::convertible_to<> 和 std::derived_from<>（二者都来自 <concepts> 模块）。不过，如果一个约束跨多个模板参数，那么简写记法可以说并不总是那么优雅，如下例所示。

```cpp
template <typename T1, std::totally_ordered_with<T1> T2>
auto& larger(const T1& a, const T2& b) { return a > b ? a : b; }
```

### 受约束的函数模板

作为约束函数模板的进一步练习，我们现在回顾第 20 章中用作示例的基于迭代器的 find_optimum<>() 模板。它的定义如下：

```cpp
template <typename Iterator, typename Comparison>
Iterator find_optimum(Iterator begin, Iterator end, Comparison compare)
{
  if (begin == end) return end;

  Iterator optimum{ begin };
  for (Iterator iter{ ++begin }; iter != end; ++iter)
  {
    if (compare(*iter, *optimum)) optimum = iter;
  }
  return optimum;
}
```

一如既往，第一步是为该模板的两个参数确立最低要求。我们邀请你花一点时间思考一下……

即使对于这样一个简单的模板，也已经有不少要求。显然，Iterator 类型的值应该是某种迭代器。更具体地说，它们应支持前缀递增（++）、相等比较（== 和 !=）、解引用（使用一元 * 运算符），以及复制构造和赋值（用于初始化和更新 optimum）。接下来，Comparison 类型的值应是接受两个值的一等函数。不过，它们的函数参数不是 Iterator 类型，而是这些迭代器所指向的任意元素类型（即 *iter 和 *optimum 的类型）。

一旦要求明确，就应尝试将它们映射到已有的概念上。既然我们处理的是迭代器，<iterator> 模块显然是开始查找的合适位置。你能为我们的模板找到合适的概念吗？（为此你需要一本标准库参考手册。）

因为 find_optimum(Iterator) 会从 *iter 和 *optimum 读取，所以 Iterator 至少必须建模 std::input_iterator。但仅此还不够，原因有几点。首先，input_iterator 不要求迭代器可用 == 或 != 进行比较，也不要求它们可复制。其次，输入迭代器允许是单遍迭代器。使用单遍迭代器时，你只能遍历（隐含的）元素序列一次，并且只有在尚未推进迭代器时才能访问当前元素。在我们的例子中，如果 Iterator 迭代器是（可复制的）单遍迭代器，那么就无法保证在递增 iter 之后仍能解引用 optimum。此时范围及其元素可能已经消失。受约束迭代器在 input_iterator 之后的细化级别是 forward_iterator。该概念增加了相等可比较性、可复制性和多遍保证，因此非常适合用来约束我们的 Iterator 参数。（所有双向迭代器、随机访问迭代器和连续迭代器也都是前向迭代器。）

用来约束 Comparison 的最合适概念稍难找到：它是 std::indirect_strict_weak_order。因此，我们模板的完整声明如下：

```cpp
template <std::forward_iterator Iterator,
          std::indirect_strict_weak_order<Iterator> Comparison>
Iterator find_optimum(Iterator begin, Iterator end, Comparison compare);
```

在 indirect_strict_weak_order 中，strict 指的是对于相等元素，Comparison 关系应求值为 false（例如，< 和 > 是严格关系，<= 和 >= 则不是）；weak 表示该关系介于偏序和强序之间；而 indirect 如前所述，表示 Comparison 函数比较的不是 Iterator 值，而是这些迭代器所指向的值。你同样可以用 <concepts> 模块中的直接 strict_weak_order 概念来写这个约束，但那样就必须先用 <iterator> 模块中的 iter_value_t<> 或 iter_reference_t<> 自己转换 Iterator 类型。可以这样做：

```cpp
template <std::forward_iterator Iterator,
          std::strict_weak_order<std::iter_reference_t<Iterator>> Comparison>
Iterator find_optimum(Iterator begin, Iterator end, Comparison compare);
```

> **注意** 对于函数模板，你还可以添加所谓的尾随 requires 子句，即出现在函数参数列表之后的 requires 子句。你甚至可以将尾随 requires 子句与常规 requires 子句和/或使用简写记法指定的约束组合起来。因此，下面这些都是 find_optimum() 函数模板的等价声明。

```cpp
// All constraints moved to a trailing requires clause
template <typename Iter, typename Comp>
Iter find_optimum(Iter begin, Iter end, Comp compare)
    requires std::forward_iterator<Iter>, std::indirect_strict_weak_order<Comp, Iter>;

// Combination of regular and trailing requires clauses
template <typename Iter, typename Comp> requires std::forward_iterator<Iter>
Iter find_optimum(Iter begin, Iter end, Comp compare)
    requires std::indirect_strict_weak_order<Comp, Iter>;

// A trailing requires clause constraining an abbreviated template’s parameter type
template <std::forward_iterator Iter>
Iter find_optimum(Iter begin, Iter end, auto compare)
    requires std::indirect_strict_weak_order<decltype(compare), Iter>;
```

### 受约束的类模板

约束类模板与约束函数模板完全类似。而且，由于大多数类模板——即使是最基础的类模板——也不能对任意类型实例化，因此最好也约束大多数类模板参数。

在第 17 章中，我们开发了一个简单的 Array<> 模板。你可能还记得，在开发过程中，我们实际上已经提到了其类型参数的大多数要求。现在只需将这些要求转换为约束，最好转换为概念表达式。下面是这样一种受约束 Array<> 模板的概要：

```cpp
template <typename T> requires std::default_initializable<T> && std::destructible<T>
class Array
{
public:
  explicit Array(size_t size);
  ~Array();
  // ...
};
```

要使用 operator new[] 创建 T 类型的动态数组，该类型必须可默认初始化。这就排除了没有可访问默认构造函数的类型，以及引用类型和 void 之类的类型。为了以后能够再次 delete[] 这个数组，该类型的析构函数也必须是 public 且未被删除的。（如前所述，std::destructible<> 还要求该析构函数为 noexcept，而这绝对是我们所乐见的。）

下面是 Array<> 的成员模板，它们各自依赖这些约束之一：

```cpp
template <typename T> requires std::default_initializable<T> && std::destructible<T>
Array<T>::Array(size_t size) : m_elements{new T[size]}, m_size{size}
{}
```

```cpp
template <typename T> requires std::default_initializable<T> && std::destructible<T>
Array<T>::~Array() { delete[] m_elements; }
```

这里要注意的主要一点是，你必须在成员模板的定义中重复受约束类模板的 requires 子句（尽管至少有一个主流编译器允许省略这一点，但 C++ 标准要求重复整个模板头）。

