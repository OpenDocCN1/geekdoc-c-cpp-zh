# LISTING 13.13  Multiple Interface Support

```
STDMETHODIMP CCoops::InterfaceSupportsErrorInfo(REFIID riid)
{
    static const IID* arr[] =
    {
        &IID_IOops,
        &IID_IOops2
    };
    for (int i=0; i < sizeof(arr) / sizeof(arr[0]); i++)
    {
        if (InlineIsEqualGUID(*arr[i],riid))
            return S_OK;
    }
    return S_FALSE;
}
```

The implementation of the CCoops::Throw() method in Listing 13.14 simply calls the CComCoClass::Error() method and returns E_FAIL.

# LISTING 13.14  ErrorInfo Client

```
// controller.cpp : Defines the entry point for the console application.

#include "stdafx.h"

#import "..\\server\\server.tlb"

int main(int argc, char* argv[])
{
    ::CoInitialize(NULL);
    {
        SERVERLib::IOopsPtr p(__uuidof(SERVERLib::IOops));
        try
        {
            p->Throw();
        }
        catch(_com_error e)
        {
            std::cout << "Error: " << e.Error() <<
                      << (char *)e.Source() << " - "
                      << (char *)e.Description() << std::endl;
        }
    }
    ::CoUninitialize();
    return 0;
}
```