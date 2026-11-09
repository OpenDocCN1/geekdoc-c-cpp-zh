```
```cpp
COM_INTERFACE_ENTRY(IMyClass)
COM_INTERFACE_ENTRY(IDispatch)
END_COM_MAP()

// IMyClass
public:
};
```
```

# Using an Object with Persistence

The next thing to do is create a client application that uses the PersistClass1 control. The example on the CD is named PersistClient. (It's in the Chapter03 directory under the PersistClient subdirectory.)

The PersistClient application is a simple MFC single-document program. The only code that was added can be found in the view class's constructor and destructor. A few member variables were added to the .h file, and they can be seen in Listing 4.6.

```
Listing 4.6  PersistClient1View.h—Member Variables Used for Persistent Storage

BOOL m_bCoInitialized;
IUnknown *m_pUnknown;
IPersistStreamInit *m_pPersistStreamInit;
IStream *m_pStream;
```

At runtime, the program goes through a predictable set of steps to initialize and load the control. These steps can be seen in Listing 4.7 as calls to CoInitialize(), CoCreateInstance(), and QueryInterface() methods are made.

The first code to make note of is the call to CreateStreamOnHGlobal(). This creates an IStream object that uses memory to which it reads and writes. This IStream object can then be used with the control's Load() and Save() methods.

Before doing the save, the InitNew() method is called so that the control is set to its default properties.

The code in the destructor simply cleans up everything. The IStream, IPersistStreamInit, and IUnknown objects are all released. CoUninitialize() is called for the final clean up. The CLSID below can be found in the .rgs file.

```
Listing 4.7  PersistClient1View.cpp—Constructor and Destructor Implementing In-Memory Persistent Storage

const CLSID CLSID_PersistClass1 =
    {0x3373305b, 0xd350, 0x11d3, {0x8d, 0x44,
```