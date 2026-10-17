
## 5.7 摄氏度和华氏度之间的转换

编写一个包含两个函数的头文件：

```cpp
/* 将摄氏度转换为华氏度 */
double celsiusToFahrenheit(double celsius)

/* 将华氏度转换为摄氏度 */
double fahrenheitToCelsius(double fahrenheit)
```

转换公式为：

$fahrenheit = (9.0 / 5) * celsius + 32$

实现该头文件并编写一个测试程序，调用这些函数显示以下表格：

| 摄氏度 | 华氏度 | 摄氏度 |
| --- | --- | --- |
| 40.0 | 104.0 | 48.89 |
| 39.0 | 102.2 | 43.33 |
| ... | ... | ... |
| 32.0 | 89.6 | 40.0 4.44 |
| 31.0 | 87.8 | 30.0 -1.11 |

## 5.8 英尺和米之间的转换

编写一个包含两个函数的头文件：

```cpp
/* 将英尺转换为米 */
double footToMeter(double foot)

/* 将米转换为英尺 */
double meterToFoot(double meter)
```

转换公式为：

$meter = 0.305 * foot$

实现该头文件并编写一个测试程序，调用这些函数显示以下表格：

| 英尺 | 米 | 英尺 |
| --- | --- | --- |
| 1.0 | 0.305 | 3.28 |
| 2.0 | 0.61 | 6.56 |
| ... | ... | ... |
| 9.0 | 2.7 | 2.7 |
| 10.0 | 3.05 | 3.1 |

## 5.9 使用 `isPrime`

使用 5.5，`Prime.cpp`，使用 `isPrime(int number)` 测试一个数是否为质数。

## 5.10 财务应用：计算税金

使用 5.4，`Compute.cpp`，编写一个计算税金的函数。头文件如下：

```cpp
double computeCommission(double salesAmount)
```

编写测试程序显示以下表格：

| 销售额 | 税金 |
| --- | --- |
| 10000 | 900.0 |
| 15000 | 1500.0 |
| ... | ... |
| 95000 | 9500.0 |
| 100000 | 10000.0 |

## 5.11 显示字符

编写一个函数打印字符，头文件如下：

```cpp
void printChars(char ch1, char ch2, int numberPerLine)
```

该函数打印 `ch1` 到 `ch2` 之间的字符，每行 `numberPerLine` 个。编写一个测试程序打印 `'A'` 到 `'Z'`。

## 5.12* 求和

编写一个函数计算以下序列：

```cpp
double sumSeries(int i)
```

编写一个测试程序显示以下表格：

| 数字 | 平方根 |
| --- | --- |
| 0 | 0.0000 |
| 2 | 1.4142 |
| ... | ... |
| 18 | 4.2426 |
| 20 | 4.4721 |

## 5.13* 求和

编写一个函数计算以下序列：

```cpp
double sumSeries(int i)
```

## 5.14* 财务应用：打印税额

使用 3.4，`Tax.cpp`，编写一个计算税额的函数。头文件如下：

```cpp
double computeTax(int status, double taxableIncome)
```

编写一个测试程序，打印从 $50,000 到 $60,000 之间、每 $50 一个间隔、所有状态的税额表，如下：

| 纳税收入 | 单身 | 夫妻共同 | 户主 |
| --- | --- | --- | --- |
| 50000 | 9846 | 7296 | 10398 |
| 50050 | 9860 | 7310 | 10412 |
| ... | ... | ... | ... |
| 59950 | 12533 | 9983 | 13190 |
| 60000 | 12546 | 9996 | 13205 |

## 5.15 年的天数

编写一个返回每年天数的函数，头文件如下：

```cpp
int numberOfDaysInYear(int year)
```

编写一个测试程序显示 2000 到 2010 年的天数。

## 5.16 显示 0 和 1 矩阵

编写一个函数显示 $n \times n$ 矩阵，头文件如下：

```cpp
void printMatrix(int n)
```

每个元素是随机生成的 0 或 1。编写一个测试程序打印 $3 \times 3$ 的矩阵，可能如下：

```
0 1 0
0 0 0
1 1 1
```

## 5.17 生成随机字符

使用 5.12 `RandomCharacter.h` 中定义的函数打印 100 个大写字母和 100 个单数字，每行十个。

## 5.18 使用 `sqrt` 函数

编写一个程序，使用 `sqrt` 函数打印以下表格：

