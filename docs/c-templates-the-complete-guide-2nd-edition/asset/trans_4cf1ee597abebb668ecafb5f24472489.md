

```cpp
};
};

int main()
{
    S s;
    Wrapper<S> w(s);
    foo(w); // OK: Wrapper<S> is a class associated with w
    foo(s); // ERROR: Wrapper<S> is not associated with s
}
```

这里，调用 `foo(w)` 是有效的，因为函数 `foo()` 是在 `Wrapper<S>` 中声明的友元，而 `Wrapper<S>` 是与参数 `w` 关联的类。² 然而，在调用 `foo(s)` 时，函数 `foo(Wrapper<S> const&)` 的友元声明不可见，因为它所定义的类 `Wrapper<S>` 并未与参数 `s` 的类型 `S` 关联。因此，即使存在从类型 `S` 到类型 `Wrapper<S>` 的有效隐式转换（通过 `Wrapper<S>` 的构造函数），这种转换也永远不会被考虑，因为候选函数 `foo()` 首先就未被找到。在 Barton 和 Nackman 发明该技巧时，友元名称注入会使友元 `foo()` 可见，并且调用 `foo(s)` 将会成功。

在现代 C++ 中，将友元函数定义在类模板中相对于简单地定义一个普通函数模板的唯一优势是语法上的：友元函数定义可以访问其封闭类的私有和受保护成员，并且不需要重述封闭类模板的所有模板参数。然而，当友元函数定义与奇异递归模板模式（CRTP）结合使用时，它会很有用，正如以下小节中描述的操作符实现所展示的那样。

## 21.2.2 操作符实现

在实现提供重载操作符的类时，通常会为多个不同但相关的操作符提供重载。例如，实现相等操作符（`==`）的类很可能会同时实现不等操作符（`!=`），而实现小于操作符（`<`）的类很可能会同时实现其他关系操作符（`>`、`<=`、`>=`）。在许多情况下，这些操作符中只有一个的定义是真正有趣的，而其他操作符可以简单地基于该操作符定义。例如，类 `X` 的不等操作符很可能基于相等操作符定义：

```cpp
bool operator!= (X const& x1, X const& x2)
{
    return !(x1 == x2);
}
```

鉴于存在大量具有相似 `!=` 定义的类型，很容易将其泛化为模板：

```cpp
template<typename T>
bool operator!= (T const& x1, T const& x2)
{
    return !(x1 == x2);
}
```

事实上，C++ 标准库在 `<utility>` 头文件中包含类似的定义。然而，在标准化过程中，这些定义（针对 `!=`、`>`、 `<=` 和 `>=`）被 relegated 到命名空间 `std::rel_ops`，当时确定如果在命名空间 `std` 中提供它们会造成问题。确实，使这些定义可见会让人觉得任何类型都有一个 `!=` 操作符（可能无法实例化），并且该操作符对它的两个参数都是精确匹配。虽然第一个问题可以通过使用 SFINAE 技术来克服（参见第 19.4 节第 416 页），使得此 `!=` 定义仅对具有合适的 `==` 操作符的类型实例化，但第二个问题仍然存在：上面的通用 `!=` 定义将被优先于需要例如派生到基类转换的用户提供的定义，这可能会让人感到意外。

基于 CRTP 的这些操作符模板的替代表述允许类选择加入通用操作符定义，在提供代码复用增加收益的同时避免了过于通用操作符的副作用：

`inherit/equalitycomparable.cpp`

```cpp
template<typename Derived>
class EqualityComparable
{
public:
    friend bool operator!= (Derived const& x1, Derived const& x2)
    {
        return !(x1 == x2);
    }
};

class X : public EqualityComparable<X>
{
public:
    friend bool operator== (X const& x1, X const& x2)
    {
        // implement logic for comparing two objects of type X
    }
};

int main()
{
    X x1, x2;
    if (x1 != x2) { }
}
```

这里，我们将 CRTP 与 Barton-Nackman 技巧结合起来。`EqualityComparable<>` 使用 CRTP 为其派生类基于派生类的 `operator==` 定义提供操作符 `!=`。它实际上通过友元函数定义提供了该定义（Barton-Nackman 技巧），这使得 `operator!=` 的两个参数对转换具有相同的行为。

