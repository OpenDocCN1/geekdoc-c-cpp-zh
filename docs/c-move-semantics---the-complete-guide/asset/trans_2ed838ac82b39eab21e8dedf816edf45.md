

## 14.3.2 构造函数和成员函数中的移动迭代器

你也可以在任何只读取一次元素的算法中使用移动迭代器。一个有用的场景可能是将源容器的元素移动到另一个容器（相同或不同类型）。例如：

```cpp
#include <iostream>
#include <string>
#include <list>
#include <vector>

template <typename T>
void print(const std::string& name, const T& coll)
{
    std::cout << name << " (" << coll.size() << " elems): ";
    for (const auto& elem : coll) {
        std::cout << "\"" << elem << "\" ";
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

该程序的输出如下：( ? 表示我们不知道该值)：

```
src (4 elems): "?" "?" "?" "?"
vec (4 elems): "don't" "vote" "for" "liars"
```

请注意，源容器中的元素数量没有改变。我们将所有元素移动到了初始化的新容器中。因此，源范围中的元素在之后处于已移动-from 状态，我们不知道它们的值。

## 14.4 总结

- C++ 标准库提供了特殊的算法来移动多个元素，称为 `std::move()`（与标记单个对象可移动的 `std::move()` 名称相同）和 `std::move_backward()`。它们会使元素处于已移动-from 状态。
- 删除算法可能会使元素处于已移动-from 状态。
- 移动迭代器允许我们在迭代元素时使用移动语义。你可以在算法或其他使用范围来初始化/设置值的地方使用这些迭代器，例如构造函数。但是，确保迭代器只使用每个元素一次。

## 第 15 章

## C++ 标准库类型中的移动语义

本章讨论了 C++ 标准库中移动语义最重要的或最显著的应用。

这可以帮助你更好地理解字符串和容器等基本类型，并让你对移动语义的棘手用法有所了解。

## 15.1 字符串的移动语义

字符串是可能为其值分配内存的对象。因此，你可以从为它们使用移动语义中受益。

我们已经在书中多次看到字符串如何支持移动语义的例子：

- 将字符串移动到 vector 中
- 为字符串实现移动构造函数
- 初始化字符串成员
- 在循环中读取字符串并在 move() 之后使用它们

在本节中，我们将更详细地介绍移动语义对字符串的影响。

### 15.1.1 字符串赋值和容量

字符串的容量（当前为值可用的内存）通常不会缩小。只有移动操作、`swap()` 或 `shrink_to_fit()` 可能会缩小容量。

考虑以下示例：

`lib/stringmoveassign.cpp`

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string s0;
    std::string s1{"short"};
    std::string s2{"a string with an extraordinarily long value"};
    std::cout << "- s0 capa: " << s0.capacity() << " ('" << s0 << "')\n";
    std::cout << "  s1 capa: " << s1.capacity() << " ('" << s1 << "')\n";
    std::cout << "  s2 capa: " << s2.capacity() << " ('" << s2 << "')\n";

    std::string s3{std::move(s1)};
    std::string s4{std::move(s2)};
    std::cout << "- s1 capa: " << s1.capacity() << " ('" << s1 << "')\n";
    std::cout << "  s2 capa: " << s2.capacity() << " ('" << s2 << "')\n";
    std::cout << "  s3 capa: " << s3.capacity() << " ('" << s3 << "')\n";
    std::cout << "  s4 capa: " << s4.capacity() << " ('" << s4 << "')\n";

    std::string s5{"quite a reasonable value"};
    std::cout << "- s4 capa: " << s4.capacity() << " ('" << s4 << "')\n";
    std::cout << "  s5 capa: " << s5.capacity() << " ('" << s5 << "')\n";

    s4 = std::move(s5);
    std::cout << "- s4 capa: " << s4.capacity() << " ('" << s4 << "')\n";
    std::cout << "  s5 capa: " << s5.capacity() << " ('" << s5 << "')\n";
}
```

在此程序中，你首先可以看到通常即使是空字符串也由于小字符串优化（SSO）而具有一些字符的容量，该优化通常为字符串本身保留 15 或 22 字节的值。超出 SSO 大小后，字符串会在堆上分配内存，其大小至少足以存储值。因此，在执行

```cpp
std::string s0;
std::string s1{"short"};
std::string s2{"a string with an extraordinarily long value"};
```

