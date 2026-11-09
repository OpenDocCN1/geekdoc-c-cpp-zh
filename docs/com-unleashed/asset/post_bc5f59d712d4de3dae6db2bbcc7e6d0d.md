
equivalent C++. The heart of this project is the controller executable that constructs, calls, and deletes objects of various types and reports on the milliseconds that it takes to construct, call, and delete these objects. Listing 9.1 shows all the code in this executable.

## LISTING 9.1 Controller Source Code

```cpp
// controller.cpp : Defines the entry point for the console application.

#include "stdafx.h"
#include "../cpp/cpp.h"
#include "../dcom/dcom.h"
#include "../dcom/dcom_i.c"
#include "../dcomserver/dcomserver.h"
#include "../dcomserver/dcomserver_i.c"

CRITICAL_SECTION cs;

DWORD WINAPI CppThread(void * p)
{
    DWORD dw = ::GetTickCount();
    for (int j=0;j<(int)((DWORD *)p)[0];j++)
    {
        CCpp * c = new CCpp();
        c->Hello();
        delete c;
    }
    dw = ::GetTickCount() - dw;
    ::EnterCriticalSection(&cs);
    std::cout << "\nCppThread ticks " << dw << std::endl;
    ::LeaveCriticalSection(&cs);
    return 0;
};

static IClassFactory * pclassfactory = NULL;
HRESULT GetUnknown(CLSID clsid, REFIID riid, IUnknown ** ppUnknown)
{
    if (pclassfactory==NULL)
    {
        ::CoGetClassObject(clsid, CLSCTX_ALL, NULL, IID_IClassFactory,
                           (void **) &pclassfactory);
        if (pclassfactory == NULL )
            return (-1);
    }
    pclassfactory->CreateInstance(NULL, riid, (void **)ppUnknown);
    return S_OK;
};

DWORD WINAPI DComThreadServer(void * p)
{
    ::CoInitialize(NULL);
    DWORD dw = ::GetTickCount();
    for (int j=0;j<*(DWORD *)p;j++)
    {
        ITestServer * i;
        GetUnknown(CLSID_TestServer, IID_ITestServer, (IUnknown **)&i);
        i->Hello();
        i->Release();
    }
    pclassfactory->Release();
    pclassfactory=NULL;
    dw = ::GetTickCount() - dw;
    ::EnterCriticalSection(&cs);
    std::cout << "\nDComThread server ticks " << dw << std::endl;
    ::LeaveCriticalSection(&cs);
    ::CoUninitialize();
    return 0;
};

DWORD WINAPI DComThread(void * p)
{
    ::CoInitialize(NULL);
    DWORD dw = ::GetTickCount();
    for (int j=0;j<*(DWORD *)p;j++)
    {
        ITestObject * i;
        GetUnknown(CLSID_TestObject, IID_ITestObject, (IUnknown **)&i);
        i->Hello();
        i->Release();
    }
    pclassfactory->Release();
    pclassfactory=NULL;
    dw = ::GetTickCount() - dw;
    ::EnterCriticalSection(&cs);
    std::cout << "\nDComThread ticks " << dw << std::endl;
    ::LeaveCriticalSection(&cs);
    ::CoUninitialize();
    return 0;
};

DWORD WINAPI DComThreadServer2(void * p)
{
    ::CoInitialize(NULL);
    DWORD dw = ::GetTickCount();
    for (int j=0;j<*(DWORD *)p;j++)
    {
        ITestServer * i;
        GetUnknown(CLSID_TestServer, IID_ITestServer, (IUnknown **)&i);
        i->Hello();
        i->Release();
    }
    pclassfactory->Release();
    pclassfactory=NULL;
    dw = ::GetTickCount() - dw;
    ::EnterCriticalSection(&cs);
    std::cout << "\nOld DComThread server ticks " << dw << std::endl;
    ::LeaveCriticalSection(&cs);
    ::CoUninitialize();
    return 0;
};

DWORD WINAPI DComThread2(void * p)
{
    ::CoInitialize(NULL);
    DWORD dw = ::GetTickCount();
    for (int j=0;j<(*(DWORD *)p);j++)
    {
        ITestObject * i;
        GetUnknown(CLSID_TestObject, IID_ITestObject, (IUnknown **)&i);
        i->Hello();
        i->Release();
    }
    pclassfactory->Release();
    pclassfactory=NULL;
    dw = ::GetTickCount() - dw;
    ::EnterCriticalSection(&cs);
    std::cout << "\nOld DComThread ticks " << dw << std::endl;
    ::LeaveCriticalSection(&cs);
    ::CoUninitialize();
    return 0;
};

int main(int argc, char* argv[])
{
    ::InitializeCriticalSection(&cs);
    DWORD dw=0;
    DWORD times=10000;
    HANDLE handle;

    handle = ::CreateThread(NULL, 0, DComThread2, &times, 0, &dw);
    ::WaitForSingleObject(handle, INFINITE);
    ::CloseHandle(handle);

    handle = ::CreateThread(NULL, 0, DComThreadServer2, &times, 0, &dw);
    ::WaitForSingleObject(handle, INFINITE);
    ::CloseHandle(handle);

    handle = ::CreateThread(NULL, 0, DComThread, &times, 0, &dw);
    ::WaitForSingleObject(handle, INFINITE);
    ::CloseHandle(handle);

    handle = ::CreateThread(NULL, 0, DComThreadServer, &times, 0, &dw);
    ::WaitForSingleObject(handle, INFINITE);
    ::CloseHandle(handle);

    handle = ::CreateThread(NULL, 0, CppThread, &times, 0, &dw);
    ::WaitForSingleObject(handle, INFINITE);
    ::CloseHandle(handle);

    ::DeleteCriticalSection(&cs);

    return 0;
}
```

