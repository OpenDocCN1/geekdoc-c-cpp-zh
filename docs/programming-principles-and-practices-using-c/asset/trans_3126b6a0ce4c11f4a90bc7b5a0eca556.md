

现在，终于到了提出“但如果**列表**为空呢？”的时候。换句话说，“如果 `lst.begin()==lst.end()` 该怎么办？”在这种情况下，`*p` 将尝试解引用最后一个元素之后的那个元素（即 `lst.end()`）：这将是一场灾难！或者——情况可能更糟——结果可能是一个随机值，这可能会被误认为是正确答案。

问题的最后一种表述形式强烈暗示了解决方案：我们可以通过比较 `begin()` 和 `end()` 来测试列表是否为空——事实上，我们可以通过比较其起始和结束位置来测试任何 STL 序列是否为空：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_761_0.png)

这就是为什么 `end` 指向最后一个元素之后而非最后一个元素本身这一设计背后更深层次的原因：空序列并不是特殊情况。我们不喜欢特殊情况，因为——根据定义——我们必须记得为它们编写特殊的代码。

在我们的示例中，可以这样使用它：

```cpp
list<int>::iterator p = high(lst.begin(), lst.end());
if (p==lst.end())      // 我们是否到达了末尾？
    cout << "The list is empty";
else
    cout << "the highest value is " << *p << '\n';
```

我们系统地使用与 `end()` 的返回值进行测试——表示“未找到”——来配合 STL 算法。

由于标准库提供了一个列表实现，我们在此不再深入探讨其实现细节。相反，我们将简要看看列表适用于什么场景（如果你对列表实现细节感兴趣，请参见练习 12–14）。

## 20.5 再次泛化 vector

显然，从 §20.3–4 的例子中可以看出，标准库的 `vector` 拥有 `iterator` 成员类型以及 `begin()` 和 `end()` 成员函数（就像 `std::list` 一样）。然而，我们在第 19 章中并没有为我们的 `vector` 提供这些成员。在 §20.3 中介绍的 STL 通用编程风格中，要让不同的容器能够或多或少互换使用，真正需要的是什么？首先，我们将概述解决方案（忽略分配器以简化问题），然后解释它：

```cpp
template<typename T>  // 要求 Element<T>() (§19.3.3)
class vector {
public:
    using size_type = unsigned long;
    using value_type = T;
    using iterator = T*;
    using const_iterator = const T*;
    // ...
    iterator begin();
    const_iterator begin() const;
    iterator end();
    const_iterator end() const;
    size_type size();
    // ...
};
```

**using** 声明为类型创建一个别名；也就是说，对于我们的 **vector**，**iterator** 是我们选择的用作迭代器的类型的同义词，即 **T\***。现在，对于一个名为 **v** 的 **vector**，我们可以写：

```cpp
vector<int>::iterator p = find(v.begin(), v.end(),32);
```

以及

```cpp
for (vector<int>::size_type i = 0; i<v.size(); ++i) cout << v[i] << '\n';
```

关键在于，要写出这些代码，我们实际上并不需要知道 **iterator** 和 **size_type** 所代表的具体类型。特别是，上述代码由于是用 **iterator** 和 **size_type** 来表达的，因此适用于那些 **size_type** 不是 **unsigned long**（在许多嵌入式系统处理器中并非如此）以及 **iterator** 不是简单指针而是类（在许多流行的 C++ 实现中也是如此）的 **vectors**。

标准类似地定义了 **list** 和其他标准容器。例如：

```cpp
template<typename T> // 要求 Element<T>() (§19.3.3)
class list {
public:
    class Link;
    using size_type = unsigned long;
    using value_type = T;
    class iterator; // 参见 §20.4.2
    class const_iterator; // 类似于 iterator，但不允许写入元素
    // ...
    iterator begin();
    const_iterator begin() const;
    iterator end();
    const_iterator end() const;
    size_type size();
    // ...
};
```

这样，我们可以编写不关心使用的是 **list** 还是 **vector** 的代码。所有标准库算法都是用这些成员类型名称（如 **iterator** 和 **size_type**）定义的，因此它们不会不必要地依赖于容器的实现或具体操作的是哪种容器（参见第 21 章）。

