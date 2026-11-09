# LISTING 11.9 Continued

```
```cpp
return hresult;
}

IMarshalClass * pmc;
hresult = GetInterface(punkUnknown, IID_IMarshalClass,
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
```

If you run Listing 11.9 before registering the proxy stub, the call to `IUnknown::QueryInterface()` will return 0x80004002 or E_NOINTERFACE. This is somewhat misleading because the interface exists, but the interface cannot be marshaled between processes. If you've already registered your proxy stub and want to unregister the proxy stub, run the Regsvr32 utility with the /U parameter. After you register your proxy-stub DLL, the code in Listing 11.9 should run without error. Additional standard marshaling code is available on the CD-ROM that accompanies this book. It can be found in the marshaling subdirectory in the chapter11 directory.

# Custom Marshaling

Generally, it is acceptable to use standard marshaling, but there are times when a more efficient custom marshaler is required. A good example of when you would want to use custom marshaling is when you are passing a value or when something is read-only and will never change. In these cases, there is no need to call the real object anymore since the proxy has stored its state. An object can implement custom marshaling by exposing an IMarshal interface. Listing 11.10 shows the definition of the IMarshal interface.

# LISTING 11.10  Definition of the IMarshal Interface

```
```cpp
interface IMarshal : IUnknown
{
    HRESULT GetUnmarshalClass([in] REFIID riid,
        [in, unique] void * pv,
        [in] DWORD dwDestContext,
        [in, unique] void * pDestContext,
```
```