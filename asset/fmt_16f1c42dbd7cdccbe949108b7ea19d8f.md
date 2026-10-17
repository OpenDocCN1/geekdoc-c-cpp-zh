
从 `C#` 示例应用程序开始，将其命名为 `DynamicObjectDemo`。向项目添加名为 `DynamicEnvironment.cs` 的新类文件。列表 10-3 显示了你应该复制到该文件的代码。

## 列表 10-3：DynamicEnvironment.cs

```csharp
using System;
using System.Dynamic;

namespace DynamicObjectDemo
{
    public class DynamicEnvironment: DynamicObject
    {
        private EnvironmentTarget _TargetEnv;
        private bool _ignoreMissingProperty;

        public DynamicEnvironment(EnvironmentTarget targetEnv, bool ignoreMissingProperty = false)
        {
            _TargetEnv = targetEnv;
            _ignoreMissingProperty = ignoreMissingProperty;
        }

        public override bool TryGet(Binder binder, out object result)
        {
            result = Environment.GetVariable(binder.Name, _TargetEnv);
            return result != null || _ignoreMissingProperty;
        }
    }
}
```

可以在 Wrox.com 下载代码文件 `DynamicEnvironment.cs`

构造函数允许你传递可选的 `EnvironmentTarget`，以设置你是否希望将对象绑定到机器或用户。`ignoreMissingProperty` true 值允许在属性不存在时返回空值，而不是抛出异常。属性解析由重写的 `TryGet` 方法处理。它接受两个参数。绑定器接收来自 DLR 的操作。在这种情况下，它处理要解析的属性名称。结果应设置为从操作检索的值，如果属性名称指向存在的环境变量，则解析成功并检索该值；否则返回空，取决于 `ignoreMissingProperty` 的值。

如果操作可以由该方法处理，则方法的返回值设置为 true；否则为 false。该方法的逻辑非常简单。列表 10-4 显示了 `Program.cs`。

## 列表 10-4：DynamicObjectDemo 的 Program.cs 文件

```csharp
using System;

namespace DynamicObjectDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            dynamic env = new DynamicEnvironment(ignoreMissingProperty: true);
            Console.WriteLine(env.Path);
            Console.WriteLine(env.Temp);
            Console.WriteLine(env.NonExisting ?? "null");
        }
    }
}
```

此程序按预期运行。由于没有名为 `NonExisting` 的环境变量，第三行将显示 "null"。将 `ignoreMissingProperty` 值设为 false，以便 `DynamicEnvironment` 在使用未知属性时抛出异常。现在运行程序将抛出 `RuntimeBinderException`（如图 10-6 所示），告诉你无法解析 `NonExisting` 属性。

![](img/b5597c749e848b27b0d305153ae16106_452_0.png)

图 10-6：抛出的 RuntimeBinderException

> 这非常简单，并不真正健壮。例如，它无法解析 USERNAME 或 MACHINENAME，因为这些无法通过 `Environment.GetVariable` 方法获取。尝试此示例，并尝试通过扩展这些功能来使其更有用！

## 类型等效

.NET 4 极大改进了 COM 互操作性。从 CLR 的角度来看，最重要的特性是类型等效。它要求在部署应用程序时，无需为其操作的 COM 组件部署 PIA。此功能实现在

CLR 级别，除了支持“No-PIA 部署”外，它还提供了创建具有松散类型耦合和良好韧性的应用程序的能力。

要与特定的 COM 接口进行交互，你必须使用封装了该接口功能的 .NET 类型。手动构建这些包装器是非常耗时的，特别是当你有几百个 COM 接口时（例如在在用 Microsoft Office 自动化模型的情况下）。PIA 是从 COM 接口生成的 .NET 程序集，用于实现强类型的互操作性。对于大对象模型，相关的 PIA 同样很大，这些程序集会轻易地增加你的应用程序的大小。当它们独立于你的应用程序进行分发时，可能会导致版本问题。

No-PIA 特性允许你在设计时继续使用 PIA，而在运行时不需要加载它们。C 编译器会将程序实际用到的 PIA 的一小部分附加到它的程序程序集中。在运行时，不需要加载 PIA。

## 具有类型等价性的 No-PIA 示例

让我们创建一个简单的示例来帮助理解类型等价的概念。该应用程序将创建一个文档，并在其中插入一些文本和表格。

启动 Visual Studio 2010 并创建一个名为 `TypeEqualityDemo` 的新 `C#` 控制台应用程序。向解决方案添加一个名为 `WordHelper` 的新 `C#` 类库项目，并从 `TypeEqualityDemo` 引用该项目。

此应用程序将使用 Word 自动化，因此你必须为 Word 对象添加 `Microsoft.Office.Interop.Word` 互操作程序集（PIA）的引用。使用“添加引用”对话框，可能会看到更多此程序的实例。选择一个版本号为 12.0.0.0 的。当你在解决方案资源管理器中选中引用的程序集时，你可以看到它的“Embed Interop Properties”（嵌入互操作类型）被设置为 true，如图 7-07 所示。

