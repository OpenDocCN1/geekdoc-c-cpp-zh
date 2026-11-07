

![](img/7b5e2088e71c7f78681d4ddbcf104c06_332_0.png)

**图 6.6** | 将学生成绩分布打印为基本条形图。（第 2 部分，共 2 部分。）

## 6.10 使用数组元素作为计数器

有时，程序使用计数器变量汇总数据，例如调查结果。图 5.3 的掷骰子模拟使用单独的计数器来跟踪程序掷骰子 60,000,000 次时每个骰子面的出现频数。图 6.7 使用频数计数器数组重新实现该模拟。

```cpp
// fig06_07.cpp
// Die-rolling program using an array instead of switch.
#include <format>
#include <iostream>
#include <array>
#include <random>

int main() {
   // set up random-number generation
   std::random_device rd; // used to seed the default_random_engine
   std::default_random_engine engine{rd()}; // rd() produces a seed
   std::uniform_int_distribution randomDie{1, 6};

   constexpr size_t arraySize{7}; // ignore element zero
   std::array<int, arraySize> frequency{}; // initialize to 0s

   // roll die 60,000,000 times; use die value as frequency index
   for (int roll{1}; roll <= 60'000'000; ++roll) {
      ++frequency.at(randomDie(engine));
   }

   std::cout << std::format("{}{:>13}\n", "Face", "Frequency");

   // output each array element
   for (size_t face{1}; face < frequency.size(); ++face) {
      std::cout << std::format("{:>4}{:>13}\n", face, frequency.at(face));
   }
}
```

**图 6.7** | 使用数组代替 switch 的掷骰子程序。（第 1 部分，共 2 部分。）

| 面值 | 频数 |
| --- | --- |
| 1 | 9997901 |
| 2 | 9999110 |
| 3 | 10001172 |
| 4 | 10003619 |
| 5 | 9997606 |
| 6 | 10000592 |

**图 6.7** | 使用数组代替 switch 的掷骰子程序。（第 2 部分，共 2 部分。）

图 6.7 使用数组 frequency（第 15 行）统计骰子值的出现次数。第 19 行取代了图 5.3 中第 23–45 行的 switch 语句。它使用随机骰子值作为索引，来确定每次掷骰子时要递增哪个 frequency 元素。第 19 行中的点（.）运算符优先级高于 ++ 运算符，因此该语句先选择一个 frequency 元素，再递增其值。

调用 randomDie(engine) 会生成 1 到 6 的随机索引，因此 frequency 必须足够大以存储六个计数器。我们使用一个七元素数组，并忽略元素 0——让骰子值 1 递增 frequency.at(1) 而不是 frequency.at(0) 更清晰。因此，每个面值直接用作 frequency 的索引。我们还通过遍历数组 frequency 来输出结果（图 6.7，第 25–27 行），从而取代图 5.3 的第 49–54 行。这里我们使用计数器控制的 for 语句，而不是基于范围的 for 语句，这样可以跳过打印 frequency 的元素 0。

### 检查点

- 1. *(代码)* 重写图 6.7 的第 22–27 行，使各列左对齐，如下所示：

```cpp
Face   Frequency
1      9997901
2      9999110
3      10001172
4      10003619
5      9997606
6      10000592
```

**答案：**

```cpp
std::cout << std::format("{:<8}{}\n", "Face", "Frequency");

// output each array element
for (size_t face{1}; face < frequency.size(); ++face) {
    std::cout << std::format("{:<8}{}\n", face, frequency.at(face));
}
```

## 6.11 使用数组汇总调查结果

下一个示例使用数组汇总调查中收集的数据。考虑以下问题陈述：

> 二十名学生被要求按 1 到 5 的等级评价学生食堂的食品质量，其中 1 表示“糟糕”，5 表示“极好”。将这 20 个回答放入一个 int 值数组中，并确定每个评分的频数。

