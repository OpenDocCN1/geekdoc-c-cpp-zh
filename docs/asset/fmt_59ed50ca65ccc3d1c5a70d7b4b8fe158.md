
Visual Studio 2015 启动并显示“开始”页面，类似于以下内容。（您的“开始”页面可能有所不同，具体取决于您使用的 Visual Studio 2015 版本。）

![](img/16f6e3fe08f01ddadb2741a92c392b0e_32_0.png)

### Note

如果这是您第一次运行 Visual Studio 2015，您可能会看到一个对话框提示您选择默认开发环境设置。Visual Studio 2015 可以根据您首选的开发语言进行定制。集成开发环境（IDE）中各种对话框和工具的默认选择设置为您选择的语言。从“开发设置”列表中选择 Visual C#，然后单击“开始 Visual Studio”按钮。经过短暂延迟后，Visual Studio 2015 IDE 出现。

- 2. 在“文件”菜单上，指向“新建”，然后单击“项目”。

“新建项目”对话框打开。此对话框列出了可作为构建应用程序起点的模板。对话框根据您使用的编程语言和应用程序类型对模板进行分类。

- 3. 在左侧窗格中，展开“已安装”节点（如果尚未展开），展开“模板”，然后单击“Visual C#”。在中间窗格中，验证窗格顶部的组合框显示 `.NET Framework 4.6`，然后单击“控制台应用程序”。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_33_0.png)

- 4. 在“位置”框中，键入 `C:\Users\YourName\Documents\Microsoft Press\VCSBS\Chapter 1`。将此路径中的文本 `YourName` 替换为您的 Windows 用户名。

### Note

为了避免重复并节省空间，在本书其余部分中，我将把路径 `C:\Users\YourName\Documents` 简称为您的“文档”文件夹。

### Tip

如果您指定的文件夹不存在，Visual Studio 2015 会为您创建它。

- 5. 在“名称”框中，键入 `TestHello`（覆盖现有的名称 `ConsoleApplication1`）。

- 6. 确保已选中“为解决方案创建目录”复选框，并且“添加到源代码控制”复选框为空，然后单击“确定”。Visual Studio 使用“控制台应用程序”模板创建项目。

如果您看到以下询问要使用哪种源代码控制机制的对话框，您忘记清除“添加到源代码控制”复选框。在这种情况下，只需单击“取消”，项目将会在不使用源代码控制的情况下创建。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_34_0.png)

Visual Studio 显示项目的启动代码，如下所示：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_34_1.png)

屏幕顶部的菜单栏提供了在编程环境中使用的功能访问。您可以使用键盘或鼠标访问菜单和命令，就像在所有基于 Windows 的程序中一样。工具栏位于菜单栏下方。它提供了运行最常用命令的按钮快捷方式。

代码和文本编辑器窗口占据屏幕的主要部分，显示源文件的内容。在多文件项目中，当您编辑

如果打开多个文件，每个源文件都有自己的标签，标签上标有源文件的名称。您可以单击标签，将命名的源文件带到代码和文本编辑器窗口的前台。

`Solution Explorer` 窗格出现在 IDE 的右侧，与代码和文本编辑器窗口相邻：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_35_0.png)

`Solution Explorer` 显示与项目关联的文件名称，以及其他项目。您也可以在 `Solution Explorer` 中双击文件名，将该源文件带到代码和文本编辑器窗口的前台。

在编写任何代码之前，请检查 `Solution Explorer` 中列出的文件，这些文件是 Visual Studio 2015 作为项目的一部分创建的：

- **Solution ‘TestHello’** 这是顶层的解决方案文件。每个应用程序包含一个解决方案文件。一个解决方案可以包含一个或多个项目，而 Visual Studio 2015 创建解决方案文件是为了帮助组织这些项目。如果您使用文件资源管理器查看 `Documents\Microsoft Press\VCSBS\Chapter 1\TestHello` 文件夹，您会看到此文件的实际名称是 `TestHello.sln`。

- **TestHello** 这是 C# 项目文件。每个项目文件引用一个或多个包含项目源代码和其他工件的文件，例如图形图像。您必须在同一个项目中用同一种编程语言编写所有的源代码。在文件资源管理器中，此文件实际称为 `TestHello.csproj`，它存储在您的 Documents 文件夹中的 `\Microsoft Press\VCSBS\Chapter 1\TestHello\TestHello` 文件夹中。

- **Properties** 这是 `TestHello` 项目中的一个文件夹。如果您展开它（单击 `Properties` 旁边的箭头），您会看到其中包含一个名为 `AssemblyInfo.cs` 的文件。`AssemblyInfo.cs` 是一个特殊文件，您可以使用它为程序添加属性，例如作者姓名、程序编写日期等。您可以指定其他属性来修改程序的运行方式。解释如何使用这些属性超出了本书的范围。

