# LISTING 13.6  Create and Access Test Object

```
```cpp
#include <windows.h>

HRESULT LaunchAndAccess()
{
    // HRESULT returned from last automation call
    HRESULT hresult;
    // IDISPATCH interface pointer for the existing object
    LPDISPATCH pdisp = NULL;
    // hold exception info here
    EXCEPINFO excepinfo;
    // hold argument error here
    UINT uArgErr;

    // Convert the progid to a clsid
    CLSID clsid;
    hresult = ::CLSIDFromProgID(OLESTR("MyObject.MyObject.1"),
                                &clsid);
    if (hresult)
    {
        // CLSIDFromProgID failed
        return hresult;
    };

    // Create the instance of the object
    LPUNKNOWN punk;
    hresult = ::CoCreateInstance(clsid, NULL, CLSCTX_SERVER,
                                 IID_IUnknown, (LPVOID FAR *)&punk);

    if (hresult)
    {
        // CoCreateInstance failed
        return hresult;
    };

    // Retrieve the interface pointer
    hresult = punk->QueryInterface(IID_IDispatch,
                                   (LPVOID FAR *)&pdisp);

    if (hresult)
    {
        // QueryInterface failed
        return hresult;
    };

    // Release the IUnknown reference.
    hresult = punk->Release();

    // return an exception if the dispatch pointer is NULL
    if (pdisp==NULL)
    {
        return E_UNEXPECTED;
```
```