
无限范围和固定大小范围。例如，第19行使用`take`范围适配器仅从我们在第16行定义的evens管道中取出前五个值。我们将结果视图传递给`std::ranges::copy`（第19行），它遍历管道，使其执行各步骤：

- **`iota`** 生成一个整数，
- **`filter`** 检查它是否为偶数，如果是，
- **`take`** 将该值传递给 **`copy`**。

如果`iota`生成的值不是偶数，`filter`会丢弃该值，`iota`接着生成序列中的下一个值。此过程重复进行，直到`take`已将指定数量的元素传递给`copy`。你可以从无限范围中获取任意数量的项，或从固定大小范围中获取最多项数。为了演示目的，我们将在后续讨论的每个管道中仅处理少量项。

```cpp
std::cout << "First five even ints: ";
std::ranges::copy(evens | std::views::take(5), output);
```

```
First five even ints: 0 2 4 6 8
```

### take_while 范围适配器

第22–23行创建了一个增强的管道，使用`take_while`范围适配器限制evens无限范围。此范围适配器返回一个视图，当`take_while`的一元谓词返回true时，从管道更早的步骤中获取元素。在本例中，我们在这些值小于12时获取偶数。第一个大于或等于12的值会终止管道。我们将`take_while`返回的视图存储在变量`lessThan12`中，供后续语句使用。第24行将`lessThan12`传递给`std::ranges::copy`，它遍历视图——执行其管道步骤——并显示结果。

```cpp
std::cout << "\nEven ints less than 12: ";
auto lessThan12{
    evens | std::views::take_while([](int x) { return x < 12; })};
std::ranges::copy(lessThan12, output);
```

```
Even ints less than 12: 0 2 4 6 8 10
```

### reverse 范围适配器

第27行使用reverse范围适配器来反转来自第22–23行lessThan12视图的整数。我们将`reverse`返回的视图传递给`std::ranges::copy`，它遍历视图——执行其管道步骤——并显示结果。

```cpp
std::cout << "\nEven ints less than 12 reversed: ";
std::ranges::copy(lessThan12 | std::views::reverse, output);
```

```
Even ints less than 12 reversed: 10 8 6 4 2 0
```

### transform 范围适配器

我们在图6.13中介绍了**transform范围适配器**。第31–33行中的管道创建了一个视图，该视图获取`lessThan12`生成的整数，将其反转，然后使用**transform**对它们的值求平方。我们将结果视图传递给`std::ranges::copy`，它遍历视图——执行其管道步骤——并显示结果。

```cpp
29    std::cout << "\nSquares of even ints less than 12 reversed: ";
30    std::ranges::copy(
31        lessThan12
32            | std::views::reverse
33            | std::views::transform([](int x) { return x * x; }),
34        output);
```

```
Squares of even ints less than 12 reversed: 100 64 36 16 4 0
```

### drop 范围适配器

第38行中的管道以**evens**产生的无限偶数序列开始，使用**drop**范围适配器跳过前1,000个偶数，然后使用**take**范围适配器取出序列中接下来的五个偶数。我们将结果视图传递给`std::ranges::copy`，它遍历视图——执行其管道步骤——并显示结果。

```cpp
36    std::cout << "\nSkip 1000 even ints, then take five: ";
37    std::ranges::copy(
38        evens | std::views::drop(1000) | std::views::take(5),
39        output);
```

```
Skip 1000 even ints, then take five: 2000 2002 2004 2006 2008
```

### drop_while 范围适配器

您还可以在一元谓词保持为true时跳过元素。第43–45行中的管道以**evens**产生的无限偶数序列开始。它使用**drop_while**范围适配器跳过无限序列开头小于或等于1,000的偶数。然后使用**take**范围适配器取出序列中接下来的五个偶数。我们将结果视图传递给`std::ranges::copy`，它遍历视图——执行其管道步骤——并显示结果。

```cpp
41    std::cout << "\nFirst five even ints greater than 1000: ";
42    std::ranges::copy(
43        evens
44            | std::views::drop_while([](int x) { return x <= 1000; })
45            | std::views::take(5),
46        output);
```

```
First five even ints greater than 1000: 1002 1004 1006 1008 1010
```

### 创建并显示罗马数字及其十进制值的map

