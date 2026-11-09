# LISTING 10.8  Continued

```
```cpp
if (IsInstalled())
    return TRUE;

SC_HANDLE hSCM = ::OpenSCManager(NULL, NULL, SC_MANAGER_ALL_ACCESS);

if (hSCM == NULL)
{
    MessageBox(NULL, _T("Couldn't open service manager"),
               m_szServiceName, MB_OK);
    return FALSE;
}

// Get the executable file path
TCHAR szFilePath[_MAX_PATH];
::GetModuleFileName(NULL, szFilePath, _MAX_PATH);

SC_HANDLE hService = ::CreateService(
    hSCM, m_szServiceName, m_szServiceName,
    SERVICE_ALL_ACCESS, SERVICE_WIN32_OWN_PROCESS,
    SERVICE_DEMAND_START, SERVICE_ERROR_NORMAL,
    szFilePath, NULL, NULL, _T("RPCSS\0"), NULL, NULL);

if (hService == NULL)
{
    ::CloseServiceHandle(hSCM);
    MessageBox(NULL, _T("Couldn't create service"), m_szServiceName,
               MB_OK);
    return FALSE;
}

::CloseServiceHandle(hService);
::CloseServiceHandle(hSCM);
return TRUE;
}

inline BOOL CServiceModule::Uninstall()
{
    if (!IsInstalled())
        return TRUE;

    SC_HANDLE hSCM = ::OpenSCManager(NULL, NULL, SC_MANAGER_ALL_ACCESS);

    if (hSCM == NULL)
    {
        MessageBox(NULL, _T("Couldn't open service manager"),
                   m_szServiceName, MB_OK);
        return FALSE;
    }

    SC_HANDLE hService = ::OpenService(hSCM, m_szServiceName,
```
```