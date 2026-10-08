
你在“新建项目”对话框模板中间窗格中看到的所有项都涵盖了整个项目，包括项目文件（已设置好属性）、所有源文件（包括资源、内容文件、关联文档文件等）以及项目引用的引用。

项目文件模板还包含 IDE 用来显示项目信息的其他元数据。例如，对话框窗格会显示项目的简短描述。数据还包括用于在 UI 中对模板分类的信息。例如，模板可以禁用“浏览”按钮。

当你从所选的项目模板创建项目实例时，模板系统会将所有文件从模板复制到指定位置。除了复制操作之外：

- 模板系统可以替换文件名及其内容中的字符串。例如，可以用项目名称替换项目文件，还可以替换源文件中的默认命名规范。
- 可以启动向导，该向导收集有关项目的信息，并在生成项目产物时使用这些信息。

假设你创建了一个名为 MyWpfApp 的新 WPF 应用程序。图 4-3 显示了让你从该项目开始的模板系统。

项目模板包含图 4-3 所示的所有文件。如你所见，项目文件名已更改为 MyWpfApp。如果你打开 `App.xml.cs` 文件，你会发现根命名空间也已重名为 MyWpfApp。

## 模板

当你基于特定模板创建项目时，你还可以向该项目添加新项，并且希望从一个定义良好的项骨架而不是空代码文件开始。这就是项用用场的地方。

在日常活动中，你通常处理几种类型的项目项，如表单、实体类、服务和控制器类型、数据库脚本等。Visual Studio 提供了大量的项模板，你可以通过“添加新项”对话框将它们添加到项目中。图 4-4 显示了你在处理 WPF 应用程序时可以选择的项。

![](img/b5597c749e848b27b0d305153ae16106_110_0.png)

图 4-3：解决方案管理器中的新项目

![](img/b5597c749e848b27b0d305153ae16106_111_0.png)

**图 4-4：** 添加新项对话框

此对话框与“新建项目”对话框非常相似，其 UI 背后的机制也是如此。模板系统处理项模板的方式与处理项目模板基本相同——所有项模板文件都会复制到项目文件夹。项模板也支持替换和向导。

项模板提供了一项功能，允许向托管该项的项目添加程序集引用。在模板定义中，项可以列出该项为了成功编译而所需的引用程序集。当项被添加到项目时，所有尚未分配给该项目的引用程序集也将被添加。

项和文件是不同的概念。虽然大多数项包含单个文件，但少数项是由多个文件组成的——例如，表单和资源，它们可能在解决方案管理器中以分级结构包含两个（或三个）依赖文件。项模板绝对不是文件模板，因此组成项的每个文件都可以（也应该）被添加到项模板中。

项模板可能包含更多要添加到项目中的项。例如，你可能为实体创建一个项，该项使用部分类（partial class）声明添加了两个文件，意图是让用户仅自定义其中一个。这些是独立的项（也就是说，你可以分别处理它们），在项目中，没有信息指示它们是单步添加的。

## 创建模板

到此为止，你已经熟悉项目模板和项模板的概念。让我们看看这些概念在实践中是如何工作的。在此过程中，你创建一个简单的项目模板和一个相关的项模板。这些活动可以为你自己的项目和项模板重复执行。

创建过程从实际实现应用程序、库、页面、表单、类或任何打算作为模板基础的产物开始。当这些产物准备就绪，你可以使用 Visual Studio 中的“导出模板向导”来物理创建模板定义并将其与 IDE 集成。你还可以向模板添加自定义点。

## 创建简单的项目模板

为了演示模板创建的步骤，让我们构建一个从窗口接收并执行命令的控制台应用程序。当然，该应用程序将非常简单且健健，此示例侧重于模板开发。

## 创建启动项目

通过文件 -> 新建 -> 项目创建一个新的 C# 项目，并在 Windows 项目类别下选择控制台应用程序。将此应用程序命名为 ConsoleBase 并点击确定。Visual Studio 会创建一个带有 `Program.cs` 和 `AssemblyInfo.cs` 文件的新应用程序。（扩展属性文件夹时可以显示此文件。）此应用程序默认不运行任何代码。因此，让我们更改 Program 类来实现一个非常简单的控制台应用程序逻辑，如代码段 4-1 所示。

字体 代码段 4-1：Program.cs

![](img/b5597c749e848b27b0d305153ae16106_112_0.png)

```
using System;

namespace ConsoleBase
{
    class Program
    {
        const string PromptText = "# >";
        const string QuitCommand = "quit";

        static void Main(string[] args)
        {
            DisplayWelcomeMessage();
            Console.Write(PromptText);
            string command;
            string[] pars;
            while (String.Compare(command = ReadCommand(out pars)),
                QuitCommand, true) != 0)
            {
                ProcessCommand(command, pars);
                Console.Write(PromptText);
            }
        }

        static void DisplayWelcomeMessage()
        {
            Console.WriteLine("Welcome to the BaseConsole application!");
            Console.WriteLine();
        }
    }
}
```

# 代码段 4-1（续）

```
static string ReadCommand(out string pars)
{
    var CommandLine = Console.ReadLine().Trim();
    var command = commandLine;
    pars = string.Empty;
    var pos = CommandLine.IndexOf(' ');
    if (pos > 0)
    {
        command = CommandLine.Substring(0, pos);
        pars = CommandLine.Substring(pos).Trim();
    }
    return command;
}

static void ProcessCommand(string command, string pars)
{
    Console.WriteLine("*{0}(\{1}) processed", command, pars);
}
```

代码文件 [Program.cs] 可在 Wrox 下载。

该类非常简单。它显示欢迎文本并循环处理用户输入的命令，除非收到“quit”命令，此时它会终止。当你不带调试并启动它时，你可以看到它是如何工作的。图 4-5 显示了输出。

![](img/b5597c749e848b27b0d305153ae16106_113_0.png)

图 4-5：BaseConsole 的示例输出

现在现在好从此应用程序创建项目了。转到文件菜单并选择“导出模板”。一个新的对话框“导出模板向导”出现在屏幕上。该向导有几个页面，其中第一页允许你选择要导出的模板类型，如图 4-6 所示。

![](img/b5597c749e848b27b0d305153ae16106_114_0.png)

图 4-6：选择模板类型页面
