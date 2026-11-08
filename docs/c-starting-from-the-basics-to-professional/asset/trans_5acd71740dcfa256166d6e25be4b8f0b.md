
与标准数组不同，你还可以将一个 `array<>` 容器赋值给另一个 `array<>` 容器，只要它们都存储相同数量且类型相同的元素即可。下面是一个示例：

```cpp
them = those;        // Copy all elements of those to them
```

此外，`array<>` 对象可以存储在其它容器内部。常规数组则不能。例如，下面使用了一个 `vector<>` 容器，它可以保存 `array<>` 对象作为元素，而每个 `array<>` 对象又依次包含三个 `int` 值：

```cpp
std::vector<std::array<int, 3>> triplets;
```

`vector<>` 容器将在下一节讨论。

## 结论与示例

到现在，要点应该已经清楚了：在代码中始终优先选择 `array<>` 容器，而不是标准数组。我们已经给出了很多理由——按我们的统计至少有七条。而且，使用 `array<>` 绝对没有任何劣势。与标准数组相比，使用 `array<>` 容器的性能可以超过数组。（也就是说，除非你使用 `at()` 函数而不是 `array<>` 的 `[]` 运算符——当然，边界检查可能会带来少量运行时开销。）

> **注意**  即使你在代码中使用 `std::array<>` 容器，也仍然完全可以调用那些期望普通数组作为输入的旧式函数。你始终可以使用 `data()` 成员访问封装在 `array<>` 对象内部的内置数组。

下面是一个演示 `array<>` 容器实际用法的示例：

```cpp
// Ex5_14.cpp
// Using array<T,N> to create Body Mass Index (BMI) table
// BMI = weight/(height*height)
// weight in kilograms, height in meters

import <iostream>;
import <format>;
import <array>;        // For array<T,N>

int main()
{
    const unsigned min_wt {100};       // Minimum weight in table (in pounds)
    const unsigned max_wt {250};       // Maximum weight in table (in pounds)
    const unsigned wt_step {10};
    const size_t wt_count {1 + (max_wt - min_wt) / wt_step};

    const unsigned min_ht {48};        // Minimum height in table (inches)
    const unsigned max_ht {84};        // Maximum height in table (inches)
    const unsigned ht_step {2};
    const size_t ht_count {1 + (max_ht - min_ht) / ht_step };

    const double lbs_per_kg {2.2};   // Pounds per kilogram
    const double ins_per_m {39.37};  // Inches per meter
    std::array<unsigned, wt_count> weight_lbs {};
    std::array<unsigned, ht_count> height_ins {};

    // Create weights from 100lbs in steps of 10lbs
    for (unsigned i{0}, w{min_wt}; i < wt_count; w += wt_step, ++i)
    {
        weight_lbs[i] = w;
    }
    // Create heights from 48 inches in steps of 2 inches
    for (unsigned i{0}, h{min_ht}; h <= max_ht; h += ht_step)
    {
        height_ins.at(i++) = h;
    }
    // Output table headings
    std::cout << std::format("{:>8}", '|');
    for (auto & w : weight_lbs)
        std::cout << std::format("{:^6}|", w);
    std::cout << std::endl;

    // Output line below headings
    for (unsigned i{1}; i < wt_count; ++i)
        std::cout << "--------";
    std::cout << std::endl;

    const unsigned inches_per_foot {12};
    for (auto h : height_ins)
    {
        const unsigned feet = h / inches_per_foot;
        const unsigned inches = h % inches_per_foot;
        std::cout << std::format("{:>2}'{:>2}\" |", feet, inches);

        const double h_m = h / ins_per_m;      // Height in meter
        for (auto w : weight_lbs)
        {
            const double w_kg = w / lbs_per_kg; // Weight in kilogram
            const double bmi = w_kg / (h_m * h_m);
            std::cout << std::format("{:2.1f}|", bmi);
        }
        std::cout << std::endl;
    }
    // Output line below table
    for (size_t i {1}; i < wt_count; ++i)
        std::cout << "--------";
    std::cout << "\nBMI from 18.5 to 24.9 is normal" << std::endl;
}
```

我们让你自己运行程序查看输出，因为它会占用相当多的空间。这里定义了两组各四个 `const` 变量，它们与 BMI 表的体重和身高范围有关。体重和身高存储在元素类型为 `unsigned`（`unsigned int` 的缩写）的 `array<>` 容器中，因为所有体重和身高都是整数。这些容器在 `for` 循环中用适当的值进行初始化。初始化 `height_ins` 的第二个循环使用了一种不同的赋值方式，只是为了演示 `at()` 函数。在这个循环中这样做是合适的，因为该循环并不受容器索引限制的控制，所以有可能出现错误，使用超出容器合法范围的索引。如果发生这种情况，程序会终止；而使用方括号引用元素时则不会如此。

接下来的两个 `for` 循环输出表列标题，以及一条将标题与表格其余部分分隔开的线。表格使用嵌套的基于范围的 `for` 循环创建。外层循环遍历身高，并在最左列以英尺和英寸输出身高。内层循环遍历体重，并为当前身高输出一行 BMI 值。

