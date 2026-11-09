Finally, add two methods to the ISum interface, Accumulate() and Add(). (Right-clicking the interface in the Class View window and choosing Add Method is the easiest way to do this.) Use Listing 16.1 as a guide to define and implement your Sum class methods—the header and .cpp files are provided. Note that the Accumulate() method uses an integer property named m_iTotal, which you must add to the class definition and initialize to zero in the constructor.

# LISTING 16.1  Simple COM Object Example

```
```cpp
// Sum.h : Declaration of the CSum
#include "resource.h"        // main symbols

/////////////////////////////////////////////
// CSum
class ATL_NO_VTABLE CSum :
    public CComObjectRootEx<CComSingleThreadModel>,
    public CComCoClass<CSum, &CLSID_Sum>,
    public IDispatchImpl<ISum, &IID_ISum, &LIBID_STATEFULLib>
{
public:
    CSum()
    {
        m_iTotal = 0;
    }

    DECLARE_REGISTRY_RESOURCEID(IDR_Sum)
    DECLARE_PROTECT_FINAL_CONSTRUCT()
    DECLARE_NOT_AGGREGATABLE(CSum)

    BEGIN_COM_MAP(CSum)
        COM_INTERFACE_ENTRY(ISum)
        COM_INTERFACE_ENTRY(IDispatch)
    END_COM_MAP()

    // ISum
public:
    STDMETHOD(Sum)(int iValue1, int iValue2, int *piTotal);
    STDMETHOD(Accumulate)(int iValue, int *pTotal);

    // Attributes (unmanaged state, yikes!)
private:
    int m_iTotal;
};

// Sum.cpp : Implementation of CSum
#include "stdafx.h"
#include "Stateful.h"
```
```