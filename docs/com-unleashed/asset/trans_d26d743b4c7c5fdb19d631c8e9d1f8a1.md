
## 旧版 COM 服务器

旧版进程外服务器通常不会注册其 `HKEY_CLASSES_ROOT\AppID\{my-clsid}`，因此不会出现在 DCOMCNFG 的可配置应用程序列表中。为了让服务器出现在该列表中，必须在 `HKEY_CLASSES_ROOT\CLSID\{my-clsid}` 注册表子项中添加 AppID 值名称，并在 `HKEY_CLASSES_ROOT\AppID` 项中创建 AppID 注册表子项。感到困惑？其实并不难。这些条目的语法如下。它取自一个进程外服务器的 RGS 文件（参见清单 13.1），你将在本章后面创建该服务器。

```text
[HKEY_CLASSES_ROOT\CLSID\{my-clsid-as-guid}]
"AppID" = "{my-clsid-as-guid}"
[HKEY_CLASSES_ROOT\AppID\{my-clsid-as-guid}]
"" = "{Description of the server}"
```

> **注意**
> 
> 第二个注册表条目的键值为 `""`。每当我指定键值为 `""` 时，我指的都是默认键值。

### 清单 13.1  注册文件示例

```text
MyProject.RGS
HKCR
{
    NoRemove AppID
    {
        {E5A784C4-3498-11D2-9C2B-444553540000} = s 'MyProject'
        {
            'MyProject.exe'
            {
                val AppID = s {E5A784C4-3498-11D2-9C2B-444553540000}
            }
        }
    }
}
MyObject.RGS
HKCR
{
    MyObject.MyObject.1 = s 'MyObject Class'
    {
        CLSID = s '{E5A784D3-3498-11D2-9C2B-444553540000}'
    }
    MyObject.MyObject = s 'MyObject Class'
    {
        CurVer = s 'MyObject.MyObject.1'
    }
    NoRemove CLSID
    {
        ForceRemove {E5A784D3-3498-11D2-9C2B-444553540000} = s 'MyObject.Class'
        {
            ProgID = s 'MyObject.MyObject.1'
            VersionIndependentProgID = s 'MyObject.MyObject'
            ForceRemove 'Programmable'
            LocalServer32 = s '%MODULE%'
            val AppID = s '{E5A784C4-3498-11D2-9C2B-444553540000}'
        }
    }
}
```

Visual C++ 会将 RGS 文件编译到模块资源中。当服务器以 RegServer 参数启动时，这些 RGS 条目会自动加载到注册表中。这是在调用 `Module.UpdateRegistryFromResource(IDR_MyProject, TRUE);` 时完成的。清单 13.2 展示了在何处编写对 `UpdateRegistryFromResource()` 的调用，以及如何在主过程中编写自注册的 RegServer 和 UnregServer 参数。该清单由 ATL AppWizard 和 ObjectWizard 生成。

### 清单 13.2  自注册可执行文件

```cpp
LPCTSTR FindOneOf(LPCTSTR p1, LPCTSTR p2)
{
    while (*p1 != NULL)
    {
        LPCTSTR p = p2;
        while (*p != NULL)
        {
            if (*p1 == *p++)
                return p1+1;
        }
        p1++;
    }
    return NULL;
}

extern "C" int WINAPI _tWinMain(HINSTANCE hInstance,
    HINSTANCE , LPSTR lpCmdLine, int )
{
    lpCmdLine = GetCommandLine(); //necessary for _ATL_MIN_CRT
    HRESULT hRes = CoInitialize(NULL);
    // If you are running on NT 4.0 or higher you can use the
    // following call instead to make the EXE free threaded.
    // This means that calls come in on a random RPC thread
    // HRESULT hRes = CoInitializeEx(NULL, COINIT_MULTITHREADED);
    ASSERTE(SUCCEEDED(hRes));
    _Module.Init(ObjectMap, hInstance);
    _Module.OutThreadID = GetCurrentThreadId();
    TCHAR szTokens[] = _T("-/");

    int nRet = 0;
    BOOL bRun = TRUE;
    LPCTSTR lpszToken = FindOneOf(lpCmdLine, szTokens);
    while (lpszToken != NULL)
    {
        if (lstrcmpi(lpszToken, _T("UnregServer"))==0)
        {
            _Module.UpdateRegistryFromResource(IDR_MyProject,
                                               FALSE);
            nRet = _Module.UnregisterServer();
            bRun = FALSE;
            break;
        }
        if (lstrcmpi(lpszToken, _T("RegServer"))==0)
        {
            _Module.UpdateRegistryFromResource(IDR_MyProject,
                                               TRUE);
            nRet = _Module.RegisterServer(TRUE);
            bRun = FALSE;
            break;
        }
        lpszToken = FindOneOf(lpszToken, szTokens);
    }

    if (bRun)
    {
        hRes = _Module.RegisterClassObjects(
            CLSCTX_LOCAL_SERVER,
            REGCLS_MULTIPLEUSE);

        ASSERTE(SUCCEEDED(hRes));

        MSG msg;
        while (GetMessage(&msg, 0, 0, 0))
            DispatchMessage(&msg);

        _Module.RevokeClassObjects();
    }

    CoUninitialize();
    return nRet;
}
```

