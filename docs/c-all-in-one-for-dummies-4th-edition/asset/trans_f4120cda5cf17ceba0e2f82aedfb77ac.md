
| predicate | regular | regular_invocable |
| --- | --- | --- |
| relation | same_as | semiregular |
| signed_integral | strict_weak_order | swappable |
| swappable_with | totally_ordered | totally_ordered_with |
| unsigned_integral |  |  |

## 容器

容器的工作方式就像你家中的容器——它们用来盛放东西。你在本书其他部分已经见过容器发挥作用。例如，队列和双端队列都是容器。Containers 类别不包含任何函数，但确实包含若干类型，包括下表中列出的类型（已移除一些类型，因为 C++11 及更高版本不出现在列表中，即使你可以在较旧版本的 C++ 中使用它们）。

| array（C++11 及以上） | deque | forward_list（C++11 及以上） |
| --- | --- | --- |
| list | map | queue |
| set | span（C++20 及以上） | stack |
| unordered_map（C++11 及以上） | unordered_set（C++11 及以上） | vector |

## 协程

协程是 C++20 中的一项新特性，它允许函数暂停执行并在稍后恢复任务。该函数将恢复任务所需的数据单独存储，而不是存储在栈上。此特性有助于支持异步执行的顺序代码，例如非阻塞 I/O，而无需使用回调。你可以在 https://blog.panicsoftware.com/your-first-coroutine/ 找到协程示例。下表包含 Coroutines 类别的类。

| coroutine_handle | coroutine_traits | noop_coroutine_handle |
| --- | --- | --- |
| noop_coroutine_promise | std::hash<std::coroutine_handle> | suspend_always |
| suspend_never |  |  |

Iterators 类别包含许多类。这些类决定你在代码中创建的迭代器种类以及该迭代器的能力。以下是迭代器类的列表（自 C++11 及更高版本起已移除的类不会出现在列表中，即使你可以在较旧版本的 C++ 中使用它们）：

|  |  |  |
| --- | --- | --- |
| `back_insert_iterator` | `bidirectional_iterator`（在 C++20 及更高版本中作为概念处理） | `bidirectional_iterator_tag` |
| `common_iterator`（C++20 及以上） | `contiguous_iterator_tag`（C++20 及以上） | `counted_iterator`（C++20 及以上） |
| `default_sentinel`（C++20 及以上） | `forward_iterator`（在 C++20 及更高版本中作为概念处理） | `forward_iterator_tag` |
| `front_insert_iterator` | `incrementable_traits`（C++20 及以上） | `indirect_result_t`（C++20 及以上） |
| `indirectly_readable_traits`（C++20 及以上） | `input_iterator`（在 C++20 及更高版本中作为概念处理） | `input_iterator_tag` |
| `insert_iterator` | `istream_iterator` | `istreambuf_iterator` |
| `iter_common_reference_t`（C++20 及以上） | `iter_difference_t`（C++20 及以上） | `iter_move`（C++20 及以上） |
| `iter_reference_t`（C++20 及以上） | `iter_rvalue_reference_t`（C++20 及以上） | `iter_swap`（C++20 及以上） |
| `iter_value_t`（C++20 及以上） | `iterator`（C++17 中已弃用） | `iterator_traits` |
| `move_iterator`（C++11 及以上） | `move_sentinel`（C++20 及以上） | `ostream_iterator` |
| `ostreambuf_iterator` | `output_iterator`（在 C++20 及更高版本中作为概念处理） | `output_iterator_tag` |
| `projected`（C++20 及以上） | `random_access_iterator`（在 C++20 及更高版本中作为概念处理） | `random_access_iterator_tag` |
| `reverse_iterator` | `unreachable_sentinel_t`（C++20 及以上） |  |

使用 abs 函数求一个数的绝对值。下表列出 Numerics 类别的头文件。

| 头文件 | C++ 版本 | 简短说明 |
| --- | --- | --- |
| `<bit>` | C++20 及以上 | 位操作 |
| `<cfenv>` | C++11 及以上 | 浮点环境访问 |
| `<cmath>` |  | 常见数学函数 |
| `<complex>` |  | 复数运算 |
| `<numbers>` | C++20 及以上 | 数学常量 |
| `<numeric>` |  | 对范围内值的操作 |
| `<random>` | C++11 及以上 | 随机数生成 |
| `<ratio>` | C++11 及以上 | 编译时有理数数学 |
| `<valarray>` |  | 与值数组交互 |

## 范围

