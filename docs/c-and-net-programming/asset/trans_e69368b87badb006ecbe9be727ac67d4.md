
数据，使其仅包含关于在所选 AppDomain 中分配的实例的信息。AppDomain 过滤器不会影响“本机内存”视图中显示的信息。

- 并非总能将实例与 AppDomain 关联起来。运行时可以在内部创建实例，非托管资源实例也可以在本机线程中创建。若要检索未与任何 AppDomain 关联的实例信息，必须将 AppDomain 选择器设置为显示（所有）AppDomain。

## 26.3 使用 CLR 对象进行自定义承载

- 在执行各种应用程序时，Windows 有多种方式可识别某个二进制文件是 .NET 应用程序。这些技术取决于 Windows 的版本。通常，Windows 通过查看 PE 头（可移植可执行文件）来执行 .exe 文件。PE 头说明了应如何将其加载到内存中、它有哪些依赖项以及入口点在哪里。为了获知 .NET 应用程序的入口点，Windows 使用某种特定技术。实际上，应用程序由某些 IL 代码组成。直接执行这些代码显然会导致崩溃。应当开始执行的不是 IL 代码，而是 .NET 运行时，最终由运行时加载 IL 代码并执行它。

- 在较新版本的 Windows 中，.NET 已预装，并且 Windows 内置了对识别 .NET 应用程序的支持。只需查看所有可执行文件和 DLL 中带有的 PE 头即可完成识别。在较旧版本的 Windows 中，执行会传递给引导代码所在的入口点。引导程序是本机代码，它使用非托管的 CLR 承载 API 在当前进程内启动 .NET 运行时，并启动真正的程序（即 IL 代码）。

### 26.3.1 CLR 承载 API

### 在非托管应用程序中承载 CLR

- 从非托管的角度来看，承载 CLR 相当简单；它其实就是 COM（组件对象模型）。首先，需要使用最合适的 API（CorBindToRuntimeEx() 或 CLRCreateInstance()）获取 ICLRRuntimeHost 的实例。ICLRMetaHost 和 ICLRRuntimeInfo。一旦获得运行时宿主，就可以通过调用 ICLRRuntimeHost::SetHostControl() 将其连接到非托管宿主。完成该操作后，就可以提供 AppDomainManager 的实现，告诉 CLR 要使用的程序集和类型，然后启动 CLR。在自定义 AppDomainManager 注册中，有一件重要的事情要做：实现 InitializeNewDomain()，以便设置标志，告诉 CLR 向非托管宿主注册新的应用程序域。下面的代码对此进行了演示。

```
public override void InitializeNewDomain(AppDomainSetup appDomainInfo)
{
    // let the unmanaged host know about the application
    InitializationFlags = AppDomainManagerInitializationOptions.RegisterWithHost;
}
```

- 设置好之后，对于每个创建的应用程序域，应用程序都会收到对 IHostControl::SetAppDomainManager() 方法的调用。为了获得更强大的承载能力，需要创建一个接口用于在非托管宿主和托管 AppDomainManager 之间通信，可能还需要一个用于反向通信的接口。

- 当 .NET 运行时在本机进程内启动时，该本机应用程序就成为该运行时的宿主。这为本机应用程序增加了 .NET 功能。

```
#include <metahost.h>
#include <mscoree.h>
#pragma comment(lib, "mscoree.lib")

ICLRMetaHost *pMetaHost = nullptr;
ICLRRuntimeHost *pRuntimeHost = nullptr;
ICLRRuntimeInfo *pRuntimeInfo = nullptr;
HRESULT hr;

hr = CLRCreateInstance(CLSID_CLRMetaHost,
    IID_ICLRMetaHost, (LPVOID*)&pMetaHost);
hr = pMetaHost->GetRuntimeVersion(IID_PPV_ARGS(&pRuntimeInfo));
hr = pRuntimeInfo->GetInterface(CLSID_CLRRuntimeHost, IID_PPV_ARGS(&pRuntimeHost));
hr = pRuntimeHost->Start();
```

- 现在运行时已经运行，但还没有加载任何用户代码。一些内部线程调度器和垃圾回收器肯定在运行，因为它们是 CLR 运行时的一部分。