### 清单 13.3  续

```idl
pointer_default(unique)
]
interface IMyObject : IDispatch
{
    [propget, id(1), helpstring("property MyProperty")]
    HRESULT MyProperty([out, retval] long *pVal);
};
[
    uuid(E5A784C3-3498-11D2-9C2B-444553540000),
    version(1.0),
    helpstring("MyProject 1.0 Type Library")
]
library MYPROJECTLib
{
    importlib("stdole32.tlb");
    importlib("stdole2.tlb");

    [
        uuid(E5A784D3-3498-11D2-9C2B-444553540000),
        helpstring("MyObject Class")
    ]
    coclass MyObject
    {
        [default] interface IMyObject;
    };
};
```

### 清单 13.4  简单的本地服务器对象头文件

```cpp
// MyObject.h : Declaration of the CMyObject

#ifndef __MYOBJECT_H_
#define __MYOBJECT_H_

#include "resource.h"        // main symbols

///////////////////////////////////////////////////////////////
// CMyObject
class ATL_NO_VTABLE CMyObject :
    public CComObjectRootEx<CComSingleThreadModel>,
    public CComCoClass<CMyObject, &CLSID_MyObject>,
    public IDispatchImpl<IMyObject, &IID_IMyObject,
                         &LIBID_MYPROJECTLib>
{
public:
    CMyObject()
    {
    }

DECLARE_REGISTRY_RESOURCEID(IDR_MYOBJECT)

BEGIN_COM_MAP(CMyObject)
    COM_INTERFACE_ENTRY(IMyObject)
    COM_INTERFACE_ENTRY(IDispatch)
END_COM_MAP()

// IMyObject
public:
    STDMETHOD(get_MyProperty)(/*[out, retval]*/ long *pVal);
};

#endif // _MYOBJECT_H
```

### 清单 13.5  简单的本地服务器对象实现

```cpp
// MyObject.cpp : implementation of CMyObject
#include "stdafx.h"
#include "MyProject.h"
#include "MyObject.h"

////////////////////////////////////////////
// CMyObject

STDMETHODIMP CMyObject::get_MyProperty(long *pVal)
{
    // TODO: Add your implementation code here
    *pVal = 10;

    return S_OK;
}
```

前面的代码不是由开发者创建的，而是由向导创建的。你唯一需要自己编写的代码是在清单 13.5 中 CMyObject::get_MyProperty() 方法里的 `*pVal = 10`。

清单 13.3 是 MyProject.dll 的 IDL 源文件。在其中可以看到接口声明。

清单 13.4 包含 CMyObject 类的声明。这是实现 IMyObject 接口的类。你还可以看到 CComSingleThreadModel 类。

清单 13.5 展示了 CMyObject 类的实现代码。内容不多，因为只有一个方法，它充当属性 get 方法。

## 默认属性

DCOMCNFG 属性表对话框的第二个选项卡是“默认属性”选项卡（见图 13.2）。此页面允许你更改四个独立的控件，我在第 8 章已经讨论过它们。它们可以在注册表的 AppID 结构中找到。

![](img/112c2326f49d26b8d59aa054e14c5747_356_0.png)

“在此计算机上启用分布式 COM+”复选框通过设置 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Ole` 项中的 enableDistributedCOM 注册表值来启用和禁用分布式对象。这控制客户端应用程序是否可以启动或连接到远程 COM+ 对象——即不在同一台计算机上的对象。

“默认身份验证级别”下拉组合框设置安全提供程序使用的身份验证级别。connect 和 Call 身份验证级别都不可用于像 UDP 这样的无连接协议。默认情况下，大多数 DCOM+ 安装使用无连接 UDP 协议。当当前级别不可用时，COM+ 会将身份验证级别提升到下一个可接受的级别。用于 Windows 95 的 DCOM+ 默认使用基于连接的 TCP 协议。如果身份验证级别设置为 None，则 COM+ 安全被禁用，导致无论单独的安全设置如何，所有连接、调用和数据包都会被接受。

“默认模拟级别”下拉组合框设置 COM+ 安全使用的模拟级别。默认值为 Identify。

最后一个控件“为引用跟踪提供额外安全”复选框，启用和禁用对 `AddRef()` 和 `Release()` 调用的安全保护。启用此额外安全会减慢 COM。除非出于某种原因需要额外安全，否则不应选中此复选框。

