

```cpp
using boost::core::demangled_name;
cout<<demangled_name(BOOST_CORE_TYPEID(i))<<'\n'; // Output: int
cout<<demangled_name(BOOST_CORE_TYPEID(f))<<'\n'; // Output: float
cout<<demangled_name(BOOST_CORE_TYPEID(double))<<'\n'; // Output: double
std::string s;
cout<<demangled_name(BOOST_CORE_TYPEID(s.begin()))<<'\n'; // Output: gnu cxx::normal_iterator<char*, std::cxx::basic_string<char>*>
cout<<demangled_name(BOOST_CORE_TYPEID(name))<<'\n'; // Output: std::map<int, std::string, std::less<int>>
std::allocator<std::pair<int, const, std::string>> alloc;
cout<<demangled_name(BOOST_CORE_TYPEID(666))<<'\n'; // Output: int
```

**Listing 28.42** Boost 的 “demangled_name” 对于输出类型名称非常有用。

## 28.7 泛函数对象的辅助类："<functional>"

`<functional>` 中的函数比 `<numeric>` 更多，它们的作用是为了补充标准库的其他部分。你很少会单独包含 `<functional>`。如果你想用 `<algorithm>` 或容器来解决一个“简单”任务，值得看一眼 `<functional>`，那里可能已经有了解决方案。

例如，如果你想对容器中的所有元素求和，可以使用来自 `<numeric>` 的 `accumulate`。但如果你想用 `*` 代替 `+`，你可以：

- 或者写一个 lambda 表达式 `[](auto a, auto b) { return a*b };`
- 或者使用 `<functional>` 中的 `multiplies`，它们的功能正是此的。

`<functional>` 中的许多其他内容也是如此。

我将 `<functional>` 提供的内容（或或少任意地）分类为以下几个领域：

- 函数 `function` 是 C++ 中所有可调用对象的中心点。`bind` 从函数对象创建一个参数少一个参数的新函数对象。`mem_fn` 从方法创建一个函数对象。在此上下文中，还有几个辅助构造结构。

- 用于算术运算（如 `multiplies`）、比较（如 `equal_to`）、逻辑运算（如 `logical_and` 等）和位运算（如 `bit_and` 等）的具体函数对象，你可以用它们代替简单的 lambda。

- 特殊的哈希函数：无序容器（unordered containers）所需的哈希对象在这里为内置类型定义。例如，你会发现模板特化 `hash<int>` 及其所有相关类。这应该是不言自明的，因此我不再详细阐述。

在第 25 章 Listing 25.15 中，有一个 `multiplies` 配合 `<numeric>` 中的 `accumulate` 使用的示例。其他定义的函数对象可以在表 28.11 到表 28.14 中找到。

| 泛函数 | 行为 | 泛函数 | 行为 |
| --- | --- | --- | --- |
| plus | a + b | divides | a / b |
| minus | a - b | modulus | a % b |
| multiplies | a * b | negate | -a |

**Table 28.11** 算术运算符的函数对象。

| 泛函数 | 行为 | 泛函数 | 行为 |
| --- | --- | --- | --- |
| equal_to | a == b | less | a < b |
| not_equal_to | a != b | greater_equal | a >= b |
| greater | a > b | less_equal | a <= b |

**Table 28.12** 比较运算符的函数对象。

| 泛函数 | 行为 | 泛函数 | 行为 |
|---|---|---|---|
| logical_and | a && b | logical_not | !b |
| logical_or | a || b | | | |

**Table 28.13** 逻辑运算符的函数对象。

| 泛函数 | 行为 | 泛函数 | 行为 |
|---|---|------|
| bit_and | a & b | bit_xor | a ^ b |
| bit_or | a \| b | bit_not | ~b |

**Table 28.14** 位运算符的函数对象。

你可以使用这些函数对象为容器和算法配备你自己的功能。

例如，在 `std::set` 的定义中，你会看到 `<functional>` 中的 `less` 被此处比较操作。

```cpp
namespace std {
    template<class Key, class Compare=less<Key>, class Allocator=allocator<Key>>
        class set;
    //...
}
```

因此，你不需要为自己的数据类型重载 `operator<`，也可以为你的数据类型对 `less` 模板进行特化，类似于你在 `unordered_set` 上下文中对 `hash` 所做的那样：

```cpp
// https://godbolt.org/z/Y3GsPd9d7
#include <set>
#include <string>

struct Dragon {
    std::string name;
};
namespace std {
    template<> struct less<Dragon> { // 模板特化
        bool operator()(const Dragon &lhs, const Dragon &rhs) const {
            return lhs.name < rhs.name;
        }
    }};
}
int main() {
    std::set<Dragon> dragons {
        Dragon("Smaug"), Dragon("Glaurung"),
        Dragon("Ancalagon"), Dragon("Scatha")
    };
}
```

所以，如果由于某种原因无法或不想为 `Dragon` 重载 `operator<`，且你不想指定模板参数 `Compare`，你也可以通过特化 `less` 来实现相同的功能。

在 Listing 28.43 中，你看到了第 8 章 Listing 8.18 中计算器的版本，它从头到尾使用了 `<functional>`。这次没有使用大型的 `switch` 语句，而是所有可能的字符存储为 map 中的键。取决于如何操作栈，操作最终进入四个 map 之一：

- binOps: 从栈弹出两个元素，对它们应用函数，并将结果存回栈中。加法就是此类示例。
- unOps: 从栈弹出一个元素，对其应用函数，并将结果存回栈中。此计算器没有此类操作。
- zeroOps: 执行一个零参数函数并将结果存储在栈上。数字正是这样做。
```

