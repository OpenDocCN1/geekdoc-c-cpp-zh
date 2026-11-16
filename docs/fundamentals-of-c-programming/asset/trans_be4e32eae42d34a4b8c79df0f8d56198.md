

```
trial_factor++)
    is_prime = (value % trial_factor != 0);
    if (is_prime)
        std::cout << value << " "; // Display the prime number
}
std::cout << '\n'; // Move cursor down to next line
end_time = clock();
// Print the elapsed time
std::cout << "Elapsed time: "
    << static_cast<double>(end_time - start_time)/CLOCKS_PER_SEC
    << " sec." << '\n';
}
```

在某个系统上，该程序平均需要 93 秒来打印小于等于 500,000 的所有质数。相比之下，更新、更高效的版本（清单 8.5，moreefficientprimes.cpp）使用了平方根优化，仅需 15 秒即可显示小于等于 500,000 的所有质数。具体时间会因计算机速度而异。

事实证明，程序执行时间的大部分花费在打印输出上，而非计算要打印的质数。我们可以通过将程序输出重定向到文件来更好地比较算法。如果可执行程序名为 primes.exe，可以在命令行中通过发出以下命令来重定向其输出：

```
primes > run1.out
```

这将创建一个名为 run1.out 的文本文件，可以用任何文本编辑器查看。其内容正是未使用重定向时本应打印到屏幕上的内容。

使用重定向运行时，时间差异更加显著：未优化版本生成小于等于 500,000 的质数需要 77 秒，而使用平方根优化的版本仅需 2 秒即可生成相同数量的质数！更快的质数生成器可在清单 11.25（fasterprimes.cpp）中找到；它使用完全不同的算法来生成质数。

在程序中使用标准时间函数，必须 #include <ctime> 头文件。

## 8.5 字符函数

C 库提供了若干对 C++ 程序员有用的字符函数。清单 8.9（touppercase.cpp）将小写字母转换为大写字母。

```
Listing 8.9: touppercase.cpp

#include <iostream>
#include <cctype>

int main() {
    for (char lower = 'a'; lower <= 'z'; lower++) {
        char upper = toupper(lower);
        std::cout << lower << " = " << upper << '\n';
    }
}
```

清单 8.9（touppercase.cpp）打印的前几行如下：

```
a = A
b = B
c = C
d = D
```

有趣的是，`toupper` 函数返回的是 `int`，而不是 `char`。在 Visual C++ 的增强警告级别 4 下，需要进行强制类型转换才能将结果赋值给变量 `upper`：

```
char upper = static_cast<char>(toupper(lower));
```

表 8.2 描述了一些更有用的字符函数。

| 函数 | 描述 |
| --- | --- |
| int toupper(int ch) | 返回给定字符的大写形式；如果不存在大写形式（例如标点符号或数字），则返回原始字符 |
| int tolower(int ch) | 返回给定字符的小写形式；如果不存在小写形式（例如标点符号或数字），则返回原始字符 |
| int isupper(int ch) | 如果 ch 是大写字母（'A'-'Z'），则返回非零值（true）；否则返回 0（false） |
| int islower(int ch) | 如果 ch 是小写字母（'a'-'z'），则返回非零值（true）；否则返回 0（false） |
| int isalpha(int ch) | 如果 ch 是字母表中的字母（'A'-'Z' 或 'a'-'z'），则返回非零值（true）；否则返回 0（false） |
| int isdigit(int ch) | 如果 ch 是数字（'0'-'9'），则返回非零值（true）；否则返回 0（false） |

表 8.2：cctype 库中的部分函数

还有其他函数可用于判断字符是否为标点字符（如逗号或分号，`ispunct`）、空格、制表符或换行符（`isspace`）。

在 C++ 程序中使用标准 C 字符函数，必须包含 `<cctype>` 头文件。

## 8.6 随机数

