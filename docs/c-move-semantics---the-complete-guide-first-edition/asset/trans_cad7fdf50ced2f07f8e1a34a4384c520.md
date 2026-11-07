
### 14.3.2 构造函数和成员函数中的移动迭代器

你还可以在算法只需读取一次元素的地方使用移动迭代器。一个有用的场景可能是将源容器中的元素移动到另一个容器（相同类型或不同类型）。例如：

*lib/moveitor.cpp*

```cpp
#include <iostream>
#include <string>
#include <list>
#include <vector>

template<typename T>
void print(const std::string& name, const T& coll)
{
    std::cout << name << " (" << coll.size() << " elems): ";
    for (const auto& elem : coll) {
        std::cout << " \"" << elem << "\"";
    }
    std::cout << "\n";
}

int main()
{
    std::list<std::string> src{"don't", "vote", "for", "liars"};

    // move all elements from the list to the vector:
    std::vector<std::string> vec{std::make_move_iterator(src.begin()),
                                 std::make_move_iterator(src.end())};

    print("src", src);
    print("vec", vec);
}
```

程序有以下输出（? 表示我们不知道其值）：

```text
src (4 elems): "?" "?" "?" "?"
vec (4 elems): "don't" "vote" "for" "liars"
```

再次注意，源容器中的元素数量没有改变。我们将所有元素移动到了初始化后的新容器中。因此，之后源范围中的元素处于被移动后的状态，我们不知道它们的值。

### 14.4 小结

- C++ 标准库提供了用于移动多个元素的特殊算法，称为 `std::move()`（与用于将单个对象标记为可移动的 `std::move()` 同名）和 `std::move_backward()`。它们会使元素处于被移动后的状态。
- 移除算法可能会使元素处于被移动后的状态。
- 移动迭代器允许我们在遍历元素时使用移动语义。你可以在算法或其他地方（例如使用范围来初始化/设置值的构造函数）使用这些迭代器。但是，请确保这些迭代器对每个元素只使用一次。

## 第15章：C++ 标准库类型中的移动语义

本章讨论移动语义在 C++ 标准库中最重要或最显著的应用。

这可能有助于你更好地理解字符串和容器等基本类型，并让你对移动语义的棘手用法有所了解。

### 15.1 字符串的移动语义

字符串是可能需要分配内存来保存其值的对象。因此，你可以从对它们使用移动语义中获益。

本书中已经有好几个关于字符串如何支持移动语义的示例：

- 将字符串移动到 vector 中
- 为字符串实现移动构造函数
- 初始化字符串成员
- 在循环中读取字符串并在 move() 之后使用它们

在本节中，我们将更详细地介绍移动语义对 string 的影响。

### 15.1.1 字符串赋值与容量

字符串的容量（当前可用于保存值的内存）通常不会缩小。只有移动操作、swap() 或 shrink_to_fit() 可能会缩小容量。

考虑以下示例：

