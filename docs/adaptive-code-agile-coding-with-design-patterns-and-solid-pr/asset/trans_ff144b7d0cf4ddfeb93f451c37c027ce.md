

你现在已经创建了一个从一个程序集到另一个程序集的依赖关系，如图 3-3 所示。你的控制台应用程序依赖于你的类库，但类库并不依赖于你的控制台应用程序。控制台应用程序是客户端，类库是服务。尽管此应用程序目前什么也不做，构建解决方案并导航到项目的 bin 目录——可执行文件就在那里。

![](img/f852e0a12c174e64d91a8e1a05146eab_98_0.png)

**图 3-3** 任何项目的引用程序集都列在其 References 节点下。

bin 目录包含 SimpleDependency.exe 文件，但它也包含 MessagePrinter.dll 文件。该文件是由 Visual Studio 构建过程复制到 bin 目录中的，因为它被可执行文件引用为依赖项。让我们做一个实验，但首先需要对代码做一点修改。因为这是一个什么也不做的控制台应用程序，它会在你反应过来之前就初始化并关闭。打开控制台应用程序的 Program.cs 文件。

清单 3-1 显示了在 Main 方法内部的添加内容（以粗体显示）。这是应用程序的入口点，目前什么也不做并快速退出。通过插入对 Console.ReadKey() 的调用，你可以确保应用程序在终止前等待用户按下一个键。

## LISTING 3-1

对 ReadKey 的调用可防止控制台应用程序立即退出。

```csharp
namespace SimpleDependency
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.ReadKey();
        }
    }
}
```

重新构建解决方案并运行应用程序。如预期，它会显示控制台窗口，等待你按下键盘上的一个键，然后在你按下后终止。在 `Console.ReadKey()` 行上设置一个断点，并从 Visual Studio 调试解决方案。

当应用程序在断点处暂停时，你可以查看已为此应用程序加载到内存中的程序集。为此，你可以使用菜单栏选择 Debug > Windows > Modules。图 3-4 显示了为应用程序加载的模块列表。

![](img/f852e0a12c174e64d91a8e1a05146eab_99_0.png)

**图 3-4** 调试时，Modules 窗口显示所有当前加载的程序集。

你是否注意到有什么奇怪之处？创建的类库没有任何提及。例如，`MessagePrinter.dll` 不应该被加载吗？实际上，不应该——这正是预期的行为。原因如下：应用程序没有使用 MessagePrinter 程序集内部的任何内容，因此 .NET 运行时不会加载它。

为了确凿地证明依赖程序集并不是真正的先决条件，再次导航到控制台应用程序的 bin 目录并删除 `MessagePrinter.dll`。再次运行应用程序，它会愉快地继续运行而不会引发异常。

让我们再重复几次这个实验，以真正弄清楚发生了什么。首先，在 Program.cs 文件顶部添加一个 using MessagePrinter 指令。这会导入 MessagePrinter 命名空间。你认为这足以导致通用语言运行时（CLR）加载该模块吗？不是。依赖关系再次被忽略，程序集未被加载。这是因为用于导入命名空间的 using 语句只是语法糖，仅用于减少你需要编写的代码量。与其每次想要使用其中的类型时都写出完整的命名空间，你可以导入命名空间并直接引用类型。using 语句不会为 CLR 生成任何要执行的指令。

这个下一个实验建立在前一个实验的基础上，因此你可以保留 using 语句。首先，在 MessagePrinter 程序集中创建 MessagePrintingService，如清单 3-2 所示。

## LISTING 3-2

一个简单的类来引入真正的依赖。

```csharp
namespace MessagePrinter
{
    public class MessagePrintingService
    {
        public void PrintMessage()
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

接下来，在 Program.cs 中，在对 Console.ReadKey() 的调用之前，构造一个 MessagePrintingService 的实例并调用 PrintMessage 方法，如清单 3-3 所示。

## LISTING 3-3

通过调用实例方法引入依赖。

```csharp
using System;
using MessagePrinter;

