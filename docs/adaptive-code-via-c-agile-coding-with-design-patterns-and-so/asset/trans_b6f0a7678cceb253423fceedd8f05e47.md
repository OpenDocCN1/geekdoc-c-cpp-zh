

## 新项目

图2-2 Visual Studio中的“新建项目”对话框允许你从许多不同的项目模板中进行选择。

- 2. 向解决方案中添加第二个项目，这次是一个类库。我把它命名为MessagePrinter。
- 3. 右键单击控制台应用程序的“引用”节点，然后选择“添加引用”。
- 4. 在“添加引用”对话框中，导航到“项目”并选择类库项目。

现在你已经在两个程序集之间创建了一个依赖关系，如图2-3所示。你的控制台应用程序依赖于类库，但类库并不依赖于控制台应用程序。控制台应用程序是客户端，类库是服务。虽然这个应用程序目前还没有做太多事情，但请生成解决方案并导航到项目的bin目录——可执行文件就在那里。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_61_0.png)

# 图2-3 任何项目的引用程序集都列在其“引用”节点下。

bin目录包含SimpleDependency.exe文件，但也包含MessagePrinter.dll文件。这个文件是由Visual Studio生成过程复制到bin目录中的，因为它被可执行文件引用为依赖项。我想给你看一个实验，但首先需要对代码稍作修改。由于这是一个什么都不做的控制台应用程序，它会在你来得及反应之前就初始化并关闭。打开控制台应用程序的Program.cs文件。

# 清单2-1 对ReadKey的调用可防止控制台应用程序立即退出。

单击此处查看代码图片

```
namespace SimpleDependency
{
    class Program
    {
        static void Main()
        {
            Console.ReadKey();
        }
    }
}
```

重新生成解决方案并运行应用程序。正如预期的那样，它会显示控制台窗口，等待你按下键盘上的某个键，然后在你按下之后终止。在Console.ReadKey()这一行设置一个断点，并从Visual Studio中调试解决方案。

当应用程序在断点处暂停时，你可以查看已为此应用程序加载到内存中的程序集。为此，你可以使用菜单栏选择“调试”>“窗口”>“模块”，也可以使用键盘快捷键Ctrl+D, M。图2-4显示了已为应用程序加载的模块列表。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_62_0.png)

图2-4 调试时，“模块”窗口会显示所有当前已加载的程序集。

你是否注意到了一些奇怪的事情？这里没有提到已创建的类库。对于这个示例，难道不应该加载MessagePrinter.dll吗？实际上，不——这正是预期的行为。原因如下：应用程序没有使用MessagePrinter程序集内的任何内容，因此.NET运行时不会加载它。

为了最终证明依赖程序集并不是真正的先决条件，请再次导航到控制台应用程序的bin目录并删除MessagePrinter.dll。再次运行应用程序，它将继续正常运行而不会引发异常。

让我们再重复几次这个实验，以便真正了解正在发生的事情。首先，在Program.cs文件的顶部添加一条`using MessagePrinter`指令。这会导入MessagePrinter命名空间。你认为这足以让公共语言运行时（CLR）加载该模块吗？并不是。依赖关系再次被忽略，程序集也不会被加载。这是因为用于导入命名空间的using语句只是语法糖，其作用仅仅是减少你需要编写的代码量。与其在每次想要使用某个类型时写出整个命名空间，你可以导入命名空间并直接引用这些类型。using语句不会生成任何可供CLR执行的指令。

下一个测试建立在第一个测试的基础上，因此你可以保留using语句。在Program.cs中，在Console.ReadLine()调用上方，添加一个对MessagePrinting.Service构造函数的调用，如清单2-2所示。

# 清单2-2 通过调用实例方法来引入依赖关系。

单击此处查看代码图片

```
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

“模块”窗口现在显示MessagePrinter.dll程序集已被加载，因为如果不将程序集的内容拉入内存，就无法构造MessagePrintingService的实例。

如果你从bin目录中删除MessagePrinter.dll并再次运行应用程序，即可证明这一点。这次会抛出异常。

单击此处查看代码图片

未处理的异常：System.IO.FileNotFoundException：无法加载文件或程序集“MessagePrinter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null”或其某个依赖项。系统找不到指定的文件。

# 框架依赖项

上一节中显示的依赖关系称为第一方依赖项。控制台应用程序及其所依赖的类库都属于同一个Visual Studio解决方案。这意味着该依赖项应该始终是可访问的，因为如有必要，依赖项目始终可以从源代码重新生成。这也意味着你可以修改第一方依赖项的源代码。

这两个项目还以.NET Framework程序集的形式拥有其他依赖项。这些程序集不属于项目本身，但预期是可用的。每个.NET Framework程序集都按其构建时所针对的.NET Framework版本进行版本管理：1、1.1、2、3.5、4、4.5，等等。某些.NET Framework程序集是特定版本新增的，无法被使用较早.NET Framework版本的项目引用。其他程序集会随着.NET Framework版本的更迭而变化，因此必须使用特定的版本。

SimpleDependency项目具有对.NET Framework的多处引用，如图2-3之前所示。其中许多依赖项是添加到所有控制台应用程序项目中的默认依赖项。示例应用程序并未使用它们，因此可以安全地移除。实际上，对于这两个项目，除了System和System.Core之外的所有引用都是多余的，因此可以从引用列表中移除。应用程序仍将正常运行。

通过移除不必要的框架依赖项，你可以更轻松地查看每个项目所需的依赖项。

# 框架程序集始终会加载

值得注意的是，与其他依赖项不同，对.NET Framework程序集的引用总是会导致这些程序集被加载。即使你实际上并未使用某个程序集，它仍然会在应用程序启动时加载。幸运的是，如果解决方案中的多个项目都引用同一个程序集，则只会将该程序集的一个实例加载到内存中，并由所有依赖方共享。

# 默认引用列表

项目的默认引用因项目类型而异。每种项目类型都有一个项目模板，其中列出了所需的引用。这就是为什么Windows窗体应用程序可以引用System.Windows.Forms程序集，而Windows Presentation Foundation应用程序可以引用WindowsBase、PresentationCore和PresentationFramework。

# 清单2-3 部分Visual Studio项目模板，用于按条件引用不同的程序集。

单击此处查看代码图片

```
<ItemGroup>
  <Reference Include="System"/>
  $if$ ($targetframeworkversion$ >= 3.5)
  <Reference Include="System.Core"/>
  <Reference Include="System.Xml.Linq"/>
  <Reference Include="System.Data.DataSetExtensions"/>
  $endif$
  $if$ ($targetframeworkversion$ >= 4.0)
  <Reference Include="Microsoft.CSharp"/>
  $endif$
  <Reference Include="System.Data"/>
  <Reference Include="System.Xml"/>
</ItemGroup>
```

