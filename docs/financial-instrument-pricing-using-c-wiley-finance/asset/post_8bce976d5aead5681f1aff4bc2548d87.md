
A simple test program based on the above code is:

```
// Client
int main()
{
    CA* pA = new CA;

    // Get an IDraw pointer.
    IDraw* pd = pA;

    std::cout << "Client: Use the IDraw interface.";
    pd->display();
    pd->print();

    // Get an ISave pointer.
    ISave* ps = pA;

    std::cout << "Client: Use the ISave interface.";
    ps->saveXML();
    ps->saveDB();

    delete pA;

    return 0;
}
```

In general, each method in an interface can have input, output and input/output parameters as well as a return type. In the above simple example the methods had no input parameters and they all had a void return type.

## 14.9.1 COM Interfaces and COM Objects

We now discuss two important concepts in COM, namely COM interfaces and COM objects. COM interfaces are special in a number of ways. We need to discuss a number of issues which will help us achieve a good understanding of how to define, discover and use these interfaces and objects.

Each system that supports COM must include an implementation of the COM library. The library contains groups of functions that provide basic services to objects and to their clients. For example, it contains functionality for clients to start an object’s server. The COM library’s services are accessed through ordinary function calls.

An interface is essentially a contract between an object that implements the interface and clients of the object. In order to make the contract work between the object and client we must address the following issues:

- A1: A way to explicitly identify an interface.
- A2: How to describe (define) the methods in an interface.
- A3: How to actually implement an interface.

Regarding activity A1, there are two ways to identify an interface. The first way is to identify the interface by a string name which humans find easy to read while the second way uses a 16-byte (128-bit) *Globally Unique Identifier* (GUID) to identify the interface in software. GUIDs are guaranteed to be unique in space and time and the chance is extremely small that two interfaces (or other entities in COM) will be assigned the same value. In the case of interfaces the unique identifier is called an *interface identifier* (IID). The next challenge is to have some *global clearinghouse* that keeps track of all names (including interface identifiers). This clearinghouse is called the *Registry* and it is the shared system database for the Windows operating system. It contains information about system hardware, software, configuration and users.

A COM component maintains a number in its state called the *reference count*. This count is incremented when a client gets an interface and it is decremented when the client is finished using the interface. Each interface must support the IUnknown interface, which has three methods:

- `QueryInterface`: the client can call this method to discover whether a component supports a particular interface. A pointer to the interface will be returned if the component supports the interface.
- `AddRef`: increments the reference count on the interface.
- `Release`: releases a reference to the interface.

The developer must implement IUnknown and its *reference counting mechanism* is similar to how both C++11 and the *Boost Smart Pointer* library automatically manage the lifetime of heap-based objects. The precise specification for IUnknown is:

```
interface IUnknown
{
    virtual HRESULT QueryInterface( [in] IID& iid, [out] void** ppv) =0;
    virtual ULONG AddRef(void) =0;
    virtual ULONG Release(void) =0;
};
```

We see that `QueryInterface` has two arguments: the first input parameter `iid` is the identifier for an interface that we wish to determine if it is supported and the second argument `ppv` is set to NULL before the call to `QueryInterface`. If the call succeeds we get a pointer to `ppv` and we can then call its methods. Notice that we can specify parameters as input or output parameters.

## 14.9.2 HRESULT and Other Data Types

Components use the 32-bit field HRESULT to communicate with clients. Its structure is shown in Figure 14.8. For example, it can signal success or failure when a method is called. Most COM functions return this integer as return type.

![](img/fe10f87cc5d3cff29b178c4d9a6e3012_477_0.png)

*FIGURE 14.8 Format of HRESULT*

The possible return types are:

- `E_ABORT`: the operation was aborted because of an unspecified error.
- `E_ACCESSDENIED`: a general access-denied error.
- `E_FAIL`: an unspecified failure has occurred.
- `E_HANDLE`: an invalid handle was used.
- `E_INVALIDARG`: one or more arguments are invalid.
- `E_NOINTERFACE`: the QueryInterface method of the interface IUnknown did not recognise the requested interface. The interface is not supported.
- `E_NOTIMPL`: the method is not implemented.
- `E_OUTOFMEMORY`: the method failed to allocate memory.
- `E_PENDING`: the data necessary to complete the operation is not yet available.
- `E_POINTER`: an invalid pointer was used.
- `E_UNEXPECTED`: a catastrophic failure occurred.
- `S_FALSE`: the method succeeded and returned the Boolean value FALSE.
- `S_OK`: the method succeeded. If a Boolean return value is expected, the returned value is TRUE.

