

……sin。它返回一个值，但不会输出任何内容。想一想，如果它输出任何东西会很烦人。当要求你编写一个函数来计算某些东西时，你应该编写一个返回给定值的函数，而不是一个输出给定值的函数。如果练习要求你输出某些内容，它会明确说明。

## 3.2 递归

函数可以调用其他函数。例如，我们的 compoundInterest 函数调用了 pow 函数。

一个更有趣的功能是函数可以调用自身。这种编程技术称为递归。

作为一个例子，考虑以下递归定义的序列：

$$x_n = n x_{n-1} \quad n >= 1$$
$$x_0 = 1$$
显然 $x_n = n!$。

可以定义一个函数来计算 $x_n$，如下所示：

```cpp
int factorial(int n) {
    if (n == 0) {
        return 1;
    }
    return n * factorial(n - 1);
}
```

如果用值 $n = 0$ 调用此函数，它将返回 1；否则，它将返回 n * factorial(n-1)。通过归纳法，它确实计算了 n!。

这个例子说明的 C++ 的另一个特性是，函数可以包含任意复杂的语句，这些语句将 if 语句和 return 语句结合在一起。事实上，函数可以有多个 return 语句。一旦执行了 return 语句，函数的处理就完成了，所有后续的代码行都会被忽略。

递归可以是一种强大的编程技术，如果使用递归，一些算法会更容易编写。虽然递归是计算机科学课程中的一个热门话题，但我们在本书中不会大量使用递归。练习应该给你一些关于使用递归可以实现什么以及其中一些陷阱的提示。

> 递归同样可以有效地用于构建悖论和拙劣的笑话，以及软件。作为一个例子，在 Unix 计算机上广泛使用的 GNU 软件系统的名称是一个*递归首字母缩略词*。GNU 代表“GNU 不是 Unix”。它甚至不值得让人叹息，不是吗？

## 3.3 库

正如我们所见，C++ 控制台应用程序需要一个 **main** 方法。然而，还有许多其他类型的程序，如 Windows 程序、Web 应用程序等等。一种特别重要的程序类型是*库*。库是一组软件例程的集合，旨在被用于其他计算机程序中。

在实践中，你编写库的可能性比编写独立应用程序的可能性更大。例如，你的工作可能是编写例程来对单个类型的金融衍生品进行定价。然后，由别人负责将你的库与其他人编写的库组装起来，以编写交易应用程序等。

因此，我们实际上对程序的 **main** 方法并不怎么感兴趣。我们将保留一个 **main** 方法用于测试目的，但你应该停止以编写程序的方式思考。从现在开始，你应该想象我们在本书中编写的软件是一个定价库，而不是一个独立程序。我们的目标是编写有用的函数，而不是编写单个程序。

## 3.4 声明和定义函数

在我们的示例代码中，我们在 **main** 函数之前定义了函数 `compoundInterest`。我们这样做是因为 **main** 函数使用了 `compoundInterest` 函数。

在更复杂的递归代码中，你可能希望编写相互调用的函数。为了支持这一点，C++ 允许你*声明*一个函数，然后稍后*定义*它。

当你*声明*一个函数时，你说明它的名称以及它所需的参数类型。当你*定义*一个函数时，你说明该函数实际执行的操作。

在我们所有的函数定义中，之前我们都将声明和定义放在一起。但如果你愿意，可以将声明和定义分开。

这里是一个独立的复利函数的*声明*。

```cpp
double compoundInterest(double P, double i, int n);
```

请注意，这与函数定义的第一行完全相同，只是大括号被分号替换了。

然后将*定义*放在代码中的任何你喜欢的位置。*定义*就是我们之前看到的所有代码：

```cpp
double compoundInterest(double P, double i, int n) {
    double interest = P * pow(1 + 0.01*i, n) - P;
    return interest;
}
```

因此，C++ 的定义实际上在开头包含了声明。

以下是我们的示例程序，重写后使得 main 方法在 compoundInterest 函数之前被*定义*。请注意，compoundInterest 函数仍然是先*声明*的。

```cpp
#include <iostream>
#include <cmath>
using namespace std;

double compoundInterest(double P, double i, int n);

int main() {
    int principal;
    double interestRate;
    int numberOfYears;
    cout << "How much are you investing ?\n";
    cin >> principal;
    cout << " What's the annual interest rate(%)?\n";
    cin >> interestRate;
    cout << "How long for ( years )?\n";
    cin >> numberOfYears;
    double interest = compoundInterest(principal, interestRate, numberOfYears);
    cout << "You will earn ";
    cout << interest;
    cout << "\n";
    return 0;
}

double compoundInterest(double P, double i, int n) {
    double interest = P * pow(1 + 0.01*i, n) - P;
    return interest;
}
```

从技术上讲，你实际上可以简化函数声明以排除参数名称。这是一个完全有效的函数声明：

```cpp
double compoundInterest(double, double, int);
```

注意它与数学陈述的类比：

$$\text{compoundInterest} : \mathbb {R} \times \mathbb {R} \times \mathbb {Z} \longrightarrow \mathbb {R} .$$

计算机忽略函数声明中的参数名称，因此它们不必与定义中的参数名称匹配。

在 C++ 中，你可以分离声明和定义的想法经常出现。另一个例子发生在变量上。你可以声明它们的类型，并单独为它们赋值。或者，如果你愿意，可以在一个语句中同时声明和定义它们。

例如：

```cpp
double principal;
```
声明了一个变量，而下面这行：

```cpp
principal = 1000.0;
```
为变量赋值。下面这行

```cpp
double principal = 1000.0;
```
在一步中执行声明和赋值。

### 提示：声明在定义之前

当你编写 C++ 文件时，将所有函数声明放在第一个定义之前。

由于函数声明不包含任何代码（因此不能使用其他函数），不同函数声明的顺序并不重要。你应该先声明最有趣的函数，以便阅读你文件的某人能迅速理解代码的意图。

抵制尝试重新排序函数以使代码在没有单独声明的情况下编译的冲动。

## 3.5 不返回值的函数

除了计算值之外，C++ 函数还可以执行诸如向屏幕写入文本、通过网络发送数据、打印文件等任务。这是计算机函数与纯粹数学上的函数概念之间的重要区别。

你经常希望函数执行一项任务，而实际上并不希望它计算一个值。为此，你使用特殊的关键词 **void** 来描述返回类型。

例如，下面给出的函数 **printHello** 简单地打印消息“Hello”然后返回。

```cpp
void printHello() {
    cout << "Hello\n";
}
```

### 危险！

如果还没有明显的话，在这段代码片段中，我们省略了需要 `#include <iostream>` 行和 `using namespace std;` 行的说明。我们通常会省略 `#include` 语句和 `using namespace std;` 语句。

## 3.6 指定默认值

有时你可能希望为参数指定默认值。例如，这里是一个函数的声明，它允许你对分红股票的看涨期权进行定价，但如果未提供，则假设分红率为零。

```cpp
double computePrice(double strike,
                    double timeToMaturity,
                    double spot,
                    double riskFreeRate,
                    double volatility,
                    double dividendRate = 0.0);
```

如果你有单独的声明和定义，你应该像这里一样将默认值放入声明中。

