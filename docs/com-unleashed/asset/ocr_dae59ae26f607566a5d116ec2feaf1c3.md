# LISTING 10.8  Continued

```
```cpp
// This provides a NULL DACL which will allow access to everyone.
CSecurityDescriptor sd;
sd.InitializeFromThreadToken();
hr = CoInitializeSecurity(sd, 1, NULL, NULL,
    RPC_C_AUTHN_LEVEL_PKT, RPC_C_IMP_LEVEL_IMPERSONATE, NULL,
    EOAC_NONE, NULL);
_ASSERT(SUCCEEDED(hr));

hr = _Module.RegisterClassObjects(CLSCTX_LOCAL_SERVER,
                                  CLSCTX_REMOTE_SERVER,
                                  REGCLS_MULTIPLEUSE);
_ASSERT(SUCCEEDED(hr));

LogEvent(_T("Service started"));
if (m_bService)
    SetServiceStatus(SERVICE_RUNNING);

MSG msg;
while (GetMessage(&msg, 0, 0, 0))
    DispatchMessage(&msg);

_Module.RevokeClassObjects();

CoUninitialize();
}

////////////////////////////////////////////////////////////
//
// extern "C" int WINAPI _tWinMain(HINSTANCE hInstance,
//     HINSTANCE /*hPrevInstance*/, LPTSTR lpCmdLine, int /*nShowCmd*/)
{
    lpCmdLine = GetCommandLine(); // this line necessary for _ATL_MIN_CRT
    _Module.Init(ObjectMap, hInstance, IDS_SERVICENAME,
                 &LIBID_ATLMYATLSERVICELib);
    _Module.m_bService = TRUE;

    TCHAR szTokens[] = _T("-/");

    LPCTSTR lpszToken = FindOneOf(lpCmdLine, szTokens);
    while (lpszToken != NULL)
    {
        if (lstrcmpi(lpszToken, _T("UnregServer")) == 0)
            return _Module.UnregisterServer();

        // Register as Local Server
        if (lstrcmpi(lpszToken, _T("RegServer")) == 0)
            return _Module.RegisterServer(TRUE, FALSE);

        // Register as Service
```
```