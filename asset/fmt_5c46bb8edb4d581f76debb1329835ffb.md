
# CTextEditorDoc 类定义

```cpp
CTextEditorDoc();

DECLARE_DYNCCREATE(CTextEditorDoc);
```

## 属性

```cpp
public:
```

## 操作

```cpp
public:
```

## 重写

```cpp
public:
    virtual BOOL OnNewDocument();
    virtual void Serialize(CArchive& ar);

#if SHARED_HANDLERS
    virtual void InitializeSearchContent();
    virtual void OnDraw(CDC& dc, LPRECT lBounds);
#endif // SHARED_HANDLERS
```

## 实现

```cpp
public:
    virtual ~CTextEditorDoc();

#ifdef _DEBUG
    virtual void AssertValid() const;
    virtual void Dump(CDump& dc) const;
#endif
```

```cpp
protected:
    // 消息映射函数
    DECLARE_MESSAGE_MAP()
```

```cpp
#ifdef SHARED_HANDLERS
    // 用于为搜索处理器设置搜索内容的辅助函数
    void SetSearchContent(const CString& value);
#endif // SHARED_HANDLERS
```

```cpp
#ifdef SHARED_HANDLERS
private:
    CString m_strSearchContent;
    CString m_strThumbnailContent;
#endif // SHARED_HANDLERS
```

大部分核心内容来自基类，因此在这里并不直观。在构造函数之后出现的 `DECLARE_DYNCCREATE` 宏（在 `CMainFrame` 中也使用了它）允许通过从文件中合成来动态创建该类的对象。当你保存一个 SDI 文档对象时，包含视图的框架会与你的数据一起保存。所有这些内容在读取时都会被恢复。向文件读取和写入文档是通过名为“序列化”（serialization）的过程支持的。你将在后续示例中看到如何序列化你自己的文档并读取它们。

文档类还包含了 `DECLARE_MESSAGE_MAP()` 宏，以便让类成员函数处理 Windows 消息。

# 视图类

我们在 SDI 应用程序中的视图类定义如下：

```cpp
// TextEditorView.h : CTextEditorView 的接口
//
#pragma once

class CTextEditorView : public CEditView
{
protected: // 仅从序列化创建
    CTextEditorView();
    DECLARE_DYNCREATE(CTextEditorView)

    // 属性
public:
    CTextEditorDoc* GetDocument() const;

    // 操作
public:
    // 重写
public:
    virtual BOOL PreCreateWindow(CREATESTRUCT& cs);

protected:
    virtual BOOL OnPreparePrinting(CPrintInfo* pInfo);
    virtual void OnBeginPrinting(CDC* pDC, CPrintInfo* pInfo);
    virtual void OnEndPrinting(CDC* pDC, CPrintInfo* pInfo);

    // 实现
public:
    virtual ~CTextEditorView();

#ifdef _DEBUG
    virtual void AssertValid() const;
    virtual void Dump(CDumpContext& dc) const;
#endif

protected:
    // 消息映射函数
    DECLARE_MESSAGE_MAP()
};

#ifdef _DEBUG // TextEditorView.cpp 中的调试版本
inline CTextEditorDoc* CTextEditorView::GetDocument() const
{
    return reinterpret_cast<CTextEditorDoc*>(m_pDocument);
}
#endif
```

正如你在应用程序向导对话框中指定的那样，视图类派自 `CEditView`，它已经包含了基础文本处理功能。`GetDocument()` 函数返回一个指向与视图对应的文档对象的指针，当你向视图类添加扩展以允许用户交互并添加或修改文档数据时，你可以使用它来访问文档对象中的数据。

在应用程序向导生成的代码中，`CEditView` 类的 `GetDocument()` 成员有两种实现。`CEditView` 的 `.cpp` 文件中的一个用于程序的调试版本。你通常会在程序开发期间使用它，因为它对存储的文档的指针值进行了验证（该值存储在视图类中继承的成员 `m_pDocument` 中）。另一个版本位于 TextEditor.h 文件中类定义之后，适用于程序的发布版本。该版本被声明为 `inline` 且不对指针进行验证。`GetDocument()` 函数为视图对象提供了访问文档对象的权限。你可以使用该函数返回的文档指针调用该类接口中的任何函数。

