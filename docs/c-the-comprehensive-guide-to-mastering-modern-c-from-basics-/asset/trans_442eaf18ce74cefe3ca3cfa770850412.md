

```cpp
adjacent_difference(data.begin(), data.end(), os, std::plus<int>{});
cout << '\n'; Output: 1 0 1 -6 0 -2
// or range adapter:
for(auto e : vs::pairwise_transform(data, std::plus<int>{}))
    cout << e << ' '
cout << '\n'; Output: 0 1 0 -6 0 -2
```

# 列表 25.16 "adjacent_difference" 和 "pairwise_transform"。

我没有使用通常用于输出容器的 `for` 循环，而是使用了一个 `ostream_iterator` 流输出迭代器：你通过 `begin()` 创建一个指向容器间接位置的迭代器，但其目标是一个输出流——在这里是 `cout`，且元素之间使用 `" "` 作为分隔符。我用它来将数据输出到控制台。

然后，我通过为结果分配空间来准备第一个 `adjacent_difference`。我首先初始化了合适大小的 `vector res`。然后执行 `adjacent_difference`——来自 `data` 元素的两两差值存储在 `res` 中。

但特别对于那些将输出写入迭代器的函数来说，准备输出容器实际上是非常繁琐的。当我实际上只是想输出结果时，也可以像第二个示例那样使用流迭代器。

```cpp
// https://godbolt.org/z/WprP79sv6
#include <numeric> // accumulate, iota
#include <algorithm> // copy
#include <iostream>
#include <iterator> // ostream_iterator
#include <vector>
#include <ranges> // iota, take, stride
using std::accumulate; using std::cout; using std::vector;
namespace vs = std::views;
struct Generator {
    int state_;

    void operator++() { state_ += state_; }
    operator int int() { return state_; }
};
int main() {
    std::ostream_iterator<int> os(std::cout, " "); // Stream输出
    vector<int> data(7);
    std::iota(data.begin(), data.end(), 10);
    std::copy(data.begin(), data.end(), os);
    cout << '\n';
    // Output: 10 11 12 13 14 15 16
    vector<int> seq(7);
    std::iota(seq.begin(), seq.end(), Generator(2));
    std::copy(seq.begin(), seq.end(), os);
    cout << '\n';
    // Output: 2 4 16 32 64 128
    for(auto i : vs::iota(0) | vs::stride(3) | vs::take(6))
        cout << i << ' ';
    cout << '\n';
} // Output: 0 3 6 9 12 15
```

# 列表 25.17 "iota", "stride" 和 "take"。

尽管看起来你只能生成升增数字序列（这已经非常好用了），但通过适当的 `operator++`，你可以生成非常有趣的序列。辅助类型 `Generator` 存储了一个状态，该状态在隐式转换为 `int` 时被获取——特别是当 `iota` 想要将值写入输出迭代器时。辅助类型上的 `operator++` 可以执行任何函数；在这里我只是让内部状态的值翻倍。结果是一个可以在变化状态上生成的几乎任意的输出序列。

在最后，你将看到 `vs::iota` 范围生成器。在这里我从 0 开始并生成无限多个值。通过 `stride`，我只取每三个值。由于该过程是惰性的（lazy），因此可以在第六个值后通过 `take` 简单停止。最后两个范围适配器是 C++23 新引入的。

在下一个一个列表中，我对一个数据集执行了 `inclusive_scan` 和 `exclusive_scan`。

```cpp
// https://godbolt.org/z/enjznvTs
#include <numeric> // scan
#include <iostream>
#include <vector>

using std::inclusive_scan; using std::exclusive_scan;
std::ostream& operator<<(std::ostream& os, const std::vector<int>& data) {
    for (auto &e : data) os << e << ' ';
    return os << '\n';
}

int main() {
    std::vector<int> data{1, 3, 10, 18, 30, 50};
    std::vector<int> result(6); // 6 elements
    auto plus = [](auto a, auto b) { return a+b };
    inclusive_scan(data.begin(), data.end(), result.begin(), plus, 100);
    std::cout << result;
    // Output: 101 104 114 132 162 212
    exclusive_scan(data.begin(), data.end(), result.begin(), 100);
    std::cout << result;
    // Output: 100 101 104 114 132 162
}
```

**列表 25.18** "inclusive_scan" 和 "exclusive_scan"。

在 `inclusive_scan` 中，输出的第一个元素已经包含了 100+1，因此第 $i$ 个结果已经包含了求和中的第 $i$ 个输入。

`exclusive_scan` 的结果从 100 开始，因此第 $i$ 个结果不包含第 $i$ 个输入，然后它是对第 $i$ 个元素排斥的（exclusive）的。`inclusive_scan` 需要一个初始值。

## 25.8 拷贝而非赋值：未初始化内存

`<algorithm>` 中的所有函数在移动元素时使用赋值。使用 `move_iterator` 时使用移动赋值 `operator=(&&)`。在这两种情况下，目标对象都必须存在。你需要先初始化整个范围。这可能看起来是繁琐且没必要的，因为无论如何，你都会覆盖整个范围。

在 `<memory>` 头文件中，有一些额外的函数不需要目标对象。在未初始化内存中使用拷贝构造函数 `E(const&)` 对象是可以被创建的。

```cpp
// https://godbolt.org/z/dkj1lf
#include <iostream>
#include <memory>
#include <alloca.h>
#include <list>

int main() {
    const std::list<int> input{1,9,2,6,8};
    const auto SZ = input.size();
    int* target = (int*)alloca(sizeof(int) * SZ);
    uninitialized_copy(input.begin(), input.end(), target);
    for(int idx=0; idx<SZ; ++idx) {
        std::cout << target[idx] << ' ';
    }
    std::cout << ''; // output: 1 9 2 6 8
}
```

`alloca` 调用在栈上分配空间（在函数退出时自动释放）。内存区域是未初始化的——与通常不同，真实的 C++ 对象也是未初始化的。然后从 `input` 将元素拷贝到 `target`——这次使用的是拷贝构造函数而不是赋值运算符。因此，没有有效对象也是好的。顺便说一下，`alloca` 应极其谨慎使用，因此只在不会出错的函数中使用。

- uninitialized_copy: 使用拷贝构造函数拷贝范围元素。
- uninitialized_copy_n: 使用拷贝构造函数从起点到目标点拷贝 $n$ 个元素。
- uninitialized_fill: 使用拷贝构造函数用特定值填充范围。
- uninitialized_fill_n: 从起点创建 $n$ 个值的拷贝。
- uninitialized_move: 将元素移动到未初始化的范围。
- uninitialized_move_n: 将 $n$ 个元素移动到未初始化的范围。
- uninitialized_default_construct: 使用默认构造函数填充范围。
- uninitialized_default_construct_n: 使用默认构造函数创建 $n$ 个对象。
- uninitialized_value_construct: 用值构造的对象填充范围。

