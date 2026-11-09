
如果你的程序集定义了多个异常类型，你必须逐个添加它们。将来，我希望这个对话框允许我浏览某个程序集，并自动将所有派生自 Exception 的类型导入 Visual Studio 的调试器。届时，每个类型还可以按程序集加以标识，从而解决不同程序集中存在两个同名类型的问题。

### 异常处理的性能考量

开发者社区一直在积极争论异常处理的性能。有些人声称异常处理的性能太差，以至于他们甚至拒绝使用异常处理。然而，我认为在面向对象平台中，异常处理不是一个可选项，而是强制性的。此外，如果你不使用它，那你会用什么来代替？你会让方法返回 `true/false` 来表示成功/失败，或者返回某种错误码 `enum` 类型吗？好吧，如果你这样做，那么你会落得两头都糟的局面：CLR 和类库代码会抛出异常，而你的代码会返回错误码。你现在不得不在代码中同时处理这两种情况。

很难比较异常处理与更传统的异常报告方式（例如 `HRESULTs`、特殊返回码等）之间的性能。如果你编写代码来检查每个方法调用的返回值，并将返回值逐层过滤给自己的调用方，那么应用程序的性能将受到严重影响。但先不谈性能，当你编写代码来检查每个方法的返回值时，你必须完成的额外编码量以及出错的可能性都会高得惊人。异常处理是一种好得多的替代方案。

然而，异常处理是有代价的：非托管 C++ 编译器必须生成代码来跟踪哪些对象已成功构造。编译器还必须生成这样的代码：当捕获到异常时，调用每个已成功构造对象的析构函数。编译器承担这一负担固然很好，但它会在你的应用程序中生成大量簿记代码，对代码大小和执行时间产生不利影响。

另一方面，托管编译器要轻松得多，因为托管对象分配在托管堆中，而托管堆由垃圾回收器监视。如果一个对象已成功构造，随后抛出了异常，垃圾回收器最终会释放该对象的内存。编译器不需要发出任何簿记代码来跟踪哪些对象已成功构造，也不需要确保已调用析构函数。与非托管 C++ 相比，这意味着编译器生成的代码更少，运行时必须执行的代码也更少，从而为你的应用程序带来更好的性能。

多年来，我在不同的编程语言、不同的操作系统和不同的 CPU 架构中使用过异常处理。在每种情况下，异常处理的实现方式都不同，每种实现在性能方面都有其优缺点。有些实现将异常处理构造直接编译到方法中，而另一些实现则将与异常处理相关的信息存储在与该方法关联的数据表中——只有当抛出异常时才会访问该表。有些编译器无法内联包含异常处理程序的方法，有些编译器则不会在方法包含异常处理程序时把变量放入寄存器。

关键在于，你无法确定使用异常处理会给应用程序增加多少额外开销。在托管世界中，这就更难判断了，因为你的程序集代码可以在任何支持 .NET Framework 的平台上运行。因此，当你的程序集运行在 x86 机器上时，JIT 编译器为管理异常处理而生成的代码，将与你的代码运行在 x64 或 IA64 处理器上时 JIT 编译器生成的代码截然不同。此外，与其他 CLR 实现（例如 Microsoft 的 .NET Compact Framework 或开源 Mono 项目）关联的 JIT 编译器很可能生成不同的代码。

实际上，我曾用 Microsoft 内部的一些不同 JIT 编译器测试过我自己的一些代码，我观察到的性能差异相当显著，令人惊讶。关键在于，你必须在你期望用户运行的各种平台上测试代码，并相应地做出更改。再次强调，我不会担心使用异常处理的性能，因为其好处通常远远超过任何负面的性能影响。

如果你有兴趣了解异常处理如何影响代码的性能，可以使用 Windows 自带的性能监视器工具。图 20-8 中的屏幕显示了随 .NET Framework 一起安装的与异常相关的计数器。

![](img/3c46ff5b170881db4209d365b1f7a808_524_0.png)

**图 20-8** 显示 .NET CLR 异常计数器的性能监视器

### 约束执行区域（CERs）

