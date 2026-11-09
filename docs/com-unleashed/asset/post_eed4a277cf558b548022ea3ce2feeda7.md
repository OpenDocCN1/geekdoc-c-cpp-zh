
### LISTING 9.6 Interface Definition of ISurrogate

```cpp
interface ISurrogate : IUnknown
{
    HRESULT LoadDllServer([in] REFCLSID clsid);
    HRESULT FreeSurrogate();
}
```

The surrogate must register itself by calling the CoRegisterSurrogate() function. COM+ will call the ISurrogate::LoadDllServer() method to load a server and the ISurrogate::FreeSurrogate() method to release the surrogate.

## IClassFactory

Class factories used to be the talk of COM+. The most important interface in COM+ was the class factory. Over time, the class factory has lost its popularity because everything that needed to be said about class factories has already been said. Most COM+ frameworks implement a class’s IClassFactory class with boilerplate code hidden behind layers of macros.

The IClassFactory interface still remains central to everything that is COM+. When you create COM+ objects, as with calls to the CoCreateInstance() or CoCreateInstanceEx() functions, you are in essence calling the IClassFactory::CreateInstance() method.

You might also have noticed that COM+ DLLs export a function called DllGetClassObject(). COM+ calls this function in order to retrieve the class factories from your in-process server. Figure 9.3 depicts how COM uses DllGetClassObject() exported function and the IClassFactory classes to create a new COM object. Note how a call to the CoCreateInstance() function creates or retrieves an instance of the class factory. The class factory in turn creates the object.

Listing 9.7 is a simplified version showing how the CoCreateInstance() function uses the IClassFactory object.

### LISTING 9.7 Code Behind the CoCreateInstance() Function

```cpp
HRESULT CoCreateInstance(REFCLSID clsid, IUnknown * pUnkOuter,
    DWORD grfContext, REFIID iid, void ** ppv)
{
    IClassFactory * pCF;
    HRESULT          hr = ::CoGetClassObject(clsid, grfContext,
                         NULL, IID_IClassFactory, (void **) &pCF);

    if (FAILED(hr))
    {
        return hr;
    }

    hr = pCF->CreateInstance(pUnkOuter, iid, (void **)ppv);
    pCF->Release();

    if (FAILED(hr))
    {
        *ppv = 0;
    }

    return hr;
}
```

### FIGURE 9.3 *Class factory creating the COM object.*

![](img/112c2326f49d26b8d59aa054e14c5747_240_0.png)

The CoCreateInstanceEx() function has a similar implementation (see Listing 9.8). The CoCreateInstanceEx() function uses an array of MULTI_QI structures in order to retrieve more than one interface to the object. The code in Listing 9.8 is pseudo-code as there are some optimizations that are implemented. CoCreateInstanceEx() can also be used to choose on which server the object gets instantiated.

### LISTING 9.8 Code Behind the CoCreateInstanceEx() Function

```cpp
struct tagMULTI_QI
{
    REFIID riid;
    void * pvObj;
    HRESULT hr;
} MULTI_QI;

HRESULT CoCreateInstanceEx(REFCLSID clsid,
    IUnknown * pUnkOuter, DWORD grfContext,
    COSERVERINFO * pServerInfo, DWORD dwCount,
    MULTI_QI * rgMultiQI)
{
    IClassFactory * pCF;
    HRESULT hr = ::CoGetClassObject(clsid, grfContext,
        pServerInfo, IID_IClassFactory, (void **)&pCF);

    if (FAILED(hr))
    {
        return hr;
    }

    hr = pCF->CreateInstance(pUnkOuter, iid, (void **)ppv);
    pCF->Release();
    for (DWORD i=0; i<dwCount; i++)
        rgMultiQI[i].hr = punk->QueryInterface(rgMultiQI[i].riid,
                                  &rgMultiQI[i].pvObj);

    if (FAILED(hr))
    {
        *ppv = 0;
    }

    return hr;
}
```

With the class factory object, you can perform something that most believe is not possible in COM: implementation inheritance.

## Inheritance

