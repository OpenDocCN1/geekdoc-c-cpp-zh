

| 标准库头文件（第3部分，共3部分） | 说明 |
|---|---|
| *一些关键的C++20新头文件* | |
| `<concepts>` | 用于约束模板所用类型的能力（在第15章“模板、C++20概念与元编程”中讨论）。 |
| `<coroutine>` | 用于协程异步编程的能力（在第17章中讨论）。 |
| `<compare>` | 支持新的三路比较运算符`<=>`（在第11章中讨论）。 |
| `<format>` | 新的简洁而强大的文本格式化能力（贯穿全书讨论）。 |
| `<ranges>` | 支持函数式编程风格的能力（在第6章和第13章中讨论）。 |
| `<span>` | 用于创建连续对象序列视图的能力（在第17章中讨论）。 |
| `<bit>` | 标准化的位操作运算。 |
| `<stop_token>`、`<semaphore>`、`<latch>`、`<barrier>` | 支持多线程的附加能力（在第17章中讨论）。 |

## 检查点

（填空）头文件“指示”编译器如何与库和用户编写的组件________。

**答案：** 接口。

## 5.8 案例研究：随机数生成

现在我们简要地（希望是有趣地）涉足一个流行的编程应用——模拟和游戏。在本节和下一节中，我们将开发一个包含多个函数的游戏程序。本节示例的程序输出是使用Visual Studio Community Edition生成的。你的输出可能因编译器和平台而异。

### 头文件`<random>`

你可以通过头文件`<random>`中的特性将随机性引入应用程序。这些特性取代了从C标准库引入C++的已弃用的`rand`函数。`rand`函数不具有“良好的统计特性”，并且是可预测的。⁹ 这使得使用`rand`的程序安全性较低。

9. Walter E. Brown，“Random Number Generation in C++11，”2013年3月12日。访问日期：2023年4月14日。https://isocpp.org/files/papers/n3551.pdf.

`<random>`中更安全的特性可以产生**非确定性随机数**——一组无法预测的随机数。此类随机数生成器用于模拟和安全性场景，这些场景中可预测性是不受欢迎的。

随机数生成是一个复杂的话题，数学家们为此开发了许多具有不同统计特性的算法。为了根据程序中随机数的使用方式提供灵活性，有许多类表示各种随机数生成引擎和分布。¹⁰

- 引擎实现一种生成随机数的随机数生成算法。
- 分布控制引擎产生的值范围、值的类型（例如`int`、`double`等）以及值的统计特性。

我们将使用默认的随机数生成引擎——`default_random_engine`——以及`uniform_int_distribution`，它能在指定范围内均匀分布随机整数。默认范围是从0到平台上最大的`int`值。如果`default_random_engine`和`uniform_int_distribution`真正随机地生成整数，那么每次程序请求一个随机数时，0到最大`int`值之间的每个数字被选中的机会（或概率）相同。

`default_random_engine`直接产生的值范围通常与特定应用所需的范围不同。例如，模拟抛硬币的程序可能只需要0表示“正面”，1表示“反面”。模拟掷六面骰子的程序需要1到6的随机整数。在视频游戏中，随机预测下一种飞越地平线的宇宙飞船类型（四种可能性之一）的程序可能需要0到3的随机整数。要指定值范围，你需要用应用所需的起始和结束值来初始化`uniform_int_distribution`。

### 5.8.1 掷六面骰子

图5.2模拟并显示了十次六面骰子的随机投掷结果。第9行创建了一个名为`engine`的`default_random_engine`对象来产生随机数。第12行用`{1, 6}`初始化`uniform_int_distribution`对象`randomDie`，表示它产生1到6范围内的`int`值。第16行的表达式`randomDie(engine)`返回一个1到6范围内的随机`int`。

```cpp
// fig05_02.cpp
// Producing random integers in the range 1 through 6.
#include <iostream>
#include <random>
using namespace std;

int main() {
   // engine that produces random numbers
   default_random_engine engine{};

   // distribution that produces the values 1-6 with equal likelihood
   uniform_int_distribution randomDie{1, 6};

   // display 10 random die rolls
   for (int counter{}; counter < 10; ++counter) {
      cout << randomDie(engine) << ' ';
   }

   cout << '\n';
}
```

```text
3 1 3 6 5 2 6 6 1 2
```

**图5.2** | 产生1到6范围内的随机整数。

### 5.8.2 掷六面骰子60,000,000次

为了表明前面程序中产生的随机值以近似相等的可能性出现，图5.3模拟了60,000,000次骰子投掷。¹¹ 1到6范围内的每个`int`应出现约10,000,000次（即投掷次数的六分之一）。程序的输出证实了这一点。

