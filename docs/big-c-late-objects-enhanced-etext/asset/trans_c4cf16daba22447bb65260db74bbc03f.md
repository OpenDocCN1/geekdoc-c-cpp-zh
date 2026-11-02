

考虑一个模拟从银行账户中提取指定金额的函数，前提是账户中有足够的资金。如果金额不足，则改为扣除10美元的罚款。该函数的使用方式如下：

```cpp
double harrys_account = 1000;
withdraw(harrys_account, 100); // Now harrys_account is 900
withdraw(harrys_account, 1000); // Insufficient funds. Now harrys_account is 890
```

下面是一个初步尝试：

```cpp
void withdraw(double balance, double amount) // Does not work
{
    const double PENALTY = 10;
    if (balance >= amount)
    {
        balance = balance - amount;
    }
    else
    {
        balance = balance - PENALTY;
    }
}
```

但这行不通。

让我们逐步分析函数调用 `withdraw(harrys_account, 100)` — 参见图6。当函数开始时，参数变量 `balance` 被创建①，并设置为与 `harrys_account` 相同的值，`amount` 被设置为100②。然后 `balance` 被修改③。当然，这种修改对 `harrys_account` 没有任何影响，因为 `balance` 是一个独立的变量。当函数返回时，`balance` 被遗忘，没有钱从 `harrys_account` 中被取出④。

> 修改值参数对调用者没有影响。

参数变量 `balance` 被称为**值参数**，因为它用传入参数的值进行初始化。我们目前编写的所有函数都使用值参数。然而，在这种情况下，我们不只希望 `balance` 与 `harrys_account` 具有相同的值。我们希望 `balance` 指向实际的变量 `harrys_account`（或 `joes_account`，或调用中提供的任何变量）。该变量的内容应该被更新。

> 引用参数指向函数调用中提供的变量。

当你想更新函数调用中提供的变量时，可以使用引用参数。当我们把 `balance` 变成引用参数时，`balance` 就不是一个新变量，而是对现有变量的引用。对 `balance` 的任何更改实际上都是对该特定调用中 `balance` 所引用的变量的更改。

![](img/d61019b035dd82beb581604273c0ee6b_263_0.png)

*银行余额的引用参数就像一张ATM卡——它允许你改变余额。相比之下，值参数只能告诉你余额是多少。*

© Winston Davidian/iStockphoto.

![](img/d61019b035dd82beb581604273c0ee6b_264_0.png)

### 图6：当balance和account是值参数时

图7显示了值参数和引用参数之间的区别。

要表示引用参数，请在类型名后放置一个&。

```cpp
void withdraw(double& balance, double amount)
```

类型 `double&` 读作“对double的引用”，或更简洁地读作“double引用”。

withdraw函数现在有两个参数变量：一个是“double引用”类型，另一个是double类型的值参数。函数体保持不变。

改变的是对balance变量赋值的含义。

![](img/d61019b035dd82beb581604273c0ee6b_264_1.png)

### 图7：引用参数和值参数

赋值语句

```cpp
balance = balance - amount;
```

现在会改变传递给函数的变量（参见图8）。

例如，调用

```cpp
withdraw(harrys_account, 100);
```

会修改变量 `harrys_account`，而调用

```cpp
withdraw(sallys_account, 150);
```

会修改变量 `sallys_account`。

修改引用参数会更新调用中提供的变量。

引用参数的实参必须始终是一个变量。如果提供一个数字，那将是错误的：

```cpp
withdraw(1000, 500); // Error: argument for reference parameter must be a variable
```

原因很清楚——函数会修改引用参数，但不可能改变一个数字的值。出于同样的原因，你不能提供一个表达式：

```cpp
withdraw(harrys_account + 150, 500);
// Error: argument for reference parameter must be a variable
```

带引用参数的函数也可以有返回值。例如，你可以修改withdraw函数，使其返回一个bool值，表示提款是否成功：

```cpp
bool withdraw(double& balance, double amount)
```

![](img/d61019b035dd82beb581604273c0ee6b_265_0.png)

### 图8：当balance是引用参数时

或者，你也可以为此目的提供第二个引用参数：

```cpp
void withdraw(double& balance, double amount, double& success)
```

### sec09/account.cpp

```cpp
#include <iostream>
using namespace std;
/**
 * Withdraws the amount from the given balance, or withdraws
 * a penalty if the balance is insufficient.
 * @param balance the balance from which to make the withdrawal
 * @param amount the amount to withdraw
 */
void withdraw(double& balance, double amount)
{
    const double PENALTY = 10;
    if (balance >= amount)
    {
        balance = balance - amount;
    }
    else
    {
        balance = balance - PENALTY;
    }
}
int main()
{
    double harrys_account = 1000;
    double sallys_account = 500;
    withdraw(harrys_account, 100);
    // Now harrys_account is 900
    withdraw(harrys_account, 1000); // Insufficient funds
    // Now harrys_account is 890
    withdraw(sallys_account, 150);
    cout << "Harry's account: " << harrys_account << endl;
    cout << "Sally's account: " << sallys_account << endl;
    return 0;
}
```

