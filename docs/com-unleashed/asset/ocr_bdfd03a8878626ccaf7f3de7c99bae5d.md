receives the IStream in which I saved the OBJECTMARSHALDATA structure. The proxy retrieves the data from the IStream object and saves the data of this structure in local storage for later use. The proxy class declaration is almost identical to the object class declaration.

Listing 11.13 shows the definition of the proxy class.

# **Listing 11.13**  Definition of the Proxy Class

```
```cpp
// marshalproxy.cpp: Implementation of CProxyApp and DLL
// registration.

#include "stdafx.h"
#include "proxy.h"
#include "marshalproxy.h"
#include "..\\Object\\bObject_i.c"
#include "..\\Object\\bObject_iinterface.h"
#include <fstream>

////////////////////////////////////////////////////////////
//

STDMETHODIMP marshalproxy::get_propertyone(long * pVal)
{
    ATLTRACE(_T("marshalproxy::get_propertyone\n"));

    std::ifstream is;
    is.open(m_szFilename, std::ios_base::in |
                         std::ios_base::binary);
    is >> *pVal;
    is.close();

    return S_OK;
}

STDMETHODIMP marshalproxy::get_propertytwo(long * pVal)
{
    ATLTRACE(_T("marshalproxy::get_propertytwo\n"));

    std::ifstream is;
    is.open(m_szFilename, std::ios_base::in |
                         std::ios_base::binary);

    is >> *pVal;
    is >> *pVal;
    is.close();

    return S_OK;
}
```
```