| 数字 | 平方根 |
| --- | --- |
| 0 | 0.0000 |
| 2 | 1.4142 |
| ... | ... |
| 18 | 4.2426 |
| 20 | 4.4721 |

## 5.19 Triangle 头文件

创建一个名为 `MyTriangle.h` 的头文件，包含以下函数：

```cpp
/* 如果任意两边之和大于第三边，则返回 true。 **/
bool isValid(double side1, double side2, double side3)
```

```cpp
/* 返回三角形的面积。 **/
double area(double side1, double side2, double side3)
```

计算面积的公式在练习 2.19 中。实现该头文件并编写一个测试程序，读取三角形的三条边，如果输入有效则计算输出。否则，显示输入无效。

# 第 5 章 函数基础

## 使用三角函数

打印下表，显示从 0 到 360 度、增量为 10 度的 `sin` 值和 `cos` 值。将数值保留小数点后四位。

| 度数 | Sin | Cos |
| --- | --- | --- |
| 0 | 0.0000 | 1.0000 |
| 10 | 0.1736 | 0.9848 |
| ... | ... | ... |
| 350 | -0.1736 | 0.9848 |
| 360 | 0.0000 | 1.0000 |

## 金融应用：计算平均值和标准差

在业务应用中，你被要求计算数据的平均值和标准差。标准差是一种统计量，用于说明一组中所有数据围绕平均值的紧密程度。例如，一个班级学生的平均年龄是多少？如果所有学生的年龄相同，则标准差为 0。编写一个程序，提示用户输入 10 个数字，并使用以下方法计算这些数字的平均值和标准差：

![](img/3b8bc24ba08ad32ac1a370eb095746a9_205_0.png)

以下是示例运行：

![](img/3b8bc24ba08ad32ac1a370eb095746a9_205_1.png)

## 金融应用：计算未来投资价值

编写一个函数，计算给定利率下指定年限的未来投资价值。未来价值根据练习 2.11 中的公式确定。使用以下函数头：

```cpp
double futureInvestmentValue(
    double investmentAmount, double monthlyInterestRate, int years)
```

例如，`futureInvestmentValue(10000, 0.05/12, 5)` 返回 12833.59。

编写一个测试程序，提示用户输入投资金额（例如 1000）和利率（例如 9%），并打印一个显示 1 到 30 年未来价值的表格，如下所示：

![](img/3b8bc24ba08ad32ac1a370eb095746a9_205_2.png)

# 第 6 章 高级函数特性

## 目标

- 通过按值传递参数 (§6.2)。
- 通过按引用传递参数 (§6.3)。
- 理解按值传递和按引用传递的区别 (§6.2–6.3)。
- 声明 `const` 参数以防止参数被意外修改 (§6.4)。
- 确定局部变量和全局变量的作用域 (§6.5)。
- 使用内联函数提高短函数的运行时效率 (§6.6)。
- 定义带有默认参数的函数 (§6.7)。
- 使用步步细化方法设计并实现函数 (§6.8)。

![](img/3b8bc24ba08ad32ac1a370eb095746a9_206_0.png)

## 6.1 引言

在前一章中，你学习了如何定义和调用函数，如何使用数学函数和字符函数。本章涵盖了函数的头文件，以及如何使用关于按值传递、按引用传递、常量参数、全局和静态变量、内联函数、默认参数以及使用函数进行步步细化的程序设计等高级主题。

## 6.2 按值传递参数

当你像前一章描述的调用带有参数的函数时，参数的值会被传递给参数。这被称为按值传递。如果参数是一个变量而不是字面量，则变量的值会被传递给参数。无论函数内部对参数进行了什么修改，该变量都不会受到影响。如列表 6.1 所示，`x` 的值 (1) 被传递给参数 `n` 以调用递增函数（第 14 行）。`x` 在函数中（第 6 行）增加了 1，但无论函数如何操作，`x` 都不会改变。

按值传递

列表 6.1 `Increment.cpp`

```cpp
#include <iostream>
using namespace std;
void increment(int n)
{
    n++;
    cout << "\tn inside the function is " << n << endl;
}
int main()
{
    int x = 1;
    cout << "Before the call, x is " << x << endl;
    increment(x);
    cout << "after the call, x is " << x << endl;
    return 0;
}
```

调用 `increment` 后，`x` 是 1。函数内部 `n` 是 2。调用后，`x` 是 1。

## 6.3 按引用传递参数

