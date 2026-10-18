

在程序的几乎任何地方到程序的几乎任何其他地方。 在编程的早期，这种不受限制的控制流是通过一种称为 goto 的构造来实现的。 编程专家现在一致认为，这种不受限制的控制流是非常糟糕的编程风格。 异常允许你恢复到这种不受限制的控制流的糟糕旧时代。 异常应该谨慎使用，并且只能以特定的方式使用。 一个好的规则如下：如果你想包含一个 throw 语句，那么就想想你如何在没有这个 throw 语句的情况下编写你的程序或类定义。 如果你想到了一种产生合理代码的替代方案，那么你可能不希望包含 throw 语句。

## 异常类层次结构

定义异常类层次结构非常有用。 例如，你可能有一个 ArithmeticError 异常类，然后定义一个 ArithmeticError 的派生类 DivideByZeroError 异常类。 由于 DivideByZeroError 是一个 ArithmeticError，因此针对 ArithmeticError 的每个 catch 块都会捕获 DivideByZeroError。 如果你在异常规范中列出 ArithmeticError，那么你实际上也将 DivideByZeroError 添加到了异常规范中，无论你是否在异常规范中按名称列出 DivideByZeroError。

## 测试可用内存

在第 13 章中，我们使用如下代码创建了新的动态变量：

```
struct Node
{
    int data;
    Node *link;
};
typedef Node* NodePtr;

NodePtr pointer = new Node;
```

只要有足够的内存来创建新的节点，这就可以正常工作。 但是，如果没有足够的内存会发生什么？ 如果没有足够的内存来创建节点，则会抛出 bad_alloc 异常。 类型 bad_alloc 是 C++ 语言的一部分。 你不需要定义它。

由于 new 在没有足够内存创建节点时会抛出 bad_alloc 异常，因此你可以按如下方式检查内存耗尽的情况：

```
try
{
    NodePtr pointer = new Node;
}
```

```
catch (bad_alloc)
{
    cout << "Ran out of memory!";
}
```

当然，你可以做除了简单地给出警告信息之外的其他事情，但你所做细节将取决于你的特定编程任务。

## 重新抛出异常

在 catch 块中抛出异常是合法的。 在极少数情况下，你可能想要捕获一个异常，然后根据细节决定抛出相同的或不同的异常以供异常处理块链中更高层处理。

## 自测练习

+   10. 当异常从未被捕获时会发生什么？
+   11. 你可以在另一个 try 块内嵌套一个 try 块吗？

## 章节总结

+   - 异常处理允许你将程序的正常情况设计和编码与处理异常情况的代码分开。
+   - 可以在一个 try 块中抛出异常。 或者，可以在一个不包含 try 块的函数定义中抛出异常（或不包含捕获该类型异常的 catch 块）。 在这种情况下，可以将函数的调用放在 try 块中。
+   - 异常在 catch 块中被捕获。
+   - 一个 try 块可以跟随一个以上的 catch 块。 在这种情况下，始终将针对更具体异常类的 catch 块列在针对更通用异常类的 catch 块之前。
+   - 不要过度使用异常。

## 自测练习答案

+   1. Try block entered.
+      Exception thrown with
+      waitTime equal to 46
+      After catch block.

2. Try block entered.
Leaving try block.
After catch block.

3. `throw waitTime;`

注意以下内容是一个 if 语句，而不是一个 throw 语句，即使它包含一个 throw 语句：

```
if (waitTime> 30)
    throw waitTime;
```

4. 当执行 throw 语句时，封闭 try 块的结束。 try 块中的其他语句不会被执行，控制权传递给随后的 catch 块(们)。 当我们说控制权传递给随后的 catch 块时，我们的意思是抛出值被插入到 catch 块参数（如果有的话），并且 catch 块中的代码被执行。

```
5. try
{
    cout << "Try block entered.";
    if (waitTime > 30)
        throw (waitTime);
    cout << "Leaving try block.";
}
```

```
6. catch(int thrownValue)
{
    cout << "Exception thrown with\n"
         << "waitTime equal to" << thrownValue << endl;
}
```

7. thrownValue 是 catch 块参数。

8. Trying.
Starting sampleFunction.
Catching.
End of program.

