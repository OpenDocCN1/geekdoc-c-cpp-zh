
### 清单 11.6

```c
NdrFcShort( 0x10 ), /* Alpha Stack size/offset = 16 */
#endif
/* 6 */ NdrFcShort( 0x0 ),  /* 0 */
/* 8 */ NdrFcShort( 0x0 ),  /* 8 */
/* 10 */ 0x4, /* 4 */
        0x1, /* 1 */

/* Return value */

/* 12 */ NdrFcShort( 0x70 ),  /* 112 */
#ifdef _ALPHA
/* 14 */ NdrFcShort( 0x4 ),
/* x86, MIPS, PPC Stack size/offset = 4 */
#else
        NdrFcShort( 0x8 ),  /* Alpha Stack size/offset = 8 */
#endif
/* 16 */ 0x08,  /* FC_LONG */
        0x0,  /* 0 */

        0x0
        }
    };

static const MIDL_TYPE_FORMAT_STRING __MIDL_TypeFormatString =
    {
        0,
        {
            0x0
        }
    };

const CInterfaceProxyVtbl * _MyMidlExperiment_ProxyVtblList[]=
    {
        ( CInterfaceProxyVtbl * ) &_IMyInterfaceProxyVtbl,
        0
    };

const CInterfaceStubVtbl * _MyMidlExperiment_StubVtblList[] =
    {
        ( CInterfaceStubVtbl * ) &_IMyInterfaceStubVtbl,
        0
    };

PCInterfaceName const _MyMidlExperiment_InterfaceNamesList[] =
    {
        "IMyInterface",
        0
    };

#define _MyMidlExperiment_CHECK_IID(n) \
    IID_GENERIC_CHECK_IID(_MyMidlExperiment, pIID, n)

int __stdcall _MyMidlExperiment_IID_Lookup( const IID * pIID,
                                             int * pIndex )
{
    if(! _MyMidlExperiment_CHECK_IID())
    {
        *pIndex = 0;
        return 1;
    }
    return 0;
}

const ExtendedProxyFileInfo _MyMidlExperiment_ProxyFileInfo =
{
    (PCInterfaceProxyVtblList * ) &
        _MyMidlExperiment_ProxyVtblList,
    (PCInterfaceStubVtblList * ) &
        _MyMidlExperiment_StubVtblList,
    (const PCInterfaceName * ) &
        _MyMidlExperiment_InterfaceNamesList,
    0, // no delegation
    & _MyMidlExperiment_IID_Lookup,
    1,
    2
};
```

## 注册文件

清单 11.7 展示了使用标准封送处理的 COM+ 类的注册文件。

### 清单 11.7 标准封送处理的示例注册文件

```text
[HKEY_CLASSES_ROOT\CLSID\{my-proxy-stub-clsid}]
@="MyInterface proxy/stub factory"

[HKEY_CLASSES_ROOT\CLSID\{my-proxy-stub-clsid}\InprocServer32]
@="{my-proxy-stub-module-path}"

[HKEY_CLASSES_ROOT\CLSID\{my-proxy-stub-clsid}\InprocServer32]
@="Both" or other

[HKEY_CLASSES_ROOT\Interface\{my-interfaces-id}]
@="IMyInterface"

[HKEY_CLASSES_ROOT\Interface\{my-interfaces-id}\ProxyStubClsid32]
@="{my-proxy-stub-clsid}"

[HKEY_CLASSES_ROOT\Interface\{my-interfaces-id}\NumMethods]
@="x"
```

## 转换 MIDL 输出文件

现在重要的一点是——如何将这些 MIDL 输出文件转换为代理桩并注册代理桩？清单 11.8 展示了用于编译链接和注册代理桩的两个命令。只有一个 DLL 文件同时包含代理和桩。因此，客户端和服务器上应存在同一个 DLL。此外，在需要跨套间时，ATL 允许你将代理/桩与真实 COM 对象放在同一个 DLL 中。如果要在另一台机器上注册代理，必须将 marshalservers.dll 复制到该机器，并使用 Regsvr32 注册它。

### 清单 11.8 编译链接并注册代理桩

```text
nmake /f marshalservers.mk
regsvr32 marshalservers.dll
```

清单 11.9 是一个有趣的控制程序，它可以展示未安装代理桩和已安装代理桩时的不同结果。

### 清单 11.9 未注册代理桩的结果