按值传递有严重的局限性。列表 6.2 说明了这些局限性。程序创建了一个用于交换两个变量的函数。通过传递两个参数来调用 `swap` 函数。然而，在函数调用后，参数的值并没有发生改变。

按值传递的局限性

列表 6.2 `TestPassByValue.cpp`

```cpp
#include <iostream>
using namespace std;
```

![](img/3b8bc24ba08ad32ac1a370eb095746a9_207_0.png)

按值传递 vs. 按引用传递

尝试交换变量无效！

```cpp
void swap(int n1, int n2)
{
    cout << "\tinside the swap function" << endl;
    cout << "\tBefore swapping n1 is " << n1 << endl;
    cout << "\tn2 is " << n2 << endl;

    // 交换 n1 和 n2
    int temp = n1;
    n1 = n2;
    n2 = temp;

    cout << "\tAfter swapping n1 is " << n1 << endl;
}

int main()
{
    // 声明并初始化变量
    int num1 = 1;
    int num2 = 2;

    cout << "\tBefore invoking the swap function, num1 is " << num1 << " and num2 is " << num2 << endl;

    // 调用 swap 函数交换两个变量
    swap(num1, num2);

    cout << "\tAfter invoking the swap function, num1 is " << num1 << " and num2 is " << num2 << endl;

    return 0;
}
```

调用 `swap` 函数之前，`num1` 是 1，`num2` 是 2。在 `swap` 函数内部，交换前 `n1` 是 1，`n2` 是 2；交换后 `n1` 是 2，`n2` 是 1。调用 `swap` 函数后，`num1` 是 1，`num2` 是 2。

![](img/3b8bc24ba08ad32ac1a370eb095746a9_208_0.png)

在调用 `swap` 函数之前（第 30 行），`num1` 是 1，`num2` 是 2。在调用 `swap` 函数后，`num1` 仍然是 1，`num2` 是 2。它们的值没有被交换。如图 6.1 所示，参数 `n1` 和 `n2` 的值被传递给函数参数，但 `n1` 和 `n2` 拥有独立于 `num1` 和 `num2` 的内存位置。因此，`n1` 和 `n2` 的更改不会影响 `num1` 和 `num2` 的内容。

## 6.3 引用传递参数

![](img/3b8bc24ba08ad32ac1a370eb095746a9_210_0.png)

**图 6.2** `aliasForcount` 和 `count` 具有相同的值。

第 15 行将 10 赋值给 `count`。对 `count` 的任何更改也会应用于 `aliasForcount`，反之亦然。现在 `count` 和 `aliasForcount` 均为 10。

注意

声明引用变量的以下符号是等价的：

```
int &refVar;
int & refVar;
int& refVar;
```

为了一致起见，本书使用了第一种写法。

你可以将引用变量作为函数的参数，并传递普通变量来调用函数。该参数变成原始变量的别名。这被称为“引用传递”（pass-by-reference）。当你通过引用变量改变值时，原始值实际上被改变了。为了演示引用传递的效果，让我们像列表 6.4 那样重写列表 6.1 中的递增函数。

引用传递

# 列表 6.4 `IncrementPassByReference.cpp`

```cpp
#include <iostream>
using namespace std;

void increment(int &n)
{
    n++;
    cout << "The address of n is " << n << endl;
    cout << "n inside the function is " << n << endl;
}

int main()
{
    int x = 1;
    cout << "the address of x is " << &x << endl;
    cout << "Before the call, x is " << x << endl;
    increment(x);
    cout << "After the call, x is " << x << endl;

    return 0;
}
```

The address of x is 0013FF60

Before the call, x is 1

The address of n is 0013FF60

n inside the function is 2

After the call, x is 2

![](img/3b8bc24ba08ad32ac1a370eb095746a9_210_1.png)

## 第 6 章 高级特性

在第 16 行调用 `increment(x)` 将变量 `x` 的引用传递给 `increment` 函数中的参数 `n`。现在 `n` 和 `x` 具有相同的地址 `0013FF60`，如输出所示。在函数中 (6) 增加 `n` 等同于增加 `x`。因此，在调用函数之前，`x` 是 1，之后，`x` 变为 2。

值传递和引用传递是将参数传递给函数参数的两种方式。值传递将值传递给独立变量，而引用传递则共享同一个变量。从语义上讲，引用传递可以描述为共享传递。现在你可以使用引用参数来实现一个正确的引用交换函数，如列表 6.5 所示。

# 列表 6.5 `TestPassReference.cpp`