某些应用程序需要表现出随机性的行为。随机数在游戏和模拟中特别有用。例如，许多棋盘游戏使用一个骰子（一对骰子中的一个）来确定玩家应前进多少格。（参见图 8.5。）骰子或一对骰子也用于其他机会游戏。骰子是一个立方体，其六个面上各带有若干点。点数范围从 1 到 6。玩家掷一个骰子，有时掷一对骰子，朝上的面在所玩的游戏中具有意义。掷骰子后某个面的点数由骰子的复杂翻滚随机决定。涉及骰子的游戏的软件改编需要一种方法来模拟随机掷骰子。

### 图 8.5 一对骰子

![](img/e84ad11adb18201d71595b31ce6c9eff_205_0.png)

所有算法随机数生成器实际上都生成伪随机数，而非真随机数。伪随机数生成器有一个特定的周期，取决于所使用算法的性质。如果生成器使用足够长的时间，生成的数字模式将精确重复。真随机数序列不会包含这样的重复子序列。好消息是，所有实用的算法伪随机数生成器的周期都足够大，足以满足大多数应用程序的需求。

C++ 程序员可以使用两个标准 C 函数来生成伪随机数：srand 和 rand：

```
void srand(unsigned)
int rand();
```

srand 建立伪随机整数值序列的第一个值。每次调用 rand 都会返回伪随机值序列中的下一个值。清单 8.10（simplerandom.cpp）展示了如何打印 100 个伪随机数的序列。

```
Listing 8.10: simplerandom.cpp

#include <iostream>
#include <cstdlib>

int main() {
    srand(23);
    for (int i = 0; i < 100; i++) {
        int r = rand();
        std::cout << r << " ";
    }
    std::cout << '\n';
}
```

程序打印的数字看起来是随机的。算法以一个种子值开始，并使用公式生成下一个值。种子值决定生成的数字序列；相同的种子值生成相同的序列。如果再次运行程序，将显示相同的序列，因为使用了相同的种子值 23。为了使每次程序运行都显示不同的序列，每次运行的种子值必须不同。我们如何为每次运行建立不同的种子值？在运行时构建“随机”种子的最佳方法是使用 ctime 库中找到的 time 函数。调用 time(0) 返回自 1970 年 1 月 1 日午夜以来的秒数。

这个值在不同程序运行之间显然不同，因此每次执行都会使用不同的种子值，生成的伪随机数序列也会不同。清单 8.11（betterrandom.cpp）引入了 time 函数，以提高多次执行时的随机性。

### 清单 8.11：betterrandom.cpp

```
#include <iostream>
#include <cstdlib>
#include <ctime>

int main() {
   srand(static_cast<unsigned>(time(0)));
   for (int i = 0; i < 100; ++i) {
      int r = rand();
      std::cout << r << " ";
   }
   std::cout << '\n';
}
```

清单 8.11（betterrandom.cpp）的每次执行都会生成不同的伪随机数序列。time 返回的实际值类型是 time_t，因此 time 调用的结果在与 srand 一起使用之前必须强制转换为 unsigned int。

请注意，rand 返回的数字可能相当大。伪随机值的范围是从 0 到依赖于实现的最大值。Visual C++ 的 rand 函数的最大值为 32,767，对应于最大的 16 位有符号 int 值。cstdlib 头文件定义了常量 RAND_MAX，表示范围内的最大值。以下语句

```
std::cout << RAND_MAX << '\n';
```

将打印特定系统上 RAND_MAX 的值。

通常我们需要更有限范围内的值，例如 1..100。使用取模运算符进行简单的算术运算可以产生我们需要的结果。如果 n 是任意非负整数，m 是任意正整数，则表达式

```
n % m
```

生成 0...m-1 范围内的值。

这意味着语句

```
int r = rand() % 100;
```

只能将 0..99 范围内的值赋给 r。如果我们确实需要 1..100 范围内的值，该怎么办？我们只需在结果上加 1 即可：

```
int r = rand() % 100 + 1;
```

该语句生成 1..100 范围内的伪随机数。

现在我们拥有编写模拟掷骰子程序所需的一切。

清单 8.12（die.cpp）模拟掷骰子。