当将行为分解到基类中同时保留最终派生类的身份时，CRTP 会很有用。结合 Barton-Nackman 技巧，CRTP 可以基于少数规范操作符为许多操作符提供通用定义。这些特性使得结合 Barton-Nackman 技巧的 CRTP 成为 C++ 模板库作者喜爱的技巧。

## 21.2.3 外观

使用 CRTP 和 Barton-Nackman 技巧来定义某些操作符是一个方便的捷径。我们可以进一步扩展这个想法，使得 CRTP 基类根据 CRTP 派生类公开的更小（但更容易实现）的接口来定义类的绝大部分或全部公共接口。这种模式称为 *外观* 模式，在定义需要满足某些现有接口要求的新类型时特别有用——数值类型、迭代器、容器等等。

为了说明外观模式，我们将实现迭代器的外观，这极大地简化了编写符合标准库要求的迭代器的过程。迭代器类型（特别是 *随机访问迭代器*）所需的接口相当庞大。以下类模板 `IteratorFacade` 的骨架展示了迭代器接口的要求：

`inherit/iteratorfacadeskel.hpp`

```cpp
template<typename Derived, typename Value, typename Category,
         typename Reference = Value&, typename Distance = std::ptrdiff_t>
class IteratorFacade
{
public:
    using value_type = typename std::remove_const<Value>::type;
    using reference = Reference;
    using pointer = Value*;
    using difference_type = Distance;
    using iterator_category = Category;

    // input iterator interface:
    reference operator*() const { ... }
    pointer operator->() const { ... }
    Derived& operator++() { ... }
    Derived operator++(int) { ... }
    friend bool operator==(IteratorFacade const& lhs,
                           IteratorFacade const& rhs) { ... }
    ...
    // bidirectional iterator interface:
    Derived& operator--() { ... }
    Derived operator--(int) { ... }

    // random access iterator interface:
    reference operator[](difference_type n) const { ... }
    Derived& operator+=(difference_type n) { ... }
    ...
    friend difference_type operator-(IteratorFacade const& lhs,
                                     IteratorFacade const& rhs) { ... }
    friend bool operator<(IteratorFacade const& lhs,
                          IteratorFacade const& rhs) { ... }
    ...
};
```

为简洁起见我们省略了一些声明，但即使为每个新迭代器实现列出的每一个也是一项繁重的工作。幸运的是，该接口可以提炼为几个核心操作：

- 对于所有迭代器：
  - `dereference()`: 访问迭代器所引用的值（通常通过操作符 `*` 和 `->` 使用）。
  - `increment()`: 将迭代器移动到序列中的下一项。
  - `equals()`: 确定两个迭代器是否引用序列中的同一项。
- 对于双向迭代器：
  - `decrement()`: 将迭代器移动到列表中的前一项。
- 对于随机访问迭代器：
  - `advance()`: 将迭代器向前（或向后）移动 *n* 步。
  - `measureDistance()`: 确定从序列中的一个迭代器到另一个迭代器的步数。

外观的作用是将仅实现这些核心操作的类型的适配为提供完整迭代器接口。`IteratorFacade` 的实现主要涉及将迭代器语法映射到最小接口。在以下示例中，我们使用成员函数 `asDerived()` 来访问 CRTP 派生类：

```cpp
Derived& asDerived()
{
    return *static_cast<Derived*>(this);
}
Derived const& asDerived() const
{
    return *static_cast<Derived const*>(this);
}
```

给定该定义，外观的大部分实现是直接的。³ 我们仅说明了一些输入迭代器要求的定义；其他定义类似：

```cpp
reference operator*() const
{
    return asDerived().dereference();
}

Derived& operator++()
{
    asDerived().increment();
    return asDerived();
}

Derived operator++(int)
{
    Derived result(asDerived());
    asDerived().increment();
    return result;
}

friend bool operator==(IteratorFacade const& lhs,
                       IteratorFacade const& rhs)
{
    return lhs.asDerived().equals(rhs.asDerived());
}
```

### 定义一个链表迭代器

有了 `IteratorFacade` 的定义，我们现在可以轻松地为一个简单的链表类定义一个迭代器。例如，假设我们将链表中的节点定义如下：

`inherit/listnode.hpp`

```cpp
template<typename T>
```