能够高效地处理值范围，对于减少你编写的代码量并确保你编写的代码易于理解很重要。大多数现代语言都提供处理值范围的快捷方式，而 C++20 标准将这一功能添加到 C++ 中。

![](img/128ab511de4e7360e167e3b15cdd5dd0_783_0.png)

不幸的是，截至撰写本文时，还没有主流编译器或库真正实现此功能，因此你需要下载并安装 range-v3 库（https://github.com/ericniebler/range-v3/）才能实际使用它。该库是 C++20 中范围支持的基础。（使用该库超出本书范围；但是，你可以在 https://ericniebler.github.io/range-v3/ 找到其文档。）

这个特定类别旨在与视图一起工作，视图描述你希望作为输出看到的内容。例如，如果你想按相反顺序对范围排序，你可以提供一个描述此需求的视图，例如 `views::reverse(v)`，其中 v 是包含你想与之交互的范围的 vector。排序可能看起来像 `ranges::sort(views::reverse(v));`。

范围也与概念一起工作，本章“概念”一节对此进行了描述。概念定义你处理的范围的种类。下表列出范围概念。

|  |  |  |
| --- | --- | --- |
| `bidirectional_range` | `common_range` | `contiguous_range` |
| `forward_range` | `input_range` | `output_range` |
| `random_access_range` | `range` | `sized_range` |
| `view` | `viewable_range` |  |

在你有了一个范围、一个关于希望如何查看它的想法以及一个目标任务之后，你可以使用 `<ranges>` 头文件中的各种类来执行工作。下表显示与该头文件标准相关的类。

|  |  |  |
| --- | --- | --- |
| `borrowed_iterator_t` | `borrowed_subrange_t` | `dangling` |
| `iterator_t` | `range_difference_t` | `range_reference_t` |
| `range_value_t`<br>`reference_t` | `range_size_t` | `range_value_t` |
| `ref_view` | `sentinel_t` | `subrange` |
| `view_interface` | `views::all` | `views::all_t` |
| `views::common`<br>`(common_view)` | `views::counted` | `views::empty`<br>`(empty_view)` |
| `views::filter`<br>`(filter_view)` | `views::iota(iota_view)` | `views::join`<br>`(join_view)` |
| `views::reverse`<br>`(reverse_view)` | `views::single`<br>`(single_view)` | `views::split`<br>`(split_view)` |
| `views::take`<br>`(take_view)` | `views::transform`<br>`(transform_view)` |  |

你还可以使用定制点对象来自定义范围的工作方式。下表列出在 `std::ranges` 命名空间中找到的这些对象。

|  |  |  |
| --- | --- | --- |
| `ranges::begin` | `ranges::data` | `ranges::empty` |
| `ranges::end` | `ranges::rbegin` | `ranges::rend` |
| `ranges::size` |  |  |

![](img/128ab511de4e7360e167e3b15cdd5dd0_784_0.png)

## 正则表达式

正则表达式支持出现在 C++11 及更高版本中。它帮助你在字符串中查找模式。例如，你可以在某人将电子邮件地址和电话号码输入数据库之前，确保它们格式正确，从而在此过程中减少一些数据错误。你还可以使用正则表达式执行搜索和替换操作。下表包含 Regular Expression 类别的类。

|  |  |  |
| --- | --- | --- |
| basic_regex | match_results | regex_error |
| regex_iterator | regex_token_iterator | regex_traits |
| sub_match |  |  |

## 字符串

Strings 类别为 C++ 中的字符串提供广泛支持。你在本书中已经见过许多使用 `<string>` 头文件（最常用的头文件）的示例。人类很容易理解字符串，但计算机把字符——因而也把字符串——当作数字来处理。为了让字符串更易于使用，你需要库支持。下表列出 String 类别的头文件及其用途。

| 头文件 | C++ 版本 | 简短说明 |
| --- | --- | --- |
| `<cctype>` |  | 判断窄字符（char）的类别。 |
| `<charconv>` | C++17 及以上 | 与字符相互转换。 |
| `<cstring>` |  | 窄字符串处理函数。 |
| `<cuchar>` | C++11 及以上 | C 风格 Unicode 字符转换函数。 |
| `<cwchar>` |  | 宽字符和多字节字符字符串处理函数。 |
| `<cwctype>` |  | 判断宽字符（wchar_t）的类别。 |
| `<format>` | C++20 及以上 | 字符串格式化功能。 |
| `<string_view>` | C++17 及以上 | 基本字符串视图处理类。 |
| `<string>` |  | 基本字符串处理类。 |
