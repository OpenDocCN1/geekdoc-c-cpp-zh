
这是 Windows 定义的一套广泛的方法，程序调用这些方法来访问 Windows 提供的各种功能。基于 API 的程序非常冗长且复杂。例如，即使是一个骨架式的基于 API 的程序也需要大约 50 行代码。执行任何有用功能的基于 API 的程序至少有数百行代码，而实际应用程序则有数千行代码。因此，在早期，Windows 程序编写和维护起来都很困难。

为了解决这个问题，创建了封装 API 功能的类库。其中最重要的是 Microsoft 基础类库 Microsoft Foundation Classes（MFC）。本书的许多读者都熟悉 MFC。MFC 用 C++ 编写，基于 MFC 的程序也用 C++ 编写。由于 MFC 带来了面向对象的优势，创建 Windows 程序的过程得以简化。然而，MFC 程序仍然相当复杂，涉及单独的头文件、代码文件和资源文件。此外，MFC 只是 API 周围的“薄包装”，因此许多基于 Windows 的活动仍然需要大量显式的程序语句。

C# 和 .NET Framework 的 Forms 库提供了一种完全面向对象的方式来处理 Windows 编程。Forms 库不仅仅提供 API 的包装，而是定义了一种精简、集成、逻辑一致的管理 Windows 应用程序开发的方式。这种集成水平得益于 C# 语言的独特特性，例如委托和事件。此外，由于 C# 使用垃圾回收，特别令人困扰的“内存泄漏”问题几乎已被消除。

如果你已经使用 API 或 MFC 为 Windows 编程过，你会发现 Windows Forms 方法令人耳目一新。Windows Forms 使创建 Windows 应用程序几乎与创建控制台应用程序一样容易。

## 编写基于窗体的 Windows 应用程序的两种方式

在开始之前，需要说明一个重要问题。Visual Studio 包含一套复杂的设计工具，可自动化创建 Windows 应用程序的大部分过程。使用这些工具，你可以直观地构建和定位应用程序使用的各种控件和菜单。Visual Studio 还会为每个功能“粗略”创建所需的类和方法。坦率地说，使用 Visual Studio 设计工具创建大多数实际的 Windows 应用程序是一个不错的选择。然而，并没有要求你使用这些工具。你也可以使用文本编辑器创建 Windows 程序然后编译它，就像你可以为基于控制台的应用程序所做的那样。

因为本书是关于 C#，而不是 Visual Studio，并且本章中的 Windows 程序都非常简短，所以所有程序都将以可使用文本编辑器输入的形式展示。然而，程序的总体结构、设计和组织与设计工具创建的程序相同。因此，本章的材料适用于任一方法。

## Windows 如何与用户交互

你必须学习的第一件事是 Windows 编程中用户与 Windows 的交互方式，因为这定义了所有 Windows 程序共享的架构。这种交互与本书其他部分所示的基于控制台的程序根本不同。当你编写控制台程序时，是你的程序发起与操作系统的交互。例如，是程序请求此类

// A form-based Windows Skeleton.
using System;
using System.Windows.Forms;

// WinSkel is derived from Form.
class WinSkel : Form {
    public WinSkel() {
        // Give the window a name.
        Text = "A Windows Skeleton";
    }
    // Main is used only to start the application.
    [STAThread]
    static void Main() {
        WinSkel skel = new WinSkel(); // create a form
        // Enable visual styles.
        Application.EnableVisualStyles();
        // Start the window running.
        Application.Run(skel);
    }
}

该程序创建的窗口如图 26-1 所示。让我们逐行检查这个程序。首先，注意同时包含了 System 和 System.Windows.Forms。System 是必需的，因为 Main() 前面有 STAThread 属性。System.Windows.Forms 支持 Windows Forms 子系统，如前所述。

接下来，创建了一个名为 WinSkel 的类。它继承 Form。因此，WinSkel 定义了一种特定的窗体类型。在本例中，它是一个最小的窗体。

WinSkel 构造函数内部有以下代码行：

Text = "A Windows Skeleton";

Text 是设置窗口标题的属性。因此，此赋值导致窗口标题栏包含 A Windows Skeleton。Text 定义如下：

public override string Text { get; set; }

图 26-1
骨架式基于窗体的窗口

![](img/7022d9b97326a713562c15aa43977d15_876_0.png)

Text 是从 **控件** 继承的。

接下来是 `Main()` 方法，其声明方式与本书其余部分中出现的 `Main()` 方法类似。它是程序执行开始的方法。注意，它前面有 `STAThread` 属性。作为一般规则，Windows 程序的 `Main()` 方法应具有此属性。它将程序的线程模型设置为单线程单元 STA。线程模型和单元的讨论超出了本章范围，但简而言之，Windows 应用程序可以使用两种不同的线程模型之一：单线程单元或多线程单元。

在 `Main()` 内部，创建了一个名为 `skel` 的 **WinSkel** 对象。然后调用静态方法 `Application.EnableVisualStyles()`。如果操作系统支持，此方法启用视觉样式主题。在 Windows Forms 应用程序中从技术上讲并非必需，但应使用它，因为它能启用更美观的控件。它应是 `Main()` 调用的第一个方法。**应用程序** 类在 **System.Windows.Forms** 中定义，它封装了所有 Windows 应用程序共有的方面。

接下来，`skel` 被传递给 `Run()` 方法，该方法也是由 **应用程序** 类定义的，如下所示：

Application.Run(skel);

这启动了窗口运行。骨架中使用的 `Run()` 方法如下所示：

public static void Run(Form form)

它接受一个窗体的引用作为参数。由于 **WinSkel** 继承 **窗体**，因此可以将 **WinSkel** 类型的对象传递给 `Run()`。

运行程序时，它会创建图 26-1 所示的窗口。窗口具有默认大小并且完全可用。可以调整大小、移动、最小化、最大化和关闭。因此，仅通过编写几行基于窗体的代码就实现了几乎所有窗口所需的基本功能。相比之下，用 C 语言编写并直接调用 Windows API 的相同程序大约需要五倍的代码行数！

前面的骨架定义了大多数基于窗体的 Windows 应用程序将采用的轮廓。一般来说，要创建窗体，你创建一个继承 **窗体** 的类。根据需要初始化窗体，创建派生类的对象，然后在该对象上调用 **Application.Run()**。

## 编译 Windows 骨架

你可以使用命令行编译器或 Visual Studio 编译 Windows 程序。对于本章中非常短的程序，命令行编译器是最简单的方法；但对于实际应用程序，你可能希望使用 IDE。另请注意，如本章开头所述，你可能希望使用 Visual Studio 提供的设计工具，但这里描述的方法并非如此。两种方式如下所示。

### 从命令行编译

假设你将骨架命名为 **WinSkel.cs**，那么从命令行编译骨架，请使用以下命令：

csc /t:winexe WinSkel.cs

`/t:winexe` 开关告诉编译器创建 Windows 应用程序而不是控制台程序。要运行程序，只需在命令行输入 **WinSkel** 即可。
