
```cpp
{
  using namespace std;
  cout << "This program determines the retail price for\n";
  cout << "an item at a Quick-Shop supermarket store.\n";
}
// 使用 iostream:
void getInput(double& cost, int& turnover)
{
  using namespace std;
  cout << "Enter the wholesale cost of item: $"";
  cin >> cost;
  cout << "Enter the expected number of days until sold: ";
  cin >> turnover;
}
// 使用 iostream:
void getOutput(double cost, int turnover, double price)
{
  using namespace std;
  cost.set(ios::fixed);
  cost.set(ios::precision(2));
  cout << "Wholesale cost = $" << cost << endl;
  cout << "Expected time until sold = $"";
  cout << turnover << " days" << endl;
  cout << "Retail price = $" << price << endl;
}

// 使用定义的常量 LOW_MARKUP, HIGH_MARKUP 和 THRESHOLD
double price(double cost, int turnover)
{
  if (turnover <= THRESHOLD)
    return (cost + (LOW_MARKUP * cost));
  else
    return (cost + (HIGH_MARKUP * cost));
}
```

### 示例对话

此程序确定 Quick-Shop 超市商店中物品的零售价格。输入商品批发价：$1.21

预计售出天数：5

批发价 = $1.21

预计售出时间 = 5 天

零售价 = $1.27

## 5.4 函数的测试与调试

## 313

## 程序测试

程序程序中的一项重要技术是测试各种输入。对于我们所说的“一类”输入，并没有精确的定义，但在实践中，通常很容易判断程序处理的输入类型。在我们的超市程序案例中，有两种类型的输入：使用 5% 低加价率的输入和使用 10% 高加价率的输入。因此，我们应该至少测试一种情况，即物品预计在货架上停留时间少于 7 天的情况，以及至少测试一种物品预计在货架上停留时间超过 7 天的情况。

测试各种输入

另一种测试策略是测试边界值。遗憾的是，边界值是另一个模糊的概念。如果一个输入（测试）值位于程序行为在预期 7 天货架期发生变化的数值上，那么该值就是边界值。因此，7 是一个边界值；程序对于小于或等于 7 天的数与大于 7 天数的行为不同。因此，我们应该至少测试一次物品预计在货架上恰好停留 7 天的情况。通常，你还应该测试距离边界值一步之遥输入，因为在判断边界位置时可能会产生一个值的误差。因此，我们应该测试预计在货架上停留 6 天的物品和预计在货架上停留 8 天的物品输入。（这在上一段中描述的测试输入之外，那些输入应该远低于 7 天且远高于 7 天。）

测试边界值

## 自测练习

- 13. 函数定义可以出现在另一个函数定义的内部吗？

- 14. 函数定义可以包含对另一个函数的调用吗？

- 15. 重写显示 5.8 中所示 `order` 函数的声明注释，以前置条件和后置条件的形式表示。

- 16. 为预定义函数 `sqrt` 给出一个前置条件和一个后置条件，该函数返回平方根。

## 5.4 函数的测试与调试

### 显示 5.11 带有存位函数的程序（2 部分中的第 2 部分）

```cpp
46  //使用了 iostream:
47  void giveOutput(double cost, int turnover, double price)
48  {
49      using namespace std;
50      cout.setf(ios::fixed);
51      cout.setf(ios::showpoint);
52      cout.precision(2);
53      cout << "Wholesale cost = $" \
```

```cpp
58  //这仅仅是一个存位函数：
59  double price(double cost, int turnover)
60  {
61      return 9.99; // 不正确，但对于某些测试已经足够了。
62  }
```

### 示例对话

此程序确定 Quick-Shop 超货商店物品的零售价。

输入商品的批发成本：$1.21

预计售出天数：5

批发成本 = $1.21

预计售出时间 = 5 天

零售价 = $9.99

第 5 章 / 所有子任务的函数

此程序使用了 `getInput` 函数，我们已经通过显示 5.10 所示的驱动程序对其进行了完整测试。此程序还包含了 `initializeScreen` 函数，我们假设它已经在它自己的驱动程序中通过了测试，尽管我们没有费力去编写那个简单的驱动程序。由于我们还没有测试 `price` 函数，因此我们使用了一个存位函数（stub）来代替它。注意，即使在还没有编写 `price` 函数之前，我们可以使用此程序。这样，我们可以在填充所有函数定义的细节之前测试基础的程序布局。

使用带有存位函数的程序大纲可以让你测试并然后“填充”你的程序大纲，而不是为了测试每个函数都编写一个完全的新程序。因此，带有存位函数的程序大纲是测试最有效的方法。一种常用方法是使用驱动程序测试一些基本函数（如输入和输出函数），然后使用带有存位函数的程序测试剩余函数。存位函数被一个一个地替换：一个存位函数被完整的函数替换并进行测试；一旦该函数经过完全测试，另一个存位函数就会被完整的函数定义替换，以此此类推，直到产生最终程序。

### 测试的根本规则

每个函数都应该在一个程序中测试，而该程序中的其他每个函数都经过了完全测试和调试。

## 自测练习

