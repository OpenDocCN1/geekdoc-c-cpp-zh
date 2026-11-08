
由于它保证将元素存储在连续的内存块中，因此适合用于 C 函数及类似的以这种方式接收输入或输出数据的函数。在这里，`vector` 与 C++20 引入的 `span` 配合得很好，因为 span 将指向开头的指针和长度捆绑在一起，这通常是 C API 所期望的。你可以确定并传递元素的地址。与容器的迭代器一样，只要不改变容器的大小或容量，指向其元素的地址就一直有效。

vector 的元素空间会根据需要自动调整、增加或减少。会为即将到来的元素预留空间，这样就不需要为每次插入而调整大小。这种处理方式非常巧妙，即使在最坏情况下，每次插入平均也能以 O(1) 的时间复杂度进行。你可以通过 `capacity()` 确定 vector 当前占用多少空间。如果事先知道 vector 中最终会有多少个元素，请使用 `reserve(size_t)` 请求内存，以避免将来扩容。

你可以在 O(1) 时间内随机访问 vector 的元素——也就是说，以最优的速度。

> **提示：局部性**
>
> 对于 CPU 来说，访问寄存器比访问缓存更好。缓存比主内存好，主内存比硬盘快。计算所需的内存区域越紧凑，计算机就越有可能为其使用快速内存。如果内存主要朝一个方向使用而不是来回使用，那么对局部性甚至更好。通常，使用具有更好局部性的策略进行相同的计算会快很多倍：可能达到 10 倍或 100 倍！
>
> 如果没有采取针对特定分配器的特殊预防措施，vector 的局部性比例如 set 更好。如果你还能按升序使用 vector，那对局部性更好。为此，让迭代器只向前移动，或者只递增索引进行访问。
>
> 如果你希望数据始终保持排序，通常会使用 set。然而，这对内存不利。如果这对你很重要，请查看针对 vector 的 `flat_set` 适配器，它自 C++23 起可用。

你可以将 C++ 类型中几乎任何东西放入 vector。这取决于你将使用的操作以及该类型是否被允许。元素类型必须是可复制或可移动的；标准库将选择合适的操作。但是，必须有 `Elem` 的析构函数，可以是编译器生成的，也可以是你自己编写的——因此你不能将析构函数标记为 `= delete`。

在实践中，建议元素类型是可移动的，并保证在移动时不会抛出异常——也就是说，要么用 `noexcept` 标记移动操作，要么由编译器生成。如果可能，请坚持元素类型的零规则；请参阅第 17 章第 17.1 节作为提醒。

假设本节中以下所有关于 `vector` 的示例都嵌入在清单 24.12 的代码中。

```cpp
// https://godbolt.org/z/WK86eaz1x
#include <vector>
#include <iostream>
using std::vector; using std::cout;

template<typename T>
std::ostream& operator<<(std::ostream& os, const vector<T>& data) {
    for(const auto &e : data) {
        os << e << ' ';
    }
    return os;
}

int main() {
    // Example code here
}
```

**清单 24.12** 这是本节中 vector 示例清单的模板。

> **运算符 “<<”**
>
> 在本章的一些示例中，我使用自定义的 `operator<<` 而不是 `cout << ... << '\n'`。我这样做只是为了演示时简洁。
>
> 不要在一个表达式中混用这两种运算符：`<<` 的运算符优先级低于 `+`，会最后执行。至多在表达式末尾使用它，也许在测试中。

## 初始化

我将举例向你介绍初始化 vector 的各种方法。这些方法大多也适用于其他容器，尤其是顺序容器。在其他地方，我会简要介绍常见的初始化方式，然后重点介绍差异。

你可以使用默认构造函数初始化 vector。

```cpp
// https://godbolt.org/z/7zMp5fo7c
vector<int> dataA;
vector<int> dataB{};
vector<int> dataC = {};    // no assignment
cout << format("{} {} {}\n", dataA.size(), dataB.size(), dataC.size()); // 0 0 0
```

**清单 24.13** 默认构造函数初始化一个空的 vector。

我在这里使用了 C++20 的 `format()`。你也可以复制 vector。在这里你还可以看到，自 C++17 起，编译器会从构造函数参数推导模板参数 `int`。

