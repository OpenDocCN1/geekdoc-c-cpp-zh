

## 第一章 使用 C# 编写第一个程序

## 你来做做

### 从命令行编译并运行程序

- 1. 转到你系统上的命令提示符。例如，在 Windows 10 中，在“搜索我所需要的”搜索框中开始输入 Developer Command Prompt（开发者命令提示符），然后点击该选项。
- 2. 将当前目录更改为存放程序的文件夹名称。你可以输入 `cd` 然后按回车键返回根目录。然后可以将路径更改为程序所在的路径。如果你将程序文件存储在名为 `CSharp` 的文件夹下的 `Chapter01` 文件夹中，则可以输入：
`cd CSharp\Chapter01`

`cd` 命令是 change directory（更改目录）的缩写。

- 3. 输入编译程序的命令：

``````
csc Hello.cs
```

如果你没有收到任何错误信息且提示符返回，则说明编译操作成功，已创建了一个名为 Hello.exe 的文件，你可以运行该程序了。如果你收到错误信息，请检查你输入的程序的每个字符，确保它们与上一个“你来做做”部分的图 1-9 一致。C# 是区分大小写的，因此大小必须完全匹配。当你纠正错误后，重复此步骤以编译程序。

- 4. 你可以通过以下方式验证是否创建了名为 Hello.exe 的文件：
  - 在命令提示符中，输入 `dir` 查看当前文件夹存储的文件目录。Hello.cs 和 Hello.exe 都应该出现在列表中。
  - 使用 Windows 资源管理器查看存储程序的文件夹内容，验证是否列出了两个 Hello 文件。

- 5. 在命令提示符中，输入 Hello（程序的名称，即可执行文件的名称），然后按回车键。或者，你也可以输入完整文件名 Hello.exe，输入 .exe 扩展名并不是必要的。输出应该像图 1-15 所示。

```
C:\CSharp\Chapter01>Hello
Hello, world!
C:\CSharp\Chapter01>
```

**图 1-15** Hello 程序的输出

## 使用 Visual Studio IDE 编译并运行程序

接下来，你使用 C# 编译器环境来编译并运行之前从命令行运行的同一个 Hello 程序。

- 1. 打开 **Visual Studio**。如果桌面上有快捷图标，你可以双击它。或者，在 Windows 10 中，你可以在 Cortana“搜索我所需要的”搜索框中开始输入 **Visual Studio**，然后选择。当你看到启动页时，点击主菜单上的 **File**（文件），然后点击 **Project**（项目）。
- 2. 在“新建项目”窗口中，点击 **Visual C#**，然后点击 **Console App**（控制台应用程序）。默认情况下项目名称设置为 **ConsoleApp1**。（如果你保留名称 ConsoleApp1，则下一个项目默认将是 **ConsoleApp2**）。

将项目名称更改为 **Hello**，并选择你想保存项目的路径（见图 1-16）。点击 **OK**。Visual C# 会在项目标题后创建一个与项目同同的新文件夹。

> 学生可能喜欢多次练习这些“你来做做”练习以巩。注意，Visual Studio 不允许你创建一个与已存储在文件夹中的项目同名的。当你额外执行这些步骤时，请在开始下一步之前删除第一个版本的项目、将新版本存储在不同的文件夹中，或给新项目一个不同的名称。

## 第一章 使用 C# 编写第一个程序

（续）

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_60_0.png)

图 1-16 启动新项目

- 3. Hello 程序的编辑窗口出现。此窗口中已经为你写好了代码，包括一些 using 语句、一个名为 Hello 的命名空间、一个名为 Program 的类以及一个 Main() 方法。要创建 Hello 程序，你需要添加语句。将光标放在最后一条语句后，按 **Enter** 开始新行，并添加额外的 using 语句：

```
```

在 Main() 方法的大括号之后，按 **Enter** 开始新行，并添加以下语句：

```
WriteLine("Hello, world!");
```

图 1-17 显示了添加 using 和 WriteLine 语句后的编辑窗口。

## 编译并运行 C# 程序

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using static System.Console;
namespace Hello
{
    class Program
    {
        static void Main(string[] args)
        {
            WriteLine("Hello, world!");
        }
    }
}
```

图 1-17 添加代码后的 Hello 应用程序编辑窗口

- 1. 通过点击菜单栏上的 File 并点击 Save All（全部保存）、或通过点击工具栏上的 Save All 按钮（显示两个磁盘）、或通过输入 Ctrl + S 来保存项目。
- 2. 编译项目，点击菜单栏上的 **Build**（生成），然后点击 **Build Solution**（生成解决方案）。你不应该收到错误信息，左下角会出现 Build succeeded 字。
- 3. 如果你喜欢从命令行编译程序，请用文本编辑器打开 Hello.cs 文件。如果你喜欢在 Visual Studio 中编译程序，请打开 Visual Studio，点击 File，指向 Open（打开）、Project/Solution（项目/解决方案），浏览正确的文件夹，双击 Hello 文件夹，双击 Hello 文件。
- 4. 将光标置于文件顶部，按 Enter 插入新行，按向上方向键回到该行，然后在文件顶部输入以下注释。每行输入后按 Enter。输入你的名字和今天的日期。
- 5. 保存文件，用这个新的注释版本替换旧的 Hello.cs 文件。
- 6. 如果你喜欢从命令行编译程序，在命令行输入 csc Hello.cs。当程序编译成功后，使用命令 Hello 执行它。如果你喜欢在 Visual Studio 中编译和运行程序，点击 Debug（调试），然后点击 Start Without Debugging（不调试启动）。

