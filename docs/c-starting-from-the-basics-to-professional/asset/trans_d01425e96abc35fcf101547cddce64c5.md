
```
radius = 0.20, area = 0.13; radius = 0.40, area = 0.50; radius = 0.60, area = 1.13;
radius = 0.80, area = 2.01; radius = 1.00, area = 3.14; radius = 1.20, area = 4.52;
radius = 1.40, area = 6.16; radius = 1.60, area = 8.04; radius = 1.80, area = 10.18;
radius = 2.00, area = 12.57; radius = 2.20, area = 15.21; radius = 2.40, area = 18.10;
radius = 2.60, area = 21.24; radius = 2.80, area = 24.63;
```

该循环包含一个 if 语句，用于每行输出三组值。你预期最后输出的是半径为 3.0 的圆面积。毕竟，只要 radius 小于或等于 3.0，循环就应继续。但显示的最后值中 radius 为 2.8；哪里出错了？

循环比预期更早结束，因为当 0.2 加到 2.8 时，结果大于 3.0。表面上看这是一件令人震惊的算术现象，但请继续读下去！原因在于 0.2 表示为二进制浮点数时存在一个非常小的误差。0.2 无法用二进制浮点数精确表示。误差出现在精度的最后一位，因此如果你的编译器支持 double 类型的 15 位精度，该误差的量级为 10⁻¹⁵。通常这无关紧要，但这里你依赖于连续加 0.2 来恰好得到 3.0——而这并没有发生。

你可以通过将循环改为每行只输出一个圆面积，并显示 3.0 与下一个值之间的差值，来查看差异是什么。

```cpp
for (double radius {0.2}; radius <= 3.0; radius += 0.2)
{
    std::cout << std::format("radius = {:.4f}, area = {:.5f}, delta to 3 = {}\n",
        radius,
        std::numbers::pi * radius * radius,
        (radius + 0.2) - 3.0
    );
}
```

在我们的机器上，最后一行输出现在是这样：

```
radius = 2.80, area = 24.63, delta to 3 = 4.440892098500626e-16
```

如你所见，radius + 0.2 比 3.0 大约 4.44 × 10⁻¹⁶。这导致循环在下一次迭代之前终止。

> **注意** 任何分母为奇数的分数都不能精确表示为二进制浮点值。

虽然这个例子可能显得有点学术化，但舍入误差在实践中确实会导致类似的 bug。作者之一记得一个真实 bug，其 for 循环类似于 Ex5_03。这个 bug 几乎导致某件价值远超 $10,000 的高科技硬件被毁——仅仅因为循环偶尔（并非总是！）多运行了一次迭代。结论：

**警告** 比较浮点数可能很棘手。直接使用 `==`、`<=` 或 `>=` 等运算符比较浮点计算结果时，你应始终保持谨慎。舍入误差几乎总是使浮点值永远无法精确等于数学上的精确值。

对于 Ex5_03 中的 for 循环，一种选择是引入一个整型计数器，专门用于控制循环。另一种选择是用一个能预见舍入误差的条件替换循环条件。在这种特定情况下，使用类似 `radius < 3.0 + 0.001` 的写法就足够了。除了 0.001，你可以使用任何充分大于预期舍入误差、同时又充分小于循环 0.2 增量的数。修正后的程序版本可在 Ex5_03A.cpp 中找到。大多数数学库和所谓的单元测试框架都会提供实用函数，帮助你以可靠的方式比较浮点数。

## 更复杂的 for 循环控制表达式

你可以在第一个 for 循环控制表达式中定义并初始化多个给定类型的变量。只需用逗号将每个变量与下一个变量分隔开。下面是一个使用该特性的可运行示例：

```cpp
// Ex5_04.cpp
// Multiple initializations in a loop expression
import <iostream>;
import <format>;

int main()
{
  unsigned int limit {};
  std::cout << "This program calculates n! and the sum of the integers "
            << "up to n for values 1 to limit.\n";

  std::cout << "What upper limit for n would you like? ";
  std::cin >> limit;

  // The format string for all rows of the table
  const auto table_format = "{:8} {:8} {:20}\n";

  // Output column headings
  std::cout << std::format(table_format, "integer", "sum", "factorial");

  for (unsigned long long n {1}, sum {}, factorial {1}; n <= limit; ++n)
  {
    sum += n;          // Accumulate sum to current n
    factorial *= n;    // Calculate n! for current n
    std::cout << std::format(table_format, n, sum, factorial);
  }
}
```

该程序对从 1 到 limit 的每个整数 n，计算从 1 到 n 的整数之和，其中 limit 是你输入的上限。它还计算每个 n 的阶乘。（整数 n 的阶乘写作 n!，是从 1 到 n 的所有整数的乘积；例如，5! = 1 × 2 × 3 × 4 × 5 = 120。）

前四条语句定义了四个初始值为 1 的变量。最后一条语句输出三个由逗号运算符分隔的赋值表达式的结果。逗号运算符是左结合的，并且优先级在所有运算符中最低，因此该表达式的求值方式如下：

```cpp
(((value1 += ++i), (value2 += ++i)), (value3 += ++i));
```

其效果将是：value1 增加 2 得到 3，value2 增加 3 得到 4，value3 增加 4 得到 5。复合表达式的值是这一系列中最右侧表达式的值，因此输出的值是 5。你可以使用逗号运算符将这些计算并入 Ex5_04.cpp 中 for 循环的第三个循环控制表达式：

```cpp
for (unsigned long long n {1}, sum {1}, factorial {1}; n <= limit;
        ++n, sum += n, factorial *= n)
{
    std::cout << std::format(table_format, n, sum, factorial);
}
```

第三个控制表达式使用逗号运算符组合了三个表达式。第一个表达式像之前一样递增 n，第二个将递增后的 n 加到 sum，第三个将 factorial 乘以同一个值。这里重要的是我们先递增 n，然后才执行另外两个计算。还要注意，这里我们将 sum 初始化为 1，而之前初始化为 0。原因是第三个控制表达式只在循环体第一次执行之后才第一次执行。如果没有这一修改，第一次迭代就会一开始打印出错误的和 0。如果你用这个新版本替换 Ex5_04.cpp 中的循环并再次运行示例，你会看到它像之前一样工作（另见 Ex5_04A）。

## 基于范围的 for 循环

基于范围的 for 循环会遍历一个值范围中的所有值。这立刻引出一个问题：什么是范围？数组是元素的范围，字符串是字符的范围。标准库提供的容器也都是范围。我们将在本章后面介绍两个标准库容器。下面是基于范围的 for 循环的一般形式：

```cpp
for ([initialization;] range_declaration : range_expression)
    loop statement or block;
```

方括号仅用于参考，它们表示初始化部分是可选的。向基于范围的 for 循环添加初始化语句的能力是在 C++20 中引入的，并且除了它是可选的之外，与常规 for 循环的初始化完全类似。你可以用它初始化一个或多个变量，然后可以在基于范围的 for 循环的剩余部分中使用这些变量。

range_expression 标识作为数据源的范围，range_declaration 标识一个变量，该变量将依次被赋值为该范围中的每个值，并在每次迭代时赋予新值。通过一个示例会更清楚。考虑这些语句：

```cpp
int values [] {2, 3, 5, 7, 11, 13, 17, 19, 23, 29};
int total {};
for (int x : values)
    total += x;
```
