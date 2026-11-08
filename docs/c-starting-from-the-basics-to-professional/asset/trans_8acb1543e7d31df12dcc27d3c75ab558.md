
下面的示例将我们刚刚开发的 removeEvenNumbers() 模板拿来试用一番。尽管它使用的是 vector<int> 容器，但我们也可以使用前面提到的任意类型：

```cpp
// Ex20_10.cpp
// Removing all elements that satisfy a certain condition
// while iterating over a container
import <vector>;
import <string_view>;
import <iostream>;

std::vector<int> fillVector_1toN(size_t N);   // Fill a vector with 1, 2, ..., N
void printVector(std::string_view message, const std::vector<int>& numbers);
void removeEvenNumbers(auto& numbers);

int main()
{
  const size_t num_numbers{20};

  auto numbers{ fillVector_1toN(num_numbers) };

  printVector("The original set of numbers", numbers);

  removeEvenNumbers(numbers);

  printVector("The numbers that were kept", numbers);
}

std::vector<int> fillVector_1toN(size_t N)
{
  std::vector<int> numbers;
  for (int i{1}; i <= N; ++i)
    numbers.push_back(i);
  return numbers;
}

void printVector(std::string_view message, const std::vector<int>& numbers)
{
  std::cout << message << ": ";
  for (int number : numbers) std::cout << number << ' ';
  std::cout << std::endl;
}
```

当然，这个程序的输出如下：

```text
The original set of numbers: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
The numbers that were kept: 1 3 5 7 9 11 13 15 17 19
```

## 数组的迭代器

迭代器的行为与指针完全一样——以至于任何指针也都是有效的迭代器。更准确地说，任何原始指针都可以充当随机访问迭代器。这一观察将使我们下一节讨论的泛型算法模板既能遍历数组，也能遍历容器。事实上，数组指针可以用在任何原本会使用迭代器的上下文中。回顾 Ex20_09 中的以下语句：

```cpp
std::vector more_numbers{ 6, 7, 8 };
numbers.insert(numbers.end(), more_numbers.begin(), more_numbers.end());
```

现在假设 more_numbers 变量改为定义为内置数组。那么追加这些数字的一种方式是利用数组-指针二元性，并结合指针算术和 std::size() 函数，如第 5 章所介绍：

```cpp
int more_numbers[]{ 6, 7, 8 };
numbers.insert(numbers.end(), more_numbers, more_numbers + std::size(more_numbers));
```

虽然这完全可行，但还有一种更优雅、更统一的方式。为此，你可以使用标准库 <iterator> 模块中定义的 std::begin() 和 std::end() 函数模板：

```cpp
int more_numbers[]{ 6, 7, 8 };
numbers.insert(numbers.end(), std::begin(more_numbers), std::end(more_numbers));
```

这些函数模板不仅适用于数组，也适用于任何容器：

```cpp
std::vector more_numbers{ 6, 7, 8 };
numbers.insert(std::end(numbers), std::begin(more_numbers), std::end(more_numbers));
```

当用于容器时，得益于 C++ 中非成员函数的名称解析方式，你甚至不必显式指定 std:: 命名空间：

```cpp
std::vector more_numbers{ 6, 7, 8 };
numbers.insert(end(numbers), begin(more_numbers), end(more_numbers));
```

毫不意外，也存在 cbegin() 和 cend() 非成员函数，它们会为数组或容器创建相应的 const 迭代器：

```cpp
std::vector more_numbers{ 6, 7, 8 };
int even_more_numbers[]{ 9, 10 };
numbers.insert(end(numbers), cbegin(more_numbers), cend(more_numbers));
numbers.insert(end(numbers), std::cbegin(even_more_numbers), std::cend(even_more_numbers));
```

这种语法的简洁性和统一性使其成为本章其余部分中我们首选的指定范围的方式。不过，对于容器改用 (c)begin() 和 (c)end() 成员函数也没有任何问题。

## 算法

标准库的泛型算法结合了本书前面探讨过的各种概念的优势，例如函数模板（第 10 章）、一等函数和高阶函数（第 19 章），当然还有迭代器（本章前面）。你会发现，这些算法与 C++11 的 lambda 表达式（第 19 章）结合使用时尤其强大且富有表现力。

> **注意** 标准库的 `<algorithm>` 和 `<numeric>` 模块合起来提供了远超过 100 个算法，远超我们在这里能够覆盖的范围。因此，我们专注于最常用的算法（本节以及章末练习中），以及在许多算法中反复出现的常见模式。一旦掌握了这些，使用其他算法几乎总是类似的。我们建议你之后浏览一份标准库参考，以了解有哪些可用算法。

> **注意** 在本节中，我们首先介绍传统的*基于迭代器对的算法*。从 C++20 起，我们预计这些算法将逐步被淘汰，并由本章最后一节介绍的、功能等价的*基于范围的算法*取代。不过，基于迭代器的算法在未来一段时间内仍将在遗留代码中随处可见。

### 第一个示例

第 19 章定义的一些高阶函数实际上已经接近一些标准算法。还记得 `findOptimum()` 模板吗？它看起来如下：

```cpp
template <typename T, typename Comparison>
const T* findOptimum(const std::vector<T>& values, Comparison compare)
{
    if (values.empty()) return nullptr;

    const T* optimum = &values[0];
    for (size_t i{1}; i < values.size(); ++i)
    {
        if (compare(values[i], *optimum))
        {
            optimum = &values[i];
        }
    }
    return optimum;
}
```

尽管这个模板已经相当通用，但它仍有两个不幸的局限：

- 它只适用于存储在 `vector<T>` 类型容器中的元素。
- 它只适用于你想考虑给定集合的所有元素的情况。若只想考虑这些元素的一个子集，目前还无法做到，除非先把它们全部复制到一个新容器中。

通过使用迭代器进一步泛化这个模板，你可以相当轻松地解决这两个缺点：

```cpp
template <typename Iterator, typename Comparison>
Iterator findOptimum(Iterator begin, Iterator end, Comparison compare)
{
    if (begin == end) return end;

    Iterator optimum = begin;
    for (Iterator iter = ++begin; iter != end; ++iter)
    {
        if (compare(*iter, *optimum))
        {
            optimum = iter;
        }
    }
    return optimum;
}
```

这个新版本不再有上述两个问题：

- 迭代器可用于遍历所有容器类型和数组类型的元素。
- 新模板可以轻松处理子范围，只需传入完整 `[begin(), end())` 迭代器范围的一部分即可。

`<algorithm>` 模块实际上提供了一个完全像这样的算法。只不过它不叫 `findOptimum()`，而叫 `std::max_element()`。既然有 `max_element()`，当然也就有 `min_element()`。让我们通过调整上一章的一些示例来看看它们两者的实际应用：

```cpp
// Ex20_11.cpp
// Your first algorithms: std::min_element() and max_element()
#include <cmath>    // For std::abs
import <string>;
import <algorithm>;
import <vector>;

int main()
{
    std::vector numbers{ 91, 18, 92, 22, 13, 43 };
    std::cout << "Minimum element: "
              << *std::min_element(begin(numbers), end(numbers)) << std::endl;
    std::cout << "Maximum element: "
              << *std::max_element(begin(numbers), end(numbers)) << std::endl;

    int number_to_search_for {};
    std::cout << "Please enter a number: ";
    std::cin >> number_to_search_for;

    auto nearer { [=](int x, int y) {
        return std::abs(x - number_to_search_for) < std::abs(y - number_to_search_for);
    } };
```