- **References** 此文件夹包含对已编译代码库的引用，您的应用程序可以使用这些库。当您的 C# 代码被编译时，它会被转换为一个库并被赋予一个唯一名称。在 Microsoft .NET Framework 中，这些库称为 *assemblies*。开发人员使用程序集打包他们编写的有用功能，以便将其分发给可能希望在自己的应用程序中使用这些功能的其他开发人员。如果您展开 `References` 文件夹，您将看到 Visual Studio 2015 默认添加到项目的引用集。这些程序集提供了对 .NET Framework 中许多常用功能的访问，并且由 Microsoft 与 Visual Studio 2015 一起提供。随着您在本<|message|> 书中练习的进行，您将了解其中许多程序集。

- **App.config** 这是应用程序配置文件。它是可选的，可能并不总是存在。您可以指定应用程序在运行时使用的设置，以修改其行为，例如用于运行应用程序的 .NET Framework 版本。您将在本书后面的章节中了解有关此文件的更多信息。

- **Program.cs** 这是一个 C# 源文件，当项目首次创建时，它会显示在代码和文本编辑器窗口中。您将在此文件中为控制台应用程序编写代码。它还包含 Visual Studio 2015 自动提供的一些代码，您将很快检查这些代码。

### 编写您的第一个程序

`Program.cs` 文件定义了一个名为 *Program* 的类，其中包含一个名为 *Main* 的方法。在 C# 中，所有可执行代码必须在方法内定义，并且所有方法都必须属于类或结构体。您将在第 7 章“创建和管理类与对象”中了解更多关于类的信息，并在第 9 章“使用枚举和结构创建值类型”中了解结构体。

*Main* 方法指定程序的入口点。此方法应以 *Program* 类中指定的方式定义为静态方法；否则，.NET Framework 可能无法将其识别为应用程序运行时 的起点。（您将在第 3 章“编写方法并应用作用域”中详细了解方法，第 7 章提供了有关静态方法的更多信息。）

### Important

C# 是一种区分大小写的语言。您必须将 `Main` 的 `M` 写成大写。

在下面的练习中，您编写代码以将消息“Hello World!”显示到控制台窗口，构建并运行您的 Hello World 控制台应用程序，并学习命名空间如何用于划分代码元素。

### 使用 Microsoft IntelliSense 编写代码

- 1. 在显示 `Program.cs` 文件的代码和文本编辑器窗口中，将光标放在 `Main` 方法中，紧跟在左大括号（ `{` ）之后，然后按 Enter 创建新行。

- 2. 在新行上，键入单词 `Console`；这是由您的应用程序引用的程序集提供的另一个类。它提供了在控制台窗口中显示消息和从键盘读取输入的方法。

当您键入单词 `Console` 开头的字母 `C` 时，会出现一个 IntelliSense 列表。

此列表包含在此上下文中有效的所有 C# 关键字和数据类型。您可以继续键入或滚动列表并用鼠标双击 `Console` 项。或者，在您键入 `Cons` 之后，IntelliSense 列表会自动聚焦到 `Console` 项，您可以按 Tab 或 Enter 键来选择它。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_37_0.png)

`Main` 应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console
}
```

### Note

*Console* 是一个内置类。

3. 在 *Console* 后立即键入一个句点。

另一个 IntelliSense 列表出现，显示 *Console* 类的方法、属性和字段。

4. 滚动列表，选择 *WriteLine*，然后按 Enter。

或者，您可以继续键入字符 **W**、**r**、**i**、**t**、**e**、**L**，直到 *WriteLine* 被选中，然后按 Enter。

IntelliSense 列表关闭，单词 *WriteLine* 被添加到源文件中。*Main* 现在应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console.WriteLine
}
```

5. 键入一个左括号，`( `。另一个 IntelliSense 提示出现。

此提示显示 *WriteLine* 方法可以接受的参数。事实上，*WriteLine* 是一个 *重载方法*，意味着 *Console* 类包含多个名为 *WriteLine* 的方法——它实际上提供了 19 个不同版本的方法。您可以使用 *WriteLine* 方法的每个版本输出不同类型的数据。（*第 3 章* 更详细地描述了重载方法。）*Main* 现在应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console.WriteLine(
}
```

### Tip

您可以通过在提示中单击上、下箭头来滚动浏览 *WriteLine* 的不同重载。

6. 键入一个右括号，`)`，然后跟一个分号，`;`。

`Main` 应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console.WriteLine();
}
```

- 7. 移动光标并在 `WriteLine` 方法后的左、右括号之间键入字符串“Hello World!”，包括引号。

`Main` 应如下所示：

点击此处查看代码图像

```
static void Main(string[] args)
{
    Console.WriteLine("Hello World!");
}
```

![](img/16f6e3fe08f01ddadb2741a92c392b0e_39_0.png)

### Tip