![](img/b5597c749e848b27b0d305153ae16106_453_0.png)

图 7-07：Embed Interop Types 已设置为 true

该属性是保持 No-PIA 特性的关键。在构建期间，编译器会检查 `Microsoft.Office.Interop.Word` 程序集，收集调用者直接或间接接触到的所有类型，并将它们烘焙到应用程序程序集中。

将 `WordHelper` 中的 `Class1.cs` 重命名为 `TableHelper.cs`，并将列表 10-5 中的代码复制到此文件中。

## 列表 10-5：TableHelper.cs

```csharp
using System;
using Word = Microsoft.Office.Interop.Word;
```

```csharp
namespace WordHelper
{
    public static void InsertTable(Word.Application wordApp, int rows, int columns)
    {
        wordApp.ActiveDocument.Tables.Add(
            Range: word.Selection.Range,
            NumRows: rows,
            NumColumns: columns,
            DefaultTableBehavior: Word.WdTableBehavior.wdDefault9TableBehavior,
            AutoFitBehavior: Word.WdAutoFitBehavior.wdAutoFixed);
    }

    public static Type WordType
    {
        return typeof(Word.Application);
    }
}
```

代码文件 `TableHelper.cs` 可在 Wrox.com 下载。

将 `TypeEquivalenceDemo` 项目中 `Program.cs` 文件的内容更改为列表 10-6 所示的内容。

## 列表 10-6：Program.cs

```csharp
using System;
using WordHelper;
using Word = Microsoft.Office.Interop.Word;
```

```csharp
namespace TypeEquivalenceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            var word = new Word.Application();
            word.Visible = true;
            word.Documents.Add();
            word.Selection.InsertText(Text: "This is a table");
            TableHelper.InsertTable(word, 3, 2);
            Console.WriteLine("Equality: {0}");
            typeof(Word.Application) == TableHelper.WordType);
        }
    }
}
```

## 列表 10-6（续）

```csharp
Console.WriteLine("Equivalence: {0}", typeof(Word.Application).IsEquivalentTo(TableHelper.WordType));
}
```

代码文件 `Program.cs` 可在 Wrox.com 下载。

当你运行此应用程序时，它执行的操作完全你从源码中预期的那样——它创建一个 Word 文档并插入“This is a table”，随后是一个三行两列的表格。有趣的地方在于它是如何实现的。由于 No-PIA 模式，一些类型被添加到 `TypeEquivalentDemo` 和 `WordHelper` 程序集中，代表了 `Microsoft.Application.Interop.Word` 程序集中的 Word 互操作性。这样的类型是 `Word.Application`。

但是，如果在两个独立的程序集中有（通过编译器）两个 `Word.Application` 声明，.NET 框架的公共类型系统会将它们处理为独立的、不相关的类型。在这种情况下，当调用定义在 `WordHelper` 程序集中的 `TableHelper.InsertTable` 并期望一个也定义在那里的 `Word.Application` 类型时，如何传递定义在 `TypeEquivalentDemo` 程序集中的 `Word.Application` 实例呢？

## 等价性的等价插入

完成上述任务在 CLR 4.0 之前的任何 CLR 中都是可能的。但在 CLR 4.0 中是可以实现的，因为有了类型等价性特性。在后台，你可以运行以下行代码：

```csharp
TableHelper.InsertTable(word, 3, 2);
```

这将导致以下编译结果：

```csharp
TableHelper.InsertTable((Word.Application)word, 3, 2);
```

在此代码中，`WordHelper` 使用了类型。类型等价特性意味着 CLR 能够执行指定的强制转换。10-6 中 `Main` 方法的最后两个语句比较了 `Word.Application` 类型的相等性（使用运算符）和等价性（使用 `IsEquivalentTo`）。第一个比较返回 false，第二个返回 true，如图 10-8 所示。

![](img/b5597c749e848b27b0d305153ae16106_455_0.png)

图 10-8：相等比较的结果

## CLR 中的等价性

如所述，CLR 4.0 支持在程序集中嵌入类型信息，而不是从互操作程序集获取这些类型信息。编译器生成简洁的代码，嵌入的类型信息仅实际使用的类型和成员。由于这种行为，两个程序集对同一个类型有不同的视图。每个程序集都有不同的 `System.Type` 对象来表示其视图。

从 CLR 的角度来看，类型等价意味着从一个程序集传递到另一个程序集的 COM 对象可以转换为接收程序集中的相应类型。

CLR 只对 COM 类型支持等价性，作为限制，还支持接口、结构体、枚举和委托。类不受此行为影响。当两个程序集满足以下标准时，两个 COM 类型被视为等价类型：

- 两个类型都是接口或结构体或枚举或委托。
- 两个都是 COM 导入类型。
- 如果它们是接口，它们应该被 `ComImportAttribute` 和 `GuidAttribute` 装饰。
- 定义这些类型的程序集（通常是两个独立的程序集）具有 `ImportedFromTypeLibAttribute` 或 `PrimaryInteropAssembly` 属性。
- 这些类型的 `GuidAttribute` 值相等。

