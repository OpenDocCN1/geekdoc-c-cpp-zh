
## C++23 中的新视图

```cpp
// cpp23Ranges.cpp

#include <ranges>

...

std::vector vec = {1, 2, 3, 4};

for (auto i : vec | std::views::adjacent<2>) {
    std::cout << '(' << i.first << ", " << i.second << ") "; // (1, 2) (2, 3) (3, 4)
}

for (auto i : vec | std::views::adjacent_transform<2>(std::multiplies<>())) {
    std::cout << i << ' ';                                  // 2 6 12
}

std::print("{}\n", vec | std::views::chunk(2));             // [[1, 2], [3, 4]]
std::print("{}\n", vec | std::views::slide(2));             // [[1, 2], [2, 3], [3, 4]]

for (auto i : vec | std::views::slide(2)) {
    std::cout << '[' << i[0] << ", " << i[1] << "] ";      // [1, 2] [2, 3] [3, 4] [4, 5]
}

std::vector vec2 = {1, 2, 3, 0, 5, 2};
std::print("{}\n", vec2 | std::views::chunk_by(std::ranges::less_equal{}));
                                                              // [[1, 2, 3], [0, 5], [2]]

for (auto i : vec | std::views::slide(2)) {
    std::cout << '[' << i[0] << ", " << i[1] << "] ";      // [1, 2] [2, 3] [3, 4] [4, 5]
}
```

### 8.1.2.1.3 `std::generator`

`std::generator` 是 C++23 中第一个具体的协程生成器。`std::generator` 通过反复恢复协程来生成元素序列。该元素序列可以是无限的。

### 8.1.2.2 模块化标准库

C++23 拥有模块化的标准库。`import std` 导入整个标准库。因此，你必须用 C++23 重写你的 hello world 程序。

```cpp
import std;

int main() {
    std::print("Hello world!");        // "Hello world!"
}
```

### 8.1.2.3 `std::print` 和 `std::println`

C++23 的便捷函数 `std::print` 和 `std::println` 用于向输出控制台写入内容。`std::println` 会在输出中添加换行符。此外，这两个函数还支持写入输出流，并支持 Unicode⁴。你必须包含头文件 `<print>`，或导入模块化的标准库。

```cpp
#include <print>                  // or import std;
...
std::print("{} {}!", "world", "Hello"); // prints "Hello world!"

std::ofstream outFile("testfile.txt");
std::print(outFile, "{} {}!", "world", "Hello"); // writes "Hello world!" into outFile
```

⁴ https://en.wikipedia.org/wiki/Unicode

### 8.1.2.4 格式化范围

C++23 支持格式化范围。

**将格式规范应用于 `std::vector` 的元素**

```cpp
// FormatVector.cpp

#include <format>
#include <iostream>
#include <string>
#include <vector>

int main() {

    std::vector<int> myInts{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    std::cout << std::format("{}\n", myInts);
    std::cout << std::format("{:+}\n", myInts);
    std::cout << std::format("{:03}\n", myInts);
    std::cout << std::format("{:b}\n", myInts);

    std::cout << '\n';

    std::vector<std::string> myStrings{"Only", "for", "testing", "purpose"};
    std::cout << std::format("{}\n", myStrings);
    std::cout << std::format("{:.3}\n", myStrings);

}
```

默认情况下（第 11 行和第 19 行），`std::vector` 以带方括号的形式显示。你也可以通过额外的冒号 `:` 将格式说明符应用于范围内的元素。

```text
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[+1, +2, +3, +4, +5, +6, +7, +8, +9, +10]
[001, 002, 003, 004, 005, 006, 007, 008, 009, 010]
[1, 10, 11, 100, 101, 110, 111, 1000, 1001, 1010]

[Only, for, testing, purpose]
[Onl, for, tes, pur]
```

**将格式规范应用于 `std::vector` 的元素**

### 8.1.2.5 容器适配器

C++23 中的四个关联容器 std::flat_map、std::flat_multimap、std::flat_set 和 std::flat_multiset 是有序关联容器^9 std::map、std::multimap、std::set 和 std::multiset 的直接替代品。更准确地说，std::flat_map 是 std::map 的直接替代品，std::flat_multimap 是 std::multimap 的直接替代品，以此类推。

扁平有序关联容器需要独立的序列容器^10 来存储它们的键和值。这些序列容器必须支持随机访问迭代器。默认使用 std::vector^11，但 std::array^12 或 std::deque^13 也是合法的。

以下代码片段展示了 std::flat_map 和 std::flat_set 的声明。