养成键入匹配字符对的习惯，例如括号——`( ` 和 `)`——和大括号——`{` 和 `}`——然后再填写其内容。在您输入内容后再添加结束字符很容易忘记。

### IntelliSense 图标

当你在类名后输入一个句号时，IntelliSense 会显示该类的每个成员的名称。在每个成员名称左侧都有一个图标，用来表示成员的类型。常见的图标及其类型如下：

| Icon | Meaning |

| --- | --- |

|  | 方法（在第 3 章中讨论） |

|  | 属性（在第 15 章“实现属性以访问字段”中讨论） |

|  | 类（在第 7 章中讨论） |

|  | 结构体（在第 9 章中讨论） |

|  | 枚举（在第 9 章中讨论） |

|  | 扩展方法（在第 12 章“使用继承”中讨论） |

|  | 接口（在第 13 章“创建接口和定义抽象类”中讨论） |

|  | 委托（在第 17 章“介绍泛型”中讨论） |

|  | 事件（在第 17 章中讨论） |

|  | 命名空间（在本章下一节中讨论） |

随着你在不同上下文中输入代码，你还会看到其他 IntelliSense 图标出现。

你经常会看到包含两个正斜杠（`//`）后跟普通文本的代码行。这些是注释，编译器会忽略它们，但对开发人员非常有用，因为它们有助于记录程序实际在做什么。例如，看看下面的例子：

Click here to view code image

```
Console.ReadLine(); // Wait for the user to press the Enter key
```

编译器会跳过从两个斜杠到行尾的所有文本。你也可以添加以正斜杠后跟星号（`/*`）开头的多行注释。编译器会跳过所有内容，直到找到星号后跟正斜杠序列（`*/`），这可能在更下面的多行之后。你被积极鼓励用尽可能多的有意义的注释来记录你的代码。

### 构建并运行控制台应用程序

- 1. 在 `Build` 菜单上，单击 `Build Solution`。

此操作会编译 C# 代码，从而生成可运行的程序。

`Output` 窗口会出现在 Code and Text Editor 窗口下方。

### Tip

如果 `Output` 窗口未出现，请单击 `View` 菜单上的 `Output` 以显示它。

在 `Output` 窗口中，你应该会看到类似以下的消息，指示程序正在被编译：

Click here to view code image

```
1>------ Build started: Project: TestHello, Configuration: Debug Any CPU ------
1>  TestHello -> C:\Users\John\Documents\Microsoft Press\Visual CSharp Step By Step\
Chapter
1\TestHello\TestHello\bin\Debug\TestHello.exe
========= Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped =========
```

如果出现任何错误，它们将在 `Error List` 窗口中报告。下面的图像显示了如果你忘记在 `WriteLine` 语句中文本 `Hello World` 后输入闭合引号会发生什么。请注意，单个错误有时会导致多个编译错误。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_42_0.png)

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace TestHello
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

| Code | Description | Project | File | Line |

|------|-------------|---------|------|------|

| CS1010 | Newline in constant | TestHello | Program.cs | 13 |

| CS1026 | ) expected | TestHello | Program.cs | 13 |

| CS1002 | ; expected | TestHello | Program.cs | 13 |

### Tip

要直接转到导致错误的行，你可以双击 `Error List` 窗口中的一项。你还应注意到，当你输入代码时，Visual Studio 会在任何无法编译的代码行下方显示波浪形红色下划线。

如果你仔细遵循了之前的说明，不应有任何错误或警告，并且程序应成功构建。

### Tip

在构建之前无需显式保存文件，因为 `Build Solution` 命令会自动保存它。

文件名称标签页上方 Code and Text Editor 窗口上方的星号表示文件自上次保存以来已被更改。

- 2. 在 `Debug` 菜单上，单击 `Start Without Debugging`。

命令窗口打开，程序运行。消息“Hello World!”出现。程序现在等待你按任意键，如以下图形所示：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_43_0.png)

### Note

提示“Press any key to continue”是 Visual Studio 生成的；你没有编写任何代码来执行此操作。如果你使用 `Debug` 菜单上的 `Start Debugging` 命令运行程序，应用程序会运行，但命令窗口会立即关闭，而不会等待你按任意键。

- 3. 确保显示程序输出的命令窗口具有焦点（即它是当前活动的窗口），然后按 Enter。

命令窗口关闭，你返回到 Visual Studio 2015 编程环境。

- 4. 在 `Solution Explorer` 中，单击 `TestHello` 项目（而不是解决方案），然后在 `Solution Explorer` 工具栏上单击 `Show All Files` 按钮。请注意，你可能需要单击 `Solution Explorer` 工具栏右侧边缘的双箭头按钮以使此按钮出现。

### Solution Explorer

Double-arrow button

Show all files button

Search Solution Explorer (Ctrl+;)

Solution 'TestHello' (1 project)

TestHello

Properties

References

App.config