这是一种常见的数组处理应用（图 6.8）。我们希望汇总每个评分（即 1–5）的回答数量。数组 responses（第 9–10 行）是一个包含学生调查回答的 20 元素整数数组。它被声明为 `constexpr`，因为其值不会（也不应）改变，并且在编译时已知。我们使用一个六元素数组 frequency（第 18 行）来统计每个回答的出现次数。每个 frequency 元素用作一个调查回答的计数器，并初始化为零。与图 6.7 一样，我们忽略元素 0。

```cpp
// Fig06_08.cpp
// Poll analysis program.
#include <format>
#include <iostream>
#include <array>

int main() {
   // place survey responses in array responses
   constexpr std::array responses{
      1, 2, 5, 4, 3, 5, 2, 1, 3, 1, 4, 3, 3, 2, 3, 3, 2, 2, 2, 5};

   // initialize frequency counters to 0
   constexpr size_t frequencySize{6}; // size of array frequency
   std::array<int, frequencySize> frequency{};

   // for each response in responses, use that value
   // as the index to determine element to increment
   for (const int& response : responses) {
      ++frequency.at(response);
   }

   std::cout << std::format("{:>6}{:>12}\n", "Rating", "Frequency");

   // output each array element
   for (size_t rating{1}; rating < frequency.size(); ++rating) {
      std::cout << std::format("{:>6}{:>12}\n",
         rating, frequency.at(rating));
   }
}
```

| 评分 | 频数 |
|---:|---:|
| 1 | 3 |
| 2 | 5 |
| 3 | 7 |
| 4 | 2 |
| 5 | 3 |

**图 6.8** | 调查分析程序。

第一个 for 语句（第 18–20 行）每次从 responses 中取出一个回答（每个都是 1–5 范围内的值），并递增 frequency.at(1) 到 frequency.at(5) 中的一个计数器。关键语句是第 19 行，它根据 response 的值递增相应的计数器。无论调查中处理多少个回答，程序只需要一个六元素数组（忽略元素零）即可汇总结果，因为所有回答值都在 1 到 5 之间，而六元素数组的索引值为 0 到 5。

## 6.12 对数组排序和搜索

将数据按升序或降序排序是最重要的计算应用之一。几乎每个组织都必须对某些数据进行排序，而且在许多情况下，数据量巨大。排序是一个引人入胜的问题，吸引了计算机科学中一些最密集的研究努力。通常可能需要确定数组是否包含与特定键值匹配的值。查找键值的过程称为搜索。本节使用内置的 C++ 标准库 sort 函数将数组中的元素按升序排列，并使用内置的 binary_search 函数确定某个值是否存在于已排序数组中。

### 演示函数 sort 和 binary_search

图 6.9 创建一个名为 colors 的、包含七个 string 对象的未排序数组（第 13–14 行）。第 10 行的 using 声明使我们能够使用 string 对象字面量初始化该数组。在字符串的结束引号后放置一个 s，即可构成 string 对象字面量。例如，在 "red"s 中，字面量后面的 s 告诉编译器该字面量是 std::string 对象。在这里使用 string 对象字面量使编译器能够从初始化器推断出数组的元素类型是 std::string。第 18–20 行显示 colors 的内容。注意，循环的控制变量声明为

```cpp
const std::string&
```

对范围变量 color 使用引用可防止循环在每次迭代时将当前 string 对象复制到 color 中。在处理大量字符串的程序中，这种复制操作会降低性能。

```cpp
// fig06_09.cpp
// Sorting and searching arrays.
#include <array>
#include <algorithm> // contains sort and binary_search
#include <format>
#include <iostream>
#include <string>

int main() {
    using namespace std::string_literals; // enables string object literals

    // colors is inferred to be an array<string, 7>
    std::array colors{"red"s, "orange"s, "yellow"s,
        "green"s, "blue"s, "indigo"s, "violet"s};

    // output original array
    std::cout << "Unsorted colors array: ";
    for (const std::string& color) {
        std::cout << std::format("{} ", color);
    }
}
```

**图 6.9** | 对数组排序和搜索。（第 1 部分，共 2 部分。）