9. Trying.
Starting sampleFunction.
Trying after call.
End of program.

10. 如果异常在任何地方都没有被捕获，则你的程序结束。

11. 是的，你可以在另一个更大的 try 块内拥有一个 try 块和相应的 catch 块。 然而，最好将内部的 try 和 catch 块放在函数定义中，并在更大的 try 块中放置对该函数的调用。

## 实践程序

*实践程序通常可以用一个简短的程序解决，该程序直接应用本章介绍的编程原理。*

+   1. 一个返回特殊错误代码的函数通常最好通过抛出异常来实现。 这样，错误代码就不会被忽略或误认为是有效数据。 下面的类维护账户余额。

```
class Account
{
private:
    double balance;
public:
    Account()
    {
        balance = 0;
    }
    Account(double initialDeposit)
    {
        balance = initialDeposit;
    }
    double getBalance()
    {
        return balance;
    }
    // returns new balance or −1 if error
    double deposit(double amount)
    {
        if (amount > 0)
            balance += amount;
        else
            return −1; // Code indicating error
        return balance;
    }
    // returns new balance or −1 if invalid amount
    double withdraw(double amount)
    {
        if ((amount > balance) || (amount < 0))
            return −1;
        else
            balance −= amount;
        return balance;
    }
};
```

![](img/88b1f375f11336dbd9dac8b1675d0698_956_0.png)

重写该类，使其抛出适当的异常而不是返回 -1 作为错误代码。 编写测试代码，尝试存取无效金额并捕获抛出的异常。

2. 标准模板库包含一个名为 exception 的类，它是 STL 函数抛出的任何异常的父类。 因此，任何异常都可以被此类捕获。 以下代码为 STL 异常设置了 try-catch 块：

```
#include <iostream>
#include <string>
#include <exception>
using namespace std;

int main()
{
    string s = "hello";
    try
    {
        cout << "No exception thrown." << endl;
    }
    catch (exception& e)
    {
        cout << "Exception caught: " <<
            e.what() << endl;
    }
    return 0;
}
```

修改代码，使异常在 try 块中被抛出。 你可以尝试使用 at 成员函数访问字符串中的无效索引。

## 编程项目

*编程项目比实践程序需要更多的解决问题，并且通常可以用许多不同的方法解决。 访问 www.myprogramminglab.com 在线完成这些编程项目中的许多项目并获得即时反馈。*

+   1. 编写一个函数，将作为 String 给出的十六进制数转换为整数值。 如果要转换的值不是有效的十六进制数，则在尝试转换之前抛出 InvalidNumberException。 你需要同时开发该函数和异常类。 编写一个驱动程序来测试对你的函数的有效和无效输入。

2. 编写一个程序，将日期从数字月/日格式转换为字母月/日（例如，1/31 或 01/31 对应于 January 31）。 对话应类似于编程项目 1 中的对话。 你将定义两个异常类，一个称为 MonthError，另一个称为 DayError。 如果用户输入的不是合法的月份数字（1 到 12 之间的整数），则你的程序将抛出并捕获 MonthError。 类似地，如果用户输入的不是有效的日期数字（1 到 29、30 或 31 之间的整数，具体取决于月份），则你的程序将抛出并捕获 DayError。 为了简化，始终允许二月有 29 天。

3. 编写一个程序，从 1 到 10 输入数值，并使用 * 输出这些值的文本直方图来计算每个值的出现次数。 程序首先询问用户要输入多少个数字。 如果用户输入的值不完全由数字组成或数字超出 1 到 10 的范围，则应捕获异常。 （提示：以字符串形式输入每个数字，然后扫描字符串以查看是否包含所有数字。 如果不是，则抛出异常。 要将字符串 str 转换为整数，请使用以下代码：

```
atoi(str.c_str());
```

atoi 函数在第 8 章中描述。） 这里是一个示例对话：

```
How many numbers to enter?
5
Enter number 1L
one
Please enter your number using digits only. Try again.
Enter number 1:
9
Enter number 2:
3
Enter number 3:
3
Enter number 4:
33
The number must be between 1-10. Try again.
Enter number 4:
3
Enter number 5:
7
```

