

## 第11章

应用程序类继承自基类中定义了相当多的成员变量，其中许多对应于 Windows API 函数中用作参数的变量。例如，成员 `m_pszAppName` 存储一个指向字符串的指针，该字符串定义了应用程序的名称。成员 `m_nCmdShow` 指定应用程序启动时应用程序窗口应如何显示。你现在不需要了解所有继承的成员变量。在开发特定于应用程序的代码时需要用到时，你会看到它们是如何使用的。

在从 `CWinApp` 派生你自己的应用程序类时，你必须重写虚函数 `InitInstance()`。你的版本会被 MFC 为你提供的 `WinMain()` 版本调用，并且你将在该函数中包含代码来创建并显示你的应用程序窗口。然而，在编写 `InitInstance()` 之前，我应该向你介绍 MFC 库中的一个类，该类定义了一个窗口。

### 窗口类

你的 MFC 应用程序需要一个窗口作为与用户的接口，称为框架窗口。你从 MFC 类 `CFrameWnd` 派生应用程序的窗口类，该类专门为此目的而设计。因为 `CFrameWnd` 类提供了为你的应用程序创建和管理窗口所需的一切，所以你只需在派生的窗口类中添加一个构造函数即可。这使你能够为窗口指定一个标题栏以适应应用程序上下文：

```cpp
class COurWnd: public CFrameWnd
{
public:
    // Constructor
    COurWnd()
    {
        Create(0, L"Our Dumb MFC Application");
    }
};
```

你在构造函数中调用的 `Create()` 函数是从基类继承而来的。它创建窗口并将其附加到正在创建的 `COurWnd` 对象上。请注意，`COurWnd` 对象并不是 Windows 显示的窗口本身——类对象和物理窗口是两个不同的实体。

`Create()` 函数的第一个参数值 0 指定你想要使用基类的默认属性来创建窗口——你会记得，在本章前面使用 Windows API 直接的示例中，你需要定义窗口属性。第二个参数指定用于窗口标题栏的窗口名称。你不会感到惊讶的是，`Create()` 函数还有其他参数，但它们都有默认值，相当令人满意，所以你在这里可以忽略它们。

### 完成程序

在为应用程序定义了窗口类之后，你可以在我们的 `COurApp` 类中编写 `InitInstance()` 函数：

```cpp
BOOL COurApp::InitInstance(void)
{
    // Construct a window object in the free store
    m_pMainWnd = new COurWnd;
    m_pMainWnd->ShowWindow(m_nCmdShow);      // ...and display it
    return TRUE;
}
```

这重写了基类 `CWinApp` 中定义的虚函数，正如我之前所说，它是由 MFC 库自动提供的 `WinMain()` 函数调用的。`InitInstance()` 函数使用 `new` 运算符在自由存储区中构造应用程序的主窗口对象。你将返回的地址存储在变量 `m_pMainWnd` 中，该变量是你的类 `COurApp` 的继承成员。其效果是窗口对象由应用程序对象拥有。你甚至不需要担心释放已创建对象的内存——提供的 `WinMain()` 函数会处理必要的清理工作。

对于一个完整 albeit 相当有限的程序，你唯一需要的其他项目是定义一个应用程序对象。在 `WinMain()` 执行之前，必须存在我们应用程序类 `COurApp` 的一个实例，因此你必须在全局作用域用语句声明它：

```cpp
COurApp AnApplication;       // Define an application object
```

该对象需要在全局作用域存在的原因是它就是应用程序，而应用程序需要在开始执行之前存在。MFC 提供的 `WinMain()` 函数调用应用程序对象的 `InitInstance()` 成员函数来构造窗口对象，因此隐式假设应用程序对象已经存在。

### 最终成品

现在你已经看到了所有代码，你可以将它添加到项目中的 `Ex11_02.cpp` 源文件中。在 Windows 程序中，类通常在 `.h` 文件中定义，而未在类定义中定义的成员函数则在 `.cpp` 文件中定义。你的应用程序非常简短，所以你不妨全部放在一个 `.cpp` 文件中。这样做的优点是你可以看到全部内容。程序代码结构如下：

```cpp
// Ex11_02.cpp
// An elementary MFC program
#include <afxwin.h>                         // For the class library

// Application class definition
class COurApp:public CWinApp
{
public:
    virtual BOOL InitInstance();
};

// Window class definition
class COurWnd:public CFrameWnd
{
public:
    // Constructor
    COurWnd()
    {
        Create(0, L"Our Dumb MFC Application");
    }
};
```

### 使用 Windows 窗体

Windows 窗体是一个代表某种窗口的实体。所说的窗口是指其最广义的含义，即屏幕上可以是按钮、对话框、常规窗口或任何其他可见 GUI 组件的区域。Windows 窗体由 `System::Windows::Forms::Form` 类的子类封装，但你最初不必过多担心这一点，因为创建窗体的所有代码都是自动生成的。为了看看它有多么简单，请使用 Windows 窗体创建一个基本窗口，该窗口具有标准菜单。

### 试试看：一个 Windows 窗体应用程序

在新建项目对话框中选择 CLR 项目类型，并选择 Windows 窗体应用程序作为项目的模板。新项目对话框窗口如图 11-7 所示。

![](img/2359b0c604600c58fba3539c738a356e_686_0.png)

图 11-7

将项目名称输入为 Ex11_03。当你单击确定按钮时，应用程序向导会生成 Windows 窗体应用程序的代码，并显示设计窗口，其中包含应用程序显示的窗体。这如图 11-8 所示。

![](img/2359b0c604600c58fba3539c738a356e_687_0.png)

图 11-8

你现在可以在设计窗格中以图形方式更改窗体，并且更改会自动反映在创建窗体的代码中。首先，你可以用鼠标光标拖动窗体的底部角落来增加窗体窗口的大小。你还可以更改标题栏中的文本——在窗体的客户区右键单击并从上下文菜单中选择属性。这会显示属性窗口，允许你更改窗体的属性。从设计窗格右侧的属性列表中选择 Text，然后在显示属性值的相邻列中输入新的标题栏文本——我输入的是 A Simple Form Window。当你按下 Enter 键时，新文本会出现在窗体的标题栏中。

只是为了看看向窗体窗口添加内容有多么容易，通过在窗口右侧选择选项卡显示工具箱窗格，如果它不存在，则按 Ctrl+Alt+X，或从视图菜单中选择工具箱。在列表中找到 MenuStrip 选项并将其拖到设计选项卡窗格中的窗体窗口上。右键单击窗体窗口下方出现的 `MenuStrip1` 并从弹出菜单中选择插入标准项。然后你将在窗体窗口中拥有一个填充了标准 File、Edit、Tools、Help 菜单的菜单，每个菜单都附带其下拉菜单项列表。此操作的結果如图 11-9 所示。

如果你通过按 Ctrl+Shift+B 构建项目，然后通过按 Ctrl+F5 执行它，你将看到带有其菜单的窗体窗口显示出来。自然地，菜单项什么也不做，因为你尚未添加任何代码来处理单击它们时产生的事件，但标题栏右侧的图标可以工作，因此你可以关闭应用程序。你将在本书后面进一步了解如何开发 Windows 窗体应用程序，包括处理事件。

![](img/2359b0c604600c58fba3539c738a356e_688_0.png)

图 11-9

### 总结

在本章中，你看到了使用 Visual C++ 2005 创建基本 Windows 应用程序的三种不同方法，你现在应该对这三种方法之间的本质差异有了感觉。在本书的剩余章节中，你将更深入地探讨如何使用 MFC 和使用 Windows 窗体开发应用程序。

