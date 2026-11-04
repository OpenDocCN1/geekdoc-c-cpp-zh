
几乎可以做任何你能想到的编程工作，从基于 Web 的数据库到密码学，再到不起眼的 Windows 对话框。

Microsoft 会声称 .NET 远优于 Sun 基于 Java 的 Web 工具套件，但这不是重点。与 Java 不同，.NET 不要求你重写现有程序。Visual Basic 程序员只需添加几行代码，就能让现有程序具备 Web 知识（也就是说，它知道如何从 Internet 获取数据）。.NET 支持所有常见的 Microsoft 语言——以及第三方供应商编写的数百种其他语言。然而，C# 是 .NET 家族中的旗舰语言。C# 始终是第一种能够访问 .NET 每项新功能的语言。

## Visual Studio 2012 是什么？Visual C# 呢？

（你确实问了很多问题。）Microsoft 的第一种“Visual”语言是 Visual Basic。Microsoft 第一种流行的基于 C 的语言是 Visual C++。与 Visual Basic 一样，它的名称中带有 Visual，因为它内置了图形用户界面（GUI——读作“GOO-ee”）。这个 GUI 包含开发漂亮精巧的 C++ 程序所需的一切。

最终，Microsoft 将其所有语言整合到一个单一环境——Visual Studio 中。随着 Visual Studio 6.0 逐渐显老，开发者焦急地等待版本 7。然而，在其发布前不久，Microsoft 决定将其重命名为 Visual Studio .NET，以突出这个新环境与 .NET 的关系。

这在我听来像是一种营销噱头——直到我开始深入研究它。Visual Studio .NET 与其前代产品差异相当大——足以值得采用一个新名称。Visual Studio 2012 是原 Visual Studio .NET 的第六代后继版本。（第 IV 部分充满了 Visual Studio 的精彩内容，包括自定义它的说明。）

![](img/80ff26f06fc9ab951e1cd4257b867366_39_0.png)

Microsoft 将其语言实现称为 Visual C#。实际上，Visual C# 不过是 Visual Studio 的 C# 组件。无论有没有 Visual Studio，C# 就是 C#。

好了，就这样。没有更多问题了。（至少目前如此。）

## 创建你的第一个控制台应用程序

Visual Studio 2012 包含一个应用程序向导，它可以生成模板程序，并为你省去从头开始做所有事情时不得不做的许多繁琐工作。（我不推荐从头开始的方法。）

通常，入门程序并不会真正做什么——至少不会做什么有用的事。（听起来像我的大多数程序。）然而，它们确实能让你越过起步阶段的最初障碍。有些入门程序相当复杂。事实上，你会惊讶于应用程序向导仅靠自己就能构建出多少功能，尤其是对于图形程序。

不过，这个入门程序甚至不是图形程序。控制台应用程序是在 Windows 内的“控制台”中运行的程序，通常称为 DOS 提示符或命令窗口。如果你按 Win+R，然后键入 cmd，就会看到一个命令窗口。应用程序将在该控制台中运行。

以下说明适用于 Visual Studio。如果你使用 Visual Studio 以外的任何工具，就必须参考你的环境附带的文档。或者，你也可以直接将源代码键入你的 C# 环境。有关 Visual Studio 的一些替代方案，请参阅本书的引言。

![](img/80ff26f06fc9ab951e1cd4257b867366_40_0.png)

## 创建源程序

要启动 Visual Studio，请按键盘上的 Windows 按钮并键入 Visual Studio。Visual Studio 2012 会作为可用选项之一出现。

完成以下步骤以创建你的 C# 控制台应用：

- 1. 打开 Visual Studio 2012，然后单击图 1-1 所示的“新建项目”链接。

![](img/80ff26f06fc9ab951e1cd4257b867366_40_1.png)

图 1-1：创建新项目会让你踏上开发更好的 Windows 应用程序之路。

Visual Studio 会向你展示许多图标，代表你可以创建的不同类型的应用程序，如图 1-2 所示。

![](img/80ff26f06fc9ab951e1cd4257b867366_41_0.png)

图 1-2：
Visual Studio 应用程序向导迫不及待地要为你创建新程序。

![](img/80ff26f06fc9ab951e1cd4257b867366_41_1.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_41_2.png)

