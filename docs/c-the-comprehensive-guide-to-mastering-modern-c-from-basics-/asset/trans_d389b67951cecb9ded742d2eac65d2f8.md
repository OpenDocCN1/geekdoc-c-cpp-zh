

```
// https://godbolt.org/z/5z4s6WMXG
#include <iostream>
#include <string>
#include <algorithm> // min, max
#include <tuple>
using std::tuple; using std::get; std::cout;
using std::string;
tuple<int,int,int> arrange(int a, int b, int c) {
    using std::min; using std::max;
    auto x = min(a,b,c);
    auto y = max(min(a,b), max(a,b,c));
    auto z = max(a,b,c);
    return make_tuple(x, y, z);
}
tuple<string, string, string, int> president(int year) {
    using namespace std::literals;
    if(year >= 2021)
        return std::make_tuple("Joseph", "Biden", "Democratic"s, 1942);
    if(year >= 2017)
        return std::make_tuple("Donald", "Trump", "Republican"s, 1946);
    if(year >= 2009)
        return std::make_tuple("Barack", "Obama", "Democratic"s, 1961);
    // Add more presidents as needed...
    return std::make_tuple("s", "s", "s", 0); // Default case
}
int main() {
    tuple<int,int,int> zs = arrange(23, 42, 7);
    cout << get<0>(zs) << ' ' << get<1>(zs) << ' ' << get<2>(zs) << '\n';
    // Output: 7 23 42
    auto ps = president(2015);
    cout << get<1>(ps) << ' '\n'; // Output: Obama
}
```

# 列表 28.2 “使用 tuple”，你可以返回任意数量的元素。

你可以像 `arrange` 和 `zs` 那样使用 `auto` 将不同类型的值组合成 tuple，也可以写出 tuple 的类型。不过，我建议使用 `auto`，如 `president` 和 `ps` 所示。这里实际上是一个 `tuple<string, string,int>`，但你可以用 `auto` 节省输入时间。

现在不再使用 `first` 和 `second` 访问元素，而是使用 `get<0>` 和 `get<1>`。对于后续元素，逻辑上使用更大的数字。请注意，在这里你只能指定固定值（constexpr）作为索引。这不能用于变量。

你甚至可以传递一个类型而不是数字，即你想要的类型。

```
// https://godbolt.org/z/TE1EcEYPv
// ... 如前 ...
int main() {
    tuple<string, string, string, int> ps = president(2015);
    cout << get<int>(ps) << '\n'; // 输出: 1940
    cout << get<string>(ps) << '\n'; // 不唯一
}
```

# 列表 28.3 “array”可以使用类型作为索引。

由于它只在 `tuple<tuple, string, string, int>` 中出现一次，你可以使用 `get<int>` 访问相应的元素。`get<string>` 不起作用，因为将是不唯一的。

> “array”作为“tuple”
对于相同类型的固定数量元素的实际数组容器（参见第 24 节第 24.6.4 节）也提供了使用 `get<...>` 访问元素的可能性。你几乎可以将 `array<int,3>` 像 `tuple<int,int,int>` 一样使用。

如果这样访问元素对你来说太麻烦了，可以使用 `tie` 将函数的返回值绑定到变量上。

```
// https://godbolt.org/z/zG7yGF3K
// ... 如前 ...
int main() {
    using std::tie; using std::ignore;
    string lastName();
    int birthYear;
    tie(ignore, lastName, birthYear) = president(2015);
    cout << lastName << '\n'; // 输出: Obama 1961
}
```

**列表 28.4** 使用“tie”和“ignore”解构 tuple。

当你像这里所示在赋值左侧使用 `tie` 时，你可以直接将 tuple 和 pair 返回的各个部分赋值给之前声明的变量。如果你只对返回的部分感兴趣，请在你不感兴趣的位置使用 `ignore`。

# 使用“auto”的结构化绑定

从 C++17 开始，直接将 tuple 或 array 的返回赋值给变量变得更加容易。这一功能是结构化绑定（structured binding）。这使得同时声明变量成为可能：

```cpp
auto [a, lastname, c, birthyear] = president(2015);
```

在这里，四个变量会自动声明正确的类型，并用返回 tuple 的相应部分初始化。为了这一点，右侧的表达式需要一个“类 tuple 接口”；即它必须支持 `get<>` 和 `tuplesize<>`，array、tuple 和 pair 都是这种情况。

# C 风格数组或结构体也可以在右侧。

tuple 重载了用于比较运算符，特别是 `<` 和 `==`，这对于像 `sort` 这样的算法和标准容器是必要的。如果 tuple 的第一个元素相等，则比较第二个元素，依此类推。这被称为字典序（lexicographical order），因为它的工作方式就像字典中的排序一样。

```cpp
// https://godbolt.org/z/5z4s6WMXG
#include <iostream>
#include <string>
#include <tuple>
#include <vector>
#include <algorithm>
using std::tuple; using std::get; using std::string;
int main() {
    std::vector<tuple<string, string, int>> armlongs = {
        {"Armstrong", "Louis", 1912},
        {"Armstrong", "Neil", 1930},
        {"Armstrong", "Buzz", 1926}
    };
    sort(armlongs.begin(), armlongs.end());
    for(const auto& a : armlongs) {
        cout << get<0>(a) << " " << get<1>(a) << " " << get<2>(a) << "\n";
    }
}
```

**28.5** tuple 的字典序

tuple 重载了用于比较运算符，特别是 `<` 和 `==`，这对于像 `sort` 这样的算法和标准容器是必要的。如果 tuple 的第一个元素相等，则比较第二个元素，依此类推。这被称为字典序，因为它的工作方式就像字典中的排序一样。

**28.6** tuple 作为键

在像 `unordered_set` 这样的容器中，你无法使用 tuple 作为键，除非你提供了哈希函数。但是，对于 `map` 这样的容器，你可以使用 tuple，因为它们只需要比较运算符。

**28.7** 使用 tie 原地构造 tuple

你自己自己实现字典序并不困难。但是，tie 工作的是引用，所以你的数据不会产生额外的拷贝。

创建 tuple 的最后一种方法是使用 `tuple_cat`。你给 `tuple_cat` 一个 tuple 列表，并接收一个大的 tuple 作为返回值，所有元素连接在一起。

```cpp
// https://godbolt.org/z/e1dgdWbe9
#include <iostream>
#include <string>
#include <tuple>
using std::tuple; using std::cout; using std::string;

int main() {
    tuple<int,string> a {12, "gnorf" };
    tuple b { 666 };
    tuple<double,double,string> c { 77.77, 33.33, "frong" };
    tuple<int,string,int,double,string> r = std::tuple_cat(a, b, c);
    cout << std::get<2>(r) << "\n"; // 输出: 666
}
```

# 列表 28.8 将多个小 tuple 合并为一个大的 tuple。

同样——可能更好——你也可以写 `r = ...` 并让编译器确定正确的类型。除了 tuple，你也可以给 `tuple_cat` 传递 pair 作为参数。在大多数情况下，这些类型是兼容的。

