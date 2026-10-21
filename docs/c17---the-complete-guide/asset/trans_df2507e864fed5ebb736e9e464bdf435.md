

std::clamp<double>(d, 0, max);  // OK

你也可以传递浮点值，前提是它们的值不是 NaN。

与 min() 和 max() 类似，你可以传递一个谓词作为比较操作。例如：

```
for (int i : {-7, 0, 8, 15}) {
    std::cout << std::clamp(i, 5, 13,
        [] (auto a, auto b) {
            return std::abs(a) < std::abs(b);
        })
        << '\n';
}
```

输出如下：

-7
5
8
13

因为 -7 的绝对值介于 5 和 13 的绝对值之间，所以在这种情况下 clamp() 会返回 -7。

clamp() 没有接受值初始化列表的重载（min() 和 max() 有）。

## 25.4 sample()

借助 sample()，C++17 提供了一个从给定值范围（总体）中提取随机子集（样本）的算法。这有时被称为蓄水池抽样或选择抽样。

考虑以下示例程序：

lib/sample1.cpp

```
#include <iostream>
#include <vector>
#include <string>
#include <iterator>
#include <algorithm>  // for sample()
#include <random>     // for default_random_engine

int main()
{
    // initialize a vector of 10,000 string values:
    std::vector<std::string> coll;
    for (int i=0; i < 10000; ++i) {
        coll.push_back("value" + std::to_string(i));
    }

    // print 10 randomly selected values of this collection:
    std::sample(coll.begin(), coll.end(),
```

```
std::ostream_iterator<std::string>{std::cout, "\n"},
10,
std::default_random_engine{});
```

在初始化一个包含大量字符串值（value0、value1、...）的向量后，我们使用 sample() 从这些字符串值中提取一个随机子集：

// print 10 randomly selected values of this collection:
sample(coll.begin(), coll.end(),
    std::ostream_iterator<std::string>{std::cout, "\n"},
    10,
    std::default_random_engine{});

我们传递：

- 提取子集值范围的开始和结束
- 用于将提取的值写入的迭代器（这里是一个 ostream 迭代器，将它们写入标准输出）
- 要提取的最大值数量（如果范围太小，可能提取更少的值）
- 用于计算随机子集的随机引擎

结果，我们打印 coll 的 10 个元素的随机子集。输出可能是，例如：

```
value132
value349
value796
value2902
value3267
value3553
value4226
value4820
value5509
value8931
```

正如你所见，元素的顺序是稳定的（与 coll 中的顺序匹配）。然而，这只有在传递范围的迭代器至少是前向迭代器时才有保证。

该算法声明如下：
namespace std {
    template<typename InputIterator, typename OutputIterator,
             typename Distance, typename UniformRandomBitGenerator>
    OutputIterator sample(InputIterator sourceBeg, InputIterator sourceEnd,
                          OutputIterator destBeg,
                          Distance num,
                          UniformRandomBitGenerator&& eng);
}

它具有以下规范和约束：

- 源范围的迭代器必须至少是输入迭代器，目标范围的迭代器必须至少是输出迭代器。如果源迭代器不是至少前向迭代器，则目标迭代器必须是随机访问迭代器。
- 与往常一样，目标迭代器会覆盖，这会导致未定义行为，如果没有足够的元素可供覆盖且未使用插入器。
- 该算法返回最后一个复制元素之后的位置。
- 目标迭代器不得在传递的源范围内。
- *num* 可以具有积分类型。如果源范围中的元素不足，则提取源范围中的所有元素。
- 提取元素的顺序是稳定的，除非源范围中的迭代器是输入迭代器。

下面是另一个演示 `sample()` 用法的示例：

```cpp
#include <iostream>
#include <vector>
#include <iterator>
#include <algorithm>  //for sample()
#include <random>     //for random devices and engines

int main()
{
    // initialize a vector of 10,000 string values:
    std::vector<std::string> coll;
    for (int i=0; i < 10000; ++i) {
        coll.push_back("value" + std::to_string(i));
    }

    // initialize a Mersenne Twister engine with a random seed:
    std::random_device rd;    // random seed (if supported)
    std::mt19937 eng{rd()};   // Mersenne twister engine

    // initialize destination range (must be big enough for 10 elements):
    std::vector<std::string> subset;
    subset.resize(100);

    // copy 10 randomly selected values from the source range to the destination range:
    auto end = std::sample(coll.begin(), coll.end(),
                           subset.begin(),
                           10,
                           eng);

    // print extracted elements (using return value as new end):
    std::for_each(subset.begin(), end,
                  [] (const auto& s) {
```