默认情况下，你的程序中包含了调试功能。除了 `GetDocument()` 的特殊版本外，MFC 代码中还包含了许多此类检查。如果你想更改这一点，可以使用工具栏上的下拉列表框选择发布配置（release configuration），该配置不包含调试代码。

# 创建可执行模块

要编译并链接程序，你可以点击“生成解决方案”（Build Solution）、或按 `F7`，或点击工具栏上的生成图标。

第一次编译并链接程序将需要一些时间。由于 C++ 预编译头文件的特性，第二次及后续操作会快一些。在初始编译期间，编译器会将头文件的编译到一个扩展名为 `.pch` 的单个文件中。如果头文件中的源码没有更改，编译器将跳过头文件的编译并使用预编译的内容，从而节省头文件的时间。

你可以通过属性对话框确定是否使用了预编译头文件并控制它们的处理方式。在类视图中右键点击 `CEEditor` 并从菜单中选择“属性”。如果你在对话框中展开 C/C++ 节点，可以选择“预编译头”。

# 运行程序

要执行程序，按 `Ctrl+F5`。由于你使用了 `CEditView` 作为基类，该应用程序具有完全的功能。

# 程序的工作原理

应用程序对象在全局作用范围内创建。你可以通过展开类视图中的“全局函数和变量”项，然后双击条目看到这一点。

```cpp
CTextEditorApp theApp;
```

这声明了 `theApp` 是我们应用程序类 `CTextEditorApp` 的实例。该语句位于 `CEEditor.cpp` 中，该文件还包含应用程序的成员声明。

`theApp` 启动后会调用 MFC 提供的 `WinMain()` 函数。这调用了 `theApp` 的两个成员函数。首先调用 `InitInstance()`，用于应用程序的任何初始化；然后调用继承自 `CWinApp` 的 `Run()` 函数，该函数为 Windows 消息提供初始处理。如果你想查看 `CWinApp` 函数的代码，可以在“基类型”中扩展 `CEEditorApp` 树。然后你可以点击 `CWinApp` 在下格中查看成员。

# InitInstance() 函数

你可以通过在类视图中高亮 `CEEditorApp` 类后双击条目来访问 `InitInstance()` 的代码——如果你赶时间，可以直接查看定义 `theApp` 对象行之后的代码。MFC 应用程序向导创建的版本有很多代码，我想指出此函数中的几个片段。第一个是：

传递给 `SetRegistryKey()` 的字符串定义了存储程序信息的注册表键。你可以将其更改为任何的内容。如果我将参数更改为 "Horton"，有关你的程序的信息将存储在注册表键下：

```cpp
SetRegistryKey(_T("Local App-Generated Applications"));
LoadStdProfileSettings(4);
```

```
HKEY_CURRENT_USER\Software\Horton\TextEditor\
```

所有的应用程序设置都存储在此键下，`LoadStdProfileSettings()` 的调用加载了上次保存的应用程序设置。当然，第一次运行程序时，还没有这些设置。

文档模板在 `InitInstance()` 内部通过以下语句动态创建：

```cpp
pDocTemplate = new CSingleDocTemplate(
    IDR_MAINFRAME,
    RUNTIME_CLASS(CTextEditorDoc),
    RUNTIME_CLASS(CMainFrame), // 主 SDI 框架窗口
    RUNTIME_CLASS(CTextEditorView)
);
```

`CSingleDocTemplate` 构造函数的第一个参数是一个符号 `IDR_MAINFRAME`，它定义了与该文档类型使用的菜单和工具栏。接下来的三个参数定义了在文档模板中绑定在一起的文档（document）、主框架（mainframe）和视图（View）对象。由于你在这里使用的是 SDI 应用程序，每个程序只有一个实例，通过一个文档模板进行管理。`RUNTIME_CLASS()` 是一个宏，允许在运行时定义类对象的类型。

关于设置应用程序实例，还有许多其他你不需要担心的相关工作。你可以根据应用程序 `InitInstance()` 函数的需求，添加任何你自定义的初始化代码。

# Run() 函数

