
该 sort 应使用 sort 定义中指定的默认二元谓词函数——即 `std::ranges::less`。这会使 sort 将元素按升序排列。less 函数对象比较它的两个参数，如果第一个小于第二个则返回 true。如果 less 返回 false，则这两个工资不满足升序，因此 sort 会重新排列相应的 Employee 对象。

- 最后一个参数指定 **投影**。这个一元函数接收范围中的一个元素，并返回该元素的一部分。这里，我们将该一元函数实现为一个 lambda，它返回其 Employee 参数的工资。**投影** 在 sort 比较元素 *之前* 应用，因此 sort 不是比较整个 Employee 对象来确定排序顺序，而是只比较 Employees 的工资。

```cpp
// sort Employees by salary; {} indicates that the algorithm should
// use its default comparison function.
std::ranges::sort(employees, {},
    [](const auto& e) { return e.getSalary(); });
std::cout << "\nEmployees sorted in ascending order by salary:\n";
std::ranges::copy(employees, output);
```

```text
Employees sorted in ascending order by salary:
Makaya   Titania  3587
Wu       Joo-won  5000
Jones    Amaia    7600
```

### 投影的简写表示法

我们可以用简写表示法替换第 46 行中作为 lambda 实现的一元函数

```cpp
&Employee::getSalary
```

这会创建一个指向 Employee 类的 getSalary 成员函数的指针，将第 45–46 行缩短为

```cpp
std::ranges::sort(employees, {}, &Employee::getSalary);
```

要作为投影使用，该成员函数必须是 public 的，且不能被重载。此外，它必须没有参数，因为 `std::ranges` 算法无法接收额外参数来传递给投影中指定的成员函数。³²

### 投影可以是指向 public 数据成员的指针

如果类有一个 public 数据成员，你可以将指向它的指针作为投影参数传递。例如，如果我们的 Employee 类有一个名为 salary 的 public 数据成员，我们可以将 sort 的投影参数指定为

```cpp
&Employee::salary
```

32. “在底层”，`std::ranges::sort` 使用 `std::invoke` 函数（头文件 `<functional>`）对每个 Employee 对象调用所提供的比较器。

### 使用投影按降序对 array<Employee> 排序

在像 sort 这样带有函数参数的算法中，你可以组合自定义函数和投影。例如，第 51–52 行同时指定了一个二元谓词函数对象和一个投影，以按工资降序对 Employees 排序。同样，我们传递三个参数：

- 第一个参数（`employees`）是要排序的范围。
- 第二个参数创建一个 `std::ranges::greater` 函数对象。这会使 `sort` 将元素按降序排列。greater 函数对象比较它的两个参数，如果第一个大于第二个则返回 true。如果 greater 返回 false，则这两个工资不满足降序，因此 sort 会重新排列相应的 Employee 对象。
- 最后一个参数是投影。在此调用中，`std::ranges::greater` 将比较 Employees 的 int 工资以确定排序顺序。

```cpp
// sort Employees by salary in descending order
std::ranges::sort(employees, std::ranges::greater{},
    &Employee::getSalary);
std::cout << "\nEmployees sorted in descending order by salary:\n";
std::ranges::copy(employees, output);
}
```

```text
Employees sorted in descending order by salary:
Jones    Anuja    7600
Wu       Joo-won  5000
Makaya   Titania  3587
```

## 14.7 C++20 视图与函数式编程

在 6.14.3 节中，我们展示了视图对范围执行操作。我们展示了视图是可组合的，因此你可以将它们链接起来，通过一条操作流水线处理范围的元素。视图并不拥有范围元素的副本——它只是让元素通过一条操作流水线。视图是 C++20 的关键函数式编程能力之一。

到目前为止，本章介绍的算法都是贪婪的——当你调用一个算法时，它会立即执行其指定的任务。你在 6.14.3 节中看到，视图是惰性的——直到你在循环中遍历它们，或将它们传递给会遍历它们的算法时，它们才产生结果。正如我们在 6.14.3 节中讨论的，惰性求值按需产生值，当不需要一次获得所有值时，这可以减少程序的内存消耗并提高性能。

### 14.7.1 范围适配器

6.14.3 节还演示了使用以下内容进行函数式风格的 filter 和 map 操作：

- `std::views::filter` 仅保留谓词函数返回 true 的视图元素，以及
- `std::views::transform` 将每个视图元素映射为新值，新值的类型可能不同。

