The newly created instance's IPersistFile::Load() method will be called by the SCM during the execution of CoGetInstanceFromFile(). The previous example uses the COM+ API function GetRunningObjectTable() to get an IRunningObjectTable interface pointer into the SCM. It then uses this interface to register its moniker in the ROT so that subsequent calls to CoGetInstanceFromFile() using the same filename won't fail when creating new objects, but will return references to this object.

The file moniker exists for two reasons. One reason is to allow objects to register themselves in the ROT so that CoGetInstanceFromFile() can find them. The second reason is to hide the use of CoGetInstanceFromFile() from the client behind the IMoniker interface. The file moniker's implementation of BindToObject() simply calls CoGetInstanceFromFile(), as seen in Listing 5.7.

# Listing 5.7 The Implementation of BindToObject()

```
~~~
// pseudo-code from OLE32.DLL
STDMETHODIMP FileMoniker::BindToObject(IBindCtx *pbc,
    IMoniker *pmkToLeft,
    REFIID riid, void **ppv) {
// assume failure
*ppv = 0;
HRESULT hr = E_FAIL;
if (pmkToLeft == 0) { // no moniker to left
    MULTI_QI mqi = { &riid, 0, 0 };
    COSERVERINFO *pcsi;
    DWORD grfMode;
    DWORD dwClsCtx;
// these three parameters are attributes of the BindCtx
    this->MyGetFromBindCtx(pbc, &pcsi, &grfMode, &dwClsCtx);
    hr = CoGetInstanceFromFile(pcsi, 0, 0, dwClsCtx,
        grfMode, this->m_pszFileName,
        1, &mqi);
    if (SUCCEEDED(hr))
        *ppv = mqi.pItf;
    }
    else { // there's a moniker to the left
// ask object to left for IClassActivator
// or IClassFactory
    }
    return hr;
}
~~~
```

Given the behavior of the file moniker, the function in Listing 5.8 that calls CoGetInstanceFromFile():