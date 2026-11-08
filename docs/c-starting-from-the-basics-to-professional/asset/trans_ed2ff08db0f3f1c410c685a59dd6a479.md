
```cpp
std::cout << "The number nearest to " << number_to_search_for << " is "
          << *std::min_element(begin(numbers), end(numbers), nearer) << std::endl;
std::cout << "The number furthest from " << number_to_search_for << " is "
          << *std::max_element(begin(numbers), end(numbers), nearer) << std::endl;
}
```

从这个示例中首先注意到的是，对于 `min_element()` 和 `max_element()`，比较回调函数是可选的。两者都提供了一个不带第三个参数的重载——这两个重载都使用小于运算符 `<` 来比较元素。除此之外，这些标准算法当然完全符合你的预期：

```text
Minimum element: 13
Maximum element: 92
Please enter a number: 42
The number nearest to 42 is 43
The number furthest from 42 is 92
```

**提示** `<algorithm>` 模块还提供了 `std::minmax_element()`，你可以用它一次性获取给定范围内的最小和最大元素。该算法返回一个 `pair<>` 迭代器对，具有预期的语义。因此，你可以将 Ex20_11 中的最后两条语句替换为：

```cpp
const auto [nearest, furthest] =
    std::minmax_element(begin(numbers), end(numbers), nearer);
std::cout << "The number nearest to " << number_to_search_for << " is "
          << *nearest << std::endl;
std::cout << "The number furthest from " << number_to_search_for << " is "
          << *furthest << std::endl;
```

关于 `pair<>` 模板和 `auto []` 语法的介绍，请参阅本章前面的内容。

## 查找元素

标准库提供了多种算法，用于在元素范围内搜索元素。在上一小节中，我们介绍了 `min_element()`、`max_element()` 和 `minmax_element()`。你可能最常使用的两个相关算法是 `std::find()` 和 `find_if()`。第一个是 `std::find()`，用于在范围内搜索等于给定值的元素（它使用 `==` 运算符比较值）。第二个是 `find_if()`，它则期望将一等回调函数作为参数。它使用这个回调函数来判断任意给定元素是否满足所需特征。

为了试用它们，让我们回顾一个以前常用的类：Box 类。因为 `std::find()` 需要比较两个 Box，所以你需要一个重载了 `operator==()` 的 Box 变体。例如，Ex13_03 中的 box 模块就完全够用：

```cpp
// Ex20_12.cpp - Finding boxes.
import <iostream>;
import <vector>;
import <algorithm>;
import box;      // From Ex13_03

int main()
{
    std::vector<Box> boxes{ Box{1,2,3}, Box{5,2,3}, Box{9,2,1}, Box{3,2,1} };

    // Define a lambda function to print the result of find() or find_if():
    auto print_result = [&](auto result) {
        if (result == end(boxes))
            std::cout << "No box found." << std::endl;
        else
            std::cout << "Found matching box at position "
                      << (result - begin(boxes)) << std::endl;
    };

    // Find an exact box
    Box box_to_find{3,2,1};
    auto result{ std::find(begin(boxes), end(boxes), box_to_find) };
    print_result(result);

    // Find a box with a volume larger than that of box_to_find
    const auto required_volume = box_to_find.volume();
    result = std::find_if(begin(boxes), end(boxes),
                          [required_volume](const Box& box) { return box > required_volume; });
    print_result(result);
}
```

输出如下：

```text
Found matching box at position 3
Found matching box at position 1
```

find() 和 find_if() 要么返回指向找到的元素的迭代器，要么在未找到符合搜索条件的元素时返回该范围的结束迭代器。

> **注意** 如果未找到元素，返回的是要搜索范围的结束迭代器，而不是容器的结束迭代器。尽管在许多情况下两者相同（在 Ex20_12 中就是如此），但这并不总是成立。

标准提供了许多变体。下面的列表展示了其中几个。更多细节请查阅标准库参考。

- `find_if_not()` 与 `find_if()` 类似，只是它搜索给定回调函数返回 false（而不是 true）的第一个元素。
- `find_first_of()` 在元素范围中搜索第一个与另一个给定范围中任意元素匹配的元素。
- `adjacent_find()` 搜索两个相等或满足给定谓词的连续元素。
- `search()` / `find_end()` 在另一个元素范围中搜索一个元素范围。前者返回第一个匹配项，后者返回最后一个匹配项。
- `binary_search()` 检查给定元素是否存在于已排序范围中。通过利用输入范围中元素已排序这一事实，它可以比 `find()` 更快地找到所需元素。元素使用 `<` 运算符或用户提供的比较回调进行比较。

