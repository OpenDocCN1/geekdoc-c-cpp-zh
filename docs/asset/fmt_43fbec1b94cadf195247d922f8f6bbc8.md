
`class CTextEditorApp : public CWinApp`

{

public:

    `CTextEditorApp()`;

// Overrides

public:

    virtual BOOL `InitInstance()`;

// Implementation

    afx_msg void `OnAppAbout()`; 

    `DECLARE_MESSAGE_MAP()`

};

extern `CTextEditorApp` `theApp`;

```
`CTextEditorApp` 继承自 `CWinApp`，包含一个构造函数、一个虚函数 `InitInstance()`、一个函数 `OnAppAbout()` 以及一个宏 `DECLARE_MESSAGE_MAP()`。
```

> 注意：宏不是 C++ 代码。它是由 `#define` 预处理器指令定义的名称，它将被替换为某些文本，这些文本通常是代码，但也可能是某种形式的常量或符号。

`DECLARE_MESSAGE_MAP()` 宏用于定义哪些 Windows 消息由该类中的哪些成员函数处理。该宏出现在任何可以处理 Windows 消息的类定义中。当然，我们的应用程序类从基类继承了许多函数和数据成员，当你扩展程序示例时，你将进一步研究这些内容。如果你正在查看类定义的代码定义，你会注意到 `#pragma once` 防止了文件被包含多次。紧随其后的是一组预处理器指令，确保 `stdafx.h` 文件在此文件之前包含。

# 框架窗口类

我们 SDI 程序的应用程序框架窗口由 `CMainFrame` 类的对象创建，该类由以下代码定义：

```cpp
// MainFrm.h : CMainFrame 类的接口
//
#pragma once
class CMainFrame : public CFrameWnd
{
protected: // 仅从序列化创建
    CMainFrame();
    DECLARE_DYNCREATE(CMainFrame)
// Attributes
public:
// Operations
public:
// Overrides
public:
    virtual BOOL PreCreateWindow(CREATESTRUCT& cs);
// Implementation
public:
    virtual ~CMainFrame();
#ifdef _DEBUG
    virtual void AssertValid() const;
    virtual void Dump(CDumpContext& dc) const;
#endif
protected: // 嵌入的控制条成员
    CToolBar m_wndToolbar;
    CStatusBar m_wndStatusBar;
// 生成的消息映射函数
protected:
    afx_msg int OnCreate(CREATESTRUCT* lpCreateStruct);
    DECLARE_MESSAGE_MAP()
};
```

该类派自 `CWnd`，它为我们的应用程序窗口提供了大部分所需功能。派生类包含两个保护数据成员——`m_wndToolbar` 和 `m_wndStatusBar`，它们分别是 MFC 类 `CToolBar` 和 `CStatusBar` 的实例。工具栏提供了访问标准菜单功能的按钮，状态栏显示在应用程序窗口的底部。

# 文档类

所创建的 `CTextEditorDoc` 类定义如下：

```cpp
// TextEditorDoc.h : CTextEditorDoc 类的接口
//
#pragma once
class CTextEditorDoc : public CDocument
{
protected: // 仅从序列化创建
    CTextEditorDoc();
    DECLARE_DYNCREATE(CTextEditorDoc);
// Attributes
public:
// Operations
public:
// Overrides
public:
    virtual BOOL OnNewDocument();
    virtual void Serialize(CArchive& ar);
#ifdef SHRED_HANDLERS
    virtual void InitializeSearchContent();
    virtual void OnDrawThumbnail(CDC& dc, LPRECT bounds);
#endif // SHRED_HANDLERS
// Implementation
public:
    virtual ~CTextEditorDoc();
#ifdef _DEBUG
    virtual void AssertValid() const;
    virtual void Dump(CDumpContext& dc) const;
#endif
#ifdef SHRED_HANDLERS
    // 设置搜索处理程序搜索内容的辅助函数
    void setSearchContent(const CString& value);
#endif // SHRED_HANDLERS
private:
    CString m_strSearchContent;
    CString m_strThumbnailContent;
#endif // SHRED_HANDLERS
};
```

大部分核心内容都来自基类，因此在这里并不直观。`DECLARE_DYNCREATE` 宏出现在构造函数之后（在 `CMainFrame` 中也使用了它），它允许通过从文件中合成数据来动态创建该类的对象。当你保存一个 SDI 文档时，框架窗口会显示所有内容在读回时都会一并保存。读取和写入文档到文件是通过名为“序列化”的过程实现的。我们将在开发的示例中展示如何序列化自己的文档并将其读回。

文档类还包含了 `DECLARE_MESSAGE_MAP()` 宏，以便让类成员函数处理 Windows 消息。

# 视图类

我们 SDI 应用程序中的视图类定义为：