### 程序运行

```text
Harry's account: 890
Sally's account: 350
```

![](img/d61019b035dd82beb581604273c0ee6b_266_0.png)

### 编程技巧5.7：优先使用返回值而不是引用参数

有些程序员使用引用参数作为设置函数结果的机制。例如，

```cpp
void cube_volume(double side_length, double& volume)
{
    volume = side_length * side_length * side_length;
}
```

然而，这个函数不如我们之前使用的 `cube_volume` 函数方便。它不能在诸如 `cout << cube_volume(2)` 的表达式里使用。只有在函数需要更新某个变量时，才使用引用参数。

![](img/d61019b035dd82beb581604273c0ee6b_267_0.png)

### 专题5.2：常量引用

值参数如果是一个大型对象（比如字符串值），其效率并不高。将对象复制到参数变量中，不如使用引用参数高效。使用引用参数时，只需要向函数传递变量的位置，而不是它的值。

你可以通过使用如下所示的常量引用，让编译器在获得引用参数的高效性的同时，又具有值参数的含义。函数

```cpp
void shout(const string& str)
{
    cout << str << "!!!" << endl;
}
```

与下面的函数完全相同：

```cpp
void shout(string str)
{
    cout << str << "!!!" << endl;
}
```

只有一个区别：调用第一个函数的执行速度会稍快一些。

## 5.10 递归函数（可选）

递归函数是调用自身的函数。这并不像乍听起来那么不寻常。假设你面临着清理整栋房子的艰巨任务。你很可能会对自己说：“我挑一个房间打扫一下，然后再打扫其他房间。”换句话说，清理任务调用了自身，但输入更简单。最终，所有房间都会被清理干净。

在C++中，递归函数使用相同的原理。这里有一个典型的例子。我们想打印如下所示的三角形图案：

```text
[]
[ ][ ]
[ ][ ][ ]
[ ][ ][ ][ ]
```

![](img/d61019b035dd82beb581604273c0ee6b_267_1.png)

*打扫房子可以递归解决：先清理一个房间，然后清理其余部分。*
© Janice Richard/iStockphoto.

```cpp
return 0;
}
```

### 程序运行

```text
Enter the side length: 10
[]
[[]]
[[[]]]
[[[[]]]]
[[[[[]]]]]
[[[[[[]]]]]]
[[[[[[[]]]]]]]
[[[[[[[[]]]]]]]]
[[[[[[[[[]]]]]]]]]
[[[[[[[[[[]]]]]]]]]]
[[[[[[[[[[[]]]]]]]]]]]
```

打印三角形图案实际上并不需要递归。你可以使用嵌套循环，像这样：

```cpp
for (int i = 0; i < side_length; i++)
{
    for (int j = 0; j < i; j++)
    {
        cout << "[ ]";
    }
    cout << endl;
}
```

然而，这对循环有点棘手。许多人觉得递归解决方案更容易理解。

![](img/d61019b035dd82beb581604273c0ee6b_270_0.png)

### 操作方法5.2：递归思考

用递归解决问题，需要与用循环编程不同的思维方式。事实上，如果你有点懒，或者假装有点懒，让别人为你完成大部分工作，这会很有帮助。如果你需要解决一个复杂的问题，假装“别人”会完成大部分繁重的工作，并为所有更简单的输入解决这个问题。然后你只需要弄清楚如何将较简单输入的解决方案转化为整个问题的解决方案。

### 问题陈述

为了说明递归思维过程，考虑第4.2节中的问题：计算一个数字各位数字之和。我们想设计一个函数 `digit_sum`，它计算整数 `n` 的各位数字之和。例如，`digit_sum(1729) = 1 + 7 + 2 + 9 = 19`。

### 第1步

将输入分解为可以成为问题本身的输入的部分。

在脑海中，为你要解决的任务固定一个特定的输入或一组输入，并思考如何简化这些输入。寻找可以由同一任务解决的简化形式，并且这些简化形式的解与原始任务相关。

在数字和问题中，考虑如何简化像 `n = 1729` 这样的输入。减去1会有所帮助吗？毕竟，`digit_sum(1729) = digit_sum(1728) + 1`。但考虑 `n = 1000`。`digit_sum(1000)` 和 `digit_sum(999)` 之间似乎没有明显的关系。

一个更有前景的想法是去掉最后一位数字，即计算 `n / 10 = 172`。172的各位数字之和与1729的各位数字之和直接相关。

找到递归解决方案的关键是，将输入简化为同一问题的一个更简单的输入。

