
使用 Visual Studio 2010，您可以通过项目属性、应用程序设置和程序集信息来配置这些属性，如图 18-6 所示。

## 动态创建和加载程序集

在开发期间，您会向程序集添加引用，使其包含在程序集引用中，并且程序集的类型可供编译器使用。在运行时，只要实例化程序集的类型或使用该类型的某个方法，被引用的程序集就会被加载。除了使用这种自动行为之外，您还可以以编程方式加载程序集。要以编程方式加载程序集，可以使用类 Assembly 及其静态方法 Load()。该方法被重载，您可以使用 AssemblyName 传递程序集的名称、程序集的名称或字节数组。

![](img/d7d2ffa0a76feaab821930e95daace93_499_0.png)

也可以即时创建程序集，如下一个示例所示。此示例演示了如何将 C# 代码输入到文本框中，通过启动 C# 编译器动态创建新程序集，并调用编译后的代码。

要动态编译 C# 代码，可以使用命名空间 Microsoft.CSharp 中的类 CSharpCodeProvider。使用此类，您可以从 DOM 树、文件和源代码编译代码并生成程序集。

应用程序的 UI 使用 WPF 创建。您可以在图 18-7 中看到 UI 的设计视图。窗口由用于输入 C# 代码的 TextBox、一个 Button 以及跨越最后一行所有列以显示结果的 TextBlock WPF 控件组成，如图 18-7 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_499_1.png)

要动态编译和运行 C# 代码，类 CodeDriver 定义了方法 CompileAndRun()。此方法编译文本框中的代码并启动生成的 方法。

```
```
using System;
using System.CodeDom.Compiler;
using System.IO;
using System.Reflection;
using System.Text;
```

到目前为止编写的程序的缺点是，每次单击“编译并运行”按钮时，都会创建一个新程序集并加载它，程序始终需要越来越多的内存。您无法从应用程序中卸载程序集。要卸载程序集，需要应用程序域。

![](img/d7d2ffa0a76feaab821930e95daace93_502_0.png)

图 18-8

## 应用程序域

在 .NET 之前，进程被用作隔离边界，每个进程都有其私有的虚拟内存；在一个进程中运行的应用程序无法写入另一个应用程序的内存，从而导致另一个应用程序崩溃。进程被用作应用程序之间的隔离和安全边界。有了 .NET 架构，您就有了应用程序的新边界：应用程序域。有了托管的 IL 代码，运行时可以确保在单个进程内无法访问另一个应用程序的内存。多个应用程序可以在单个进程内的多个应用程序域中运行（见图 18-9）。

程序集加载到应用程序域中。在图 18-9 中，您可以看到进程 4711 具有两个应用程序域。在应用程序域 A 中，实例化了对象一和对象二，对象一在程序集一中，对象二在程序集二中。进程 4711 中的第二个应用程序域有一个实例一。为了最小化内存消耗，程序集的代码只加载一次到应用程序域中。实例和静态成员在应用程序域之间不共享。无法直接访问另一个应用程序域中的对象；需要使用代理代替。因此，在图 18-9 中，应用程序域 B 中的对象一如果没有代理，就无法直接访问应用程序域 A 中的对象一或对象二。

![](img/d7d2ffa0a76feaab821930e95daace93_502_1.png)

图 18-9

AppDomain 类用于创建和终止应用程序域、加载和卸载程序集和类型，以及枚举域中的程序集和线程。在本节中，您将编写一个小型示例来查看应用程序域的实际运行情况。

首先，创建一个名为 AssemblyA 的 C# 控制台应用程序。在 Main() 方法中添加一个 Console.WriteLine()，以便您可以看到何时调用此方法。此外，添加一个名为 Demo 的类，其构造函数有两个 int 值作为参数，这将用于使用 AppDomain 类创建实例。AssemblyA.exe 程序集将由随后创建的第二个应用程序加载：

```
using System;

namespace Wrox.ProCSharp.Assemblies
{
    public class Demo
    {
        public Demo(int val1, int val2)
        {
            Console.WriteLine("Constructor with the values {0}, {1} " +
                "in domain {2} called", val1, val2,
                AppDomain.CurrentDomain.FriendlyName);
        }
    }