```cpp
#include <windows.h>
#include <iostream>
#include "marshalserver\\marshalserver.h"
#include "marshalserver\\marshalserver_i.c"

char s[1024];

HRESULT GetUnknown(WCHAR * strProgID, IUnknown ** ppunknown)
{
    CLSID clsid;
    HRESULT hresult = ::CLSIDFromProgID(strProgID, &clsid);
    if (FAILED(hresult))
    {
        // CLSIDFromProgID failed
        std::cout << "CLSIDFromProgID failed "
                  << _ltoa(hresult, s, 16) << std::endl;
        ::DebugBreak();
        return hresult;
    }

    hresult = ::CoCreateInstance(clsid, NULL, CLSCTX_SERVER,
                                 IID_IUnknown, (void **)punknown);
    if (FAILED(hresult))
    {
        // CoCreateInstance failed
        std::cout << "CoCreateInstance failed "
                  << _ltoa(hresult, s, 16) << std::endl;
        ::DebugBreak();
        return hresult;
    }

    return S_OK;
};

HRESULT GetInterface(IUnknown * punknown, REFIID riid,
                     IUnknown ** ppunknown)
{
    HRESULT hresult = punknown->QueryInterface(riid,
                              (void **)ppunknown);
    if (FAILED(hresult))
    {
        // QueryInterface failed
        std::cout << "QueryInterface failed "
                  << _ltoa(hresult, s, 16) << std::endl;
        ::DebugBreak();
        return hresult;
    }

    return S_OK;
};

int main()
{
    CoInitialize(NULL);
    std::cout << "Start" << std::endl;

    IUnknown * punknown;
    HRESULT hresult = GetUnknown(L"MarshalClass.MarshalClass.1",
                                  &punknown);
    if (FAILED(hresult))
    {
        // GetUnknown failed
        return hresult;
    }

    IMarshalClass * pmc;
    hresult = GetInterface(punknown, IID_IMarshalClass,
                           (IUnknown **)&pmc);

    if (FAILED(hresult))
    {
        // GetUnknown failed
        return hresult;
    }

    std::cout << "End" << std::endl;
    CoUninitialize();
    return 0;
}
```

如果在注册代理桩之前运行清单 11.9，则对 `IUnknown::QueryInterface()` 的调用将返回 0x80004002 或 E_NOINTERFACE。这有些误导，因为接口确实存在，但该接口无法在进程之间进行封送。如果你已经注册了代理桩，并且想要注销代理桩，请使用 /U 参数运行 Regsvr32 实用工具。注册代理桩 DLL 后，清单 11.9 中的代码应能无错误地运行。本书附带的 CD-ROM 中提供了更多标准封送处理代码。可在 chapter11 目录下的 marshaling 子目录中找到。

## 自定义封送处理

通常，使用标准封送处理是可以接受的，但有时需要更高效的自定义封送器。需要使用自定义封送处理的一个很好的例子是：传递值，或者某个对象是只读的且永远不会改变。在这些情况下，由于代理已经存储了其状态，因此不再需要调用真实对象。对象可以通过公开 IMarshal 接口来实现自定义封送处理。清单 11.10 展示了 IMarshal 接口的定义。

### 清单 11.10 IMarshal 接口的定义

```cpp
interface IMarshal : IUnknown
{
    HRESULT GetUnmarshalClass([in] REFIID riid,
        [in, unique] void * pv,
        [in] DWORD dwDestContext,
        [in, unique] void * pvDestContext,
        [in] DWORD mshlflags,
        [out] CLSID * pClsid);
    HRESULT GetMarshalSizeMax([in] REFIID riid,
        [in, unique] void * pv,
        [in] DWORD dwDestContext,
        [in, unique] void * pvDestContext,
        [in] DWORD mshlflags,
        [out] DWORD * pSize);
    HRESULT MarshalInterface([in, unique] IStream * pStm,
        [in] REFIID riid,
        [in, unique] void * pv,
        [in] DWORD dwDestContext,
        [in, unique] void * pvDestContext,
        [in] DWORD mshlflags);
    HRESULT UnmarshalInterface([in, unique] IStream * pStm,
        [in] REFIID riid, [out] void ** ppv);
    HRESULT ReleaseMarshalData([in, unique] IStream * pStm);
    HRESULT DisconnectObject([in] DWORD dwReserved);
}
```

自定义封送处理的优点在于，你可以从多种进程间或网络通信协议中进行选择，包括但不限于 Microsoft RPC、命名管道、TCP（流）、UDP（数据报）和 HTTP。相比之下，标准封送处理仅使用 Microsoft RPC。

下一个示例使用文件 I/O 和同步事件在代理与服务器对象之间执行封送处理（参见图 11.2）。在此示例中，我创建了三个组件来演示自定义封送处理：一个 ATL 对象服务器、一个 ATL 代理和一个 Win32 客户端。

### 图 11.2
自定义代理。

![](img/112c2326f49d26b8d59aa054e14c5747_306_0.png)

ATL 对象服务器比实际需要的更复杂，因为我实现了大量不必要的代码。例如，完全没必要实现 IMyInterface 接口，因为实际实现方法调用的是封送器。为了便于阅读，我实现了该 COM+ 对象。图 11.2 中的 COM+ 对象被划掉，以表明没有理由在服务器中实现该 COM+ 对象。