`CEditorApp` 类继承了 `CWinApp` 的 `Run()` 函数。由于该函数被声明为虚函数（`virtual`），你可以用自己的 `Run()` 替换继承来的版本，但这通常没有必要。`Run()` 接收来自 Windows 的所有应用程序消息，并确保每条消息都传递给程序中指定的处理函数（如果该函数存在的话）。然后，只要应用程序运行，该函数就会持续执行。

你可以将应用程序的操作简化为四个步骤：

1. 创建应用程序对象 `theApp`。
2. 执行 `WinMain()`，该函数由 MFC 提供。
3. `WinMain()` 调用 `InitInstance()`，它创建文档模板、主框架窗口、文档和视图。
4. `WinMain()` 调用 `Run()`，它执行主消息循环以获取并分发 Windows 消息。

# 创建 MDI 应用程序

现在，让我们使用 MFC 向导创建一个 MDI 应用程序。按 `Ctrl+Shift+N` 并将项目命名为 Sketch —— 打算保留它。在随后的章节中，你将将其扩展为一个绘图程序。执行此过程时应该不会遇到问题，只有几处需要与创建 SDI 应用程序有所不同。

1. 对于应用程序类型（Application Type）选项：
    - 保留默认选项“多文档”（Multiple documents），但不要选“标签页文档”（Tabbed documents）。
    - 保留文档/视图架构支持（Document/View architecture support）。
    - 选择 MFC 作为项目样式，并将 Windows 原生/默认（Windows Native/Default）作为视觉样式和颜色选项。
    - 保留 Unicode 库选项。

2. 复合文档支持（Compound Document Support）应为默认选择“无”（None）。

3. 对于对话框中的文档模板属性（Document Template Properties）设置选项：
    - 指定文件扩展名为 `.ske`。你会发现自动定义了一个针对 `.ske` 文档的过滤器。
    - 将文档类型名称（Doc type name）更改为 Sketch。
    - 将新建短名称（File new short name）更改为 Sketch。

4. 将数据库支持（Database Support）选项保持默认设置“无”（None）。

5. 用户界面功能（User Interface features）选项：
    - 保留经典菜单（classic menu）以及子选项“使用经典停靠工具栏”（Use a classic docking toolbar）。
    - 保留默认选中的其他选项：粗框（Thick frame）、最小化框（Minimize box）、最大化框（Maximize box）、系统菜单（System menu）、初始状态（Initial status）、子最小化框（Child minimize box）和子最大化框（Child maximize box）。

6. 对于高级功能（Advanced features）选项：
    - 保留打印和预览（Printing and preview）选项。
    - 取消选择 ActiveX 控制（ActiveX controls）、常用控件清单（Common Control Manifest）和支持重启管理器（Support Restart Manager）。

7. 将生成的类（Generated Classes）保持默认设置，因为 `CSSketcherView` 的基类是 `CView`。

你可以在“生成的类”对话框中看到，与 `TextEditor` 相比，你的应用程序多了一个类，即 `CChildFrame` 类，它派自 `CMDIChildWnd`。该类为文档提供了一个框架视图，它显示在由 `CMainFrame` 对象创建的应用程序窗口内部。在 SDI 应用程序中，只有一个文档和一个视图，因此视图显示在框架的客户端区域。在 MDI 应用程序中，你可以打开多个文档，且每个文档都可以有多个视图。为了实现这一点，每个文档都拥有自己的框架视图。

# 运行程序

你可以通过 `F5` 运行程序，运行 Sketch。

# 总结

在本章中，我们主要关注使用向导的机制。你已经看到了向导生成的 SDI 和 MDI 应用程序的基本组件。你可能对细节还不熟悉，但不用担心，在后续章节开始开发应用程序后，你会变得清晰。

# 练习题

本章无法提供编程示例，因为它只是介绍了创建应用程序的机制。你将通过练习题检查自己的答案。

1. 文档和视图之间的关系是什么？
2. 在 MFC 程序中，文档模板的作用是什么？
3. 为什么在使用向导时需要小心并提前规划程序结构？
4. 编写编辑器代码。编译调试和发布版本，并观察生成的文件类型和大小。
5. 尝试不同的项目样式多次生成文本编辑器。