```cpp
// https://godbolt.org/z/cE6G1aErs
auto count(vector<int> arg) { return arg.size(); }
// …
vector input{1,2,3};              // vector<int>
vector outputA(input);            // copy
vector outputB = input;           // also copy, no assignment
cout << count(input) << '\n';     // call by copy-by-value
```

**清单 24.14** 使用构造函数或隐式复制 vector。

无论是编译器自动执行，还是有意使用 `std::move`，vector 也可以窃取另一个 vector 的数据。借助 `make_move_iterator`，你可以修改任何迭代器，使其对每个单独的元素应用 `std::move`。因此，你不仅可以移动另一个容器的所有元素，还可以移动一个 range 中的元素。

```cpp
// https://godbolt.org/z/f5v5WEe97M
#include <list>
#include <string>
#include <iterator>                         // make_move_iterator
using std::make_move_iterator; using std::string;
vector<int> create() { return vector<int>{8, 9, 10}; }
size_t count(vector<int> d) { return d.size(); }
// …
vector input{1,2,3};
vector outputA(std::move(input));           // move
vector outputB = std::move(input);           // also move, not assignment
vector data = create();                      // Return-Value-Optimization
cout << count(input) << '\n';                // call by Copy-by-Value
// move elements from another container
std::list<string> source{ "a", "a", "a", "BB", "CC", "DD", "b", "b" };
auto from = source.begin();
std::advance(from, 3);  // 3/3 forward, but slow in list
auto to = from;
std::advance(to, 3);    // another 3 forward
vector target(make_move_iterator(from), make_move_iterator(to));
// source is now {"a", "a", "a", "", "", "", "b", "b"}, target is now {"BB", "CC", "DD"}
```

**清单 24.15** 对于返回值，编译器通常也可以进行移动。

由 `make_move_iterator` 创建的 `move_iterator` 确保在 `target` 的逐元素初始化过程中，每个 `a = b` 都变成 `a = std::move(b)`。对于 `string`，这意味着之后 `b` 将包含空字符串。从 source 到 target 移动三个元素不会移动整个元素，而是逐元素地应用移动操作——也就是说，移动的是元素的内容，而不是元素本身。

所有容器都支持使用初始化列表进行初始化，并且自 C++17 起，通常可以为你推断模板参数。但是，请避免将 C 字符串字面量放入初始化列表的陷阱。在这种情况下，请显式编写 `vector<string>` 来强制转换，或者为 string 使用 `"s"` 后缀（甚至为 `string_view` 使用 `"sv"`）。

```cpp
// https://godbolt.org/z/6rG393Wa5
vector<int> primes{ 2,3,5,7,11 };
vector<unsigned> evens{ 2,4,6,8,10 };
vector<int> notLikeThis{ 'a', 4.3, 8L };  // "Narrowing" double not okay
vector<string> names{ "are", "only" };    // converts arguments
vector sound{ "smoke", "fume" };         // dangerous: vector<const char*>
vector wtf{ "rain"s, "water"s };           // vector<string>
vector cold{ "ice"sv, "pole"sv };         // vector<string_view>
```

**清单 24.16** 使用初始化列表预填充 vector。请注意列表中的正确类型。

> ### 窄化转换与初始化列表
>
> *窄化转换*是将数值数据类型 A 隐式转换为另一种类型 B，而 B 无法容纳 A 的整个值范围，例如 int 到 char 或 double 到 int。
>
> 在 *初始化列表* 中，编译器不允许此类转换，以保护你免受典型且难以发现的错误的影响。
>
> 在清单 24.16 中，编译器会抱怨你试图将 double 值 4.3 转换为 int。对于 long 值 8L，它不会抱怨，因为它足够聪明，意识到 int 对此足够。800000000L 对于 32 位 int 是允许的，但除此之外不允许。

所有标准容器在接收到迭代器时，都可以从其他容器复制数据。

```cpp
// https://godbolt.org/z/h8Pze74ME
#include <deque>
#include <ranges>                 // C++20
// ...
std::deque in{1,2,33,34,35,99};
vector thirty(in.begin()+2, in.begin()+5);
for(auto &e : thirty) {
    cout << e << ' ';
}
```

