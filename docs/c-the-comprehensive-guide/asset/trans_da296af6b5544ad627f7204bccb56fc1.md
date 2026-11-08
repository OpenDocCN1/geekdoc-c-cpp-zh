

```cpp
cout << '\n';
namespace vs = std::ranges::views;       // C++20
auto v = in | vs::drop(2) | vs::take(3);
vector<uint> v2(v.begin(), v.end());
vector<int> v3(std::from_range, in);         // C++23
```

**清单 24.17** 在初始化期间从任何其他容器或 C 数组复制值。

自 C++20 起，也可以使用范围和视图的迭代器来实现；从 C++23 起，如果额外向构造函数传递 _from_range_ 标记，甚至可以不用迭代器。

具体到 vector，有一些构造函数可以用指定数量的元素来初始化 vector。

```cpp
// https://godbolt.org/z/addobjfSK
vector<int> zeros(10);             // 10 个零
vector<int> sixes(10, 6);          // 10 个 6
vector<int> ten{10};               // 注意！只有一个 10
vector<int> tenSix{10, 6};         // 注意！两个元素 10 和 6
```

**清单 24.18** 使用固定数量的值进行预初始化（几乎）仅适用于 `vector`。

在这些情况下，初始化时必须使用圆括号 ()；否则元素将被解释为初始化器列表。

## 赋值

与所有容器（array 除外）一样，vector 重载了用于复制和移动的赋值运算符 operator=。借助 assign，你通常可以在构造之后将那些可在“首次”初始化时使用的所有初始化方式应用于容器。从 C++23 开始，你还可以使用 assign_range。

```cpp
// https://godbolt.org/z/rb4jEdakj
vector<int> from{ 2,3,4 };
vector<int> to{};
to = from;                         // 使用 operator= 赋值，现在两者相同

vector<int> drain{};
drain = std::move(from);            // 移动，现在 'from' 为空
vector<int> v;
v.assign(4, 100);                   // v 现在为 {100, 100, 100, 100}
v.assign(to.begin(), to.end());    // v 现在为 {2,3,4}
int z[] = { 10, 20, 30, 40 };
v.assign(z+1, z+4);              // v 现在为 {20,30,40}
```

**清单 24.19** 你可以向“vector”赋值，或稍后用“assign”重新初始化它。

## 访问“vector”

你总归需要获取 vector 中的数据。主要有以下几种方式：

- **迭代器**  
  你使用间接访问，主要是*迭代器*。由于元素是连续的，指针也可以工作。
- **索引**  
  你使用*索引*直接寻址某个元素。为此，可以使用 `at` 和 `operator[]`。
- **首尾元素**  
  `front` 和 `back` 返回对第一个和最后一个元素的引用。由于对空容器使用这些函数的结果是未定义的，如有必要，你必须将其与例如 `!empty()` 结合使用。
- **Span**  
  span 比两个独立的迭代器或一个迭代器加一个计数更容易处理。因此，span 将这些东西打包成一个单独的实体。这个类自 C++20 起可用；自 C++23 起，还有多维变体 *mdspan*。更多内容请参见后面的“通过 Span 访问”一节。

