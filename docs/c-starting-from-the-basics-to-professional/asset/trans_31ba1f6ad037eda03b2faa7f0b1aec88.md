
## 第 9 章：词汇类型

有些数据类型会像 int 或 double 这样的基本类型一样，成为你日常词汇的一部分。你会在所有地方、所有时间使用它们：在函数签名中、在算法中、作为类的成员变量（见后文）等等。我们称这样的类型为词汇类型。在现代 C++ 中，它们是可理解、可维护且安全代码的基石之一。

事实上，你已经知道一些词汇类型：std::unique_ptr<>、std::shared_ptr<>、std::string、std::array<>、std::vector<> 等。到目前为止，这些类型有一个共同点：它们取代了核心语言中某些不安全且不方便的类型（原始指针、const char* 字符串、底层动态内存等）。本章介绍的三个词汇类型类似，但存在理由略有不同：它们旨在让你的代码更具自文档性、更高效、重复更少。

在本章中，你将学习

-   如何最好地为函数定义可选输入
-   如何定义可能返回、也可能不返回值的函数，这取决于其输入或应用程序的当前状态
-   如何最好地定义接受字符串但不修改字符串的函数
-   如何定义一个单一函数，使其能操作你传入的任何顺序范围，无论是 C 风格数组、vector 还是任何其他顺序容器

### 处理可选值

在编写自己的函数时，你经常会遇到可选输入参数，或者只有在一切顺利时才能返回值的函数。考虑以下示例：

```cpp
int find_last(const std::string& s, char char_to_find, int start_index);
```

从这个原型中，你可以想象 find_last() 函数从给定起始索引开始，从后向前在给定字符串中搜索给定字符。一旦找到，它就会返回该字符最后一次出现的索引。但如果该字符没有出现在字符串中呢？如果你希望算法考虑整个字符串呢？如果传入 -1 作为第三个参数，它或许能工作吗？遗憾的是，如果没有接口文档，或者不查看实现代码，就无法知道这个函数会如何表现。

一种传统解决方案是挑选某个或某些特定值，供调用者在希望函数使用默认设置时使用，或在无法计算出实际值时作为返回值。对于数组或字符串索引，典型选择是 -1。因此，find_last() 的一种可能规范是：如果 char_to_find 未出现在给定字符串中，则返回 -1；如果传入 -1 或任何负值作为 start_index，则搜索整个字符串。事实上，std::string 自己的 find() 函数就使用了这种确切技术；只不过它使用的不是 -1，而是常量 std::string::npos（size_t 是无符号类型，因此 -1 不是有效值）。

问题在于，一般来说，很难记住每个函数如何编码“未提供输入”或“未计算结果”。不同库之间，甚至同一库内部，约定往往不同。有些在失败时返回 0，另一些返回负数。有些接受 nullptr 作为输入，另一些则不接受。诸如此类。

为了帮助函数的使用者，可选参数通常会给定一个有效的默认值。下面是一个示例：

```cpp
int find_last(const std::string& s, char char_to_find, int start_index = -1);
```

然而，这种技术并不能扩展到返回值。另一个问题是，一般来说，甚至可能没有一种明显的方式来编码可选值。第一个原因可能是可选值的类型。想一想：例如，你会如何编码一个可选的 bool？第二个原因可能是具体情境。例如，假设你需要定义一个函数来读取某个配置文件。那么你可能会定义如下形式的函数：

```cpp
// Return the 'default' value provided by the caller if the setting is not found
int read_int_setting(const string& file, const string& settingName, int defaultValue);

// Output setting in output parameter and return true if found; return false otherwise
bool read_int_setting(const string& file, const string& settingName, int& output);
```

但是，如果配置文件中不包含具有给定名称的设置项，应该发生什么？由于这打算作为一个通用函数，你不能先验地假定 0、-1 或任何其他 int 值不是所请求设置项的有效值。传统的变通方法包括以下这些：

```cpp
// Return the 'default' value provided by the caller if the setting is not found
int read_int_setting(const string& file, const string& settingName, int defaultValue);

// Output setting in output parameter and return true if found; return false otherwise
bool read_int_setting(const string& file, const string& settingName, int& output);
```

虽然这些方法可行，但 C++ 标准库提供了更好的替代方案：std::optional<>。这个词汇类型会让你的函数声明更简洁、更易读。

> **注意** 词汇类型，尤其是 std::optional<>，在本书后半部分定义你自己的类时同样有用。例如，Car 对象可以有一个 optional<SpareTire>，Person 可以有一个用于中间名的 optional<string>，或者 Boat 可以有一个 optional<Engine>。不过目前，我们只会用函数来示例这些新的词汇类型。

### std::optional

从 C++17 起，标准库提供了 `std::optional<>`，旨在取代我们前面展示的所有可选值的隐式编码。使用这个词汇类型，任何可选输入或输出都可以用 `std::optional<>` 显式声明，如下所示：

