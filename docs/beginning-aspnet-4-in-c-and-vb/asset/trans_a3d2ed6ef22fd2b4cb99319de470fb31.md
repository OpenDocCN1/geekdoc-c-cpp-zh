
```
}
[ComVisible(true)]
public class DotnetComponent: IWelcome, IMath
{
    public DotnetComponent()
    {
    }

    public string Greeting(string name)
    {
        return "Hello " + name;
    }

    public int Add(int val1, int val2)
    {
        return val1 + val2;
    }

    public int Sub(int val1, int val2)
    {
        return val1 - val2;
    }
}
}
```

代码片段 DotnetServer/DotnetServer.cs

构建项目后，您可以创建一个类型库。

## 创建类型库

可以使用命令行实用工具 tlbexp 创建类型库。命令

`tlbexp DotnetServer.dll`

创建类型库 DotnetServer.tlb。您可以使用实用工具 OLE/COM 对象查看器 oleview32.exe 查看类型库。该工具是 Microsoft SDK 的一部分，您可以从 Visual Studio 2010 命令提示符启动它。选择 File > View TypeLib 打开类型库。现在您可以看到的接口定义与之前使用 COM 服务器创建的接口非常相似。

类型库的名称由程序集的名称创建。类型库的头还在一个自定义属性中定义了程序集的完整名称，并且所有接口都在定义之前被前向声明。

```
// Generated .IDL file (by the OLE/COM Object Viewer)
//
// typelib filename: DotnetServer.tlb

[
    uuid(1F47A17A-B970-41DA-B3B1-B6205F188FAD),
    version(1.0),
    custom(9083BF05-3028-11D2-8F17-00A0C9A6186D, "DotnetServer, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null")
]
library DotnetServer
{
    // TLib : // mscorlib.dll : {BED7F4EA-1A96-11D2-8F08-00A0C9A6186D}
    importlib("mscorlib.tlb");
    // TLib : OLE Automation : {00020430-0000-0000-C256-000000000046}
    importlib("stdole2.tlb");

    // Forward declare all types defined in this typelib
```

```
interface IWelcome;
interface IMath;
interface _DotnetComponent;
```

在以下生成的代码中，您可以看到接口 IWelcome 和 IMath 被定义为 COM 双接口。您可以看到在 C# 代码中声明的所有方法都列在此处类型库定义中。参数已更改；.NET 类型映射为 COM 类型（例如，从 String 类到 BSTR 类型），并且签名已更改，以便返回 HRESULT。由于接口是双接口，因此也生成了调度 ID：

```
[
    odl,
    uuid(6AE7C9C-7471-3B6A-9E13-51C2294266F0),
    version(1.0),
    dual,
    oleautomation,
    custom(0F21F359-AB84-41E8-9A78-36D1106D2D9,
    'Wrox.ProCSharp.Interop.Server.IWelcome')
]

interface IWelcome : IDispatch {
    [id(0x60020000)]
    HRESULT Greeting(
        [in] BSTR name,
        [out, retval] BSTR* pRetVal);
};
```

```
[
    odl,
    uuid(AEFD0B6F-3460-3EB8-B974-155609635C0B),
    version(1.0),
    dual,
    oleautomation,
    custom(0F21F359-AB84-41E8-9A78-36D1106D2D9,
    'Wrox.ProCSharp.Interop.Server.IMath')
]

interface IMath : IDispatch {
    [id(0x60020000)]
    HRESULT Add(
        [in] long val1,
        [in] long val2,
        [out, retval] long* pRetVal);

    [id(0x60020001)]
    HRESULT Sub(
        [in] long val1,
        [in] long val2,
        [out, retval] long* pRetVal);
};
```

coclass 部分标记了 COM 对象本身。头中的 uuid 是用于实例化对象的 CLSID。类 DotnetComponent 支持接口 _DotnetComponent、_Object、IWelcome 和 IMath。_Object 在之前代码部分中包含的文件 mscorlib.tlb 中定义，并提供了基类 Object 的方法。组件的默认接口是 _DotnetComponent，它在 coclass 部分之后作为调度接口定义。在接口声明中，它被标记为 dual，但由于不包含方法，因此它是一个调度接口。通过此接口，可以使用后期绑定访问组件的所有方法：

```
{
    uuid(2F1E78D4-1147-33AC-9233-C0F51121DAA),
    version(1.0),
    custom(0F21F359-AB84-41E8-9A78-36D1106D2D9,
    'Wrox.ProCSharp.Interop.Server.DotnetComponent*')
}
```

## COM 注册

在 .NET 组件可用作 COM 对象之前，有必要在注册表中配置它。此外，如果您不想将程序集复制到客户端应用程序的同一目录，则有必要将程序集安装到全局程序集缓存中。全局程序集缓存本身在第 18 章中讨论。

要将程序集安装到全局程序集缓存中，您必须使用强名称对其进行签名（使用 Visual Studio 2010，您可以在解决方案的属性中定义强名称）。然后您可以将程序集注册到全局程序集缓存中：

```
gacutil -i DotnetServer.dll
```