### 26.3.2 在托管应用程序中承载 CLR - 运行托管代码

要从宿主启动托管应用程序，可以编写如下代码：

```
AppDomain.CurrentDomain.ExecuteAssembly(assemblyName);
```

### 旧版 API

在 CLR 承载接口的早期版本中，**托管代码**是通过名为 GetDefaultDomain 的 API 执行的，该 API 返回一个 AppDomain。

```
HRESULT hr = CorBindToRuntimeEx(..., IID_ICorRuntimeHost, (void**)&pRuntimeHost);
hr = pRuntimeHost->Start();
_AppDomain* pCurrentDomain = nullptr;
hr = pRuntimeHost->GetDefaultDomain(&pCurrentDomain);
pCurrentDomain->ExecuteAssembly(assemblyFilename);
```

但出于一些充分的原因，这个接口已被弃用。旧版 API 有相当大一部分在非托管代码中，这被证明是一个很大的缺点。在非托管代码中从 AppDomain 检索值或操作对象会导致大量封送（序列化），这会严重影响性能。封送还是隐式的，因此并不总是很清楚它发生在哪里。有时甚至整个 AppDomain 都会被封送。新版 API 使所有自定义代码得以在 AppDomain 内运行。

### 新版 API

CLR 承载接口的新版本经过了重新设计。大部分 API 已从非托管代码移到托管代码。为了获取 AppDomain 实例，必须注册 AppDomainManager 实现。要注册新的 AppDomainManager，需要 ICLRControl 接口。该接口包含一个方法 SetAppDomainManagerType，用于加载 AppDomainManager 的托管实现。代码如下所示：

```
ICLRControl* pCLRControl = nullptr;
hr = pRuntimeHost->GetCLRControl(&pCLRControl);
LPCWSTR assemblyName = L"TechAppDomainManager";
LPCWSTR appDomainManagerTypename = L"TechAppDomainManager.CustomAppDomainManager";
hr = pCLRControl->SetAppDomainManagerType(assemblyName, appDomainManagerTypename);
```

这就是覆盖它的方式。**AppDomain** 不是直接使用的，以避免所有数据封送，如下所示：

```
hr = pRuntimeHost->Start();
DWORD returnValue = 0;
// Executing public static Start(string arg)
hr = pRuntimeHost->ExecuteInDefaultAppDomain(totalPath, L"TechApp1.Program", L"Start", L"", &returnValue);
hr = pRuntimeHost->Stop();
```

### IHostControl 类

这是一个类，CLR 会查询它来获取备选管理器（Manager）的实现；如果有任何管理器，应实例化自定义版本并返回它们。

下面列出了可以使用用户实现覆盖的处理程序或管理器的示例：

- IID_IHostTaskManager
- IID_IHostThreadpoolManager
- IID_IHostSyncManager
- IID_IHostAssemblyManager
- IID_IHostGcManager
- IID_IHostPolicyManager

在 AppDomainManager 的情况下，CLR 实际上会调用 IHostControl::SetAppDomainManager，并传入一个指向它被告知要创建的类实例的指针。上文有一个名称类似的方法 ICLRRuntimeHost::SetAppDomainType。

## 两分题（附答案）

Q.1 什么是程序集？程序集有哪些不同类型？

答：程序集是逻辑单元的集合。逻辑单元指的是使用 .NET Framework 构建应用程序并部署它们所需的类型和资源。CLR 使用这些信息进行类型实现。基本上，程序集是 EXE 和 DLL 的集合。它是可移植且可执行的。

有两种类型的程序集：私有程序集和共享程序集。

- 私有程序集，顾名思义，只能由应用程序访问。它安装在应用程序的安装目录中。
- 共享程序集可以被多个应用程序共享。它安装在 GAC 中。

Q.2 解释程序集的不同部分。

答：程序集的不同部分包括：

- 清单（Manifest）——它包含程序集版本的信息。它也称为程序集元数据。
- 类型元数据（Type Metadata）——程序的二进制信息。
- MSIL——Microsoft 中间语言代码。
- 资源（Resources）——相关文件的列表。

