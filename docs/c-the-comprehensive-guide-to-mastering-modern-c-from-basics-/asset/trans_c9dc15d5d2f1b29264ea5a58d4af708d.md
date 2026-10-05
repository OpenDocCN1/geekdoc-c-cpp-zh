
处理起来比位操作容易一些。在表 24.13 中，你可以看到 bitset 的功能。

| 算符 | 示例 | 说明 |
|---|---|--|
| 构造函数 | bitset<8> | 创建一个包含八个零的 bitset |
| | bitset<8>(255) | 将整数转换为位序列 |
| | bitset<8>("1100") | 从字符串创建一个 00001100 的 bitset |
| | ... ("#. ,2,','.','#") | 两个字符；. false 表示 # 为 true |
| == | as == bs | 检查相等性 |
| != | as != bs | 检查不相等 |
| [] | bs[3] | 访问单个位 |
| test | bs.test(2) | 测试单个位的状态 |
| all | bs.all() | 检查是否所有位都设置为1 |
| any | bs.any() | 检查是否至少有一个位被设置为1 |
| none | bs.none() | 检查是否没有位被设置为1 |
| count | bs.count() | 计算置1位的个数 |

| 算符 | 示例 | 说明 |
| --- | --- | --- |
| size | bs.size() | bitset 的宽度 |
| &, |, ^ | as & bs | 位与、位或、位异或操作 |
| <<, >> | bs << 1 | 位移算符 |
| &=, |=, ^= | bs &= bs | 赋值位操作 |
| <=, >= | bs <= 1 | 赋值位移 |
| set | bs.set(4) | 设置所有或单个位 |
| reset | bs.reset(4) | 重置所有或单个位 |
| flip | bs.flip(4) | 反转所有或单个位 |
| to_string | bs.to_string() | 转换为字符串 |
| to_ulong | bs.to_ulong() | 转换为无符号长整数 |
| to_ulong | bs.to_ullong() | 转换为无符号长整数 |

**表 24.13** “bitset”方法与操作。

# 关于性能的说明

`vector<bool>` 将多个值打包到单个内存单元中，这节省了空间。然而，这种方法有一个缺点：更改单个值时需要读取并写回相邻的值，这会消耗时间。

bitset 将每个值存储在自己独立的内存单元中。如果你想更改单个值，可以直接写入。然而，这种数据结构需要（至少）八倍的空间。

在 C++ 中，良好的性能一方面意味着内存占用低，另一方面意味着时间消耗少——或者两者兼顾。关于内存，有一个明确的结论：`vector<bool>` 节省空间。速度呢？这很难回答，取决于系统。如果不考虑相邻位会更快，还是因为内存加缓存太慢，导致使用八倍内存反而更快？

如果这对你的问题很重要，请进行测量和比较！我可以为你提供一个参考点。在 Intel i7-4xxx 上，单项实验表明，浪费空间的 bitset 速度是节省空间的 `vector<bool>` 的两倍——甚至是简单的 `bool[]` 实现的五倍。

# #24.12 特殊情况：使用 "valarray<>" 的值数组

valarray 并不是像其他那容器。它的重点不在于与迭代器、算法和其他容器的兼容性上，而在于数值数据处理的并行化能力。

你通常只对数值类型使用 valarray，因为它为这些类型提供了专门的函数。它还配备了所有可以想象的算术算符重载，允许你像处理数字一样为 valarray 编写整个算术表达式，类似于数学家处理（数学）向量和矩阵的方式。

如果你曾希望能够简单地用 `+` 按元素相两个 `vector<double>` 或用 `*` 相乘，那么 valarray 正是你需要的：

```
// https://gdbbolt.org/z/KPP16bdK9
#include <iostream>
#include <valarray>
using std::ostream; using valarray;
stream& operator<<(ostream&os, const valarray<double>&vs) {
    os << "[";
    for(auto& v : vs) os << v << " ";
    return os << "]";
}

int main() {
    valarray a{1.0, 2.0, 3.0, 4.0}; // valarray
    valarray b{2.0, 4.0, 6.0, 8.0};
    valarray c{2.5, 1.75, 0.5, 0.125};
    valarray<double> x = { a + b };
    cout << ": " << x << "\n"; // 输出: [7.5 10.5 4.5 11.5 ]
    auto y = ( a + b ) / 2;
    // y 不一定是一个 valarray!
```

```cpp
std::cout << "y" << y << "\n"; // 输出: [1.5 3 4.5 6 ]
}
```

valarray 将数据存储在一个一维数组中，但它也是为了多维情况设计的。你之后会看到相关的示例。

一个特别重要的特性是，valarray 刻意避免了某些形式的别名（aliasing），从而允许多维情况的处理。