The controller simply creates five different threads to test the five different types of objects. The five objects are native C++ objects (Thread), in-process one-threading model (DComThread), out-of-process one-threading model (DComThreadServer), in-process mixed-threading model (DComThread2), and out-of-process mixed-threading model (DComThreadServer2).

The executable demonstrates how in-process COM+ servers that use a threading model different than the client's threading model are nearly as slow as out-of-process COM+ servers, as shown in both Table 9.1 and Figure 9.1. This is because COM+ is marshaling calls between the apartments.

**Table 9.1. Comparison of Clock Ticks for 350MHz Pentium**

| Thread | Ticks |
|---|---:|
| Old DComThread | 73556 |
| Old DComThread server | 78984 |
| DComThread | 200 |
| DComThread server | 76320 |
| CppThread | 10 |

![](img/112c2326f49d26b8d59aa054e14c5747_232_0.png)

**FIGURE 9.1**  
*The results of running the controller program.*

The lesson here is that in order to run at reasonable speeds, your in-process COM+ servers must have the same threading model as the calling client. Unfortunately, it is not always possible to have the same threading model as all calling clients. Or is it? COM+ has conveniently provided the capability to specify an in-process COM+ server as being both single-threaded and multithreaded. In order for your in-process COM+ server to be capable of both single-threaded and multithreaded use, you must ensure that the COM+ classes in this server are thread-safe.

So, to maximize the speed of your in-process COM+ server, you must specify in the registry that it is capable of being both single-threaded and multithreaded, and it must also be thread-safe.

I've explained some optimizations that, when applied correctly, can greatly increase the speed of your application. But hundreds of other optimizations are out there. The best way to help you optimize is to describe what is going on underneath the hood and hope that you can use this information to find optimizations for your own applications.

I'll begin by explaining how the D (distributed) works in DCOM. How does COM+ provide for remote activation, reference counting, pinging, marshalling, and all that jazz?

## Remote Activation

The Service Control Manager (SCM) is responsible for launching local and remote COM+ servers. The SCM launches remote COM+ servers using the IRemoteActivation interface. Listing 9.2 shows the definition of the IRemoteActivation interface.

## LISTING 9.2 Interface Definition of IRemoteActivation

```cpp
interface IRemoteActivation
{
    HRESULT RemoteActivation(
        [in] handle_t                  hRpc,
        [in] ORPCTHIS                 *ORPCTHIS,
        [out] ORPCTHAT                *ORPCThat,
        [in] GUID                     *Clsid,
        [in, string, unique] WCHAR    *pwszObjectName,
        [in, unique] MInterfacePointer *pObjectStorage,
        [in] DWORD                     ClientImpLevel,
        [in] DWORD                     Mode,
        [in] DWORD                     Interfaces,
        [in, unique_size_is(Interfaces)] IID *pIIDs,
        [in] unsigned short            cRequestedProts,
        [in, size_is(cRequestedProts)]
             unsigned short            RequestedProts[],
        [out] OXID                    *pOxid,
        [out] DUALSTRINGARRAY         **ppdsaOxidBindings,
        [out] IPID                    *pipidRemUnknown,
        [out] HRESULT                 *pAuthnHint,
        [out] COMVERSION              *pServerVersion,
        [out] HRESULT                 *phr,
        [out, size_is(Interfaces)] MInterfacePointer **ppInterfaceData,
        [out,size_is(Interfaces)] HRESULT *pResults
};
```

The SCM on the client machine calls the SCM on the server machine by using this `RemoteActivate()` RPC function. The server SCM reads the `Clsid` parameter and creates a local COM object with the CLSID. The local COM object is queried for all the interfaces matching the `pIIDs` array parameter. The server SCM returns an array of marshaled interfaces (`ppInterfaceData`).

The `RemoteActivate()` RPC function also returns an interface pointer identifier (IPID). IPIDs are similar to interface pointers, except that they also identify the server where the object behind this interface is active. The returned `pipidRemUnknown` parameter is the IPID of the `IRemUnknown` interface of the object. The `IRemUnknown` interface is described later in this chapter.

The `MInterfacePointer` structure contains the marshaled interface pointers that are returned to the client machine. The SCM on the client machine can now refer to the remote object by using the returned data structures.

## Remote Reference Counting

How many times does an application call the `IUnknown::AddRef()` and `IUnknown::Release()` methods? How many ants live in North America? Because COM+ uses the `IUnknown::AddRef()` and `IUnknown::Release()` methods to perform reference counting, it would be a drain on performance if you waited one network cycle every time
