```
```cpp
CreateFileMoniker();
HRESULT CreateFileMoniker(
        [in, string] const OLECHAR *pszFileName,
        [out] IMoniker **pmk);
```
```

If the persistent object has already registered its File Moniker in the ROT, `CoGetInstanceFromFile()` simply returns a pointer to the already running object. If the object is not found in the ROT, COM+ creates a new instance of the file’s class and initializes it from the persistent image via the instance’s `IPersistFile::Load()` method, as seen in Listing 5.5.

# **LISTING 5.5**  The IPersistFile Interface Declaration

```
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
```

It’s the responsibility of the object implementation to load any persistent state from the file as well as to register itself with the local ROT to ensure that only one instance per file is running at a time. This can be seen in Listing 5.6.

# **LISTING 5.6**  Loading the Persistent State

```
```cpp
STDMETHODIMP Example::Load(const OLECHAR *pszFileName,
                           DWORD grfMode)
{
// read in persistent state
  HRESULT hr = this->MyReadStateFromFile(pszFile, grfMode);
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
```