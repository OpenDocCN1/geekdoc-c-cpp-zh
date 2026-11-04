
```csharp
static void Main() {
    var nums = GetNumbers();
    if (nums.MoveNext())
        Console.WriteLine(nums.Current);

    // Want to start with 0 again... Simply get a new iterator object.
    nums = GetNumbers();
    if (nums.MoveNext())
        Console.WriteLine(nums.Current);
}
```

一般来说，看到 NotSupportedException 意味着你的代码调用了不应该访问的东西。然而，当通过从外部传入的抽象（如 Stream 对象）进行调用时，情况会变得复杂一些：是否应该直接调用 Seek 方法并准备捕获异常呢？事实证明，Seek 方法的可用性与可在调用前检查的 CanSeek 属性配对。

来自 System.IO 命名空间的这个示例应该能让你很好地了解如何处理引入接口或基类的 API 设计，其中操作允许由实现者或子类型不支持。在这种情况下，要求 API 用户仅仅为了弄清楚收到的对象能做什么而捕获 NotSupportedException 是不合理的。应改为提供以 Can 为前缀的属性，这些属性应被实现或重写以表示操作的可用性。

## FormatException

很常见的是，字符串对象被用来接收具有某种结构化形式的输入，比如数字的字符串表示或 URI。在这种情况下，String 类型本身并不足以验证输入，需要由字符串对象的消费者进行额外的检查。例如，一个数字由数字组成，可能还包含小数分隔符字符、符号字符或用于科学记数法的指数。如果字符串输入不符合此格式，就会引发 FormatException。

示例可以在数值类型的静态 Parse 方法上找到：

```csharp
int invalid = int.Parse("Hello");
```

请注意，这些方法提供了额外的参数来规范接受的输入格式（例如，使用十六进制格式时）以及要使用的区域性。后者在使用本地化用户输入时很重要，其中数字的各个部分使用不同的字符（例如，小数分隔符符号）取决于区域性：

```csharp
var res = int.Parse("1A", NumberStyles.HexNumber,
    NumberFormatInfo.InvariantInfo);
```

FormatException 通常可以通过使用同类型提供的 TryParse 方法来检查输入而得以避免。

抛出此类型的异常以表示无效的字符串输入。在此过程中，编写验证和解析代码时，通常不会太麻烦地添加一个仅执行验证的单独方法：

```csharp
public static bool TryParse(string input, out MyData data) {
    // Parse the input, e.g. using System.Text.RegularExpressions.
}
```

```csharp
public static MyData Parse(string input) {
    MyData res;
    if (!TryParse(input, out res))
        throw new FormatException(...);
    return res;
}
```

## AggregateException

异常是按线程处理的。然而，随着对并行计算的重视程度提高，多条线程上出现多个异常的情况成为新的挑战。当 API 启动并行任务并且不同执行的任务抛出多个异常时，你也不希望无法从外部分析所有这些。

一个很好的例子是 .NET 4 中引入的新 System.Threading 并行构造，包括在 Parallel 静态类上公开的并行循环构造：

```csharp
Parallel.For(0, 10, i => {
    if (i % 2 == 0)
        throw new Exception("Even number!");

    // Do meaningful work.
});
```

前面的代码为每次循环体执行生成并行任务，使用循环迭代值作为输入执行指定的 lambda 表达式。For 调用本身会等待所有并行任务完成。在循环体内部，可能会发生异常，需要以某种方式在对 For 的调用中暴露出来。然而，由于并行任务正在进行，任何数量的任务都可能失败。

由于 For 方法只能抛出一个异常，所有任务的异常都会被收集并使用单个 AggregateException 抛出，该异常使用 InnerExceptions 属性公开所有异常：

```csharp
public class AggregateException : Exception {
    ...
    public ReadOnlyCollection<Exception> InnerExceptions { get; }
}
```

在进行并行编程时，如果各个并行任务可能会抛出你愿意从外部处理的异常，你就会习惯处理这种类型的异常。有一个有用的 Handle 方法可用于分析所有异常并有选择地处理它们：

```csharp
public void Handle(Func<Exception, bool> predicate);
```

谓词委托会逐一为 AggregateException 的 InnerExceptions 集合中的所有异常调用。如果对所有异常都返回 true，表示你已处理该异常，则方法 simply 返回。如果有任何异常未被处理（即一个或多个委托调用返回 false），未处理的异常将被收集到 AggregateException 中，并从 Handle 中抛出。