- 17. 测试的根本规则是什么？为什么这是测试函数的好方法？

- 18. 什么是驱动程序？

- 19. 为显示 5.11 所示的函数编写一个驱动程序。

- 20. 为练习 11 中的 `addTax` 函数编写一个驱动程序。

- 21. 什么是存位函数（stub）？

- 22. 为下面给出的声明函数写一个存位函数。不要写整个程序，只写放入其中的存位函数即可。（提示：它会非常短。）

```cpp
double rainProb(double pressure, double humidity, double temp);
// 前提条件：pressure 是汞柱
// 英制，
// humidity 是百分比表示的相对湿度，
// temp 是华氏度温度。
// 返回降雨概率，这是一个在 0 到 1 之间的数字。
// 0 表示不下雨，1 表示一定下雨。
```

## 5.5 调试技术

通过使用存位函数和驱动程序进行仔细测试，可以检测程序中存在的大量 bug。然而，仅检查代码和测试用例的输出可能不足以追踪逻辑错误。在这种情况下，有许多通用的调试技术可以采用。

### 保持开放的心态

从整体检查系统，不要假设 bug 发生在某处。如果程序给出了错误的输出值，那么你应该检查源代码、输入和输出值的不同测试用例，以及算法背后的逻辑。例如，考虑显示 5.9 中确定价格的代码。如果显示了错误的价格，错误可能仅仅是输入值与你在测试用例中预期的值不符，导致了程序错误。

初学者会“随机”修改代码的部分，希望这能修复错误。务必避免这样做！有时这种方法在你编写的前几个程序中会有效。但对于较大的程序，它几乎会失败，并且经常引入新错误。在提交修改之前，确保你理解代码的更改会产生什么影响。最后，如果老师允许，你可以把程序给别人看。新鲜的视角可以快速发现你错过的错误。休息一下，并在几小时后或第二天回到问题也有助于发现错误。

### 常见错误

你应该寻找的首要错误之一是容易犯的常见错误，正如教科书中“陷阱”（Pitfall）和“编程提示”（Programming Tip）部分描述的那样。常见错误来源包括：

1) 未初始化的变量，2) 差一错误（off-by-one errors），3) 超过数据边界，4) 自动类型转换，以及 5) 使用 `=` 而不是 `==`。

### 错误定位

确定 bug 的精确原因和位置是修复错误的第一步之一。检查不同测试用例的输入和输出行为是定位错误的一种方法。相关技术是在程序的策略位置添加计数语句，打印出关键变量的值。计数语句如显示 5.13 所示，在程序中打印关键变量的值。

如显示 5.13 所示，这种策略打印关键变量的值。

例如，考虑显示 5.12 中的代码，用于将华氏度转换为摄氏度的公式为 $C = \frac{5(F-32)}{9}$。

例如，考虑显示 5.9 中确定价格的代码。如果显示了错误的价格，错误可能仅仅是输入值与你在测试用例中预期的值不符，导致了程序错误。

初学者会“随机”修改代码的部分，希望这能修复错误。务必避免这样做！有时这种方法在你编写的前几个程序中会有效。但对于较大的程序，它几乎会失败，并且经常引入新错误。在提交修改之前，确保你理解代码的更改会产生什么影响。最后，如果老师允许，你可以把程序给别人看。新鲜的视角可以快速发现你错过的错误。休息一下，并在几小时后或第二天回到问题也有助于发现错误。

### 显示 5.12 带有 Bug 的温度转换程序

```cpp
#include <iostream>
using namespace std;

int main() {
    double fahrenheit;
    double celsius;

    cout << "Enter temperature in Fahrenheit." << endl;
    cin >> fahrenheit;
    celsius = (5 / 9) * (fahrenheit - 32);
    cout << "Temperature in Celsius is " << celsius << endl;

    return 0;
}
```

### 示例对话

输入华氏度温度：100

摄氏度温度为 0

### 显示 5.13 带有 cout 语句的调试

```cpp
#include <iostream>
using namespace std;

int main() {
    double fahrenheit;
    double celsius;

    cout << "Enter temperature in Fahrenheit." << endl;
    cin >> fahrenheit;

    // 注释掉原始代码行但将其保留
    // 在程序中供参考
    // celsius = (5 / 9) * (fahrenheit - 32);

    // 添加 cout 语句以验证 (5 / 9) 和 (fahrenheit - 32)
    // 是否正确计算
    double conversionFactor = 5 / 9;
    double tempFahrenheit = (fahrenheit - 32);

    cout << "fahrenheit - 32 = " << tempFahrenheit << endl;
    cout << "conversionFactor = " << conversionFactor << endl;
    celsius = conversionFactor * tempFahrenheit;
    cout << "Temperature in Celsius is " << celsius << endl;

    return 0;
}
```

### 示例对话

|  输入华氏度温度：

100

fahrenheit - 32 = 68

conversionFactor = 0

摄氏度温度为 0 |

# 322 第5章 / 用于所有子任务的函数

指示编译器计算两个整数相除，结果为零。简单的修复方法是将其中一个操作数改为浮点类型以执行浮点除法而不是整数除法，例如：

