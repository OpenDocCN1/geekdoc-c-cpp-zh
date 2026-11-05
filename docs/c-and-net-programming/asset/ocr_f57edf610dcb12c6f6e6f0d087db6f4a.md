AppDomainManager register, InitializeNewDomain() is implemented so that the flags are set to tell the CLR to register new application domains with unmanaged host. It illustrated in below code,

```
public override void InitializeNewDomain(AppDomainSetup appDomainInfo)
{
    // let the unmanaged host know about the application
    InitializationFlags = AppDomainManagerInitializationOptions.RegisterWithHost;
}
```

+   - With that set application will get a call into the IHostControl::SetAppDomainManager() method for each application domain that's created. For additional hosting powers one need to create an interface for communicating between unmanaged host and the managed AppDomainManager, and possibly one for communicating back the other way.
+   - When the .NET runtime starts inside a native process, that native application becomes a host for the runtime. This adds .NET capabilities to the native applications.

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
hr = pMetaHost->GetRuntimeVersion, IID_PPV_ARGS(&pRuntimeInfo));
hr = pRuntimeInfo
>GetInterface(CLSID_CLRRuntimeHost,IID_PPV_ARGS(&pRuntimeHost));
hr = pRuntimeHost->Start();
```

+   - Now the runtime is running, but it hasn't got any loaded user code yet. Some internal thread scheduler and garbage collector are surely running, because they are part of the CLR runtime.

# 26.3.2 Hosting the CLR in Managed app - Running Managed Code

+   - To start a managed app from the host, below code can be written,
+   - AppDomain.CurrentDomain.ExecuteAssembly(assemblyName);