namespace SimpleDependency
{
    class Program
    {
        static void Main()
        {
            var service = new MessagePrintingService();
            service.PrintMessage();
            Console.ReadKey();
        }
    }
}
```

Modules 窗口现在显示 MessagePrinter.dll 程序集已被加载，因为没有办法在不将程序集的内容拉入内存的情况下构造 MessagePrintingService 的实例。

如果你从 bin 目录删除 MessagePrinter.dll 并再次运行应用程序，可以证明这一点。这次会抛出异常。

```text
Unhandled Exception: System.IO.FileNotFoundException: Could not load file or assembly 'MessagePrinter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null' or one of its dependencies. The system cannot find the file specified.
```

## Framework dependencies

上一节中显示的依赖关系称为第一方依赖关系。控制台应用程序和它所依赖的类库都属于同一个 Visual Studio 解决方案。这意味着依赖关系应该始终可访问，因为如果需要，依赖项目始终可以从源代码重建。这也意味着你可以修改第一方依赖项的源代码。

两个项目都有其他依赖项的形式为 .NET Framework 程序集。这些不属于项目的一部分，但预计可用。每个 .NET Framework 程序集都是为框架的特定版本构建的：1、1.1、2、3.5、4、4.5 等。一些 .NET Framework 程序集是特定版本的新增内容，不能被使用较早 .NET Framework 版本的项目引用。其他程序集会随着 .NET Framework 版本的变化而变化。

SimpleDependency 项目对 .NET Framework 有多个引用，如图 3-3 之前所示。其中许多依赖项是默认添加到所有控制台应用程序项目的。示例应用程序未使用它们，因此可以安全地删除。事实上，对于两个项目，除了 System 和 System.Core 之外的所有内容都是多余的，因此可以从引用列表中删除。应用程序仍能正确运行。

通过删除不必要的框架依赖项，你可以更轻松地可视化每个项目所需的依赖项。

## Framework assemblies always load

值得注意的是，与其他依赖项不同，对 .NET Framework 程序集的引用将始终导致这些程序集加载。即使你实际上没有使用某个程序集，它仍会在应用程序启动时加载。幸运的是，如果解决方案中的多个项目都引用同一个程序集，则只会将该程序集的一个实例加载到内存中（每个 AppDomain），并在所有依赖项之间共享。

项目的默认引用因项目类型而异。每个项目类型都有一个项目模板，其中列出了所需的引用。这就是 Windows 窗体应用程序引用 System.Windows.Forms 程序集，而 Windows Presentation Foundation 应用程序引用 WindowsBase、PresentationCore 和 PresentationFramework 的方式。

## LISTING 3-4

Visual Studio 项目模板的一部分，用于有条件地引用不同的程序集。

```xml
<ItemGroup>
  <Reference Include="System"/>
  $if $(targetframeworkversion$ >= 3.5)
    <Reference Include="System.Core"/>
    <Reference Include="System.Xml.Linq"/>
    <Reference Include="System.Data.DataSetExtensions"/>
  $endif
  $if $(targetframeworkversion$ >= 4.0)
    <Reference Include="Microsoft.CSharp"/>
  $endif
  <Reference Include="System.Data"/>
  <Reference Include="System.Xml"/>
</ItemGroup>
```

这些文件中有一些逻辑可以改变模板生成真实项目实例的方式。具体来说，引用取决于用于生成项目的 .NET Framework 版本。在这里，Microsoft.CSharp 程序集仅在项目以 .NET Framework 4 或更高版本为目标时才被引用。这是有意义的，因为它通常仅在你使用在 .NET Framework 4 中引入的 dynamic 关键字时才需要。

## Third-party dependencies

最后一种依赖类型是第三方开发者开发的程序集的依赖。通常，如果 .NET Framework 未提供某些功能，你可以通过创建第一方依赖项自行实现解决方案。这可能是一项繁琐的任务，具体取决于所需解决方案的大小。相反，你可以选择使用第三方解决方案。例如，你不太可能想要自己实现对象/关系映射器（ORM），因为这样一大块基础设施代码可能需要数月才能发挥作用，数年才能完成。相反，你可以先查看 Entity Framework，它是 .NET Framework 的一部分。如果它不能满足你的需求，你可以改而查看 NHibernate，这是一个成熟的 ORM 库，已经过大量测试。