```cpp
double conversionFactor = 5.0 / 9;
```

一旦确定错误，我们现在可以删除或注释掉调试代码，并通过计算公式的行来返回原始程序的修正版本：

```cpp
c = (5.0 / 9) * (fahrenheit - 32);
```

添加调试代码和引入计数语句是一种在几乎任何编程环境中都有效的简单技术。然而，在程序中添加大量的计数语句有时会非常繁琐。此外，计数语句的输出可能很长或难以解释，引入调试代码甚至可能引入新的错误。许多编译器和集成开发环境都包含一个独立的程序——**调试器（**debugger）**，它允许程序员在特定的代码行（称为**断点**）处停止程序执行，并逐行通过代码的执行。当调试器逐行执行代码时，程序员可以检查变量的内容，甚至更改存储在这些变量中的值。检查关键变量的值不需要计数语句。不同C++编译器的调试器界面、命令和功能各不相同，请检查您的用户手册或咨询您的导师以了解如何使用这些功能。

# assert 宏

在5.3中，我们讨论了子程序的前置条件（preconditions）和后置条件（postconditions）。`assert` 宏是一个工具，用于确保在 `assert` 语句的位置预期条件为真。如果不满足条件，程序将显示错误消息并终止。首先，通过以下语句在程序中包含 `assert` 的定义：

```cpp
#include <cassert>
```

要使用 `assert`，在您想要强制断言的位置添加以下代码行，并带上一个结果应为真的布尔表达式：

```cpp
assert(boolean_expression);
```

`assert` 语句是一个宏，是一种类似于函数的结构。例如，考虑一个使用牛顿法计算数字 $n$ 的平方根的子程序：

```latex
sqrt_{i+1} = \frac{1}{2}(sqrt_i + \frac{n}{sqrt_i})
```

在这里，$sqrt_i = 1$，且随着 $i$ 趋于无穷，$sqrt$ 接近 $n$ 的平方根。实现此算法的子程序要求 $n$ 为正数，且我们重复计算的迭代次数也为正数。我们可以通过在所示子程序中添加 `assert` 来保证这一点：

```cpp
// 使用牛顿迭代法
// 接近 n 的平方根
// 前置条件：n 为正数，numIterations 为正数
// 后置条件：返回 n 的平方根
double newtonSsqrt(double n, int numIterations)
{
    double answer = 1;
    int i = 0;

    assert(n > 0 && (numIterations > 0);
    while (i < numIterations) {
        answer = 0.5 * (answer + n / answer);
        i++;
    }
    return answer;
}
```

如果我们尝试使用任何负数参数执行此子程序，程序将终止并显示失败的断言。`assert` 语句可以用类似的方式用于任何您想要强制的断言，它是防御性编程的一种极佳技术。

如果您要分发程序，您可能不希望可执行文件包含 `assert` 语句，因为用户可能会收到他们无法理解的错误消息。如果您在代码中添加了许多 `assert` 语句，删除所有它们可能会很麻烦。幸运的是，您可以通过在程序开头、在包含 `<cassert>` 的语句之前添加以下行来禁用所有 `assert` 宏：

```cpp
#define NDEBUG
#include <cassert>
```

如果您以后更改程序并需要再次调试，可以通过删除 `#define NDEBUG` 行（或将其注释掉）来重新开启 `assert` 语句。

第5章 / 用于所有子任务的函数

## 自测练习

23. 在计算语句：`x = (x * y / z);` 时，你如何使用 `assert` 宏来避免除以零？

24. 什么是调试器？

25. 你可以使用哪些通用技术来确定错误的来源？

# 本章总结

- 程序中的所有子任务都可以实现为函数，既可以是返回值的函数，也可以是 `void` 函数。

- 形式参数（formal parameter）是一种占位符，在调用函数时用实际参数填充。执行这种替换的方法有两种：值传递（call-by-value）和引用传递（call-by-reference）。

- 值传递替换机制：用参数的值替换其对应的形式参数。引用传递替换机制：参数应该是一个变量，并用整个变量替换对应的参数。

- 在函数定义中指示引用传递参数的方法是在形式参数的类型后附上取地址符 `&`。

- 对应值传递参数的参数不能通过函数调用更改。对应引用传递参数的参数可以通过函数调用进行更改。如果你想让函数更改变量的值，必须使用引用传递。

- 编写函数注释的一种好方法是使用前置条件和后置条件。前置条件说明了调用函数时假设什么为真。后置条件描述了执行函数后什么将为真。

- 每个函数都应该在一个其他函数已通过测试的程序中测试。

- 驱动程序（driver program）是一个仅用于测试函数的程序。

- 函数的简化版本称为存根（stub）。存根用于尚未测试或尚未编写的函数。

- 调试器、策略性的 `cout` 语句以及 `assert` 宏都是帮助调试程序的工具。

## 自测练习答案

1. Hello

Goodbye

One time time:

Hello

End of program.

2. 不，`void` 函数定义不需要返回语句。`void` 函数定义可以包含返回语句，但不是必须。
