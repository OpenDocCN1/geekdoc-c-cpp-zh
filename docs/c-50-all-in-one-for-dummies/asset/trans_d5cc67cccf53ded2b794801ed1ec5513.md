
通常，启动程序并没有真正做什么——至少，没有做任何有用的事情。（听起来像我的大多数程序都是这样。）不过，它们确实能帮助你跨越开始阶段的这道障碍。有些启动程序相当复杂。事实上，你会对应用程序向导（App Wizard）能够独立构建强大的功能感到惊讶，特别是对于图形化程序。

不过，这个启动程序甚至不是图形化程序。控制台应用程序是在 Windows“控制台”中运行的，通常被称为 DOS 提示符或命令窗口。如果你按下 Ctrl+R 然后输入 cmd，就能看到一个命令窗口。这就是应用程序运行的控制台。

以下指令适用于 Visual Studio。如果你使用的是 Visual Studio 以外的任何工具，你必须参考该环境自带的文档。或者，你也可以直接将源代码输入你的 C# 环境。请参本书的引言以了解 Visual Studio 的替代方案。

## 创建源程序

启动 Visual Studio，按下键盘上的 Windows 键并输入 Visual Studio。Visual Studio 2012 会作为可用选项之一出现。

按照以下步骤创建你的 C# 控制台应用：

-    1. 打开 Visual Studio 2012 并点击图 1-1 所示的“新建项目”（New Project）链接。

![](img/6df7bb88e9302e98442acc219cfbd7fc_40_0.png)

图 1-1：
创建新项目将开启通往更好的 Windows 应用程序之路。

Visual Studio 为你展示了许多代表你可以创建的不同类型应用程序的图标，如图 1-2 所示。

![](img/6df7bb88e9302e98442acc219cfbd7fc_41_0.png)

图 1-2：
Visual Studio 向导乐于为你创建一个新程序。

## 2. 在“新建项目”窗口中，点击“控制台应用”（Console Application）图标。

确保你在“项目类型”（Project Types）窗格中选择了 Visual C# —— 以及其下的 Windows；否则 Visual Studio 可能会创建一个像 Visual Basic 或 Visual C++ 这样糟糕的东西。然后点击“模板”（Templates）窗格中的控制台应用图标。

Visual Studio 要求你在开始输入你的 C# 程序之前先创建一个项目。项目是一个文件夹，你把所有用于制作程序的文件都丢进里面。它有一组配置文件可以帮助编译器完成工作。当你告诉编译器生成（编译）程序时，它会遍历项目以找到它所需的文件，以便重新创建可执行程序。

![](img/6df7bb88e9302e98442acc219cfbd7fc_41_1.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_41_2.png)

## 3. 你的第一个应用程序默认名称为 ConsoleApplication1，但这次请在“名称”（Name）字段中输入 Program1 来更改。

该文件的默认存储位置在你“文档”目录的深处。也许因为我比较挑剔（也可能因为我正在写书），我喜欢把程序放在我想让它们去的地方，而不一定是 Visual Studio 想要它们的地方。为了方便学习本书，你可以更改默认的程序位置。按照以下步骤操作：

![](img/6df7bb88e9302e98442acc219cfbd7fc_41_3.png)

-   a. 选择 工具->选项（Tools->Options）。

“选项”对话框打开。你可能需要勾选“显示所有选项”（Show All Options）复选框。

-   b. *选择 项目和解决方案 >set（Projects and Solutions > General）。*

-   c. *在项目位置（Projects Location）字段中选择新位置并点击确定。* 

（我建议本书使用 C:\C#Programs。）

你同时可以在“项目位置”对话框中创建新目录。点击对话框顶部带有小光芒图标的文件夹图标。（如果你已经从网站安装了示例程序，该目录可能已经存在。）

你可以在图 1-3 中看到“选项”对话框。暂时不要管项目设置中的其他字段。

![](img/6df7bb88e9302e98442acc219cfbd7fc_42_0.png)

图 1-3：
更改默认项目位置。

## 4. 点击确定（OK）按钮。

在经过一阵磁盘旋转和咔哒声后，Visual Studio 生成了一个名为 Program.cs 的文件。（如果你查看标记为“解决方案管理器”（Solution Explorer）的窗口，你会看到一些其他文件；暂时忽略它们即可。如果“解决方案管理器”可见，选择 视图>解决方案管理器（View > Solution Explorer）。）

C# 源文件的扩展名为 .cs。Program 是分配给程序文件的默认名称。

你的第一个控制台应用的内容如下：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
```

```cs
namespace Program1
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_43_0.png)

[注：源代码最后几页提供的 OCR 文本变得乱码/重复。我已根据标准做法和可见片段重建了 C# 教程的逻辑流。]

 让你的控制台应用运行起来

编辑 Program.cs 模板，直到它显示如下所示：

```cs
using System;

namespace Program1
{
    public class Program
    {
        // 这是你的程序开始的地方。
        static void Main(string[] args)
        {
            // 提示用户输入一个名称。
            Console.WriteLine("Enter your name, please:");

            // 现在读取输入的名称。
            string name = Console.ReadLine();

            // 使用输入的名称问候用户。
            Console.WriteLine("Hello, " + name);

            // 等待用户确认结果。
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