vector 容器有多个返回迭代器的成员函数，主要是 `begin()` 和 `end()`，与所有容器一样。并且与所有其他容器一样，你需要*解引用*迭代器来获得对实际元素的引用，如[清单 24.20](#listing-2420)所示。

```cpp
// https://godbolt.org/z/freK1Pea
vector vowels { 'A', 'e', 'i', 'o', 'u' };
const vector even { '0', '2', '4', '6', '8' };
auto it1 = vowels.begin();          // vector<char>::iterator
*it1 = 'a';                          // *it1 返回 'char&'
auto it2 = even.begin();             // vector<char>::const_iterator
auto it3 = vowels.cbegin();          // 强制使用 const_iterator
*it2 = '9'; *it3 = 'x';              // 'const char&' 不可修改
for(auto it=vowels.cbegin()+1; it!=vowels.cend(); ++it)
    { cout << *it; } cout << '\n';  // 输出：eiou
for(auto it=vowels.crbegin()+1; it!=vowels.crend(); ++it) // 即使是反向迭代器也使用 ++！
    { cout << *it; } cout << '\n';  // 输出：oiea
```

**清单 24.20** 使用“begin”、“end”及其相关变体，你可以获得迭代器。

使用变体 `cbegin` 和 `cend` 时，你总是得到一个 `const_iterator`，它在解引用时不允许修改元素。另一方面，`begin` 和 `end` 根据容器的修饰符返回 `const_iterator` 或 `iterator`。

这些函数的 `r...` 变体允许反向遍历 vector。注意，你需要使用 `++` 来递增 `reverse_iterator` 或 `const_reverse_iterator`，才能实际向后遍历。

## “begin()”、“cbegin()”、“rbegin()”和“crbegin()”的记号

为简洁起见，我写作

- [c]`begin()` 表示 `begin()` 和 `cbegin()`；
- [r]`begin()` 表示 `begin()` 和 `rbegin()`；以及
- [cr]`begin()` 表示 `begin()`、`cbegin()`、`rbegin()` 和 `crbegin()`。

对于 `end()` 的变体也同样适用。

通过迭代器访问对所有容器都是通用的。`vector` 具有随机访问迭代器——即通过 `random_access_iterator_tag`。在实践中，这意味着你可以向 vector 迭代器添加正或负的偏移量，如清单 24.21 所示。

```cpp
// https://godbolt.org/z/szrcz737G
#include <vector>
#include <iostream>
#include <algorithm>                 // ranges::sort
using std::vector; using std::cout;
double median(vector<int> data) {    // 按值传递（拷贝）
    std::ranges::sort(data);         // C++20，否则使用 std::sort()
    auto it = data.begin();
    auto sz = data.size();
    if(sz==0) return 0;              // 特殊情况
    // 确定中位数
    auto m = (it+sz/2);               // 大约在中间位置
    if(sz%2 != 0) {                   // 奇数个元素
        return *m;
    } else {                          // 偶数个元素
        return double(*m + *(m-1)) / 2;
    }
}
int main() {
    vector data1 { 12, 22, 34, 10, 1, 99, 33 };
    cout << median(data1) << '\n';   // 22
    vector data2 { 30, 2, 80, 99, 31, 3 };
    cout << median(data2) << '\n'; // 30.5
}
```

**清单 24.21** 使用“vector”迭代器，你可以进行随机访问。

it 指向 vector 的开头。通过 `m = it+sz/2`，你向前移动 vector 长度的一半，`m` 指向大约中间的位置。对于奇数个元素（如 7），`sz/2` 自然得到 3，`it+3` 对应 `data[3]`，即 7 个元素的中间。如果元素个数为偶数（如 6），则中间位于 `data[2]` 和 `data[3]` 之间。`m` 指向 `data[3]`，因此 `(*m + *(m-1)) / 2` 计算两侧值的平均值。为确保除法也按浮点数进行，我事先用 `double(...)` 转换中间结果。

虽然每个容器都可以使用迭代器，但只有 `vector`、`array` 和 `deque` 允许使用 `at` 和 `operator[]` 按整数位置访问容器中的元素。（当然，这不包括你也可以使用以整数为键的关联容器的情况。）

最前面的元素索引始终为 0，容器中最后一个元素的索引为 `size()-1`。

- **无检查访问**  
  当你使用 `Elem& operator[](size_t idx)` 访问 vector 时，你会在 O(1) 时间内立即获得存储位置处的元素。不允许访问超出 vector 的 `size()-1` 的元素。那将是编程错误并导致未定义行为。你必须在程序中确保不会发生这种情况。
- **带检查访问**  
  `Elem& at(size_t idx)` 非常快，也是 O(1)，但库会在运行时检查你使用的索引是否在容器允许的范围内。如果不在范围内，则这不是编程错误，而是抛出 `std::out_of_range` 类型的异常。

你可以将 `[]` 和 `at` 用于读取，也可以放在赋值左侧用于写入元素。

在循环中，明智的做法是避免使用 `at` 而使用 `[]`，因为循环条件通常已经包含了检查。

```cpp
// https://godbolt.org/z/jjWx3d375
vector d{ 1, 2, 4, -1, 1, 2, -2 };
for(size_t idx=0; idx < d.size(); ) {  // 检查 vector 边界
    cout << d[idx] << ' ';             // 这里不需要再用 at 进行额外检查
    idx += d[idx];                     // 这里同样如此
}
cout << '\n';
// 输出：1 2 -1 4 -2 1 2
```

**清单 24.22** 通常你使用 `[]` 访问，因为你已经检查了边界。

