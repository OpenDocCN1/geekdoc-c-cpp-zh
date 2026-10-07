
### 示例对话

此程序确定 Quick-Shop 超市商店物品的零售价。
输入物品批发价: $1.21
输入预计售出前的天数: 5
批发价 = $1.21
预计售出时间 = 5 天
零售价 = $9.99

## 318 第 5 章 / 适用于所有子任务的函数

gram。此程序使用了 `getInput` 函数，我们已经使用显示 5.10 所示的驱动程序完全测试了它。此程序还包含了 `giveOutput` 函数，我们还没有测试它。此程序还包含了 `price` 函数，它目前是一个存根。在这种情况下，我们可以使用缺失或未测试函数的简化版本。这些简化版的函数被称为存根。这些存根并不一定会执行正确的计算，但将提供足够测试的数值，而且它们足够简单，让你对它们的性能有信心。例如，显示 5.11 中的程序设计用于测试显示 5.9 中的 `giveOutput` 函数以及程序的基本布局。

此程序使用了 `getInput` 函数，我们已经使用显示 5.10 所示的驱动程序完全测试了它。此程序还包含了 `giveOutput` 函数，我们还没有测试它。此程序还包含了 `price` 函数，它目前是一个存根。在这种情况下，我们可以使用缺失或未测试函数的简化版本。这些简化版的函数被称为存根。这些存根并不一定会执行正确的计算，但将提供足够测试的数值，而且它们足够简单，让你对它们的性能有信心。例如，显示 5.11 中的程序设计用于测试显示 5.9 中的 `giveOutput` 函数以及程序的基本布局。

此程序使用了 `getInput` 函数，我们已经使用显示 5.10 所示的驱动程序完全测试了它。此程序还包含了 `giveOutput` 函数，我们还没有测试它。此程序还包含了 `price` 函数，它目前是一个存根。在这种情况下，我们可以使用缺失或未测试函数的简化版本。这些简化版的函数被称为存根。这些存根并不一定会执行正确的计算，但将提供足够测试的数值，而且它们足够简单，让你对它们的性能有信心。例如，显示 5.11 中的程序设计用于测试显示 5.9 中的 `giveOutput` 函数以及程序的基本布局。

此程序使用了 `getInput` 函数，我们已经使用显示 5.10 所示的驱动程序完全测试了它。此程序还包含了 `giveOutput` 函数，我们还没有测试它。此程序还包含了 `price` 函数，它目前是一个存根。在这种情况下，我们可以使用缺失或未测试函数的简化版本。这些简化版的函数被称为存根。这些存根并不一定会执行正确的计算，但将提供足够测试的数值，而且它们足够简单，让你对它们的性能有信心。例如，显示 5.11 中的程序设计用于测试显示 5.9 中的 `giveOutput` 函数以及程序的基本布局。

此程序使用了 `getInput` 函数，我们已经使用显示 5.10 所示的驱动程序完全测试了它。此程序还包含了 `giveOutput` 函数，我们还没有测试它。此程序还包含了 `price` 函数，它目前是一个存根。在这种情况下，我们可以使用缺失或未测试函数的简化版本。这些简化版的函数被称为存根。这些存根并不一定会执行正确的计算，但将提供足够测试的数值，而且它们足够简单，让你对它们的性能有信心。例如，显示 5.11 中的程序设计用于测试显示 5.9 中的 `giveOutput` 函数以及程序的基本布局。

此程序使用了 `getInput` 函数，我们已经使用显示 5.10 所示的驱动程序完全测试了它。此程序还包含了 `giveOutput` 函数，我们还没有测试它。此程序还包含了 `price` 函数，它目前是一个存根。在这种情况下，我们可以使用缺失或未测试函数的简化版本。这些简化版的函数被称为存根。这些存根并不一定会执行正确的计算，但将提供足够测试的数值，而且它们足够简单，让你对它们的性能有信心。例如，显示 5.11 中的程序设计用于测试显示 5.9 中的 `giveOutput` 函数以及程序的基本布局。

| 测试的基本规则 |
| :--- |
| 每个函数都应该在一个以其本身为“待测试函数”的程序中进行测试。然而，在测试其他函数时，使用已完全测试的函数是可以的。 | 有时，在不使用尚未编写或尚未测试的其他函数的情况下，测试某个函数是不可能的或不方便的……你可以使用缺失或未测试函数的简化版本。这些简化版的函数被称为存根。这些存根并不一定会执行正确的计算，但将提供足够测试的数值，而且它们足够简单，让你对它们的性能有信心。例如，显示 5.11 中的程序设计用于测试显示 5.9 中的 `giveOutput` 函数以及程序的基本布局。 |

## 自测题

- 17. 测试的基本规则是什么？
- 18. 为什么这种测试方法很好？
- 19. 什么是驱动程序？
- 20. 为显示 5.11 中的函数编写一个驱动程序。
- 21. 什么是存根？
- 22. 为下述函数编写一个存根。

