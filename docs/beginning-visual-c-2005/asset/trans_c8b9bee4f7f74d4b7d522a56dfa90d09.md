

图 18-4

图 18-5

## 第 18 章

既然 MFC DLL 向导已经完成了它的工作，你可以查看为你生成的代码。如果在“解决方案资源管理器”窗格中查看项目内容，你会看到 MFC DLL 向导已经生成了几个文件，其中包含一个 .txt 文件，里面描述了其他文件的用途。你可以在 .txt 文件中阅读它们的用途，但在实现我们的 DLL 时，下面两个文件是目前最值得关注的：

| 文件名 | 内容 |
| --- | --- |
| ExtDLLExample.cpp | 该文件包含函数 DllMain()，是 DLL 的主要源文件。 |
| ExtDLLExample.def | 该文件中的信息在编译期间使用。它包含 DLL 的名称，你也可以在其中添加 DLL 中可供使用该 DLL 的程序访问的项的定义。在本例中，你将使用另一种更简单的方式来标识这些项。 |

当你的 DLL 被加载时，首先发生的事情是执行 DllMain()，因此或许你应该先看一下它。

### 理解 DllMain()

如果你查看 ExtDLLExample.cpp 的内容，你会看到 MFC DLL 向导已经为你生成了一个版本的 DllMain()，如下所示：

```
extern "C" int APIENTRY
DllMain(HINSTANCE hInstance, DWORD dwReason, LPVOID lpReserved)
{
    // Remove this if you use lpReserved
    UNREFERENCED_PARAMETER(lpReserved);

    if (dwReason == DLL_PROCESS_ATTACH)
    {
        TRACE0("EXTDLLEXAMPLE.DLL Initializing!\n");

        // Extension DLL one-time initialization
        if (!AfxInitExtensionModule(ExtDLLExampleDLL, hInstance))
            return 0;

        // Insert this DLL into the resource chain
        // NOTE: If this Extension DLL is being implicitly linked to by
        // an MFC Regular DLL (such as an ActiveX Control)
        // instead of an MFC application, then you will want to
        // remove this line from DllMain and put it in a separate
        // function exported from this Extension DLL. The Regular DLL
        // that uses this Extension DLL should then explicitly call that
        // function to initialize this Extension DLL. Otherwise,
        // the CDynLinkLibrary object will not be attached to the
        // Regular DLL's resource chain, and serious problems will
        // result.

        new CDynLinkLibrary(ExtDLLExampleDLL);
    }
    else if (dwReason == DLL_PROCESS_DETACH)
    {
        TRACE0("EXTDLLEXAMPLE.DLL Terminating!\n");
        // Terminate the library before destructors are called
        AfxTermExtensionModule(ExtDLLExampleDLL);
    }
    return 1;    // ok
}
```

调用 `DllMain()` 时会向它传递三个参数。第一个参数 `hInstance` 是一个由 Windows 创建的句柄，用于标识 DLL。Windows 下的每个任务都有一个唯一标识它的实例句柄。第二个参数 `dwReason` 指示调用 `DllMain()` 的原因。你可以看到该参数在 `DllMain()` 的 `if` 语句中被测试。第一个 `if` 测试 `DLL_PROCESS_ATTACH` 值，它表示某个程序即将使用该 DLL；第二个 `if` 测试 `DLL_PROCESS_DETACH` 值，它表示某个程序已经使用完该 DLL。第三个参数是一个保留给 Windows 使用的指针，因此你可以忽略它。

当程序第一次使用 DLL 时，它会被加载到内存中，并以 `dwReason` 参数设置为 `DLL_PROCESS_ATTACH` 来执行 `DllMain()` 函数。这会导致调用 Windows API 函数 `AfxInitExtensionModule()` 来初始化 DLL，并在堆上创建类 `CDynLinkLibrary` 的一个对象。Windows 使用此类的对象来管理扩展 DLL。如果你需要添加自己的初始化代码，可以将其添加到此块的末尾。你需要的任何 DLL 清理代码都可以添加到第二个 `if` 语句的块中。

### 向扩展 DLL 添加类

你将使用该 DLL 来包含 Sketcher 形状类的实现，因此请将文件 `Elements.h` 和 `Elements.cpp` 从包含 Sketcher 源代码的文件夹移动到包含 DLL 的文件夹。务必确保你是在移动而不是复制这些文件。因为 DLL 将为 Sketcher 提供形状类，所以你不想将它们留在 Sketcher 的源代码中。

你还需要从 Sketcher 项目中移除 `Elements.cpp`。为此，请打开 Sketcher 项目，在“解决方案资源管理器”窗格中单击 `Elements.cpp` 文件以将其突出显示，然后按 Delete 键。如果不这样做，当你尝试编译项目时，编译器会抱怨找不到该文件。按照同样的过程，从解决方案资源管理器窗格的“头文件”文件夹中移除 `Elements.h`。