```cpp
std::optional<int> find_last(const std::string& s, char c, std::optional<int> startIndex);
std::optional<int> read_int_setting(const std::string& file, const std::string& setting);
```

现在，所有可选输入和输出都在函数原型中、在代码层面被显式标记出来。不再需要额外文档，也不需要查看实现来知道什么是可选的。结果是干净、自文档化的函数声明。你的代码会立刻变得更容易理解和使用。

> **注意** `std::optional<>` 是一个类模板，就像 `std::vector<>` 和 `std::array<>` 一样。你可以用任意类型 T 实例化它，从而得到该类型的一个新的可选版本。你稍后会学习如何创建自己的类模板，但使用类模板应该不再有任何问题。

让我们看一些真实代码中 `std::optional<>` 的基本用法：

```cpp
// Ex_01.cpp
// Working with std::optional<>
import <optional>;     // std::optional<> is defined in the <optional> module
import <iostream>;
import <string>;

std::optional<size_t> find_last(
    const std::string& string, char to_find,
    std::optional<size_t> start_index = std::nullopt); // Or ... start_index = {};

int main()
{
    const auto string = "Growing old is mandatory; growing up is optional.";

    const std::optional<size_t> found_a{ find_last(string, 'a') };
    if (found_a)
        std::cout << "Found the last a at index " << *found_a << std::endl;

    const auto found_b{ find_last(string, 'b') };
    if (found_b.has_value())
        std::cout << "Found the last b at index " << found_b.value() << std::endl;

    // Following line gives an error (cannot convert std::optional<size_t> to size_t)
    // const size_t found_early_i{ find_last(string, 'i') };
    const auto found_early_i{ find_last(string, 'i', 10) };
    if (found_early_i != std::nullopt)
        std::cout << "Found an early i at index " << *found_early_i << std::endl;
}
```

```cpp
std::optional<size_t> find_last(const std::string& string, char to_find,
                                std::optional<size_t> start_index)
{
    // code below will not work for empty strings
    if (string.empty())
        return std::nullopt;        // or: 'return std::optional<size_t>{};'
                                    // or: 'return {};'

    // determine the starting index for the loop that follows:
    size_t index = start_index.value_or(string.size() - 1);

    while (true) // never use while (index > 0) here, as size_t is always >= 0!
    {
        if (string[index] == to_find) return index;
        if (index == 0) return std::nullopt;
        --index;
    }
}
```

该程序产生的输出如下：

```
Found the last a at index 46
Found an early i at index 4
```

为了展示 `std::optional<>`，我们定义了前面用作示例的 `find_last()` 函数的一个变体。注意，由于 `find_last()` 使用无符号的 `size_t` 索引而不是 `int` 索引，-1 作为第三个参数的默认值就不那么明显了。我们将其替换为等于 `std::nullopt` 的默认值。这个特殊常量由标准库定义，用于初始化尚未（或还没有）分配 T 值的 `optional<T>` 值。你很快就会看到，为什么它对函数参数也是一个有用的默认值。

在函数原型之后，你会看到程序的 `main()` 函数。在 `main()` 中，我们三次调用 `find_last()`，在某个示例字符串中搜索字母 'a'、'b' 和 'i'。这些调用本身确实没有什么令人惊讶的。如果你想要非默认的起始索引，只需向 `find_last()` 传入一个数字，就像我们在第三次调用中所做的那样。然后编译器会隐式地将这个数字转换为 `std::optional<>` 对象，完全如你所料。不过，如果你接受默认起始索引，就可以省略相应参数。此时默认参数值会负责创建一个空的 optional<>。

以下是 `main()` 函数中两个最值得注意的要点：

-   如何检查 `find_last()` 返回的 `optional<>` 值是空，还是已被赋予实际值
-   随后如何从 `optional<>` 中提取这个值

对于前一个问题，`main()` 按以下顺序展示了三种替代方式：让编译器替你把 `optional<>` 转换为布尔值，调用 `has_value()` 函数，或者将 `optional<>` 与 `nullopt` 进行比较。对于后一个问题，`main()` 展示了两种替代方式：你可以使用 `*` 运算符，或者调用 `value()` 函数。然而，将 `optional<size_t>` 返回值直接赋值给 `size_t` 是不可能的。编译器无法将 `optional<size_t>` 类型的值转换为 `size_t` 类型的值。

在 `find_last()` 的函数体中，除了空字符串和无符号索引类型带来的一些有趣挑战之外，请特别注意与 `optional<>` 相关的另外两个方面。首先，注意返回值很直接。你可以返回 `std::nullopt`，也可以返回实际值。随后编译器会将两者都转换为合适的 `optional<>`。其次，我们在那里使用了 `value_or()`。