```cpp
// fig05_03.cpp
// Rolling a six-sided die randomly 60,000,000 times.
#include <iostream>
#include <random>
using namespace std;

int main() {
   // set up random-number generation
   default_random_engine engine{};
   uniform_int_distribution randomDie{1, 6};

   int frequency1{0}; // count of 1s rolled
   int frequency2{0}; // count of 2s rolled
   int frequency3{0}; // count of 3s rolled
   int frequency4{0}; // count of 4s rolled
   int frequency5{0}; // count of 5s rolled
   int frequency6{0}; // count of 6s rolled

   // summarize results of 60'000'000 rolls of a die
   for (int roll{1}; roll <= 60'000'000; ++roll) {
      // determine roll value 1-6 and increment appropriate counter
      switch (const int face{randomDie(engine)}) {
         case 1:
            ++frequency1; // increment the 1s counter
            break;
         case 2:
            ++frequency2; // increment the 2s counter
            break;
         case 3:
            ++frequency3; // increment the 3s counter
            break;
         case 4:
            ++frequency4; // increment the 4s counter
            break;
         case 5:
            ++frequency5; // increment the 5s counter
            break;
         case 6:
            ++frequency6; // increment the 6s counter
            break;
         default: // invalid value
            cout << "Program should never get here!";
            break;
      }
   }

   cout << format("{:>4}{:>13}\n", "Face", "Frequency"); // headers
   cout << format("{:>4}{:>13}\n", 1, frequency1)
        << format("{:>4}{:>13}\n", 2, frequency2)
        << format("{:>4}{:>13}\n", 3, frequency3)
        << format("{:>4}{:>13}\n", 4, frequency4)
        << format("{:>4}{:>13}\n", 5, frequency5)
        << format("{:>4}{:>13}\n", 6, frequency6);
}
```

| 面值 | 频率 |
|---:|---:|
| 1 | 9997896 |
| 2 | 10000608 |
| 3 | 9996800 |
| 4 | 10000729 |
| 5 | 10003444 |
| 6 | 10000523 |

**图5.3** | 随机掷六面骰子60,000,000次。（第1部分，共2部分；第2部分，共2部分。）

11. 联合作者Harvey Deitel在1976年首次为他的课堂实现此示例时，只执行了600次骰子投掷——因为6000次会花费太长时间。在我们的系统上，此程序完成60,000,000次骰子投掷大约需要五秒。600,000,000次骰子投掷大约需要一分钟。骰子投掷是顺序执行的。我们的并发章节探讨了如何并行化应用程序以利用当今的多核计算机。

### 数字分隔符

在C++程序中输入像60,000,000这样的数字时，写作60000000很容易出错。你可以使用数字分隔符`'`（单引号字符）使此类数字更具可读性并减少错误，将其插入数字组之间，如第21行所示。

### 汇总频率

`switch`初始化器（第23行）中`face`变量的定义前面有`const`。对于任何在初始化后不应改变的变量，这都是一个好做法。这使编译器能够在你不小心尝试修改变量时报告错误。

`switch`的`default`情况（第42–44行）绝不应执行，因为控制表达式（`face`）的值始终在1到6之间。许多程序员在每个`switch`语句中都提供`default`情况以捕获错误，即使他们确信自己的程序没有错误。在第6章引入数组后，我们将展示如何用一条语句优雅地替换图5.3中的整个`switch`。

### 5.8.3 为随机数生成器设定种子

再次执行图5.2的程序会产生

```text
3 1 3 6 5 2 6 6 1 2
```

这与图5.2中显示的序列相同。这些怎么可能是随机数呢？

`default_random_engine`实际上生成的是伪随机数。重复执行图5.2和图5.3的程序会产生看似随机的数字序列。然而，这些序列在每次程序执行时实际上会重复。在调试模拟程序时，随机数的可重复性对于证明对程序的修改是否正确至关重要。

一旦你彻底调试了模拟程序，你可以调整它，使每次执行产生不同的随机数序列。这称为随机化。你用`unsigned int`参数初始化`default_random_engine`，为`default_random_engine`设定种子，使其产生不同的随机数序列。

### 为`default_random_engine`设定种子

图5.4演示了用你输入的`unsigned int`（第12行）为`default_random_engine`设定种子（第15行）。只要你输入不同的种子，程序每次执行时就会产生不同的随机数序列。我们在第一次和第三次执行时使用了相同的种子，因此每次显示的都是相同的10个数字的序列。出于安全考虑，你必须确保程序在每次执行时以不同的方式（且仅一次）为随机数生成器设定种子；否则，攻击者可能推断出将产生的伪随机数序列。

```text
    1 // Fig05_04.cpp
    2 // Randomizing the die-rolling program.
    3 #include <iostream>
    4 #include <random>
    5
```

**图5.4** | 为掷骰子程序增加随机性。（第1部分，共2部分。）

