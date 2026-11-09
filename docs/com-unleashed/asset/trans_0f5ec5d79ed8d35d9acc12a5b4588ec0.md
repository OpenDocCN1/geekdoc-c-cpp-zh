

**清单6.16（续）**

```cpp
}

DWORD WINAPI CMyEventSource::ThreadStart(void * pCookie)
{
    CMyEventSource * object = (CMyEventSource *)pCookie;
    Sleep(1000 * object->m_lSeconds);
    object->Fire_Timeout();
    return 0;
}
```

如第7章“COM+ 线程处理”所述，这种线程被称为*工作线程*。它使主线程能够继续正常处理，而任务在后台执行。在本例中，后台任务是`CMyEventSource::ThreadStart`静态方法，它只是等待指定的秒数，然后触发超时事件。

我本可以编写`CMyEventSource::FireEvent()`的代码，使其像清单6.14那样调用事件接收器处理例程。但Visual C++提供了一种更安全、更简单的替代方法来生成代码。使用这种方法，我将事件通知代码缩减为一行，即`CMyEventSource::Fire_Timeout()`。`CMyEventSource::Fire_Timeout()`背后的代码是由Visual C++ 6.0的ATL代理生成器生成的。

## ATL 代理生成器

ATL代理生成器具有生成向所有已连接的事件接收器广播事件通知所需源代码的功能。这使得编码更加容易，因为事件源中的事件通知只需一行代码，而不是清单6.14中使用的约20行。

> **注意**
>
> ATL代理生成器在Visual C++ 6.0中不再作为独立工具提供，它已集成到DevStudio的类视图（ClassView）窗格中。保存你的IDL并编译它，以便生成类型库。你可以通过右键单击DevStudio的文件视图（FileView）窗格中的IDL文件，并在弹出菜单中选择“编译”选项来编译IDL。
>
> 类型库编译完成后，右键单击类视图窗格中的事件源类，并在弹出菜单中选择“实现连接点”。在出现的“实现连接点”对话框中，你可以选择事件接口，并单击“确定”。
>
> IDL文件将生成一个类似于清单6.17的头文件，并自动生成从新生成的代理类继承的代码。

为了生成事件源代理代码，请保存IDL文件并将其编译为所需的类型库。在本例中，类型库文件是`vbSink.tlb`。现在，在IDE中，依次选择“项目”、“添加到项目”、“组件和控件”。选择“Developer Studio组件”文件夹，然后选择“ATL代理生成器”项。选择“插入”，并在确认弹出框中单击“确定”。将出现ATL代理生成器对话框，它应类似于图6.2。

![](img/112c2326f49d26b8d59aa054e14c5747_156_0.png)

在对话框中，在“类型库名称”编辑控件中添加带完整路径的类型库文件名。你可以使用省略号按钮浏览类型库。突出显示事件接收器调度接口，并单击“->”将该接口从“未选择”窗格移动到“已选择”窗格。在“代理类型”框中选择“连接点”，并单击“插入”按钮。代码生成器将要求输入文件名。你只需单击“保存”按钮，即可接受代码生成器提供的文件名。

清单6.17显示了从你的类型库生成的代码。

**清单6.17 IConnectionPoint 处理程序**

```cpp
////////////////////////////////////////////////////////////////////
// CProxyDMyEventSink
template <class T>
class CProxyDMyEventSink :
    public IConnectionPointImpl<T, &DIID_DMyEventSink,
                         CComDynamicUnkArray>
{
public:
//methods:
//DMyEventSink : IDispatch
public:
    void Fire_Timeout()
    {
        T* pT = (T*)this;
        pT->Lock();
        IUnknown** pp = m_vec.begin();
        while (pp < m_vec.end())
        {
            if (*pp != NULL)
            {
                DISPPARAMS disp = { NULL, NULL, 0, 0 };
                IDispatch* pDispatch =
                    reinterpret_cast<IDispatch*>(*pp);
                pDispatch->Invoke(0x1, IID_NULL, LOCALE_USER_DEFAULT,
                    DISPATCH_METHOD, &disp, NULL, NULL, NULL);
            }
            pp++;
        }
        pT->Unlock();
    }
};
```

