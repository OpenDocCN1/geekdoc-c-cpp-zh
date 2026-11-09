# **LISTING 13.4**  Continued

```
DECLARE_REGISTRY_RESOURCEID(IDR_MYOBJECT)

BEGIN_COM_MAP(CMyObject)
    COM_INTERFACE_ENTRY(IMyObject)
    COM_INTERFACE_ENTRY(IDispatch)
END_COM_MAP()

// IMyObject
public:
    STDMETHOD(get_MyProperty)(/*[out, retval]*/ long *pVal);
};

#endif // _MYOBJECT_H
```

# **LISTING 13.5**  Simple Local Server Object Implementation

```
// MyObject.cpp : implementation of CMyObject
#include "stdafx.h"
#include "MyProject.h"
#include "MyObject.h"

////////////////////////////////////////////
// CMyObject

STDMETHODIMP CMyObject::get_MyProperty(long *pVal)
{
    // TODO: Add your implementation code here
    *pVal = 10;

    return S_OK;
}
```

The previous code is not created by the developer but by the Wizard. The only code you must write yourself is the *pVal = 10 to the CMyObject::get_MyProperty() method in Listing 13.5.

Listing 13.3 is the IDL source for MyProject.dll. In it, you can see the interface declaration.

Listing 13.4 contains the declaration for the CMyObject class. This is the class that implements the IMyObject interface. You can see the CComSingleThreadModel class as well.

Listing 13.5 shows the implementation code for the CMyObject class. There isn’t much to it because there’s only a single method, which acts as a property get method.