除了 Handle 之外，还有一个 Flatten 方法可将 InnerExceptions 集合中包含的 AggregateException 展平为单个 AggregateException。在处理嵌套的并行调用（例如两个 Parallel.For 调用）时，这非常有用。内部的 Parallel.For 调用可能会抛出 AggregateException，而外部的 Parallel.For 会将其包装在另一个 AggregateException 中。为了消除中间的聚合，可以使用 Flatten。

## Summary

在本章中，你学习了异常的重要性以及如何从消费者和生产者角度处理它们。你看到了如何使用 try 语句捕获异常，并了解了其关联的 catch 和 finally 块。本章还涵盖了与何时以及为何（或为何不）捕获异常相关的若干最佳实践。关于产生异常，我们讨论了创建自己的异常类型。

我们还介绍了 .NET Framework BCL 中出现的一些最基本且常用的异常类型。

## CHAPTER 24 Namespaces

### 本章内容

- 在命名空间中组织类型 1213
- 声明命名空间 1219
- 导入命名空间 1223

在继续研究 C# 编程语言和 .NET 平台时，我们一直在将较小的构造组合成较大的构造。首先，我们研究了表达式能为我们做什么，然后是关于语句的章节。接下来，我们将这些代码块分组为成员，这些成员被组织到类型中。

最后，我们到达了最顶层的构造，它们允许将类型组织成分层命名方案并充当部署的容器。第一个是称为命名空间的语言构造，也支持跨语言场景。第二个是程序集，它是 CLR 对代码、元数据和资源容器的模型。

在本章中，你将学习如何将类型组织到命名空间中，从而避免名称冲突并提供功能的逻辑组织。除了声明命名空间之外，你还将看到如何导入和使用它们，包括使用别名和 extern 别名时的一些更棘手的场景。

### 在命名空间中组织类型

简而言之，命名空间提供了一种为 .NET 库和应用程序中的类型建立分层命名方案的方法。在语言层面，可以声明包含各种类型的新的命名空间。除了提供命名空间之外，还有使用它们的行为，这基于在代码中导入它们的概念。

在语言之下的一层，运行时实际上对命名空间知之甚少，因为类型始终由完全限定名引用。当完整类型名看起来像 System.Collections.Generic.List<int> 时，如果包含的命名空间已被导入，你只需写 List<int>。换句话说，使用命名空间会产生类型名的缩写。

### 曾经的故事

在 Win32 和 COM 的世界里，很少有支持将代码组织成逻辑单元，导致出现扁平的应用程序编程接口（API）。尽管 C++ 有命名空间的概念，但许多 API 源自命名空间的使用并非其设计理念的一部分的早期时代。

例如，Win32 基本上是一个由函数和一些数据类型组成的 API，没有面向对象的抱负。所有这些函数都生活在单个“命名空间”中，因此完全可能出现两个同名函数冲突的情况。这种问题在编译时就会显现，因为编译器（在 C/C++ 中，我们还应提到链接器）无法弄清楚你的意思。为了稍微减少这个问题，你可以使用头文件来建立一些组织，尽管在包含多个头文件时仍可能出现问题：

```csharp
#include <windows.h>
```

```csharp
void SaveData(__in LPCWSTR file)
{
    HANDLE hFile = CreateFile(file,
        GENERIC_WRITE,
        0,
        NULL,
        CREATE_ALWAYS,
        FILE_ATTRIBUTE_NORMAL,
        NULL);
}
```

除了名称冲突的可能性之外，平坦的声明空间还存在其他问题。其中一个问题与 API 的可发现性有关。正如你所能想象的，可用的函数或数据类型的数量会迅速爆炸，尤其是在包含内容丰富的头文件（如 windows.h）时。虽然各种函数在逻辑上属于一起（例如，处理文件 I/O 的函数），但没有任何东西反映这一点。

图 24.1 仅说明了所有以 Create 开头的函数中的一小部分，为不熟悉 API 的开发人员造成了巨大的搜索负担。

尽管部分问题源于缺乏封装状态并将其与操作该状态的函数捆绑在一起的类型，但在 COM 世界中，情况仍然相当混乱，其中接口提供了更好的逻辑组织。从某种意义上说，所有这些都买来了