作为表示某个容器 **C** 的 **C::iterator** 的替代方案，我们通常更喜欢使用 **Iterator< C >**。这可以通过一个简单的模板别名来实现：

```cpp
template<typename C> using Iterator = typename C::iterator; // Iterator<C> 意味着 typename C::iterator
```

出于语言技术原因，我们需要在 **C::iterator** 前加上 **typename** 以说明 **iterator** 是一个类型，这也是我们偏爱 **Iterator< C >** 的原因之一。类似地，我们定义：

```cpp
template<typename C> using Value_type = typename C::value_type;
```

这样，我们就可以写 **Value_type< C >**。这些类型别名不在标准库中，但你可以在 **std_lib_facilities.h** 中找到它们。

**using** 声明是 C++11 中用于替代并推广 C 和 C++ 中所谓的 **typedef**（A.16）的记法。

### 20.5.1 容器遍历

使用 `size()`，我们可以从 `vectors` 的第一个元素遍历到最后一个元素。例如：

```cpp
void print1(const vector<double>& v)
{
    for (int i = 0; i<v.size(); ++i)
        cout << v[i] << '\n';
}
```

这对列表不起作用，因为 `list` 不提供下标操作。然而，我们可以使用更简单的范围-`for`-循环（S4.6.1）来遍历标准库的 `vector` 和 `list`。例如：

```cpp
void print2(const vector<double>& v, const list<double>& lst)
{
    for (double x : v)
        cout << x << '\n';

    for (double x : lst)
        cout << x << '\n';
}
```

这既适用于标准库容器，也适用于“我们的” `vector` 和 `list`。怎么做到的？“技巧”在于范围-`for`-循环是通过返回指向我们 `vector` 元素第一个及末尾之后位置的迭代器的 `begin()` 和 `end()` 函数来定义的。范围-`for`-循环仅仅是使用迭代器对序列进行循环的“语法糖”。当我们为 `vector` 和 `list` 定义 `begin()` 和 `end()` 时，我们“意外地”提供了范围-`for` 所需要的东西。

### 20.5.2 auto

当我们不得不编写遍历通用结构的循环时，命名迭代器可能真的是一种麻烦。考虑：

```cpp
template<typename T>           // 要求 Element<T>
void user(vector<T>& v, list<T>& lst)
{
    for (vector<T>::iterator p = v.begin(); p!=v.end(); ++p) cout << *p << '\n';

    list<T>::iterator q = find(lst.begin(), lst.end(),T{42});
}
```

最让人烦恼的是，编译器显然已经知道 *list* 的 *iterator* 类型和 *vector* 的 *size_type*。为什么我们要告诉编译器它已经知道的东西呢？这样做只会困扰我们中那些打字辛苦的人，并制造出错的机会。幸运的是，我们不需要这样做：我们可以将变量声明为 *auto*，意思是使用 *iterator* 的类型作为变量的类型：

```cpp
template<typename T>       // 要求 Element<T>()
void user(vector<T>& v, list<T>& lst)
{
    for (auto p = v.begin(); p!=v.end(); ++p) cout << *p << "\n";

    auto q = find(lst.begin(), lst.end(),T{42});
}
```

在这里，**p** 是 *vector<T>::iterator*，**q** 是 *list<T>::iterator*。我们可以几乎在所有包含初始化器的定义中使用 *auto*。例如：

```cpp
auto x = 123;     // x 是一个 int
auto c = 'y';     // c 是一个 char
auto& r = x;      // r 是一个 int&
auto y = r;       // y 是一个 int（引用被隐式解引用）
```

请注意，字符串字面量的类型是 *const char\**，因此对字符串字面量使用 *auto* 可能会导致不愉快的意外：

```cpp
auto s1 = "San Antonio";       // s1 是一个 const char*（意外吗？！）
string s2 = "Fredricksburg";   // s2 是一个 string
```

当我们确切知道想要的类型时，使用 *auto* 往往和直接指定类型一样容易。

使用 *auto* 的常见用途之一是指定范围-**for**-循环中的循环变量。考虑：

```cpp
template<typename C>       // 要求 Container<T>
void print3(const C& cont)
{
    for (const auto& x : cont)
        cout << x << "\n";
}
```

