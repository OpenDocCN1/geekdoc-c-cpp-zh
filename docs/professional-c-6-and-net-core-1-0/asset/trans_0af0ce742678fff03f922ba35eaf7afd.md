

```csharp
static void Main()
{
    try
    {
        var balance = new Currency(50,35);

        WriteLine(balance);
        WriteLine($"balance is {balance}");

        uint balance3 = (uint) balance;

        WriteLine($"Converting to uint gives {balance3}");
    }
    catch (Exception ex)
    {
        WriteLine($"Exception occurred: {ex.Message}");
    }
}
```

运行示例现在会得到以下结果：

```
50
balance is $50.35
Converting to uint gives 50
```

输出显示转换到 uint 已成功，不过正如预期的那样，在进行此转换时你已丢失了 Currency 的分部分。将负浮点数转换为 Currency 也产生了预期的溢出异常，因为 float 到 Currency 的转换本身现在定义了一个已检查的上下文。

然而，输出也展示了你在处理转换时需要意识到的最后一个潜在问题。输出的第一行并没有正确显示余额，显示的是 50 而不是 50.35。

发生了什么？问题在于当你将转换与方法重载结合使用时，你会得到另一个不可预测性的来源。

使用格式字符串的 WriteLine 语句会隐式调用 Currency.ToString 方法，确保 Currency 以字符串形式显示。

然而，第一个 WriteLine 方法只是将原始 Currency 结构体传递给 WriteLine。现在，WriteLine 有许多重载，但其中没有一个接受 Currency 结构体。因此，编译器开始寻找它可以将 Currency 转换为什么类型以使其匹配 WriteLine 的某个重载。碰巧的是，WriteLine 的其中一个重载是为快速高效地显示 uint 而设计的，并且它接受 uint 作为参数——你现在提供了一个将 Currency 隐式转换为 uint 的转换。

事实上，WriteLine 还有另一个重载接受 double 作为参数并显示该 double 的值。如果你仔细查看之前运行示例的输出，其中不存在转换到 uint，你会看到第一行输出将 Currency 显示为 double，使用了这个重载。在那个示例中，没有从 Currency 到 uint 的直接转换，所以编译器选择 Currency 到 float 再到 double 作为其匹配可用转换到可用 WriteLine 重载的首选方式。然而，现在在 SimpleCurrency2 中存在直接转换到 uint，编译器选择了这条路径。

由此得出的结论是，如果你有一个具有多个重载的方法调用，并且你尝试传递一个数据类型与任何重载都不完全匹配的参数，那么你就迫使编译器不仅决定使用什么转换来执行数据转换，还要决定选择哪个重载，以及因此选择哪种数据转换。编译器总是按逻辑并根据严格规则工作，但结果可能不是你所期望的。如果有任何疑问，你最好明确指定要使用的转换。

## Summary

本章介绍了 C# 提供的标准运算符，描述了对象相等性的机制，并检查了编译器如何将标准数据类型从一种转换为另一种。它还演示了如何使用运算符重载在你的数据类型上实现自定义运算符支持。最后，你研究了一种特殊的运算符重载类型，即转换运算符，它使你能够指定如何将你的类型的实例转换为其他数据类型。

下一章将解释委托、lambda 表达式和事件。

## 9 Delegates, Lambdas, and Events

### What’s In This Chapter?

- Delegates
- Lambda expressions
- Closures
- Events
- Weak Events

### Wrox.com Code Downloads for This Chapter

本章在 www.wrox.com/go/professionalcsharp6 的 Download Code 标签下可以找到 wrox.com 代码下载。本章的代码分为以下主要示例：

- Simple Delegates
- Bubble Sorter
- Lambda Expressions
- Events Sample
- Weak Events

### Referencing Methods

委托是 .NET 中指向方法的地址的变体。将其与 C++ 相比，在 C++ 中，函数指针只不过是指向内存位置的指针，而且不是类型安全的。你不知道指针到底指向什么，诸如参数和返回类型等项目是未知的。这与 .NET 完全不同；委托是类型安全的类，定义了返回类型和参数类型。委托类不仅包含对方法的引用，还可以保存对多个方法的引用。

Lambda 表达式与委托直接相关。当参数是委托类型时，你可以使用 lambda 表达式来实现从委托引用的方法。

本章解释了委托和 lambda 表达式的基础知识，并展示了如何使用 lambda 表达式实现由委托调用的方法。它还演示了 .NET 如何使用委托作为实现事件的手段。

### Delegates

委托适用于你想要将方法传递给其他方法的情况。要了解这意味着什么，请考虑这行代码：

```
int i = int.Parse("99");
```

你已经习惯于将数据作为参数传递给方法，就像这个例子一样，以至于你不会有意识地思考它，所以将方法而不是数据传递的想法可能听起来有点奇怪。然而，有时你有一个执行某些操作的方法，而不是对数据进行操作，该方法可能需要执行某些涉及调用另一个方法的操作。更复杂的是，你在编译时并不知道这个第二方法是什么。该信息只有在运行时才可用，因此需要作为参数传递给第一个方法。这听起来可能令人困惑，但通过几个例子应该会变得更清晰：

- **Threads and tasks**—在 C# 中，可以让计算机在并行于当前正在执行的操作的同时启动一个新的执行序列。这种序列被称为 *thread*，你使用 `System.Threading.Thread` 基类之一实例上的 `Start` 方法来启动它。如果你告诉计算机启动一个新的执行序列，你必须告诉它从哪里开始该序列；也就是说，你必须提供一个方法在其中可以开始执行的细节。换句话说，`Thread` 类的构造函数接受一个参数，该参数定义了线程将调用的方法。

- **Generic library classes**—许多库包含执行各种标准任务的代码。通常，这些库可以是自包含的，因为你在编写库时确切知道任务必须如何执行。然而，有时任务包含一个子任务，只有使用库的单个客户端代码才知道如何执行。例如，假设你想编写一个类，它接受一个对象数组并按升序对它们进行排序。排序过程的一部分涉及反复取出数组中的两个对象并比较它们以查看哪个应该排在前面。如果你想使该类能够对任何对象的数组进行排序，就没有办法提前知道如何进行此比较。向你的类提供对象数组的客户端代码还必须告诉你的类如何为其想要排序的特定对象执行此比较。客户端代码必须向你的类传递适当方法的详细信息，以便调用该方法来执行比较。

- **Events**—这里的总体思路是，通常你有需要被告知某些事件发生时代码。当事件被引发时，运行时需要知道应该执行什么方法。这是通过将处理事件的方法作为参数传递给委托来完成的。本章后面会讨论这一点。

在 C 和 C++ 中，你可以简单地取一个函数的地址并将其作为