We can check the return type in code by calling the macros SUCCEEDED and FAILED as the following examples show:

```
HRESULT hr = SetStrings ();
if (FAILED (hr))
    return hr;
```

```
HRESULT hr2 = PropBag->Read();
if (SUCCEEDED(hr2))
{
    // code
}
```

It is advisable to use these macros when testing a method’s return value instead of comparing the result hr against the raw values; however, it is allowed to use these values as return types in code, for example:

```
HRESULT FinalConstruct()
{
    return S_OK;
}
```

## 14.9.3 Interface Definition Language

COM supports a tool that allows us to define interfaces in a standard way. It is called *Interface Definition Language* (IDL) and it is an extension of the IDL in Microsoft’s *Remote Procedure Call* (RPC) which is based on the IDL in the Open Software Foundation’s *Distributed Computing Environment* (OSF DCE). IDL describes a COM object’s interfaces in an unambiguous manner. It allows us to associate the methods of an interface with its IID. We can also specify the details of the interface in a form that can be machine processed to produce marshalling code when we create *dynamic link libraries* (DLLs):

```
// Interface IDraw
[
    object,                         // 1.
    uuid(D6FCCE1F-8A2D-4303-A974-09AEC422EFFE),  // 2.
    helpstring("My drawing interface"),          // 3.
    pointer_default(unique)                         // 4.
]

interface IDraw : IUnknown
{
    HRESULT draw();
};
```

## 14.9.4 Class Identifiers

A COM object is an instance of some class. Each class is assigned a GUID called a *class identifier* (CLSID). A client can pass a CLSID to the COM library to create an instance of the class. However, this is not mandatory. The primary use of a CLSID is to identify a specific piece of code for the COM library to load and execute for instances of the class corresponding to the CLSID.

## 14.10 AN EXAMPLE

We give a simple example to show how to define both COM interfaces and COM objects. We focus on the language issues that we have discussed. In this case we define interfaces and a class that implements one of them. The interface definitions are:

```
// Interfaces
interface IDraw : IUnknown
{
    virtual void __stdcall display() = 0;
};

interface ISave : IUnknown
{
    virtual void __stdcall save() = 0;
};
```

The corresponding generated IDs are:

```
// IIDs
//
// {32bb8320-b41b-11cf-a6bb-0080c7b2d682}
static const IID IID_IDraw =
    {0x32bb8320, 0xb41b, 0x11cf,
    {0xa6, 0xbb, 0x0, 0x80, 0xc7, 0xb2, 0xd6, 0x82}};

// {32bb8321-b41b-11cf-a6bb-0080c7b2d682}
static const IID IID_ISave =
    {0x32bb8321, 0xb41b, 0x11cf,
    {0xa6, 0xbb, 0x0, 0x80, 0xc7, 0xb2, 0xd6, 0x82}};
```

We now create a class called MyClass that implements IDraw that we defined earlier in Section 14.9; notice that this class must also implement the methods of IUnknown:

```
//
// Component
//
class MyClass : public IDraw
{
public:
    // IUnknown implementation
    virtual HRESULT __stdcall QueryInterface(const IID& iid, void** ppv) ;

    virtual ULONG __stdcall AddRef() ;
    virtual ULONG __stdcall Release() ;

    // Interface IDraw implementation
    virtual void __stdcall display() { cout << "display" << endl ;}

    // Constructor
    MyClass() : m_cRef(0) {}

    // Destructor
    ~MyClass() { std::cout << "Bye, bye\n";}

private:
    long m_cRef;
};
```

The implementation of this component is:

```
HRESULT __stdcall MyClass::QueryInterface(const IID& iid, void** ppv)
{
    if (iid == IID_IUnknown)
    {
```