COM+ enables you to use both interface and implementation inheritance. Using interface inheritance, one interface can inherit methods from another interface. An example of interface inheritance is the IDispatch interface, which inherits the QueryInterface(), AddRef(), and Release() methods from the IUnknown interface.

COM+ also enables you to use implementation inheritances. This type of inheritance enables one COM+ class to inherit an implementation from another COM+ class. Implementation inheritance is not fully implemented in COM+. That is, COM+ classes that inherit an implementation from another COM+ class do not have access to the implementation data of the inherited class. Because of this shortcoming, it is sometimes said that COM does not support implementation inheritance.

Two types of implementation inheritance are provided for in COM+: containment and aggregation. Containment inheritance is implemented by having a COM+ class reimplement the methods of the inherited class. These implementations would simply redirect calls to the contained COM+ class.

## Aggregation

Aggregation inheritance enables clients to call inherited methods directly. One disadvantage of this method is that the aggregated object's IUnknown methods must be integrated with the aggregator's IUnknown methods. Another disadvantage is that only in-process servers can implement aggregation inheritance.

Aggregation inheritance is accomplished using the IClassFactory interface. Each COM+ class, whether it can be aggregated or not, must implement a class factory object that implements the IClassFactory interface. The class factory object is responsible for creating the COM+ class. Listing 9.9 shows the definition of the IClassFactory interface.

### LISTING 9.9 Definition of the IClassFactory Interface

```cpp
interface IClassFactory : IUnknown
{
    HRESULT CreateInstance(IUnknown * pUnkOuter,
        REFIID iid, void ** ppvObj);
    HRESULT LockServer(BOOL fLock);
}
```

All COM+ objects are created by calling this IClassFactory::CreateInstance() method. If the first parameter of the call to the IClassFactory::CreateInstance() method is NULL, the object being created will not be aggregated. If this same parameter is a pointer to an IUnknown, the object being created will be aggregated and delegate all calls to its IUnknown methods to the alternate IUnknown interface.

Aggregation is a very powerful feature of COM+ that is rarely used. ATL enables you to take advantage of aggregation by writing two proxy code. In aggregation inheritance, we say that an aggregator inherits the implementation of an aggregate. You’ll need to know this to understand the next ATL code listings.

ATL classes can serve as aggregates as long as they do not define the DECLARE_NOT_AGGREGABLE macro. This makes coding aggregates easy because it requires no additional code in the aggregate. Listing 9.10 shows the class that I will be using as the aggregate. Again, no additional coding is needed to support aggregation in the aggregate.

### LISTING 9.10 Declaration of Aggregate Class

```cpp
// MyAggregate.h : Declaration of the CMyAggregate

#ifndef __MYAGGREGATE_H_
#define __MYAGGREGATE_H_

#include "resource.h"       // main symbols

/////////////////////////////////////////////////////////////////////////////
// CMyAggregate
class ATL_NO_VTABLE CMyAggregate :
    public CComObjectRootEx<CComSingleThreadModel>,
    public CComCoClass<CMyAggregate, &CLSID_MyAggregate>,
    public IDispatchImpl<IMyAggregate, &IID_IMyAggregate,
        &LIBID_AGGREGATELib>
{
public:
    CMyAggregate()
    {
    }

DECLARE_REGISTRY_RESOURCEID(IDR_MYAGGREGATE)

BEGIN_COM_MAP(CMyAggregate)
    COM_INTERFACE_ENTRY(IMyAggregate)
    COM_INTERFACE_ENTRY(IDispatch)
END_COM_MAP()

// IMyAggregate
public:
    STDMETHOD(Hello)();
};

#endif // __MYAGGREGATE_H_
```

The ATL aggregator is slightly more complex. As with the aggregate earlier, I generated a standard ATL class using the ATL object wizard and added one method called Hello. Listing 9.11 shows an aggregator class declaration.

### LISTING 9.11 Declaration of Aggregator Class

```cpp
// MyAggregator.h : Declaration of the CMyAggregator

#ifndef __MYAGGREGATOR_H_
#define __MYAGGREGATOR_H_

#include "resource.h"       // main symbols
#include "..\aggregate\aggregate.h"
```