> **注意** 在本章前面，我们解释过，set 和 map 容器本身已经非常擅长查找元素。因为它们了解自己数据的内部结构，所以查找元素的速度比任何泛型算法都快得多。因此，这些容器提供了一个 `find()` 成员函数，你应该始终使用它，而不是泛型 `std::find()` 算法。一般来说，只要容器提供了在功能上等价于某个算法的成员函数，你就应该始终使用前者。

## 处理多个输出值

`find()`、`find_if()`、`find_if_not()`——这三个算法都搜索满足特定要求的第一个元素。但如果你想要找出全部符合条件的元素，而不是只找第一个，该怎么办呢？如果你浏览标准库提供的所有算法，你会发现没有名为 `find_all()` 这样的算法。幸运的是，至少有三个算法可以让你获取给定范围内满足给定条件的所有元素：

- `std::remove_if()` 可用于移除所有不满足条件的元素。我们将在下一小节讨论这个算法。
- `std::partition()` 会重新排列范围内的元素，使满足回调条件的元素移到范围前面，不满足的移到后面。我们会把这一选项留给你在后面的练习中尝试。
- `std::copy_if()` 可用于将所有需要的元素复制到第二个输出范围。

```cpp
// Ex20_13.cpp — Extracting all odd numbers.
import <iostream>;
import <set>;
import <vector>;
import <algorithm>;

std::set<int> fillSet_intoN(size_t N);       // Fill a set with 1, 2, ..., N
void printVector(const std::vector<int>& v); // Print the contents of a vector to std::cout

int main()
{
    const size_t num_numbers{20};

    const auto numbers = fillSet_intoN(num_numbers);

    std::vector<int> odd_numbers( numbers.size() ); // Caution: not { numbers.size() } here!

    auto end_odd_numbers = std::copy_if(begin(numbers), end(numbers), begin(odd_numbers),
                                        [](int n) { return n % 2 == 1; });
    odd_numbers.erase(end_odd_numbers, end(odd_numbers));

    printVector(odd_numbers);
}
```

你可以复用 Ex20_09 中的 printVector() 函数，而 fillSet_intoN() 类似于 Ex20_10 中的 fillVector_intoN() 函数。现在编写这两个函数应该是常规操作了。

相反，让我们把注意力集中在程序中关键的三行代码上：也就是将所有奇数从 numbers 复制到 odd_numbers 的那几行。std::copy_if() 的前两个参数是所谓的输入迭代器。它们确定可能需要复制的元素范围。然后，第四个参数中的回调函数决定这些元素中哪些会被实际复制。不过，这里特别值得注意的是 copy_if() 的第三个参数。这是你看到的第一个输出迭代器的示例——输出迭代器决定算法将输出写入何处。它的工作方式最好通过一些代码来解释。将所有函数调用（包括 lambda 表达式的调用）内联后，Ex20_13 中的 copy_if() 语句的作用如下：

```cpp
auto output_iter = begin(odd_numbers);
for (auto input_iter = begin(numbers); input_iter != end(numbers); ++input_iter)
    if (*input_iter % 2 == 1)
        *output_iter++ = *input_iter;        // <- working of an output iterator
// return output_iter;
auto end_odd_numbers = output_iter;
```

算法必须输出的每个元素都会被赋给输出迭代器当时指向的位置。记住：解引用迭代器会得到一个（值）引用。在我们的示例中，这意味着表达式 *output_iter 的类型是 int&。每次赋值后，输出迭代器都会递增，以便准备接收下一个输出。

如果使用普通输出迭代器，那么目标范围——Ex20_13 中的 vector<> odd_numbers——必须足够大，以容纳算法将输出的所有元素，这一点至关重要。因为你并不总是事先知道将有多少个元素，所以你可能被迫分配比所需更大的内存缓冲区。你在 Ex20_13 中也会看到这一点：odd_numbers 用一个包含 numbers.size() 个元素（全为零）的动态数组初始化。由于这个数组大到足以容纳所有 numbers，它肯定也大到足以容纳所有奇数。但当然，结果它会比实际所需的大一倍。为此，std::copy_if() 算法返回一个指向输出范围的迭代器，它指向最后被复制元素之后的位置。你可以使用这个迭代器从目标容器中删除所有多余元素，就像 Ex20_13 中所做的那样。

> **注意** 注意不要忘记调用 erase() 时的第二个参数！它必须是容器的结束迭代器。如果忘记这个第二个参数，erase() 只会删除作为第一个参数传入的迭代器所指向的单个元素。（换句话说，在 Ex20_13 中，odd_numbers 中只会删除原始零中的一个！）

许多算法会以类似于 std::copy_if() 的方式将输出复制或移动到目标范围（std::copy()、move()、replace_copy()、replace_copy_if()、remove_copy()——这样的例子还有很多……）。因此，原则上它们都可以使用相同的模式：保守地分配一个过大的目标范围，然后使用算法返回的迭代器将其缩小到合适的大小。
