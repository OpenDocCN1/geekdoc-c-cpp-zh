
## IMoniker::GetTimeOfLastChange()

IMoniker::GetTimeOfLastChange() 方法可用于确定该名字对象上次更改的时间。如果你正在缓存来自该名字对象的数据，这会很有用。

## IMoniker::CommonPrefixWith() and IMoniker::RelativePathTo()

IMoniker::CommonPrefixWith() 方法创建一个新的名字对象，用于确定此名字对象与另一个名字对象的共同部分。例如，文件名字对象 c:\mydir\subdir\myfile.doc 和 c:\mydir\otherdir\myfile.doc 的共同前缀将是 c:\mydir。

IMoniker::RelativePathTo() 方法创建一个新的相对名字对象，用于确定从此名字对象到另一个名字对象的相对路径。使用前面的示例文件名字对象，得到的相对名字对象将具有显示名称 ..\otherdir\myfile.doc。

## IMoniker::GetDisplayName()

IMoniker::GetDisplayName() 方法检索名字对象的显示名称。对于文件名字对象，此函数将返回你创建该名字对象时所用的同一文件名。

## IMoniker::IsSystemMoniker()

IMoniker::IsSystemMoniker() 方法返回名字对象类型。清单 5.3 展示了使用 IMoniker::IsSystemMoniker() 方法的示例。该清单输出数字 2，它是文件名字对象的类型。

### LISTING 5.3 Using IMoniker::IsSystemMoniker()

```cpp
#include <windows.h>
#include <iostream>

int main()
{
    IBindCtx *pbindctx;
    IMoniker *pmoniker;
    ULONG ul;
    HRESULT hresult = ::CreateBindCtx(0, &pbindctx);
    hresult = ::MkParseDisplayName(pbindctx, L"e:\\old.doc", &ul,
        &pmoniker);
    DWORD dw;
    pmoniker->IsSystemMoniker(&dw);
    std::cout << dw << std::endl;
    pbindctx->Release();
    pmoniker->Release();

    return 0;
}
```

## Exploring Moniker Types

提供名字对象的组件使该名字对象可被其他对象访问。理解各种系统提供的名字对象类之间的差异非常重要，这样才能知道哪些类适合给定对象。COM 还提供了使用 COM 提供的名字对象类来创建名字对象的函数。在本节中，我将介绍文件名字对象、运行对象表、项名字对象、类名字对象和指针名字对象。

### File Monikers

最简单的名字对象类型是文件名字对象。它们可用于标识存储在其自身文件中的任何对象。文件名字对象充当本机文件系统分配给该文件的路径名的包装器。对此名字对象调用 IMoniker::BindToObject() 将导致该对象被激活，然后返回指向该对象的接口指针。由该名字对象命名的对象的源必须提供 IPersistFile 接口的实现，以支持绑定文件名字对象。（有关更多详细信息，请参见第 4 章“持久存储”。你也可以在本章后面找到该接口声明。）文件名字对象可以表示完整路径或相对路径。

例如，存储为文件 C:\FINANCIAL\PROJECTIONS.XLS 的电子表格对象的文件名字对象将包含与该路径名等效的信息。然而，该名字对象不一定由相同的字符串组成。该字符串只是其显示名称，是对名字对象内容的一种表示，对最终用户有意义。显示名称可通过 IMoniker::GetDisplayName() 方法获得，仅在向最终用户显示名字对象时使用。此方法获取任何名字对象类的显示名称。在内部，名字对象可能以对执行名字对象操作更高效、但对用户没有意义的格式存储相同的信息。然后，当通过调用 BindToObject() 方法绑定同一对象时，该对象将被激活，可能是通过将文件加载到电子表格中。

COM+ 提供了名字对象提供程序以及辅助 API CreateFileMoniker()，后者创建一个文件名字对象，并将该对象的指针返回给提供程序。

![](img/112c2326f49d26b8d59aa054e14c5747_126_0.png)

COM+ 支持三种激活原语：绑定到类对象、绑定到新的类实例，以及绑定到存储在文件中的持久对象。这可以在 COM+ API 函数 `CoGetInstanceFromFile()` 中看到，如清单 5.4 所示。

### LISTING 5.4 The CoGetInstanceFromFile Declaration

