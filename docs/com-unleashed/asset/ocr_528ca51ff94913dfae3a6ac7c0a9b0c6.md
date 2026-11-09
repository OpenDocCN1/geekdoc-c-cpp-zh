# ## LISTING 7.7 Continued

```
```cpp
SetEvent(hEventShutdown);
// tell monitor that we transitioned to zero
}

return 1;
}
```
```

You must add the `DECLARE_CLASSFACTORY_AUTO_THREAD()` macro to your COM+ class definitions (see Listing 7.8).

# ## LISTING 7.8  Implement AUTO_THREAD() Class Factory

```
```cpp
class CATObject :
    public CComObjectRootEx<CComSingleThreadModel>,
    public CComCoClass<CATObject, &CLSID_ATObject>,
    public IDispatchImpl<IATObject, &IID_IATObject,
                        &LIBID_APARTMENTTHREADEDLIB>
{
public:
    CATObject()
    {
    }

DECLARE_REGISTRY_RESOURCEID(IDR_ATOBJECT)

DECLARE_PROTECT_FINAL_CONSTRUCT()

DECLARE_CLASSFACTORY_AUTO_THREAD()

BEGIN_COM_MAP(CATObject)
    COM_INTERFACE_ENTRY(IATObject)
    COM_INTERFACE_ENTRY(IDispatch)
END_COM_MAP()

// IATObject
public:
    STDMETHOD(get_Thread)(/*[out, retval]*/ long *pVal);
};
```
```

The apartment-threaded server exists so that legacy thread-unsafe COM+ objects can continue to exist without causing concurrency issues in these objects that are assumed to be incapable of maintaining integrity in a multithreaded environment. If you are willing to take the time to make your COM+ object thread-safe, I suggest you create your COM+ servers using the free-threaded threading model.