要实现此连接点模板类，只需从该模板派生事件源类，并将调度接口ID添加到连接点映射中。清单6.18显示了新的事件源类声明。

**清单6.18 事件源类**

```cpp
// MyEventSource.h : Declaration of the CMyEventSource

#ifndef __MYEVENTSOURCE_H_
#define __MYEVENTSOURCE_H_

#include "resource.h"       // main symbols
#include "cpvbsink.h"

/////////////////////////////////////////////////////////////////////////////
// CMyEventSource
class ATL_NO_VTABLE CMyEventSource :
    public CComObjectRootEx<CComMultiThreadModel>,
    public CComCoClass<CMyEventSource, &CLSID_MyEventSource>,
    public IConnectionPointContainerImpl<CMyEventSource>,
    public IDispatchImpl<IMyEventSource, &IID_IMyEventSource,
        &LIBID_VBSINKLib>,
    public CProxyDMyEventSink<CMyEventSource>
{
public:
    CMyEventSource()
    {
    }

DECLARE_REGISTRY_RESOURCEID(IDR_MYEVENTSOURCE)

BEGIN_COM_MAP(CMyEventSource)
    COM_INTERFACE_ENTRY(IMyEventSource)
    COM_INTERFACE_ENTRY(IDispatch)
    COM_INTERFACE_ENTRY_IMPL(IConnectionPointContainer)
END_COM_MAP()

BEGIN_CONNECTION_POINT_MAP(CMyEventSource)
    CONNECTION_POINT_ENTRY(DIID_DMyEventSink)
END_CONNECTION_POINT_MAP()

// IMyEventSource
public:
    STDMETHOD(FireEvent)(long lSeconds);
private:
    long m_lSeconds;
    static DWORD WINAPI ThreadStart(void * pCookie);
};

#endif // __MYEVENTSOURCE_H_
```

我没有重写控制程序或事件接收器客户端。相反，我将用Visual Basic编写客户端，以证明此类事件处理与Visual Basic兼容。

### 编写 Visual Basic 客户端

编写VB客户端相当容易。创建一个简单的Visual Basic可执行文件，其中包含一个窗体和类文件。转到“项目”、“引用”，并启用对包含你所使用的COM对象的类型库的引用。将清单6.19中的代码添加到窗体源代码中。

**清单6.19 启动事件**

```vb
Option Explicit
Dim vbsinkcls As Class1

Private Sub Command1_Click()

    Set vbsinkcls = New Class1
    DoEvents
    vbsinkcls.Go

End Sub
```

注意，`Class1`是类文件的名称。如果更改了类文件的名称，则还必须更改窗体源代码中的代码。

最后，你必须创建COM对象、调用`FireEvent`方法并响应`Timeout`事件通知。清单6.20显示了类文件中执行这些操作的代码。

**清单6.20 调用事件触发器并处理事件通知的类**

```vb
Option Explicit
Dim WithEvents vbsink As VBSINKLib.MyEventSource
Attribute vbsink.VB_VarHelpID = -1

Private Sub Class_Initialize()

    Set vbsink = New VBSINKLib.MyEventSource

End Sub

Private Sub Class_Terminate()

    Set vbsink = Nothing

End Sub

Private Sub vbsink_Timeout()

    MsgBox "Timeout"

End Sub

Sub Go()

    vbsink.FireEvent 10

End Sub
```

`vbsink`对象的类型必须是IDL文件中定义的类型库名称，以及同样在IDL文件中定义的coclass的类名。COM类在`Class_Initialize()`子例程中创建，并在`Class_Terminate()`子例程中销毁。`Go()`子例程调用COM对象的`FireEvent`方法，参数指明在发送超时事件前延迟10秒。

此类文件中最重要的部分是接收事件通知的`vbsink_Timeout()`子例程。当Visual Basic收到事件通知时，它会查找与对象名称匹配的子例程名称，该名称的格式为：对象名称 + 下划线 + 通知方法的名称。

运行VB可执行文件，并单击“Trigger”按钮。十秒钟后，事件通知将被发送，并显示一个标题为“Timeout”的消息框。就是这样。