```
std::cout << "random elem: " << s << '\n';
});
}
```

在初始化一个包含大量字符串值（value0、value1、...）的向量后，我们初始化一个使用随机种子初始化的随机数引擎：

// initialize a Mersenne Twister engine with a random seed:
std::random_device rd;  // random seed (if supported)
std::mt19937 eng{rd()};  // Mersenne Twister engine

以及一个目标范围：

// initialize destination range (must be big enough for 10 elements):
std::vector<std::string> subset;
subset.resize(100);

对 sample() 的调用现在将（最多）10 个源范围的元素复制到目标范围：

// copy 10 randomly selected values from the source range to the destination range:
auto end = sample(coll.begin(), coll.end(),
                subset.begin(),
                10,
                eng);

end 初始化的返回值包含最后一个随机提取元素之后的<|message|>位置，可以在之后用来打印提取的元素：

// print extracted elements (using return value as new end):
for_each(subset.begin(), end,
    [] (const auto& s) {
        std::cout << "random elem: " << s << '\n';
    });

## 25.5 Afternotes

size()、empty() 和 data() 最初由 Riccardo Marcangelo 在 http://wg21.link/n4017 中提出。最终被接受的措辞由 Riccardo Marcangelo 在 http://wg21.link/n4280 中制定。

as_const() 最初由 ADAM David Alan Martin 和 Alisdair Meredith 在 http://wg21.link/n4380 中提出。最终被接受的措辞由 ADAM David Alan Martin 和 Alisdair Meredith 在 http://wg21.link/p0007r1 中制定。

clamp() 最初由 Martin Moene 和 Niels Dekker 在 http://wg21.link/n4536 中提出。最终被接受的措辞由 Martin Moene 和 Niels Dekker 在 http://wg21.link/p002501 中制定。

sample() 最初由 Walter E. Brown 在 http://wg21.link/n3842 中提出。最终被接受的措辞由 Walter E. Brown 在 http://wg21.link/n3925 中制定。

本页特意留空

## Chapter 26

### Container and String Extensions

C++ 标准库的标准容器有一些细微或小的更改，这些更改在本章中描述。

- 修改（无序）映射的键或（无序）集合的值
- 在（无序）集合和映射中使用移动语义
- 在（无序）集合和映射之间移动元素
- 将元素从一个（无序）集合或映射合并到另一个

例如，考虑以下程序：

```
```cpp
#include <iostream>
#include <string>
#include <map>

int main()
{
    std::map<int, std::string> m{1, "mango"},
    {2, "papaya"},
    {3, "guava"}};

auto nh = m.extract(2); // nh has type decltype(m)::node_type
nh.key() = 4;
}
```
```

## 26.1.2 Moving Nodes Between Containers

你也可以使用节点句柄将元素（拼接）从一个容器移动到另一个容器。容器甚至可以在以下方面有所不同：

- 一个支持重复而另一个不支持（例如，你可以将元素从 multimap 移动到 map）
- 比较函数和哈希函数可能不同

例如，考虑以下程序：

lib/nodemove.cpp

```
#include <iostream>
#include <string>
#include <map>

template<typename T1, typename T2>
void print(const T1& coll1, const T2& coll2)
{
    std::cout << "values:\n";
    for (const auto& [key, value] : coll1) {
        std::cout << " [" << key << ":" << value << "]";
    }
    std::cout << '\n';
    for (const auto& [key, value] : coll2) {
        std::cout << " [" << key << ":" << value << "]";
    }
    std::cout << '\n';
}

int main()
{
    std::multimap<double, std::string> src {{1.1, "one"},
                                            {2.2, "two"},
                                            {3.3, "three"}};

    std::map<double, std::string> dst {{3.3, "old data"}};

    print(src, dst);

    // move some elements from multimap src to map dst:
    dst.insert(src.extract(src.find(1.1)));  // splice using an iterator
    dst.insert(src.extract(2.2));            // splice using the key

    print(src, dst);
}
```