- 2. 在此“新建项目”窗口中，单击“控制台应用程序”图标。

确保在“项目类型”窗格中选择 Visual C#——以及其下的 Windows——否则 Visual Studio 可能会创建像 Visual Basic 或 Visual C++ 应用程序这样糟糕的东西。然后在“模板”窗格中单击“控制台应用程序”图标。

Visual Studio 要求你先创建一个项目，然后才能开始输入你的 C# 程序。项目是一个文件夹，你把构成程序的所有文件都扔进去。它有一组配置文件，帮助编译器完成工作。当你让编译器生成（编译）程序时，它会梳理项目，找出重新创建可执行程序所需的文件。

![](img/80ff26f06fc9ab951e1cd4257b867366_41_3.png)

- 3. 你的第一个应用程序的默认名称是 ConsoleApplication1，但这次请在“名称”字段中键入 Program1，将其更改。

存储此文件的默认位置在“文档”目录深处的某个地方。也许因为我不好对付（或者也许因为我在写书），我喜欢把程序放在我希望它们去的地方，而不一定是 Visual Studio 希望它们去的地方。为了简化本书的操作，你可以更改默认程序位置。请按以下步骤操作：

- a. 选择“工具”→“选项”。

“选项”对话框会打开。你可能需要勾选“显示所有选项”复选框。

- b. 选择*“项目和解决方案”→“常规”。*
- c. 在*“项目位置”*字段中选择新位置，然后单击**确定**。

    （我建议本书使用 C:\C# Programs。）

你可以在“项目位置”对话框中同时创建新目录。单击对话框顶部带小旭日图案的文件夹图标。（如果你已从网站安装了示例程序，该目录可能已经存在。）

你可以在图 1-3 中看到“选项”对话框。暂时不要动项目设置中的其他字段。有关 Visual Studio 自定义的更多内容，请阅读第 IV 部分。

![](img/80ff26f06fc9ab951e1cd4257b867366_42_0.png)

**图 1-3：** 更改默认项目位置。

- 4. 单击**确定**按钮。

在一阵磁盘呼呼作响和咔嗒声之后，Visual Studio 会生成一个名为 *Program.cs* 的文件。（如果你查看标有*“解决方案资源管理器”*的窗口，会看到其他一些文件；暂时忽略它们。如果“解决方案资源管理器”不可见，请选择*“视图”→“解决方案资源管理器”*。）

（C# 源文件的扩展名为 `.cs`。名称 *Program* 是指派给程序文件的默认名称。

你的第一个控制台应用的内容如下所示：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
```

```csharp
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

![](img/80ff26f06fc9ab951e1cd4257b867366_43_0.png)

在代码窗口的左边缘，你会看到方框中有几个小的加号（+）和减号（−）。单击 using ... 旁边的 + 号。这会展开一个代码区域，这是 Visual Studio 的一个便捷功能，可尽量减少杂乱。以下是展开默认控制台应用中的区域时出现的指令：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

区域通过隐藏你不在处理的代码，帮助你专注于正在处理的代码。某些代码块——例如命名空间块、类块、方法和其他代码项——会自动获得 +/-，而无需 #region 指令。如果你愿意，还可以通过在一个代码段上方键入 #region、在其下方键入 #endregion 来添加自己的可折叠区域。为区域提供一个名称会很有帮助，例如 Public methods。这个代码段看起来像这样：

```
#region Public methods
... your code
#endregion Public methods
```

![](img/80ff26f06fc9ab951e1cd4257b867366_43_1.png)

这个名称可以包含空格。此外，你可以将一个区域嵌套在另一个区域内，但区域不能重叠。

目前，using System; 是你真正需要的唯一 using 指令。你可以删除其他指令；编译器会告诉你是否缺少某个指令。

## 进行试运行

要将你的 C# 程序转换为可执行程序，请选择“生成”→“生成 Program1”。Visual Studio 会响应以下消息：

```
- Build started: Project: Program1, Configuration: Debug Any CPU -

Csc.exe /noconfig /nowarn ... (and much more)

Compile complete -- 0 errors, 0 warnings

Program1 -> C:\Program Files\... (and more)==Build: 1 succeeded or up-to-date, 0 failed, 0 skipped==
```

这里的关键是最后一行中的 1 succeeded 部分。