这些就是范围适配器。视图就像一扇窗口，使你能够“看到”某个范围并观察其元素——视图并不拥有这些元素的副本。每个范围适配器接收一个 `std::ranges::viewable_range` 作为参数，并返回该范围的一个视图，以便在操作流水线中使用（在 6.14 节中介绍）。`viewable_range` 是能够“安全转换为视图”的范围。³³ 由于视图不拥有它们所“看到”的数据，因此临时对象不能转换为 `viewable_range`。

下表列出了许多 C++20 范围适配器（头文件 `<ranges>`），³⁴ 它们支持 **函数式编程**（在 6.14 节中介绍）。**范围适配器** 定义在命名空间 `std::ranges::views` 中，通常通过别名 `std::views` 访问。

| 范围适配器 | 描述 |
|---|---|
| `filter` | 创建一个视图，仅表示 **谓词** 返回 true 的范围元素。 |
| `transform` | 创建一个将元素映射为新值的视图。 |
| `common` | 用于将视图转换为 `std::ranges::common_range`，这使范围可用于要求同类型 begin/end 迭代器对的 common-range 算法。 |
| `all` | 创建一个表示范围所有元素的视图。 |
| `counted` | 创建一个视图，包含从范围开头或从特定迭代器位置开始的指定数量的元素。 |
| `reverse` | 创建一个用于按相反顺序处理双向视图的视图。 |
| `drop` | 创建一个视图，忽略另一个视图开头的指定数量的元素。 |
| `drop_while` | 创建一个视图，只要谓词返回 true，就忽略另一个视图开头的元素。 |
| `take` | 创建一个视图，包含另一个视图开头的指定数量的元素。 |
| `take_while` | 创建一个视图，只要谓词返回 true，就包含另一个视图开头的元素。 |
| `join` | 创建一个合并多个范围元素的视图。 |
| `split` | 基于分隔符拆分视图。新视图为每个子范围包含一个单独的视图。 |
| `keys` | 创建一个键值对中键的视图，例如 map 中的键值对。键是键值对中的第一个元素。 |
| `values` | 创建一个键值对中值的视图，例如 map 中的键值对。值是键值对中的第二个元素。 |
| `elements` | 对于包含 tuple、pair 或 array 的视图，创建一个由每个对象中指定索引处的元素组成的视图。 |

33. “`std::ranges::viewable_range`。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/ranges/viewable_range

34. “Ranges Library。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/ranges。

### 14.7.2 使用范围适配器和视图

图 14.18 演示了上表中的几个 `std::views`，并介绍了 `std::views::iota` 的无限版本。第 13 行定义了一个 lambda，如果其参数是偶数整数则返回 true。我们将在流水线中使用这个 lambda。

```cpp
// fig14_18.cpp
// Working with C++20 std::views.
#include <algorithm>
#include <iostream>
#include <iterator>
#include <map>
#include <ranges>
#include <string>
#include <vector>

int main() {
    std::ostream_iterator<int> output{std::cout, " "};
    auto isEven{[](int x) { return x % 2 == 0; }}; // true if x is even
```

**图 14.18** | 使用 C++20 `std::views`。

### 使用 `std::views::iota` 创建无限范围

在图 6.13 中，我们介绍了 `std::views::iota`，它被称为范围工厂——它是一个视图，当你遍历它时，会惰性地创建一连串连续整数。图 6.13 中的 `iota` 版本需要两个参数——起始整数值，以及 `iota` 应生成的序列末尾之后的值。第 16 行使用 `iota` 的无限范围版本，它只接收序列中的起始整数（0），并将其递增 1，直到你告诉它停止——你马上就会看到如何做到。第 16 行中的流水线创建一个视图，过滤 `iota` 生成的整数，仅保留 lambda `isEven` 返回 true 的整数。此时，尚未生成任何整数。同样，视图是惰性的——直到你用循环或标准库算法遍历它们时，它们才会执行。视图是可以存储在变量中的对象，因此你可以复用它们的处理步骤，甚至以后添加更多处理步骤。我们将这个视图存储在 `evens` 中，甚至将用它来构建几个增强的流水线。

```cpp
// infinite view of even integers starting at 0
auto evens{std::views::iota(0) | std::views::filter(isEven)};
```

### take 范围适配器

尽管无限范围在逻辑上是无限的，³⁵ 但要在循环中处理它，或将它传递给标准库算法，你必须限制流水线将产生的元素数量；否则，你的程序将包含无限循环。做到这一点的一种方法是使用限制要处理元素数量的范围适配器。此类适配器可与