*lib/stringmoveassign.cpp*

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string s0;
    std::string s1{"short"};
    std::string s2{"a string with an extraordinarily long value"};
    std::cout << " s0 capa: " << s0.capacity() << " ('" << s0 << ")\n";
    std::cout << " s1 capa: " << s1.capacity() << " ('" << s1 << ")\n";
    std::cout << " s2 capa: " << s2.capacity() << " ('" << s2 << ")\n";

    std::string s3{std::move(s1)};
    std::string s4{std::move(s2)};
    std::cout << " s1 capa: " << s1.capacity() << " ('" << s1 << ")\n";
    std::cout << " s2 capa: " << s2.capacity() << " ('" << s2 << ")\n";
    std::cout << " s3 capa: " << s3.capacity() << " ('" << s3 << ")\n";
    std::cout << " s4 capa: " << s4.capacity() << " ('" << s4 << ")\n";

    std::string s5{"quite a reasonable value"};
    std::cout << " s4 capa: " << s4.capacity() << " ('" << s4 << ")\n";
    std::cout << " s5 capa: " << s5.capacity() << " ('" << s5 << ")\n";

    s4 = std::move(s5);
    std::cout << " s4 capa: " << s4.capacity() << " ('" << s4 << ")\n";
    std::cout << " s5 capa: " << s5.capacity() << " ('" << s5 << ")\n";
}
```

在这个程序中，你首先可以看到，由于*小字符串优化（SSO）*，通常空字符串也有一定字符的容量，这种优化通常会在字符串自身中为值预留 15 或 22 字节。超过 SSO 的大小后，字符串会在堆上分配内存，其大小至少足以存储该值。因此，在以下代码之后

```cpp
std::string s0{};
std::string s1{"short"};
std::string s2{"a string with an extraordinarily long value"};
```

我们可能会得到类似以下输出之一：

- 平台 A：
  - `s0 capa: 15 ('')`
  - `s1 capa: 15 ('short')`
  - `s2 capa: 43 ('a string with an extraordinarily long value')`

- 平台 B：
  - `s0 capa: 22 ('')`
  - `s1 capa: 22 ('short')`
  - `s2 capa: 47 ('a string with an extraordinarily long value')`

### 15.2 容器的移动语义

容器通常是必须分配内存来保存其元素的对象。因此，你可以从对它们使用移动语义中获益。然而，有一个例外：`std::array<>` 不在堆上分配内存，这意味着对 `std::array<>` 适用特殊规则。

本书中已经有好几个关于容器如何支持移动语义的示例。在引出移动语义的初始示例中，我们看到了以下对移动语义的支持：

- 通过重载 `push_back()`，C++ 标准支持插入新元素时的移动语义。
- 通过提供移动构造函数和移动赋值运算符，容器使复制临时对象（例如返回值）变得廉价。

这是典型情况。所有容器在执行以下操作时都支持移动语义：

- 复制容器
- 赋值容器
- 向容器中插入元素

然而，还有更多内容要说。

### 15.2.1 容器整体的基本移动支持

所有容器都定义了移动构造函数和移动赋值运算符，以支持对未命名临时对象和用 `std::move()` 标记的对象的移动语义。

例如，类 `std::list<>` 的声明如下：

```cpp
template<typename T, typename Allocator = allocator<T>>
class list {
public:
    ...
    list(const list&);                         // copy constructor
    list(list&&);                              // move constructor
    list& operator=(const list&);              // copy assignment
    list& operator=(list&&) noexcept(...);     // move assignment
    ...
};
```

这使得按值返回/传递容器以及赋值返回值变得廉价。例如：

```cpp
std::list<std::string> createAndInsert()
{
    std::list<std::string> coll;
    ...
    return coll;          // move constructor if not optimized away
}

std::list<std::string> v;
...
v = createAndInsert();  // move assignment
```

但是，请注意，对于除 std::array<> 之外的所有容器，其移动构造函数和移动赋值运算符还有额外要求和保证。这些要求和保证本质上意味着，被移动后的容器通常是空的。

### 移动构造函数的容器保证

对于移动构造函数：

```cpp
ContainerType cont1{...};
ContainerType cont2{std::move(cont1)};   // move the container
```

C++ 标准规定了常数复杂度。这意味着移动的持续时间不依赖于元素数量。

有了这一保证，实现者别无选择，只能将元素的整个内存从源对象 cont1 “窃取”到目标对象 cont2，使源对象 cont1 处于初始/空状态。

你可能会争辩说，移动构造函数也可以在源对象中创建一个新值，但这没有多大意义，因为它只会使操作更慢。

对于 vector，在被移动后的对象中提供值甚至是被间接禁止的，因为 std::vector<> 的移动构造函数保证不抛出异常：

```cpp
template<typename T, typename Allocator = allocator<T>>
class vector {
public:
  ...
  vector(const vector&);        // copy constructor
  vector(vector&&) noexcept;    // move constructor
  ...
};
```

总之，实际上，对于在移动构造函数中用作源的容器，在使用后我们有以下保证：

- 对于 vector，本质上要求被移动后的容器为空。
- 对于其他容器（std::array<> 除外），并不严格要求为空，但通常实现其他状态没有意义。

### 移动赋值运算符的容器保证

对于移动赋值运算符：

```cpp
ContainerType cont1{...}, cont2{...};
cont2 = std::move(cont1);          // move assign the container
```

C++ 标准保证该操作要么覆盖、要么销毁目标对象 cont2 的每个元素。这保证目标容器 cont2 的元素在进入时拥有的所有资源都会被释放。因此，实现移动赋值只有两种方式：

- 销毁旧元素，并将源的全部内容移动到目标（即，将指向内存的指针从源移动到目标）。