```cpp
HRESULT CoGetInstanceFromFile(
    [in, unique] COSERVERINFO *pcsi,  // host/security info
    [in, unique] CLSID        *pClsid, // explicit CLSID (opt)
    [in, unique] IUnknown     *punkOuter, // for aggregation
    [in] DWORD dwClsCtx,               // locality?
    [in] DWORD grfMode,               // file open mode
    [in, string] OLECHAR *pwszName,    // file name of object
    [in] DWORD cmqi,                  // how many interfaces?
    [out, size_is(cmqi)] MULTI_QI *prgmi // where to put iQfs
);
```

CoGetInstanceFromFile() 例程将文件名作为输入。此文件名引用对象的持久状态。使用 CoGetInstanceFromFile() 方法可保证该对象正在运行。然后，它返回一个或多个指向已激活（或重新激活）对象的接口指针。为了完成此操作，CoGetInstanceFromFile() 首先需要确定对象的 CLSID。需要 CLSID 有两个原因。首先，如果对象未运行，COM+ 将需要此 CLSID 来创建新实例，并从持久映像初始化该实例。其次，如果调用方没有指定要将激活调用转发到的显式主机名，COM+ 将使用 CLSID 来确定要在哪台机器上激活该对象。

如果调用方未显式传递 CLSID，则 CoGetInstanceFromFile() 函数会通过调用 COM+ API 函数 `GetClassFile()` 从文件本身派生 CLSID：

```cpp
HRESULT GetClassFile([in, string] OLECHAR *pwszFileName,
                     [out] CLSID *pclsid);
```

`GetClassFile()` 使用文件中的头信息以及注册表信息来确定文件中包含的对象类型。

一旦确定了类和主机，COM+ 就会检查目标主机上的运行对象表（ROT），以确定该对象是否已经激活。ROT 是 SCM 的一项设施，它将任意名字对象映射到本地主机上正在运行的实例。持久对象应在加载时在本地 ROT 中注册自身。为了将持久对象的文件名表示为名字对象，COM+ 提供了一种标准名字对象类型，称为文件名字对象，它将文件名包装在 `IMoniker` 接口之后。文件名字对象可以通过将文件名传递给 `MkParseDisplayName()` 来创建，也可以通过调用显式 API 函数 `CreateFileMoniker()` 来创建：

```cpp
HRESULT CreateFileMoniker(
    [in, string] const OLECHAR *pszFileName,
    [out] IMoniker **pmk);
```

如果持久对象已将其文件名字对象注册到 ROT 中，则 `CoGetInstanceFromFile()` 只需返回指向已运行对象的指针。如果在 ROT 中找不到该对象，COM+ 将创建该文件类的新实例，并通过该实例的 `IPersistFile::Load()` 方法从持久映像初始化它，如清单 5.5 所示。

### LISTING 5.5 The IPersistFile Interface Declaration

```cpp
[ object, uuid(0000010b-0000-0000-C000-000000000046) ]
interface IPersistFile : IPersist {
// called by CoGetInstanceFromFile to initialize object
  HRESULT Load(
        [in, string] const OLECHAR *pszFileName,
        [in] DWORD grfMode
  );
// remaining methods deleted for clarity
}
```

对象实现负责从文件加载任何持久状态，并在本地 ROT 中注册自身，以确保每个文件一次只有一个实例在运行。这可以在清单 5.6 中看到。

### LISTING 5.6 Loading the Persistent State

```cpp
STDMETHODIMP Example::Load(const OLECHAR *pszFileName,
                           DWORD grfMode)
{
// read in persistent state
  HRESULT hr = this->MyReadStateFromFile(pszFileName, grfMode);
  if (FAILED(hr)) return hr;
// get pointer to ROT from SCM
  IRunningObjectTable *prot = 0;
  hr = GetRunningObjectTable(0, &prot);
  if (SUCCEEDED(hr)) {
// create a file moniker to register in ROT
    IMoniker *pmk = 0;
    hr = CreateFileMoniker(pszFileName, &pmk);
    if (SUCCEEDED(hr)) {
// register self in ROT
      hr = prot->Register(0, this, pmk, &m_dwReg);
      pmk->Release();
    }
    prot->Release();
  }
  return hr;
}
```
