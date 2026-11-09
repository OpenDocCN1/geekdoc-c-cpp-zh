# # A Simple Transaction Example

To make it easy for you to understand what I’ve talked about so far, and to give you a picture of how to implement transactions in your COM+ code, I’ve written a very simple example. I made a point of keeping it as simple as possible so that you can easily understand the important points that relate to transactions.

The component was written in Visual C++ using ATL, and the client program was written in Visual Basic. Both can be found in the Chapter17\SimpleTrans directory on the CD-ROM.

Listing 17.1 shows you the important code from the COM+ component, and Listing 17.2 shows you the Visual Basic code for the client application. An explanation follows the code listings.

**LISTING 17.1** A Very Simple Transaction Component

```
```cpp
// First.cpp: Implementation of CFirst
#include "stdafx.h"
#include "SimpleTrans.h"
#include "First.h"

////////////////////////////////////////////////////////////
// CFirst

STDMETHODIMP CFirst::DoIt()
{
    AFX_MANAGE_STATE(AfxGetStaticModuleState())

    // Get the object context.
    IObjectContext *pObjectContext = NULL;
    HRESULT hRes = GetObjectContext (&pObjectContext );

    // Make sure we didn't get an error while getting
    // the object context.
    if( FAILED( hRes ) )
    {
        if( hRes == E_INVALIDARG )
            m_strTransactionResult = "Invalid argument.";
        else if( hRes == E_UNEXPECTED )
            m_strTransactionResult = "Unexpected error.";
        else if( hRes == CONTEXT_E_NOCONTEXT )
            m_strTransactionResult = "No context associated with object.";
        else
            m_strTransactionResult = "Object context could not be obtained.";
```
```