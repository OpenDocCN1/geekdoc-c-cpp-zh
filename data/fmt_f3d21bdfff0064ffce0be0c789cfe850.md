
- 1. 对于应用程序类型（Application type）组：
    - 忽略默认选项“多文档”（Multiple documents）中的“标签页文档”（Tab documents）。
    - 保留文档/视图（Document/View）架构支持。
    - 选择 MFC 标准（MFC standard）作为项目样式，Windows 原生/默认（Windows Native/Default）作为视觉样式和颜色选项。
    - 保留 Unicode 库选项。

- 2. 复合文档支持（Compound Document Support）应为默认选择“无”（None）。

- 3. 对于对话框中的文档模板属性（Document Template Properties）设置选项：
    - 指定文件扩展名为 *ske*。你会发现它自动定义了针对 *.ske* 文件的过滤器。
    - 将文档类型（Doc type）名称更改为 Sketch。
    - 将文件新建简称更改为 Sketch。

- 4. 将数据库支持（Database Support）选项保持默认设置“无”（None）。

- 5. 对于用户界面特性（User Interface features）：
    - 保留经典菜单以及子选项“使用经典停靠工具栏”（Use a classic docking toolbar）。
    - 保留默认选择的其他选项：粗框（Thick frame）、最小化框（Minimize box）、最大化（Maximize）、系统菜单（System menu）、初始状态（Initial status）、子框（Child box）和子最大化框（Child maximize box）。

- 6. 对于高级特性选项（advanced features）：
    - 保留打印和预览选项。
    - 取消选择 ActiveX 控制、控件列表（Control List）和支持重启管理器（Support Restart Manager）。

- 7. 将生成的类（Generated Classes）保持默认设置，因为 `CSetcherView` 类的基类是 `CView`。

你可以看到生成的类，它为你使用 TextEditor 示例创建的应用程序提供了一个额外类 `CChildFrame`，该类派生自 `CMDIWnd`。该类为文档提供了一个框架窗口，显示在 `CMainFrame` 对象创建的应用程序窗口内部。在 SDI 应用程序中，只有一个文档和一个视图，视图显示在主框架的客户区域。在 SDI 应用程序中，你可以有多个文档，每个文档可以有多个视图。为了实现这一点，每个文档视图都有一个由 `CChildFrame` 对象创建的自己的子窗口。正如你之前看到的，视图显示在一个窗口中，但一个恰恰填满框架窗口的客户区域。最后，点击“完成”（Finish）生成项目。

## 运行程序

你可以按 `Ctrl+F5` 编译并运行程序。你会得到图 12-12 所示的应用程序窗口。

除了主应用程序窗口，你还有一个标题为 Sketch1 的独立文档窗口。Sketch1 是初始文档的默认名称，如果你保存它，它的扩展名为 `.ske`。你可以通过选择“窗口->新建窗口”（Window->New Window）菜单选项为文档创建额外的视图。

![](img/382e3fc55bbc8265676aa869d85a0e73_697_0.png)

（注：原文此处存在大量重复的句子，翻译已根据句意整合处理）

## 总结

在本章中，你主要关注了使用应用程序向导（Application Wizard）的机制。你已经看到了应用程序向导为 SDI 和 MDI 生成的基本组件。你现在可能对细节还不完全熟悉。（注：原文此处也存在大量重复的句子）

## 练习

本章无法提供编程示例，因为本部分刚刚介绍了创建应用程序的基本机制。你将在屏幕上亲自看到答案，或者可以通过文本核对你的答案。

- 1. 文档和视图之间是什么关系？
- 2. MFC 程序中文档模板的作用是什么？
- 3. 为什么在使用应用程序向导时需要小心并提前规划程序结构？
- 4. 编写文本编辑器程序的代码。编译 debug 和 release 版本，并检查每情况下产生的文件类型和大小。
- 5. 多次生成文本编辑器应用程序，尝试应用程序类型中的不同项目样式。

## 本章学到了什么

| 主题 | 概念 |
| --- | --- |
| 应用程序向导 | MFC 应用程序向导为你生成一个完整的、可运行的框架 Windows 应用程序，供你根据需求进行自定义。 |
| SDI 和 MDI 程序 | 应用程序向导可以生成单文档接口（SDI）应用程序（处理单个文档和单个视图），或多文档接口（MDI）程序（可以同时处理具有多个视图的多个文档）。 |
| SDI 程序中的类 | SDI 应用程序中派自基类的四个类是应用程序类、框架窗口类、文档类和视图类。 |
| 应用程序对象 | 程序只能有一个应用程序对象。该对象由应用程序向导在全局作用域自动定义。 |
| 文档对象 | 文档类对象存储应用程序数据，视图类对象显示文档对象的内容。 |
| 文档模板 | 文档模板类对象用于将文档、视图和窗口结合在一起。对于 SDI 应用程序使用 `CSingleDocTemplate` 类，对于 MDI 应用程序使用 `CMultiDocTemplate` 类。它们都是基类，通常不需要派生应用程序特定的类。 |