形状类使用你在文件 `OurConstants.h` 中定义的常量，因此请将此文件从 Sketcher 项目文件夹复制到包含 DLL 的文件夹。注意，变量 `VERSION_NUMBER` 仅由形状类中的 `IMPLEMENT_SERIAL()` 宏使用，因此你可以将其从 Sketcher 程序中使用的 `OurConstants.h` 文件中删除。

现在你需要将包含形状类实现的 `Elements.cpp` 添加到扩展 DLL 项目中，因此请打开 ExtDLLExample 项目，选择菜单选项“项目 > 添加现有项”，然后在对话框的列表框中选择文件 `Elements.cpp`，如图 18-6 所示。

![](img/2359b0c604600c58fba3539c738a356e_953_0.png)

图 18-6

### 从扩展 DLL 导出类

项目还应该包含形状类的定义和你的常量的文件，因此请对 Elements.h 和 OurConstants.h 重复该过程，将这些文件添加到项目中。你可以通过在“添加现有项”对话框中选择文件时按住 Ctrl 键，在一步中添加多个文件。最终，你应该会在“解决方案资源管理器”窗格中看到所有文件，并在项目的“类视图”窗格中看到所有形状类。

在 DLL 中定义的、可供使用它的程序访问的类的名称必须以某种方式加以标识，以便在程序和 DLL 之间建立适当的链接。正如你之前看到的，一种方法是在 DLL 的 .def 文件中添加信息。这涉及到向 DLL 添加所谓的修饰名称（decorated name），并将修饰名称与称为序号（ordinal）的唯一标识数值相关联。对象的修饰名称是编译器生成的一个名称，它会在你赋予对象的名称上附加一个额外的字符串。这个额外的字符串提供有关对象类型的信息，或者，例如对于函数，提供有关函数参数类型的信息。此外，它还确保每个对象都有唯一的标识符，并使链接器能够区分重载函数。

获取修饰名并为要从 DLL 导出的项分配序号工作量很大，而且在 Windows 中不是最佳或最简单的方法。要标识要从 DLL 导出的类，一种更简单的方法是修改 Elements.h 中的类定义，在每个类名之前加上关键字 AFX_EXT_CLASS，如下面的 CLine 类所示：

```
// Class defining a line object
class AFX_EXT_CLASS CLine: public CElement
{
DECLARE_SERIAL(CLine)

public:
virtual void Draw(CDC* pDC, CElement* pElement=0); // Function to display a line
virtual void Move(CSize& aSize);                     // Function to move an element

// Constructor for a line object
CLine(CPoint Start, CPoint End, COLORREF aColor, int PenWidth);

virtual void Serialize(CArchive& ar);// Serialize function for CLine

protected:
    CPoint m_StartPoint;            // Start point of line
    CPoint m_EndPoint;              // End point of line

    CLine(void);                    // Default constructor - should not be used
};
```

![](img/2359b0c604600c58fba3539c738a356e_953_0.png)

图 18-6

AFX_EXT_CLASS 关键字指示该类将从 DLL 导出。其效果是使完整的类对任何使用该 DLL 的程序可用，并自动允许访问该类公共接口中的任何数据和函数。使用 DLL 的程序可以访问的 DLL 中的内容集合称为 DLL 的接口。将对象作为 DLL 接口一部分的过程称为导出该对象。

你需要将关键字 AFX_EXT_CLASS 添加到所有其他形状类，包括基类 CElement。为什么必须从 DLL 中导出 CElement？毕竟，程序只创建从 CElement 派生的类的对象，而不是 CElement 类本身的对象。原因是你在 CElement 中声明了公共成员，这些成员构成了派生形状类接口的一部分，并且使用 DLL 的程序几乎肯定需要这些成员。如果不导出 CElement 类，诸如 GetBoundRect() 之类的函数将不可用。

最后需要的修改是添加指令：

```
#include <afxtempl.h>
```

到 DLL 项目的 stdafx.h 中，以便 CList 的定义可用。

你已经完成了将形状类添加到 DLL 所需的一切工作。剩下的就是编译并链接项目以创建 DLL。

### 生成 DLL

你生成 DLL 的方式与生成任何其他项目完全相同——使用“生成 | 生成解决方案”菜单选项，或选择对应的工具栏按钮。不过，生成的输出有些不同。对于 Debug 生成，你可以在项目文件夹的 debug 子文件夹中看到生成的文件；对于 Release 生成，则可以在 release 子文件夹中看到。DLL 的可执行代码包含在文件 ExtDLLExample.dll 中。执行使用该 DLL 的程序时，此文件必须可用。文件 ExtDLLExample.lib 是一个导入库文件，其中包含从 DLL 导出的项的定义，在链接使用该 DLL 的程序时，链接器必须可以使用它。

> 如果你发现 DLL 生成失败，原因是 Elements.cpp 包含了一条针对 Sketcher.h 的 #include 指令，只需将其移除即可。在我的系统上，类向导在创建 CElement 类的代码时添加了这条 #include 指令，但并不是必需的。