    class Program
    {
        static void Main()
        {
            Console.WriteLine("Main in domain {0} called",
                AppDomain.CurrentDomain.FriendlyName);
        }
    }
}
```

代码片段 AssemblyA/Program.cs

运行应用程序会产生以下输出：

Main in domain AssemblyA.exe called.

您创建的第二个项目再次是一个 C# 控制台应用程序：DomainTest。首先，使用 AppDomain 类的 FriendlyName 属性显示当前域的名称。使用 CreateDomain() 方法创建一个新的应用程序域，其友好名称为 New AppDomain。接下来，将程序集 AssemblyA 加载到新域中并通过调用 ExecuteAssembly() 来调用 Main() 方法：

```
using System;
using System.Reflection;

namespace Wrox.ProCSharp.Assemblies
{
    class Program
    {
        static void Main()
        {
            AppDomain currentDomain = AppDomain.CurrentDomain;
            Console.WriteLine(currentDomain.FriendlyName);
            AppDomain secondDomain = AppDomain.CreateDomain("New AppDomain");
            secondDomain.ExecuteAssembly("AssemblyA.exe");
        }
    }
}
```

代码片段 DomainTest/Program.cs

在启动程序 DomainTest.exe 之前，使用 DomainTest 项目引用程序集 AssemblyA.exe。使用 Visual Studio 2010 引用程序集会将程序集复制到项目目录，以便可以找到它。如果找不到程序集，将抛出 System.IO.FileNotFoundException 异常。

当运行 DomainTest.exe 时，您会得到以下控制台输出。DomainTest.exe 是第一个应用程序域的友好名称。第二行是 New AppDomain 中新加载的程序集的输出。使用进程查看器，您将看不到进程 AssemblyA.exe 在执行，因为没有创建新进程。AssemblyA 已加载到进程 DomainTest.exe 中。

```
DomainTest.exe
Main in domain New AppDomain called
```

除了在新加载的程序集中调用 Main() 方法之外，您还可以创建一个新实例。在下面的示例中，将 ExecuteAssembly() 方法替换为 CreateInstance()。第一个参数是程序集的名称，AssemblyA。第二个参数定义应实例化的类型：Wrox.ProCSharp.Assemblies.Demo。第三个参数 true 表示忽略大小写。System.Reflection.BindingFlags.CreateInstance 是一个绑定标志枚举值，用于指定应调用构造函数：

```
AppDomain secondDomain = AppDomain.CreateDomain("New AppDomain");
// secondDomain.ExecuteAssembly("AssemblyA.exe");
secondDomain.CreateInstance("AssemblyA", "Wrox.ProCSharp.Assemblies.Demo",
true, BindingFlags.CreateInstance, null, new object[] { 7, 3 },
null, null);

代码片段 DomainTest/Program.cs
```

应用程序成功运行的结果如下：

```
DomainTest.exe
Constructor with the values 7, 3 in domain New AppDomain called
```

现在您已经了解了如何创建和调用应用程序域。在运行时主机中，应用程序域会自动创建。ASP.NET 为在 Web 服务器上运行的每个 Web 应用程序创建一个应用程序域。Internet Explorer 创建应用程序域，在其中托管控件将运行。对于应用程序，如果您想卸载程序集，创建应用程序域会很有用。只能通过终止应用程序域来卸载程序集。

> 如果以动态方式加载程序集，并且存在使用后卸载程序集的需求，则应用程序域是一个非常有用的构造。在主应用程序域中，不可能摆脱已加载的程序集。但是，可以结束应用程序域，其中仅在该应用程序域中加载的所有程序集都会从内存中清除。

有了关于应用程序域的这些知识，现在可以更改之前创建的 WPF 程序。新的类 CodeDriverInAppDomain 使用 AppDomain.CreateDomain 创建一个新的应用程序域。在此新应用程序域内，使用 CreateInstanceAndUnwrap() 实例化类 CodeDriver。在卸载新应用程序域之前，使用 CodeDriver 实例调用 CompileAndRun() 方法。

```
using System;
using System.Runtime.Remoting;

namespace Wrox.ProCSharp.Assemblies
{
    public class CodeDriverInAppDomain
    {
        public string CompileAndRun(string code, out bool hasError)
        {
            AppDomain codeDomain = AppDomain.CreateDomain("CodeDriver");
            CodeDriver codeDriver = (CodeDriver)