# 13

# 菜单与工具栏操作

你将在本章中学到：

- 基于 MFC 的程序如何处理消息
- 如何创建和修改菜单资源
- 如何创建和修改菜单属性
- 如何创建处理菜单消息的函数
- 如何添加更新菜单属性的处理器
- 如何添加与菜单项关联的工具栏按钮

本章的 WROX.COM 下载

你可以在 `www.wrox.com/remitle.cgi?isbn=978118368084` 的 Download 选项卡找到本章的 wrox.com 代码下载。代码位于第 13 章下载中，并根据章节中的名称进行单独命名。

# 与 Windows 通信

Windows 通过向你的程序发送消息来与其通信。消息处理的繁琐工作由 MFC 应用程序处理，因此你不需要担心提供 `WndProc()` 函数。MFC 允许你提供函数来处理你感兴趣的单个消息，并忽略其他消息。这些函数被称为*消息处理器*（message handlers）或简单的*处理器*（handlers）。在基于 MFC 的程序中，消息处理器总是你应用程序中某个类的类的成员。

特定消息与程序中处理它的函数之间的关联是通过消息映射（message map）建立的，程序中处理 Windows 消息的每个类都将有一个消息映射。消息映射是一个处理 Windows 消息的成员函数表，由一对宏界定。消息映射的开始由 `BEGIN_MESSAGE_MAP()` 宏指示，结束由 `END_MESSAGE_MAP()` 宏标记。消息映射中的每个条目将一个成员函数与特定消息关联：当发生给消息时，就会调用相应的函数。只有与该类相关的消息才会出现在它的消息映射中。

类的消息映射是在创建项目时由 MFC 向导创建，或者在添加处理消息的类时由类向导（Class Wizard）创建。消息映射的添加和删除主要由类向导管理，但在某些你需要手动修改消息映射。让我们通过 Sketcher 观察消息映射是如何运行的。

# 理解消息映射

MFC 应用程序向导为程序中的每个类建立了消息映射。`CSketcherApp`、`CSketcherDoc`、`CSketcherView`、`CMainFrame` 和 `CChildFrame` 都有自己的消息映射。类的消息映射出现在 `.cpp` 文件中。当然，消息映射中的函数也在类中声明，但它们在消息映射中被智能地标识出来。查看 `Sketcher.h` 中 `CSketcherApp` 的定义。

```cpp
class CSketcherApp : public CWnd
{
public:
    CSketcherApp();
    // Overrides
public:
    virtual BOOL OnInitInstance();
    virtual int ExitInstance();
    // Implementation
    afx_msg void OnAppAbout();
    DECLARE_MESSAGE_MAP()
};
```

`OnAppAbout()` 是类中声明的唯一消息处理器。`OnAppAbout()` 函数将其标识为消息处理器。`afx_msg` 没有其他用途，并会被预处理器转换为空格，因此它对编译编译后的程序没有影响。

`DECLARE_MESSAGE_MAP()` 宏表示该类可以包含作为消息处理器的成员，并且在 `.cpp` 文件中永久拥有消息映射。任何以 `CCmdTarget` 为直接或间接基类的类都拥有消息处理器，因此此类类始终将包含此宏作为类定义的一部分，无论是通过 MFC 应用程序向导还是通过你用于添加新类的添加类向导。

`CSketcherApp` 类以 `CCmdTarget` 为间接基类，因此允许 `DECLARE_MESSAGE_MAP()` 宏。Sketcher 中的所有其他应用程序类最终派生自 `CMTarget`，因此它们都可以处理 Windows 消息。

当你向类添加自己的成员时，最好将 `DECLARE_MESSAGE_MAP()` 宏留作类定义中的最后一行。如果你在 `DECLARE_MESSAGE_MAP()` 之后添加成员，你需要为它们包含访问说明符：`public`、`protected` 或 `private`。

# 消息处理器

包含 `DECLARE_MESSAGE_MAP()` 宏的定义在其 `.cpp` 文件中具有 `BEGIN_MESSAGE_MAP()` 和 `END_MESSAGE_MAP()` 宏。如果你查看 `Sketcher.cpp`，你会看到以下代码作为 `CSketchApp` 实现的一部分：

```cpp
BEGIN_MESSAGE_MAP(CSketchApp, CWnd)
ON_COMMAND(ID_APP_ABOUT, &CSketchApp::OnAbout)
// 标准文件文档命令
ON_COMMAND(ID_FILE_NEW, &CWnd::OnFileNew)
ON_COMMAND(ID_FILE_OPEN, &CWnd::OnFileOpen)
// 标准打印设置命令
ON_COMMAND(ID_FILE_PRINT_SETUP, &CWnd::OnPrintErrorSetup)
END_MESSAGE_MAP()
```