到目前为止，为了简单起见，我们一直专注于处理整数范围，但您也可以处理更复杂类型的范围以及各种容器。接下来，我们将处理一个map中的键值对，其中键是string对象，值是int。键是罗马数字，值是对应的十进制值。第49行的using声明使我们能够在第51–52行构建每个键值对时使用string对象字面量。例如，在值`"I"s`中，字符串字面量后面的`s`表示该字面量是一个string对象。第53–54行创建了一个lambda，我们在第56行使用std::ranges::for_each显示map中的每个键值对。

```cpp
48     // allow std::string object literals
49     using namespace std::string_literals;
50
51     std::map<std::string, int> romanNumerals{
52         {"I"s, 1}, {"II"s, 2}, {"III"s, 3}, {"IV"s, 4}, {"V"s, 5}};
53     auto displayPair{[](const auto& p) {
54         std::cout << p.first << " = " << p.second << '\n';
55     }};
56     std::ranges::for_each(romanNumerals, displayPair);
```

```
romanNumerals:
I = 1
II = 2
III = 3
IV = 4
V = 5
```

### keys 和 values 范围适配器

在管道中处理map时，每个键值对被视为包含键和值的pair对象。您可以使用范围适配器keys（第60行）和values（第63行）分别仅获取键和值的视图：

- **keys** 创建一个视图，仅选择每个**pair**中的*第一*项。
- **values** 创建一个视图，仅选择每个**pair**中的*第二*项。

我们将每个管道传递给`std::ranges::copy`，它遍历管道并显示结果。

```cpp
58     std::ostream_iterator<std::string> stringOutput{std::cout, " "};
59     std::cout << "\nKeys in romanNumerals: ";
60     std::ranges::copy(romanNumerals | std::views::keys, stringOutput);
61
62     std::cout << "\nValues in romanNumerals: ";
63     std::ranges::copy(romanNumerals | std::views::values, output);
```

```
Keys in romanNumerals: I II III IV V
Values in romanNumerals: 1 2 3 4 5
```

### elements 范围适配器

有趣的是，**keys**和**values范围适配器**也适用于每个元素为**tuple**或**array**的范围。即使每个元素包含多于两个元素，**keys始终选择第一项**，**values始终选择第二项**。如果范围中的**tuple或array**元素包含多于两个元素，elements范围适配器可以按索引选择**项**，正如我们使用romanNumerals的**键值对**所演示的那样。第67行仅选择范围中每个pair对象的元素0，第70行仅选择元素1。在这两种情况下，我们将管道传递给`std::ranges::copy`，它遍历管道并显示结果。

```cpp
65     std::cout << "\nKeys in romanNumerals via std::views::elements: ";
66     std::ranges::copy(
67         romanNumerals | std::views::elements<0>, stringOutput);
68
69     std::cout << "\nValues in romanNumerals via std::views::elements: ";
70     std::ranges::copy(romanNumerals | std::views::elements<1>, output);
71     std::cout << "\n";
72 }
```

```
Keys in romanNumerals via std::views::elements: I II III IV V
Values in romanNumerals via std::views::elements: 1 2 3 4 5
```

## 14.8 并行算法简介

几十年来，每隔几年，计算机处理能力大约以低廉的成本翻一番。这就是所谓的摩尔定律——以英特尔联合创始人戈登·摩尔命名，他在20世纪60年代指出了这一趋势。计算机处理器公司NVIDIA和Arm的高管们表示，摩尔定律已不再适用。³⁶,³⁷ 计算机处理能力仍在不断提高，但硬件供应商现在依赖于新的处理器设计，例如**多核处理器**，它能够实现真正的并行处理以获得更好的性能。C++一直专注于性能。然而，直到C++11——该语言诞生32年后——才首次在标准中支持并行。

并行化一个算法并非像“拨动开关”那样简单地说“我想并行运行这个算法”。并行化对算法所做的事情以及哪些部分能够在多核硬件上真正并行运行非常敏感。程序员必须仔细确定如何划分任务以进行并行执行。此类算法必须能够扩展到任意数量的核心——给定时间内可用的核心数量可能多也可能少，因为它们是

36. Esther Shein，“摩尔定律迎来55岁：它仍然重要吗？”，2020年4月17日。访问于2023年4月18日。https://www.techrepublic.com/article/moores-law-turns-55-is-it-still-relevant/

37. Nick Heath，“摩尔定律已死：关于未来计算机的三个预测”，2018年9月19日。访问于2023年4月18日。https://www.techrepublic.com/article/moores-law-is-dead-three-predictions-about-the-computers-of-tomorrow/