```cpp
// TextEditorView.h : CTextEditorView 的接口
//
#pragma once
class CTextEditorView : public CEditView
{
protected: // 仅从序列化创建
    CTextEditorView();
    DECLARE_DYNCREATE(CTextEditorView)
    // Attributes
public:
    CTextEditorDoc* GetDocument() const;
    // Operations
public:
    // Overrides
public:
    virtual BOOL PreCreateWindow(CREATESTRUCT& cs);
    virtual BOOL PreparePrinting(CPrintInfo* pInfo);
    virtual void OnBeginPrinting(CDC* pDC, CPrintInfo* pInfo);
    virtual void OnEndPrinting(CDC* pDC, CPrintInfo* pInfo);
    // Implementation
public:
    virtual ~CTextEditorView();
#ifdef _DEBUG
    virtual void AssertValid() const;
    virtual void Dump(CDumpContext& dc) const;
#endif
protected:
    // 生成的消息映射函数
protected:
    DECLARE_MESSAGE_MAP()
};
#ifdef _DEBUG // TextEditorView.cpp 中的调试版本
inline CTextEditorDoc* CTextEditorView::GetDocument()
{ return reinterpret_cast<CTextEditorDoc*>(m_pDocument); }
#endif
```

如应用程序向导所示，视图类派自 `CEditView`，它包含了基本的文本处理能力。`GetDocument()` 函数返回指向文档对象的指针，当你为类添加扩展功能时，可以使用它来访问文档中的数据。

# 创建 MFC

## 创建可执行模块

要编译并链接程序，你可以点击 Build > Solution，按 F7，或者点击工具栏上的 Build 图标。

第一次编译和链接程序时需要一些时间。由于 C++ 预编译头文件的特性，第二次以后会快一些。在初始编译期间，编译器会将预编译头文件保存为扩展名为 `.pch` 的文件。在随后的构建中，如果头文件没有更改，编译器将跳过头文件的编译并使用预编译代码，从而节省时间。

你可以通过属性对话框确定是否使用预编译头文件以及如何处理它们。在 Class View 中右键点击 `CTextEditor` 并从菜单中选择 Properties。如果你展开对话框中的 C/C++ 节点，可以选择 Precompiled Headers 来设置或取消此属性。

# 运行程序

按 Ctrl+F5 执行程序。由于你选择了 `CEditView` 作为 `CTextEditor` 类的基类，该程序是一个简单的文本编辑器。你可以在窗口中输入文本，如图 12-11 所示。

注意，应用程序具有滚动条，用于查看窗口区域之外的文本，当然，你可以通过拖动边界来调整窗口大小。菜单下的所有项目都可以完全运行，你可以保存和检索文件，剪切和粘贴文本，并打印。

图 12-11

在窗口中输入文本——而且无需编写单行代码！当你将光标悬停在工具栏按钮或菜单选项上，状态栏中会出现描述其功能的提示；如果你将光标停留在工具栏按钮上，则会显示一个显示其用途的工具提示。（你将在第 13 章中详细学习工具提示）。

## 程序是如何运作的

应用程序对象在程序的全局作用域中创建。如果你在类视图（Class View）中展开“全局函数和变量”（Global Functions and Variables）项，然后双击 App，就可以看到这一点。在编辑器窗口中，你会看到这条语句：

```
CTextEditorApp app;
```

这声明 `app` 为我们应用程序类 `CTextEditorApp` 的实例。该语句位于 `TextEditor.cpp` 中，其中还包含了应用程序类的成员声明以及 `CABDlg` 类的定义。

在 `app` 创建后，会调用 MFC 提供的 `WinMain()` 函数。这会调用 `app` 对象的两个成员函数。首先，它调用 `InitInstance()`，为应用程序提供任何必要的初始化；然后调用从 `CWinApp` 继承的 `Run()` 函数，为 Windows 消息提供初始处理。如果你想查看 `CWinApp` 函数，可以在类视图中扩展 `CTextEditorApp` 树并扩展“基类型”（Base Types）。然后你可以点击 `CWinApp` 来查看下方窗格中的成员。`WinMain()` 没有显式地出现在项目源代码中，因为它是由 MFC 库提供的，并在应用程序启动时自动被调用。

### InitInstance() 函数

你可以通过在类视图中高亮 `CTextEditorApp` 类后双击其项来访问 `InitInstance` 的代码——或者，如果你赶时间，直接查看定义 `app` 对象的行之后的代码即可。MFC 应用程序向导创建的版本有很多代码，因此我想说明该函数中的几个函数。第一个是：

```
SetRegistryKey(T("Local App\GeneratedApplications")); // 加载标准 INI 文件选项（包括 MRU）
LoadProfileSettings(4);
```

传递给 `SetRegistryKey()` 的字符串定义了存储程序信息的注册表键。你可以将其更改为任何想要的内容。如果我将参数改为 "Horton"，那么关于我们程序的信息将存储在注册表键下：

```
HKEY_CURRENT_USER\Software\Horton\TextEditor\
```

所有的应用程序设置都存储在此键下，包括最近使用的文件。对 `LoadProfileSettings()` 调用加载了上次保存的设置。当然，当你第一次运行程序时，还没有设置。

在 `InitInstance()` 期间，通过以下语句动态创建一个文档模板：

```
pDocTemplate = new CSingleDocTemplate(
ID_MAINFRAM,
```