```cpp
double rainProb(double pressure, double humidity,
      double temp);
```
前置条件：`pressure` 是汞柱，
`humidity` 是百分比表示的相对湿度，
`temp` 是摄氏温度。
返回降水概率，概率是一个 0 到 1 之间的数字
0 表示没有降水概率。1 表示 100%
确定。

## 5.5 通用调试技术

通过存根和驱动程序的细致测试可以检测程序中可能存在的大量 bug。然而，对代码和用例输出的检查可能不足以跟踪许多逻辑错误。在这种情况下，有很多通用调试技术可以使用。

### 保持开放心态

从整体上检查系统，不要假设 bug 发生在某处。如果程序给出了错误的输出值，那么你应该检查源代码、不同的输入输出用例，以及算法本身的逻辑。例如，考虑显示 5.9 中超市示例的价格代码。如果显示了错误的价格，错误可能只是输入值与你在用例中预期的值不同，导致程序编写错误。休息一下并在几小时后或第二天回到问题上也有助于发现你一直忽略的错误。

### 检查常见错误

你首先应该寻找易犯的常见错误，正如贯穿书中“陷阱”（Pitfall）和“编程提示”（Programming Tip）部分描述的那样。常见错误的来源包括 (1) 未初始变量、(2) 差一错误、(3) 越界数据边界、(4) 自动类型转换以及 (5) 使用 `=` 代替 `==`。

## 定位错误

确定 bug 的精确原因和位置是修复错误的第一步之一。通过检查不同测试用例的输入和输出行为是定位错误的一种方法。相关技术是在程序中的策略位置添加语句，打印关键变量的值。`cout` 语句显示了程序正在执行的内容。这是在第 3 章中针对循环描述的变量追踪策略，但即使代码中没有循环也可以使用。

例如，考虑显示 5.12 中的代码，其意图是使用公式将温度从华氏度转换为摄氏度

```
$C = \frac{5(F - 32)}{9}$
```

当该程序在输入为 100 华氏度时运行时，输出为“Temperature in Celsius is 0°”。这显然是错误的，因为正确答案是 37.8 摄氏度。
为了追踪错误，我们可以打印关键变量的值。在这种情况下，转换公式似乎出了问题，因此我们尝试两步法：第一步计算 `(Fahrenheit - 32)`，第二步计算 `(5 / 9)`，然后同时计算这两个值。这是插/

### 显示 5.12 带有 bug 的温度转换程序

```cpp
#include <iostream>
using namespace std;
int main()
{
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

Enter temperature in Fahrenheit.
100
Temperature in Celsius is 0

## 5.5 通用调试技术

在显示 5.13 中所示。我们还通过在行开头放置 `//` 注释了原始代码行。这告诉编译器忽略原始代码行，但仍将其保留在程序中以供我们参考。如果我们想恢复代码，只需删除 `//` 即可，而不需要在被删除后重新输入该行。

通过检查代码语句的结果，我们现在确定了 bug 的精确位置。在这种情况下，转换因子没有被正确计算。由于我们将转换因子设置为 5 / 9，这

### 显示 5.13 使用 count 语句进行调试

```cpp
#include <iostream>
using namespace std;
int main() {
{
    double fahrenheit;
    double celsius;
    cout << "Enter temperature in Fahrenheit." << endl;
    cin >> fahrenheit;
    // 注释原始代码行但将其保留
    // 在程序中供我们参考
    // celsius = (5 / 9) * (fahrenheit - 32);
    // 添加 count 语句来验证 (5 / 9) 和 (fahrenheit - 32)
    // 我们是否计算正确
    double conversionFactor = 5 / 9;
    double tempFahrenheit = (fahrenheit - 32);
    cout << "fahrenheit - 32 = " << tempFahrenheit << endl;
    cout << "conversionFactor = " << conversionFactor << endl;
    celsius = conversionFactor * tempFahrenheit;
    cout << "Temperature in Celsius is " << celsius << endl;
    return 0;
}
}
```

### 示例对话

| Enter temperature in Fahrenheit. 100 | fahrenheit - 32 = 68 | conversionFactor = 0 | Temperature in Celsius is 0 |

## 第 5 章 / 用于所有子任务的函数

指示编译器计算两个整数相除，结果为零。简单的修复方法是通过将其中一个操作数改为浮点类型来执行浮点除法而非整数除法，例如：

```cpp
double conversionFactor = 5.0 / 9;
```

一旦确定了 bug，我们现在可以移除或注释调试代码，并通过修改计算公式的行来返回原始程序的修正版本：

```cpp
c = (5.0 / 9) * (fahrenheit - 32);
```

