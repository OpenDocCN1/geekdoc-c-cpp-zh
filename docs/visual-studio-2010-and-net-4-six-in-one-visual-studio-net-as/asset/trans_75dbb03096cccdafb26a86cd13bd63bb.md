

如果你有多个应用程序配置，需要部署到不同的客户端机器上，那么情况就会变得更加复杂。从投入的角度来看，这意味着开发者大约花费 20% 的精力开发原始应用程序，而花费 80% 的精力在多年后对其进行维护。你可以将那痛苦的 80% 中的一部分转化为更有用的东西（例如，投资于创造更好的业务价值或改进用户体验），这样你的客户和老板都会很高兴，你的薪水也会更高。这就是 MEF 发挥用场的地方。

## 动态组合

为什么动态组合如此重要？如果你从较小的独立组件创建应用程序，就可以对应用程序进行架构设计，使得职责划分更好，边界更加清晰。根据这些职责，你可以单独测试组件、发现 bug 并修复它们。单独处理这些小部分比维护它们要容易得多。然而，问题在于，你该如何将这些单独的部分组合成一个完整的应用程序呢？

嗯，这就是 MEF 所做的——部分声明它们与其他部分共同工作的意图，然后 MEF 将它们所有的部分整合到应用程序中。你得到的不是一个单式的、静态编译的软件，而是一个动态组合的软件，你甚至可以“插入”一个新部分（就像向现有组合中插入一个新的乐高积木一样）。微软利用 MEF 的第一个应用程序之一是 Visual Studio 2010，其代码编辑器实际上是用 MEF 构建的。

## 开/闭原则

你可能认为动态组合应用程序和静态编译应用程序的设计方法非常不同。你不能说其中一个更容易而另一个更复杂。它们只是简单地不同。然而，从动态性的角度来看，有一个主要的设计原则将成为你的指路之星。

这就是开/闭原则，它归功于 Bertrand Meyer 他的著作《面向对象的软件构造》（Upper Saddle, New Jersey: Prentice-Hall, 2000）。该原则指出，你应该创建软件实体（组件），使得它们对扩展是开放的，但对修改是关闭的。这可以被翻译为：如果你创建软件实体，你应该创建在不改变其源代码的情况下具有扩展机会的对象。

该原则的一个例子是当你创建一个带有虚方法的基类以将其作为扩展点时。当需要修改行为时，你保持基类不变，并编写一个重写了虚方法的派生类。

该原则背后的原因是，修改现有（即使是经过测试的）组件的源代码会引入风险，且缓解成本相对较高。你可能会引入新的 bug、改变预期的逻辑，甚至破坏现有的接口。开/闭原则实际上是说你可以在不改变现有代码的情况下修改系统。相反，你添加新的（当然是经过测试的）代码。

对于由小部分动态组合的应用程序，该原则建议创建不允许更改源代码的软件组件，但允许加载更改行为的部分。

## 一个简单的 MEF 示例

理解 MEF 如何应对动态软件组合挑战的最佳方法是创建一个简短的示例。

启动 Visual Studio 并创建一个名为 MefGreetings 的 C# 控制台应用程序。该应用程序将是考虑了扩展性的“Hello, World”的重构形式。你将创建一个负责问候用户的独立组件。向项目添加两个代码文件，并将其命名为 Greetings.cs 和 SimpleGreeting.cs。将插图 10-17 中的源代码复制到 IGreetings.cs，将插图 10-18 中的代码复制到 SimpleGreeting.cs。

![](img/b5597c749e848b27b0d305153ae16106_506_0.png)

- 录图 10-17: IGreetings.cs

```
namespace MefGreetings
{
    interface IGreetings
    {
        string SayHello();
    }
}
```

> 代码文件 [IGreetings.cs] 可在 Wrox.com 下载

![](img/b5597c749e848b27b0d305153ae16106_506_1.png)

- 录图 10-18: SimpleGreeting.cs

```
namespace MefGreetings
{
    class SimpleGreeting : IGreetings
    {
        public string SayHello()
        {
            return "Hello from Visual Studio 2010";
        }
    }
}
```

> 代码文件 [SimpleGreeting.cs] 可在 Wrox.com 下载

如录图 10-19 所示更改 Program.cs 文件，示例应用程序即可准备好构建和运行。

## 录图 10-19: Program.cs

```
using System;

namespace MefGreetings
{
    class Program
    {
        static void Main(string[] args)
        {
            var greetings = new SimpleGreeting();
            Console.WriteLine(greetings.SayHello());
        }
    }
}
```

> 代码文件 [Program.cs] 可在 Wrox.com 下载

运行应用程序，它完全按照你预期的工作——它显示了“Hello from Visual Studio 2010”消息。尽管对应用程序进行了重构，SimpleGreeting 和 Program 仍然紧耦合耦合。尽管问候文本通过 IGreeting 接口与控制台类解耦，但 SimpleGreeting 类是被直接实例化的。现在，让我们把你的应用程序变成一个“MEFish”应用程序吧！

## 让 MEF 加入游戏

要使用 MEF，请向 System.ComponentModel.Composition 程序集添加引用，因为 MEF 类型和属性在这里声明。你将在几几个步骤内将此应用程序转换为动态组合的应用程序。

用 `Export` 属性装饰 SimpleGreeting。该属性将表示 SimpleGreeting 是一个可组合的部分，向外部世界提供服务。该属性有一个 `typeof(IGreeting)` 参数，它是 SimpleGreeting 即将导出的合约标识符。录图 10-20 显示了更改后的 SimpleGreetings.cs。

## 录图 10-20: 带有 Export 属性的 SimpleGreeting

```
using System.ComponentModel.Composition;

namespace MefGreetings
{
    [Export(typeof(IGreeting))]
    class SimpleGreeting : IGreeting
    {
        public string SayHello()
        {
            return "Hello from Visual Studio 2010";
        }
    }
}
```

> 代码文件 [SimpleGreetings.cs] 可在 Wrox.com 下载

在 Main 方法中，你必须告诉应用程序使用实现 IGreetings 服务合约的组件，而不是实例化 SimpleGreeting 类。使用 MEF，这只需要几行代码，如录图 10-21 所示。

## 录图 10-21: 组合应用程序部分

```
using System;
using System.Reflection;
using System.ComponentModel.Composition.Hosting;
using System.ComponentModel.Composition;

namespace MeGreetings
{
    class Program
    {
        [Import]
        private IGreetings Greetings { get; set; }

        static void Main(string[] args)
        {
            var program = new Program();
            program.Run();
        }

        private void Run()
        {
            var catalog = new AssemblyCatalog(Assembly.GetExecutingAssembly());
            var container = new CompositionContainer(catalog);
            container.ComposeParts(this);

            Console.WriteLine(Greetings.SayHello());
        }
    }
}
```

> 代码文件 [Program.cs] 可在 Wrox.com 下载

当你运行这段代码时，你可以看到它仍然显示了“Hello from Visual Studio 2010”消息。但是，正如你所见，应用程序中没有显式初始化 Greetings 属性的代码。因此，你可能会预期在运行程序时遇到 NullReferenceException，但这种情况并没有发生

