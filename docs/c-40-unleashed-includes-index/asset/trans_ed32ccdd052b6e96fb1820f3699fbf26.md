
```
var asm = Assembly.ReflectionOnlyLoadFrom(@"\\temp\\calc.dll");

// Reflection is permitted.
foreach (var type in asm.GetTypes())
    Console.WriteLine(type);

// But invoking operations, such as instantiation of types, is not.
try
{
    dynamic calc = asm.CreateInstance("Calc");
    Console.WriteLine(calc.Add(1, 2));
}
catch (ArgumentException)
{
    Console.WriteLine("Thrown due to reflection-only load.");
}

var asm2 = Assembly.LoadFrom(@"\\temp\\calc.dll");
foreach (var type in asm2.GetTypes())
    Console.WriteLine(type);

// In the regular LoadFrom context, instantiation and invocation is permitted.
dynamic calc2 = asm2.CreateInstance("Calc");
Console.WriteLine(calc2.Add(1, 2));
```

关于程序集加载（无论是否仅反射加载），有一个关键知识点：加载操作无法撤销。换句话说，`Assembly` 对象上不存在一个 `Unload` 方法能让程序集从内存中消失。原因有很多。例如，可能已经加载了其他依赖某个程序集存在的程序集。也可能存在引用某程序集中定义的函数的委托。

基于前面的陈述，你可能会想，摆脱程序集的唯一方法是不是彻底关闭进程。幸运的是，并非如此；CLR 有一种介于两者之间的隔离概念，称为应用程序域。它们可以加载和卸载，稍后你会在“应用程序域”一节中看到。

除了应用程序域之外，.NET 4 运行时的 System.Reflection.Emit API 还允许你创建标记为 `RunAndCollect` 的动态程序集。在某些限制条件下，这些可收集程序集可以在不卸载其创建时所处应用程序域的情况下被卸载。MSDN 文档在一篇题为“用于动态类型生成的可收集程序集”的文章中概述了这些限制。

## 应用程序域

现代操作系统、运行时、服务器软件等投入大量精力在不同的用户之间提供有意义的隔离边界。在操作系统层面，这种隔离不仅用于在用户账户之间建立屏障，还存在于更基础的层面。特别是，进程为应用程序提供了隔离边界，确保一个进程中运行的代码不会影响另一个进程中运行的代码。换个角度说，为了克服操作系统提供的根本性隔离，进程之间的所有交互模式都必须非常显式地完成（例如，利用跨进程通信设施或共享内存段）。

.NET 运行时同样希望提供一个能够建立隔离边界的基础。这些边界带来诸多好处，从可靠性（例如，不会意外地踩到别人的内存）、安全性（例如，一个代码执行容器比另一个更不受信任）到对代码加载和卸载的控制。在 .NET 的世界里，这些隔离的容器被称为应用程序域。图 25.39 展示了承载 CLR 的进程与包含一个或多个应用程序域（作为已加载程序集的容器）之间的关系。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1306_0.png)

图 25.39　操作系统进程、应用程序域和程序集。

那么，这个神秘的 `ObjectHandle` 是怎么回事？基本上，它们是一种通信原语，用于引用跨域创建的对象。我们忽略它们的复杂性，直接使用 `Unwrap` 方法来完全避开它们。

为了演示在应用程序域中创建类型实例的技术，我们首先创建一个单独的程序集库作为要加载的目标。为简单起见，让我们再次使用计算器示例：

```
using System;

public class Calc
{
    public int Add(int a, int b)
    {
        Console.WriteLine(AppDomain.CurrentDomain);
        return a + b;
    }
}
```

将上述代码编译成 .dll 程序集（例如，使用类库项目）。将程序集命名为 `calc.dll`。接下来，我们创建宿主应用程序，通过 `CreateInstanceFromAndUnwrap` 加载该程序集：

```
class Program
{
    static void Main()
    {
        var ad = AppDomain.CreateDomain("AddIn");

        dynamic calc = ad.CreateInstanceFromAndUnwrap("Calc.dll", "Calc");
        Console.WriteLine(calc.Add(1, 2));

        AppDomain.Unload(ad);

        foreach (var asm in AppDomain.CurrentDomain.GetAssemblies())
            Console.WriteLine(asm);
    }
}
```

关于这个示例，有几点需要注意。首先，`CreateInstanceFromAndUnwrap` 返回一个类型为 `System.Object` 的对象。由于我们的宿主应用程序没有现成的 `Calc` 类型可用于转换返回的对象，我们需要采用其他技巧来调用该对象公开的功能。为简单起见，我们在这里使用 C# 4.0 的 `dynamic` 特性，但稍后在“使用接口契约”一节中，你将看到如何正确地构建宿主和加载项，使用公共接口来表示契约。其次，在卸载加载项的应用程序域后，我们打印默认域中的所有程序集。

要运行宿主应用程序，请确保将 `calc.dll` 文件放在宿主可执行程序集旁边，以便能够找到加载项程序集。但是，此时如果你尝试运行带有加载项的宿主，会引发异常，如图 25.41 所示。这为我们解释跨不同应用程序域使用的类型需要满足的要求提供了一个很好的起点。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1310_0.png)

图 25.41　无法在应用程序域之间建立通信。

在解决此问题之前，我们需要进一步研究远程处理设施，以真正理解 `SerializationException` 到底是什么。由于这些主题本身足以写成整本书，我们只讨论要点。

### 远程处理的形式

跨边界（此处为应用程序域）传递对象可以通过两种不同的方式完成。要么通过称为*序列化*的机制按值传递，要么按引用传递。图 25.42 描绘了第一种机制，即按值复制对象。当目标域试图从第一个域获取某个 point 实例时，对象的数据会被复制到目标域中。显然，两个域都需要知道 `Point` 类型的结构才能实现这一点。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1310_1.png)

图 25.42　使用序列化实现按值复制。

由于这个原因（以及其他原因，如对远程对象的访问协调），业界已转向更面向服务的编程风格，web 服务等技术就是例证。在这种环境中，调用方在（无状态的）web 服务“门面”上定义的操作，将对象或唯一标识符序列化传递。例如，支付给我们的 John 这个人，可以通过调用某个 `Pay(8491, 124.45m)` 来完成，其中 8491 是 John 的唯一标识符。使用（静态的）web service 门面方法带来了更粗粒度的通信形式。现在，透明性仅限于 web 服务代理对象上定义的操作，而不会与整个对象图纠缠在一起。

### 基于 MarshalByRefObject 的计算器加载项

为了继续探索对象之间的跨域通信，我们通过让 `Calc` 类型按引用封送来修复它。如前所述，你也可以随意尝试使用可序列化的对象。以下是修改后的代码，使我们的 `Calc` 类型适用于跨应用程序域使用：

```
using System;

public class Calc : MarshalByRefObject
{
    public int Add(int a, int b)
    {
        Console.WriteLine(AppDomain.CurrentDomain);
        return a + b;
    }
}
```

使用我们之前展示的现有宿主代码，现在我们可以让计算器正常工作，不再出现图 25.41 所示的异常。如果我们将鼠标悬停在 `calc` 对象上并查看其类型，.NET 远程处理的使用就变得显而易见，该类型反映了透明代理的使用。图 25.44 显示了远程对象的类型名如何被 .NET 远程处理基础设施设置的一系列间接引用所掩盖。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1313_0.png)

图 25.44　由 .NET 远程处理引入的透明代理类型。

由于我们的计算器 `Add` 方法会打印其正在执行的应用程序域，我们可以看出调用发生在 `AddIn` 域中。尝试执行相同的宿主，但