添加调试代码和引入 count 语句是一种在几乎任何编程环境中都有效的简单技术。然而，在程序中添加大量的 count 语句有时可能是繁琐的。此外，count 语句的输出可能很长或难以解释，调试代码的引入甚至可能引入新的错误。许多编译器和集成开发环境包含一个单独的程序调试器（debugger），它允许程序员在特定的代码行（称为断点）处停止程序执行，并逐行单步执行代码。在程序调试器逐行执行代码时，程序员可以检查变量的内容，甚至更改存储在这些变量中的值。查看关键变量的值不需要 count 语句。不同 C++ 编译器之间的调试器接口、命令和功能不相同，请查看您的手册或咨询教师以了解如何使用这些功能。

## assert 宏

在 5.3 中，我们讨论了子程序的前置条件（preconditions）和后置条件（postconditions）。`assert` 宏是一个用于确保预期条件在 assert 语句所在位置为真的的工具。如果不满足条件，程序将显示错误消息并终止。若要使用 assert，首先通过以下包含在程序中引入 assert 的定义：

```cpp
#include <cassert>
```

# 自测练习答案

- 1. Hello
Goodbye
再次：
Hello
程序结束。。

- 2. 不，`void` 函数定义不需要包含 `return` 语句。`void` 函数定义可以包含 `return` 语句，但不是必须。

- 3. 在显示 5.2 中，在 `initializeScreen` 函数定义中省略 `return` 语句对程序的行为完全没有影响。程序将能够编译、运行，且行为完全相同。同样，在 `showResults` 函数定义中省略 `return` 语句也不会对程序的行为产生影响。然而，如果你在 `celsius` 函数定义中省略了 `return` 语句，那是一个严重错误，会导致程序无法运行。区别在于 `initializeScreen` 和 `showResults` 是 `void` 函数，而 `celsius` 不是 `void` 函数。

```cpp
#include <iostream>
void productOut(int n1, int n2, int n3);
int main()
{
    using namespace std;
    int num1, num2, num3;
    cout << "Enter three integers: ";
    cin >> num1 >> num2 >> num3;
    productOut(num1, num2, num3);
    return 0;
}
```

```cpp
void productOut(int n1, int n2, int n3)
{
    using namespace std;
    cout << "The product of the three numbers "
    << n1 << " * " << n2 << " * and "
    << n3 << " is " << (n1 * n2 * n3) << endl;
}
```

- 5. 这些答案取决于系统。

- 6. 调用 `void` 函数并后跟一个分号是一个语句。调用返回值的函数是一个表达式。

# 第 5 章 / 适用于所有子任务的函数

- 7. 10 20 30
1 2 3
1 20 30

Enter two integers: 5 10
In reverse order the numbers are: 5 5

parValue in function call = 111
par2Ref in function call = 222
n1 after function call = 1
n2 after function call = 2

- 10. `void zeroBoth(int& n1, int& n2)`

```cpp
{
  n1 = 0;
  n2 = 0;
}
```

- 11. `addTax(double taxRate, double& cost )`

```cpp
cost = cost + ( taxRate/100.0 ) * cost;
```

除以 100 是为了将百分比转换为分数。例如，10% 是 10/100.0 或成本的 1/10。

- 12. 返回值的函数可以有一个引用传递的参数。是的，函数可以拥有按值传递和引用传递参数的组合。

- 13. 不，函数定义不能出现在另一个函数定义的体内部。

- 14. 函数定义可以包含另一个函数。

- 15. `void order(int& n1, int& n2);`
// 前置条件：变量 `n1` 和 `n2` 有值。
// 后置条件：`n1` 和 `n2` 中的值已经过
// 排序，使得 `n1 <= n2`。

- 16. `double sqrt(double n);`
// 前置条件：`n >= 0`。
// 返回 `n` 的平方根。

如果你愿意，可以将注释行重写为如下内容，但之前的版本是返回值函数的常用形式：

```cpp
//后置条件：返回 n 的平方根。
```

17. 测试函数的根本规则是，每个函数都应该在某个环境下进行测试，在该环境下程序中的其他每个函数已经经过了充分测试和调试。这是一个测试函数的好方法，因为如果你遵循这条规则，当你发现 bug 时，你将知道 bug 位于哪个函数中。

18. 驱动程序（driver program）是唯一唯一为了测试某个函数而编写的程序。

19. ```cpp
#include <iostream>
void introduction();
// 后置条件：程序描述被写在
// 屏幕上。
int main() {
    using namespace std;
    introduction();
    cout << "End of test.\n";
    return 0;
}
// 使用 iostream
void introduction() {
    using namespace std;
    cout << "This program determines the retail price for\n";
    cout << "an item at a Quick-Stop supermarket store.\n";
}
```

20. // 用于函数 `addTax` 的驱动程序。
#include <iostream>

```cpp
void addTax(double taxRate, double &cost) {
// 前置条件：taxRate 是百分比形式的销售税额，
// 且 cost 是物品在加税前的成本。
// 后置条件：cost 已更改为添加销售税后
// 物品的成本。
```

```cpp
int main() {
    using namespace std;
    double cost, taxRate;
    char ans;
    cout.setf(ios::fixed);