在构建过程中，编译器会检查类型是否在假设类型等等的上下文中。在这种情况下，它会检查是否符合标准。在出现问题时，编译器会引发相应的错误消息。

编译器使用 `TypeIdentifierAttribute` 和 `CompilerGeneratedAttribute` 属性解码类型声明。

### 并行计算

在过去的 15 年里，计算机 CPU 变得非常快，而且根据摩尔定律，它们的计算能力每 18 个月翻倍。这在显卡和 GPU 上尤为引注目，它们的性能提升甚至超过了摩尔定律。长期以来，这种惊人的进展是通过提高 CPU 时钟频率实现的，而且，处理器架构也发生了演进。

时钟频率的提高意味着应用程序性能随之提高（几乎是线性增长），而无需更改软件架构。

## 多核转型的挑战

根据摩尔定律，单位芯片表面放置的晶体管数量翻倍的趋势仍在持续。然而，对于 CPU 时钟频率并非如此！时钟频率的进一步增加意味着更多的热量需要散热，冷却处理器正成为制造商的一个大问题。此外，还存在物理极限——光速不会更快。

尽管 CPU 的速度无法显著提高，但单位面积晶体管数量仍然可以增加。制造商将在原来只放置一个核心的面积内放置两个或四个 CPU 核心。因此，如果 CPU 时钟频率无法根据摩尔定律进行改进，它们的处理能力可以！

图 10-9 显示了 Windows 任务管理器在单台计算机上显示 128 个满载的 CPU 核心的示例。这不是戏法——这是一个真实的服务器！

![](img/b5597c749e848b27b0d305153ae16106_457_0.png)

图 10-9：服务器计算机中的 128 个 CPU 核心

这是另一个有趣的事实：微软 Windows 7 可以扩展到 256 个 CPU 核心。多核转型不是未来；它已经到来！

## 软件：最弱的环节

通过增加 CPU 核心数量来提高计算能力可以很好用于 Web 应用。Web 服务器架构轻松允许将用户请求分配给不同的处理器。开发者在添加新核心时，无需任何特殊编码即可让 Web 实现扩展。然而，在 Web 应用的数据库层设置瓶颈会限制扩展。

如果你没有这种数据库瓶颈，那么有一件事是不改变架构就无法解决的。尽管你可能拥有大量的处理器，单个用户请求的响应时间也无法低于某个阈值。如果用户请求运行的算法是顺序执行的（它只能在单线程上运行），即使有一百个 CPU 也无法将响应时间降低到该阈值以下。

（多核）CPU 的优势无法应用于桌面应用程序中，因为架构限制只允许顺序执行。当然，拥有多个核心意味着多个应用程序可以并行运行，但这无法帮助缓慢应用程序的运行时间。这类应用程序无法从在桌面机器中放入两个、四个甚至更多核心中获益。

因此，对于使用“顺序风格”设计和实现的应用程序，使用多个核心是不值得的。多核开启了新的视野——但需要软件架构来实现潜在的收益。

从这个角度来看，今天大多数软件都是最弱的环节。

## 多线程问题

如果你想开发一个支持算法某些部分并发执行的应用程序，你就无法避免直接使用线程。管理多个线程绝对具有挑战性。为了构建一个健壮且无臭的应用程序，你面临着几个需要正确解决的任务。多线程引入了你需要处理变量和资源同步、利用为顺序使用设计的数据结构的流控制、竞态条件、死锁、锁冲突以及许多其他情况。

讨论并发编程的文献非常浩瀚，涵盖了各个方面，甚至为模式语境建议了设计模式——但并没有简化多线程。即使你发现了一个简单的原理或模式来将任务转换为并行任务，你仍然必须应对更多的困难，包括以下：

- 并行的方面将渗透到整个任务中。你必须找到将任务拆分为更小的独立的可并行化任务的原理。你必须将这些部分封装到线程中，并负责管理公共资源、同步它们的访问。任务之间的流控制应该被仔细管理——例如，在结束时，任务应该等待每个任务完成其工作。
- 在使你的算法受益于并行的最终代码中，真实的业务代码（即实现业务功能的代码）将与源自并行方面的代码混合在一起。后者会显著增加业务代码的行数规模。代码的任何进一步更改都需要额外的开发资源，因为整个代码变长了。你更有可能在代码中迷失，或者触碰到基础设施代码而不是业务代码。
- 测试这些代码更具挑战性且浪费资源。为了保持代码覆盖率在特定水平，你必须编写更多的单元测试用例。并行基础设施的正确性（例如避免竞态条件）也需要额外的测试用例。

开发完成后，这些多线程应用程序在支持阶段会产生更多工作。如果应用程序运行不符合要求，捕获了一些错误（例如，怀疑是竞态条件），并行会为故障排除增加一些额外任务，包括以下：

- 你必须猜测问题是在设计中还是在实现中。