```cpp
template<class Key, class T,
         class Compare = less<Key>,
         class KeyContainer = vector<Key>, class MappedContainer = vector<T>>
class flat_map;

template<class Key,
         class Compare = less<Key>,
         class KeyContainer = vector<Key>>
class flat_set;
```

扁平有序关联容器比有序关联容器具有更好的时间和空间特性。与非扁平有序版本相比，扁平版本需要更少的内存，读取速度也更快。下面的比较将更详细地介绍扁平与非扁平有序关联容器。

#### 扁平有序关联容器与其非扁平版本之间的比较

扁平版本提供更好的读取性能，例如遍历容器，并且需要更少的内存。它们还要求元素必须可复制或可移动。扁平版本支持随机访问迭代器^14。

非扁平版本在插入或删除元素时具有更好的写入性能。此外，非扁平版本保证在插入或删除元素后迭代器仍然有效。非扁平版本支持双向迭代器^15。

- ^9 https://en.cppreference.com/w/cpp/container
- ^10 https://en.cppreference.com/w/cpp/container
- ^11 https://en.cppreference.com/w/cpp/container/vector
- ^12 https://en.cppreference.com/w/cpp/container/array
- ^13 https://en.cppreference.com/w/cpp/container/deque
- ^14 https://en.cppreference.com/w/cpp/random_access_iterator
- ^15 https://en.cppreference.com/w/cpp/iterator/bidirectional_iterator

### 8.1.2.6 std::expected

std::expected<T, E> 提供了一种存储两个值之一的方式。std::expected 的实例始终持有一个值：要么是类型 T 的期望值，要么是类型 E 的非预期值。这个词汇类型需要头文件 <expected>。借助 std::expected，你可以实现要么返回值要么返回错误的函数。存储的值直接分配在 expected 对象所占用的存储空间内，不会发生动态内存分配。

std::expected 拥有与 std::optional 类似的接口。与 std::optional 相比，std::expected 可以返回错误消息。

各种构造函数允许你定义一个带有期望值的 expected 对象 exp。exp.emplace 会在原地构造包含的值。你可以显式询问 std::expected 是否有值，也可以在逻辑表达式中检查它。exp.value 返回期望值，exp.value_or 返回期望值或默认值。如果 exp 含有非预期值，调用 exp.value 将抛出 std::bad_expected_access 异常。

std::unexpected 表示存储在 std::expected 中的非预期值。

#### **std::expected**

```cpp
1  // expected.cpp
2
3  #include <iostream>
4  #include <expected>
5  #include <vector>
6  #include <string>
7
8  std::expected<int, std::string> getInt(std::string arg) {
9      try {
10        return std::stoi(arg);
11    }
12    catch (...) {
13        return std::unexpected(std::string(arg + ": Error"));
14    }
15 }
16
17
18 int main() {
19
20    std::vector<std::string> strings = {"66", "foo", "-5"};
21
22    for (auto s : strings) {
23        auto res = getInt(s);
24        if (res) {
25            std::cout << res.value() << ' ';    // 66 -5
26        }
27        else {
28            std::cout << res.error() << '\n';    // foo: Error
29        }
30    }
31
32    std::cout << '\n';
33
34    for (auto s : strings) {
35        auto res = getInt(s);
36        std::cout << res.value_or(2023) << ' ';    // 66 2023 -5
37    }
38 }
```

函数 getInt 将每个字符串转换为整数，并返回一个 `std::expected<int, std::string>`。`int` 表示期望值，`std::string` 表示非预期值。两个基于范围的 for 循环（第 22 行和第 34 行）遍历 `std::vector<std::string>`。在第一个基于范围的 for 循环（第 22 行）中，会显示期望值（第 25 行）或非预期值（第 28 行）。在第二个基于范围的 for 循环（第 34 行）中，会显示期望值或默认值 2023（第 36 行）。

`std::expected` 支持方便函数组合的单子操作：`exp.and_then`、`exp.transform`、`exp.or_else` 和 `exp.transform_error`。`exp.and_then` 在给定函数调用存在时返回其结果，否则返回一个空的 `std::expected`。`exp.transform` 返回包含变换后值的 `std::expected`，否则返回空的 `std::expected`。此外，`exp.or_else` 在 `expected` 包含值时返回该值，否则返回给定函数的结果。

#### 对 `std::expected` 的单子操作

```cpp
// expectedMonadic.cpp

#include <expected>

std::expected<int, std::string> getInt(std::string arg) {
    try {
        return std::stoi(arg);
    }
    catch (...) {
        return std::unexpected<std::string>(arg + " : Error");
    }
}

std::vector<std::string> strings = {"66", "foo", "-5"};

for (auto s : strings) {
    auto res = getInt(s);
```