## 使用 std::vector<T> 容器

`vector<T>` 容器是一种序列容器，看起来可能很像 `array<T,N>` 容器，但实际上要强大得多。不需要在编译时预先知道 `vector<>` 将存储多少个元素。事实上，甚至不需要在运行时预先知道它将存储多少个元素。也就是说，`vector<>` 的大小可以自动增长，以容纳任意数量的元素。你可以现在添加一些元素，之后再添加更多。你可以删除中间的一些元素，然后再插入一些。使用 `vector<>` 容器，这一切都非常容易。随着你不断添加元素，`vector<>` 会增长；每当需要时，都会自动分配额外的空间。实际上也没有真正的最大元素数量——当然，除了你的进程可用内存量所施加的限制之外——这就是为什么你只需要类型参数 `T`。使用 `vector<>` 时不需要 `N`。使用 `vector<>` 容器需要在源文件中导入 `<vector>` 模块。

下面是一个创建 `vector<>` 容器来存储 `double` 类型值的示例：

```cpp
std::vector<double> values;
```

这通常还没有为元素分配空间，因此当你添加第一个数据项时，需要动态分配内存。你可以使用容器对象的 `push_back()` 函数添加元素。下面是一个示例：

```cpp
values.push_back(3.1415);    // Add an element to the end of the vector
```

`push_back()` 函数会将你作为参数传入的值——在本例中是 3.1415——作为新元素添加到现有元素的末尾。由于这里还没有现有元素，所以它将成为第一个元素，这很可能会第一次触发内存分配。

你可以用预先定义的元素数量来初始化一个 `vector<>`，像这样：

```cpp
std::vector<double> values(20);    // Vector contains 20 double values - all zero
```

与内置数组或 `array<>` 对象不同，`vector<>` 容器总是会初始化其元素。在本例中，我们的容器一开始有 20 个元素，它们都被初始化为零。如果你不喜欢将零作为元素的默认值，可以显式指定另一个值：

```cpp
std::vector<long> numbers(20, 99L);    // Vector contains 20 long values - all 99
```

括号中的第二个参数指定所有元素的初始值，因此全部 20 个元素都将是 `99L`。与你目前见过的大多数其他数组类型不同，指定元素数量的第一个参数——在本例中是 20——不需要是常量表达式。它可以是运行时执行的表达式的结果，也可以是从键盘读取的值。当然，你可以使用 `push_back()` 函数向这个或其他任何 vector 的末尾添加新元素。

创建 `vector<>` 的另一种选择是使用花括号列表来指定初始值：

```cpp
std::vector<int> primes { 2, 3, 5, 7, 11, 13, 17, 19 };
```

`primes` vector 容器将创建为包含八个元素，并使用给定的初始值。如果你用至少一个给定值初始化 `vector<>`，C++17 编译器可以再次推导出模板类型参数，这可能会显得有些令人惊讶。下面有两个可行的示例：

```cpp
std::vector primes { 2, 3, 5, 7, 11, 13, 17, 19 };  // Deduced type: std::vector<int>
std::vector numbers(20, 99L);                         // Deduced type: std::vector<long>
```

**警告**  你可能已经注意到，我们没有使用通常的花括号初始化器语法来初始化 `values` 和 `numbers` 这两个 `vector<>` 对象，而是使用了圆括号：

```cpp
std::vector<double> values(20);     // Vector contains 20 double values - all zero
std::vector<long> numbers(20, 99L);  // Vector contains 20 long values - all 99
```

这是因为在这里使用花括号初始化器会产生显著不同的效果，正如语句旁边的注释所解释的那样：

```cpp
std::vector<double> values{20};     // Vector contains 1 double value: 20
std::vector<long> numbers{20, 99L};  // Vector contains 2 long values: 20 and 99
```

当你使用花括号初始化 `vector<>` 时，编译器总是将其解释为一系列初始值。这是所谓统一初始化语法并不那么统一的少数场合之一。要用给定数量的相同值来初始化 `vector<>`——也就是说，不必一遍又一遍地重复同一个值——你不能使用花括号。如果这样做，编译器会将其解释为包含一个或两个初始值的列表。

你可以使用方括号中的索引为现有元素设置值，或者只是在表达式中使用其当前值。下面是一个示例：

```cpp
values[0] = std::numbers::pi;       // Pi
values[1] = 5.0;                     // Radius of a circle
values[2] = 2.0*values[0]*values[1];  // Circumference of a circle
```

`vector<>` 的索引值从 0 开始，就像标准数组一样。你始终可以使用方括号中的索引引用现有元素，但不能通过这种方式创建新元素。要创建新元素，你需要使用例如 `push_back()` 函数。像这样对 vector 进行索引时，索引值不会被检查，因此你可能意外访问 vector 范围之外的内存，并使用方括号中的索引将值存储到这些位置。`vector<>` 对象同样提供了 `at()` 函数，就像 `array<>` 容器对象一样，因此只要索引有可能超出合法范围，你就可以考虑使用 `at()` 函数来引用元素。
