
为此，添加一个成员变量（一个数组），用于保存按成分涨跌幅排序的股票列表索引。将此数组命名为 `sortIndicesGainLoss`。当打印按成分涨跌幅排序的列表时，使用数组 `sortIndicesGainLoss` 来打印该列表。数组 `sortIndicesGainLoss` 的元素将指出接下来要打印股票列表中的哪个成分。

- c. 编写一个程序，使用这两个类来自动化公司的股票数据分析。
- 18. 编写本章未给出的类 `arrayListType` 和 `unorderedArrayListType` 的成员函数定义。还要编写一个程序来测试你的函数。
- 19. 编写从类 `arrayListType` 派生的类模板 `orderedArrayList` 的定义，以实现有序表。如第13章那样，在此类中添加函数 `insert`。提供非抽象函数的定义。还要编写一个程序来测试你的类。
- 20. **（无序集合）** 使用模板重做第13章的编程练习12。
- 21. **（有序集合）** 使用模板重做第13章的编程练习13。

![](img/f97f778697507bb6fdd80c5991210cba_960_0.png)

## 第15章：异常处理

本章中，你将：

- 了解什么是异常
- 学习如何在程序内处理异常
- 了解如何使用 try/catch 块处理异常
- 熟悉 C++ 异常类
- 学习如何创建自己的异常类
- 了解如何抛出和重新抛出异常
- 探索栈展开

异常是在程序执行期间可以检测到的不期望情况的发生。例如，除以零就是一个异常。类似地，尝试打开一个不存在的输入文件也是异常，数组索引越界也是异常。

到目前为止，我们通过使用 `if` 语句或 `assert` 函数处理了某些异常。例如，在示例5-3和5-4中，在将 `sum` 除以 `counter` 或 `count` 之前，我们检查了 `counter` 或 `count` 是否非零。类似地，在编程示例 `newString`（第14章）中，我们使用 `assert` 函数来确定数组索引是否在边界内。

另一方面，有些地方我们只是忽略了异常。例如，在确定字符串中的子串时（第8章），我们从未检查子串的起始位置是否在范围内。此外，我们没有处理数组索引越界异常。然而，在所有这些情况下，如果程序执行期间发生异常，我们要么包含了终止程序的代码，要么程序以适当的错误消息终止。例如，如果我们在函数 `main` 中打开一个输入文件，而该输入文件不存在，我们终止了函数 `main`，因此程序被终止。

有些情况下会发生异常，但你不想让程序只是忽略异常并终止。例如，监控股票表现的程序不应在账户余额低于某个水平时自动卖出。它应该通知股东并请求采取适当的操作。类似地，如果血压变得很高，监控患者心跳的程序不能被终止。如果卫星的某个部分发生临时电源故障，监控太空中卫星的程序不能被终止。

处理异常的代码取决于你开发的应用程序类型。提供异常处理代码的一种常见方式是在可能发生错误的位置添加异常处理代码。这种技术使阅读代码的程序员能够将异常处理代码与实际代码一起看到，并确定错误检查代码是否被正确实现。这种方法的缺点是程序可能会因异常处理代码而变得杂乱，这会使理解和维护程序变得困难。这可能会分散程序员的注意力，使其无法确保程序正常运行。

### 在程序内处理异常

在第3章中，我们注意到，如果你试图将无效数据输入到变量中，输入流会进入失败状态，因此发生异常。例如，如果你试图将字母输入到 `int` 变量中，就会发生这种情况。第3章还展示了如何清除和恢复输入流。第4章介绍了 `assert` 函数，并解释了如何使用它来避免某些不可预见的错误，例如除以零。尽管函数 `assert` 可以检查表达式是否满足所需条件，但如果条件不满足，它会终止程序。如上一节所述，有些情况下，如果出现问题，程序不应被简单地终止。

本节讨论如何处理异常。不过，首先我们提供一些示例，说明如果未处理异常会发生什么。我们还回顾一些处理异常的方法。

示例15-1中的程序展示了当发生除以零且该问题未被处理时会发生什么。

**示例 15-1**

```cpp
// Division by zero.

#include <iostream>

using namespace std;

int main()
{
    int dividend, divisor, quotient;                    //Line 1

    cout << "Line 2: Enter the dividend: ";             //Line 2
    cin >> dividend;                                     //Line 3
    cout << endl;                                        //Line 4

    cout << "Line 5: Enter the divisor: ";              //Line 5
    cin >> divisor;                                      //Line 6
    cout << endl;                                        //Line 7

    quotient = dividend / divisor;                       //Line 8
    cout << "Line 9: Quotient = " << quotient
         << endl;                                        //Line 9

    return 0;                                            //Line 10
}
```

**示例运行 1：**

```text
Line 2: Enter the dividend: 12
Line 5: Enter the divisor: 5
Line 9: Quotient = 2
```

**示例运行 2：**

```text
Line 2: Enter the dividend: 24
Line 5: Enter the divisor: 0
CPP_Proj1.exe has encountered a problem and needs to close. We are
sorry for the inconvenience.
```

在示例运行1中，divisor 的值非零，因此不会发生异常。程序计算并输出商，然后正常终止。

在示例运行2中，为 divisor 输入的值是0。第8行的语句将 dividend 除以 divisor。然而，程序在将 dividend 除以 divisor 之前没有检查 divisor 是否为0。因此程序崩溃，并显示所示消息。注意，错误消息依赖于平台，也就是说，依赖于 IDE。某些 IDE 可能不会给出此错误消息，而可能只是挂起。

接下来，考虑示例15-2。这与示例15-1中的程序相同，不同之处在于第8行中程序检查 divisor 是否为零。

**示例 15-2**

```cpp
// Checking division by zero.

#include <iostream>

using namespace std;

int main()
{
    int dividend, divisor, quotient;                  //Line 1

    cout << "Line 2: Enter the dividend: ";           //Line 2
    cin >> dividend;                                  //Line 3
    cout << endl;                                     //Line 4

    cout << "Line 5: Enter the divisor: ";            //Line 5
    cin >> divisor;                                   //Line 6
    cout << endl;                                     //Line 7

    if (divisor != 0)                                 //Line 8
    {
        quotient = dividend / divisor;                //Line 9
        cout << "Line 10: Quotient = " << quotient
             << endl;                                 //Line 10
    }
    else                                              //Line 11
        cout << "Line 12: Cannot divide by zero."
             << endl;                                 //Line 12

    return 0;                                         //Line 13
}
```

**示例运行 1：**

```text
Line 2: Enter the dividend: 12

Line 5: Enter the divisor: 5

Line 10: Quotient = 2
```

