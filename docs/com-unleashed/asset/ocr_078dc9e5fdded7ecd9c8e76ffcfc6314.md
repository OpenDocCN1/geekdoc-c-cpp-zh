```
LPCTSTR lpServiceName, // pointer to name of service to start
DWORD dwDesiredAccess // type of access to service
);

BOOL StartService(
    SC_HANDLE hService, // handle of service
    DWORD dwNumServiceArgs, // number of arguments
    LPTSTR *lpServiceArgVectors // array of argument strings
);
```

# Manipulating Services

After you have a handle to the service and the service is started, you can call the ControlService() and the QueryServiceStatus() functions to pause, unpause, stop, and query the status of the service. Listing 10.12 shows an example of using both of these functions to stop a service.

# **LISTING 10.12** Stop a Service Example

```
void StopService(const char * szServiceName)
{
    SC_HANDLE handle = ::OpenSCManager(NULL, NULL, SC_MANAGER_ALL_ACCESS);
    SC_HANDLE hService = ::OpenService(handle, szServiceName,
                                        SERVICE_ALL_ACCESS);
    SERVICE_STATUS servicestatus;
    ::QueryServiceStatus(hService, &servicestatus);
    if (servicestatus.dwCurrentState == SERVICE_RUNNING)
    {
        if( ::ControlService(hService, SERVICE_CONTROL_STOP, &servicestatus) )
        {
            // Handle situation where service did not stop.
        }
    }
    ::CloseServiceHandle(hService);
    ::CloseServiceHandle (handle);
}
```

You can also use the ControlService() function to send the proprietary messages discussed earlier in this chapter to the ServiceCtrlHandlers() function.

# Installing Services via the Registry

In order to install a service on a machine, you must add a few values under the HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services key in the registry.