之后，我们可能会得到以下输出之一：

| 平台 | `s0` | `s1` | `s2` |
|----------|------|------|------|
| A | `capa: 15 ('')` | `capa: 15 ('short')` | `capa: 43 ('a string with an extraordinarily long value')` |
| B | `capa: 22 ('')` | `capa: 22 ('short')` | `capa: 47 ('a string with an extraordinarily long value')` |

这里，两个平台似乎都支持 SSO（最多 15 或 22 个字符），第二个平台在只需要 43 个字符的内存时分配了 47 个字符的内存。

在所有平台上，已移动-from 的字符串通常为空。这即使在值未存储在外部分配的内存中（因此我们必须复制所有字符）时也适用。在执行：

```cpp
std::string s3{std::move(s1)};
std::string s4{std::move(s2)};
```

之后，我们通常会得到类似以下的结果：

| 变量 | 平台 A | 平台 B |
|----------|------------|------------|
| `s1` | `capa: 15 ('')` | `capa: 22 ('')` |
| `s2` | `capa: 15 ('')` | `capa: 22 ('')` |
| `s3` | `capa: 15 ('short')` | `capa: 22 ('short')` |
| `s4` | `capa: 43 ('a string with an extraordinarily long value')` | `capa: 47 ('a string with an extraordinarily long value')` |

然而，请注意，没有保证 `s1` 会变为空。如同通常情况，C++ 标准库只保证已移动-from 的字符串处于有效但未指定的状态，这意味着 `s1` 仍可能具有值 `"short"` 或甚至任何其他值。

移动赋值不同的字符串值可能会缩小容量。示例程序的最后两个步骤本质上执行了：

```cpp
std::string s4{"a string with an extraordinarily long value"};
std::string s5{"quite a reasonable value"};
s4 = std::move(s5);
```

在实践中你可以找到以下输出：

| 平台行为 | 状态 | `s4` | `s5` |
|---|---|---|---|
| 交换内存 | 移动前 | `capa: 43 ('a string with an extraordinarily long value')` | `capa: 24 ('quite a reasonable value')` |
| 交换内存 | 移动后 | `capa: 24 ('quite a reasonable value')` | `capa: 43 ('')` |
| 移动内存（在释放旧内存之后） | 移动前 | `capa: 47 ('a string with an extraordinarily long value')` | `capa: 31 ('quite a reasonable value')` |
| 移动内存（在释放旧内存之后） | 移动后 | `capa: 31 ('quite a reasonable value')` | `capa: 22 ('')` |

正如你所见，`s4` 的容量通常会缩小，有时缩小到源的容量，有时缩小到空字符串的最小容量。然而，两者都不是有保证的。

## 15.2 容器的移动语义

容器通常是必须分配内存来保存其元素的对象。因此，你可以从为它们使用移动语义中受益。但是有一个例外：`std::array<>` 不会在堆上分配内存，这意味着对于 `std::array<>` 特殊规则适用。

我们已经在书中多次看到容器如何支持移动语义的例子。在最初激发移动语义的示例中，我们看到了以下对移动语义的支持：

- 通过重载 `push_back()`，C++ 标准支持为插入新元素使用移动语义。
- 通过提供移动构造函数和移动赋值运算符，容器使复制临时对象（例如返回值）变得廉价。

这是典型的。所有容器在执行以下操作时都支持移动语义：

- 复制容器
- 赋值容器
- 向容器中插入元素

然而，还有更多内容。

### 15.2.1 容器整体的基础移动支持

所有容器都定义了移动构造函数和移动赋值运算符，以支持对未命名临时对象和用 `std::move()` 标记的对象的移动语义。

例如，类 `std::list<>` 声明如下：

```cpp
template<typename T, typename Allocator = allocator<T>>
class list {
public:
    ...
    list(const list&);                // copy constructor
    list(list&&);                     // move constructor
    list& operator=(const list&);     // copy assignment
    list& operator=(list&&) noexcept(...);  // move assignment
    ...
};
```

这使得按值返回/传递容器以及为返回值赋值变得廉价。例如：

```cpp
std::list<std::string> createAndInsert()
{
    std::list<std::string> coll;
    ...
    return coll;    // move constructor if not optimized away
}

std::list<std::string> v;
...
v = createAndInsert();  // move assignment
```