现在，您可以使用 regasm 实用工具在注册表中配置组件。选项 /tlb 提取类型库并同时在注册表中配置类型库：

```
regasm DotnetServer.dll /tlb
```

写入注册表的 .NET 组件信息如下。所有 COM 配置都在配置单元 HKEY_CLASSES_ROOT（HKCR）中。ProgID 的键（在此示例中为 Wrox.DotnetComponent）连同 CLSID 一起直接写入此配置单元。

键 HKCR\CLSID\{CLSID}\InProcServer32 具有以下条目：

- **mscoree.dll** — mscoree.dll 代表 CCW。这是一个真正的 COM 对象，负责托管 .NET 组件。此 COM 对象访问 .NET 组件以向客户端提供 COM 行为。文件 mscoree.dll 通过正常的 COM 实例化机制从客户端加载并实例化。
- **ThreadingModel=Both** — 这是 mscoree.dll COM 对象的属性。此组件以提供对 STA 和 MTA 的双重支持的方式进行编程。
- **Assembly=DotnetServer, Version=1.0.0.0, Culture=neutral, PublicKeyToken=5cd57c93b4d9c1a** — Assembly 的值存储程序集的完整名称，包括版本号和公钥标记，以便可以唯一标识程序集。此处注册的程序集将由 mscoree.dll 加载。
- **Class=Wrox.ProCSharp.Interop.Server.DotnetComponent** — 类的名称也将由 mscoree.dll 使用。这是要实例化的类。
- **RuntimeVersion=v4.0.20826** — 注册表项 RuntimeVersion 指定将用于托管 .NET 程序集的 .NET 运行时版本。

除了此处显示的配置之外，所有接口和类型库也都使用其标识符进行配置。

## 创建 COM 客户端应用程序

现在，是时候创建一个 COM 客户端了。开始时创建一个简单的 C++ Win32 控制台应用程序项目，并将其命名为 COMClient。您可以保留默认选项选中并在项目向导中单击 Finish。

在文件 COMClient.cpp 的开头，添加预处理器命令以包含 <iostream> 头文件并导入您为 .NET 组件创建的类型库。导入语句创建一个“智能指针”类，使处理 COM 对象变得更容易。在构建过程中，导入语句会创建 .tlh 和 .tli 文件，您可以在项目的调试目录中找到它们，其中包含智能指针类。然后添加 using namespace 指令以打开命名空间 std，该命名空间将用于向控制台写入输出消息，以及在智能指针类内部创建的命名空间 DotnetComponent：

// COMClient.cpp: Defines the entry point for the console application.
//
#include "stdafx.h"
#include <iostream>
```

## AI核心算法

- **机器学习**
  - 监督学习
  - 无监督学习
  - 强化学习
- **深度学习**
  - 神经网络
  - 大语言模型
  - 自然语言处理

## 添加连接点

为 .NET 组件添加对 COM 事件的支持需要在 .NET 类的实现中进行一些更改。提供 COM 事件不仅仅是使用 event 和 delegate 关键字那么简单；有必要添加一些额外的 COM 互操作属性：

首先，您必须向 .NET 项目添加一个接口：IMathEvents。此接口是组件的源或传出接口，将由客户端中的 sink 对象实现。源接口必须是调度接口或自定义接口。脚本客户端仅支持调度接口。调度接口通常被首选为源接口：

```
[InterfaceType(ComInterfaceType.InterfaceIsIDispatch)]
[ComVisible(true)]
public interface IMathEvents
{
    [DispId(46200)]
    void CalculationCompleted();
}
```

代码片段 DotnetServer/DotnetServer.cs

对于类 DotnetComponent，必须指定源接口。这可以使用属性 [ComSourceInterfaces] 完成。添加属性 [ComSourceInterfaces]，并指定之前声明的传出接口。您可以使用属性类的不同构造函数添加多个源接口；然而，唯一支持多个源接口的客户端语言是 C++。Visual Basic 6.0 客户端仅支持一个源接口。

```
[classInterface(ClassInterfaceType.None)]
[ProgId("Wrox.DotnetComponent")]
[Guid("{77839717-4D0D-4876-8297-35B984802C7*}")]
[ComSourceInterfaces(typeof(IMathEvents))]
[ComVisible(true)]
public class DotnetComponent : IWelcome, IMath
{
    public DotnetComponent()
    {
    }
}
```

在类 DotnetComponent 内部，您必须为源接口的每个方法声明一个事件。方法的类型必须是委托的名称，并且事件的名称必须与源接口内部方法的名称完全相同。您可以将事件调用添加到 Add() 和 Sub() 方法中。这是第 8 章中讨论的调用事件的正常 .NET 方法。

```
public event Action CalculationCompleted;

public int Add(int val1, int val2)
{
    int result = val1 + val2;
    if (CalculationCompleted != null)
        CalculationCompleted();
    return result;
}

public int Sub(int val1, int val2)
{
    int result = val1 - val2;
    if (CalculationCompleted != null)
        CalculationCompleted();
    return result;
}
```