许多应用程序不需要具备健壮性，也不需要从任何种类的失败中恢复。许多客户端应用程序都是如此，例如 Notepad.exe 和 Calc.exe。当然，我们中的许多人都见过 Microsoft Office 应用程序（如 WinWord.exe、Excel.exe 和 Outlook.exe）因未处理异常而终止。此外，许多服务器端应用程序（如 Web 服务器）是无状态的，如果因未处理异常而失败，它们会自动重新启动。当然，有些服务器（如 SQL Server）完全围绕状态管理，因未处理异常而丢失数据的潜在后果要灾难性得多。

在 CLR 中，我们有应用程序域（AppDomains，在第 22 章讨论），它们包含状态。当卸载一个应用程序域时，它的所有状态都会被卸载。因此，如果应用程序域中的某个线程遇到未处理异常，那么卸载该应用程序域（这会销毁其所有状态）而不终止整个进程是可以的。^8

按照定义，CER 是一段必须能够抵御失败的代码块。由于应用程序域可以被卸载，从而销毁其状态，因此 CER 通常用于操作由多个应用程序域或进程共享的任何状态。当试图在意外抛出异常的情况下维护状态时，CER 很有用。有时我们将这类异常称为*异步异常*。例如，在调用方法时，CLR 必须加载程序集、在应用程序域的加载器堆中创建类型对象、调用该类型的静态构造函数、将 IL JIT 编译为本机代码，等等。这些操作中的任何一个都可能失败，而 CLR 会通过抛出异常来报告失败。

如果这些操作中的任何一个在 **catch** 或 **finally** 块内失败，那么你的错误恢复或清理代码将不会完整执行。下面是一个展示该潜在问题的代码示例：

```csharp
private static void Demo1() {
    try {
        Console.WriteLine("In try");
    }
    finally {
        // Type1's static constructor is implicitly called in here
        Type1.M();
    }
}

private sealed class Type1 {
    static Type1() {
        // if this throws an exception, M won't get called
        Console.WriteLine("Type1's static ctor called");
    }

    public static void M() { }
}
```

运行上面的代码时，我得到以下输出：

```
In try
Type1's static ctor called
```

我们想要的是，除非我们知道关联的 **catch** 和 **finally** 块中的代码保证（或尽可能接近保证）会执行，否则甚至不要开始执行上面 **try** 块中的代码。我们可以通过如下修改代码来实现这一点：

```csharp
private static void Demo2() {
    // Force the code in the finally to be eagerly prepared
    RuntimeHelpers.PrepareConstrainedRegions(); // System.Runtime.CompilerServices namespace
    try {
        Console.WriteLine("In try");
    }
    finally {
        // Type2's static constructor is implicitly called in here
        Type2.M();
    }
}

public class Type2 {
    static Type2() {
        Console.WriteLine("Type2's static ctor called");
    }

    // Use this attribute defined in the System.Runtime.ConstrainedExecution namespace
    [ReliabilityContract(Consistency.WillNotCorruptState, Cer.Success)]
    public static void M() { }
}
```

现在，当我运行这个版本的代码时，我得到以下输出：

```
Type2's static ctor called
In try
```

**PrepareConstrainedRegions** 方法是一个非常特殊的方法。当 JIT 编译器看到在 **try** 块之前立即调用此方法时，它会急切地编译 **try** 的 **catch** 和 **finally** 块中的代码。JIT 编译器将加载任何程序集、创建任何类型对象、调用任何静态构造函数，并对任何方法进行 JIT 编译。如果这些操作中的任何一个导致异常，那么异常会在该线程进入 **try** 块之前发生。

当 JIT 编译器急切地准备方法时，它还会遍历整个调用图，急切地准备被调用的方法。然而，JIT 编译器只准备那些应用了 **ReliabilityContractAttribute** 且其参数为 **Consistency.WillNotCorruptState** 或 **Consistency.MayCorruptInstance** 的方法，因为 CLR 无法对可能损坏应用程序域或进程状态的方法做出任何保证。在你通过调用 **PrepareConstrainedRegions** 来保护的 **catch** 或 **finally** 块内部，你要确保只调用那些按照我刚才描述的方式设置了 **ReliabilityContractAttribute** 的方法。

^8 如果线程的整个生命周期都位于单个应用程序域内（例如在 ASP.NET 和托管 SQL Server 存储过程场景中），这绝对是正确的。但是，如果线程在其生命周期内跨越应用程序域边界，你可能不得不终止整个进程。
