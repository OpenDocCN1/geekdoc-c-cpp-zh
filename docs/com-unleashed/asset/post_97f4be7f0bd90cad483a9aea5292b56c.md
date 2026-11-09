

## LISTING 24.5 Continued

```cpp
} while ( iChoice != '0' );

//Uninitialize COM+ and return success
CoUninitialize();
return 0;
}

void CreateQueue()
{
    //Get an interface pointer to a QueueInfo object
    HRESULT hr;
    IMSMQQueueInfo * pInfo;
    hr = CoCreateInstance( CLSID_MSMQQueueInfo,
                           NULL,
                           CLSCTX_SERVER,
                           IID_IMSMQQueueInfo,
                           (LPVOID *)&pInfo );

    //Check result
    if ( FAILED( hr ) )
    {
        wprintf(L"Error creating queue info object: %x\n",hr);
        return;
    }

    //Create a default queue
    VARIANT varTransactional;
    varTransactional.vt = VT_BOOL;
    varTransactional.boolVal = FALSE;
    VARIANT varWorldReadable;
    varWorldReadable.vt = VT_BOOL;
    varWorldReadable.boolVal = FALSE;
    pInfo->put_PathName(QUEUEPATHNAME);
    hr = pInfo->Create( &varTransactional, &varWorldReadable );

    //Check result
    if ( FAILED(hr) )
    {
        wprintf(L"Error creating queue: %x\n",hr);
        pInfo->Release();
        return;
    }

    //Display format name
    BSTR bstrFormatName;
    pInfo->get_FormatName(&bstrFormatName);
    wprintf(L"Queue created with format name: %s\n",bstrFormatName);
    SysFreeString(bstrFormatName);
}

//Release the QueueInfo object
pQIInfo->Release();

}

void SendMessage()
{
    //Get an interface pointer to a QueueInfo object
    HRESULT hr;
    IMSMQQueueInfo * pQIInfo;
    hr = CoCreateInstance(    CLSID_MSMQQueueInfo,
                              NULL,
                              CLSCTX_SERVER,
                              IID_IMSMQQueueInfo,
                              (LPVOID *)&pQIInfo );

    //Check result
    if ( FAILED( hr ) )
    {
        wprintf(L"Error creating queue info object: %x\n\n",hr);
        return;
    }

    //Setup queue info path & get interface pointer to queue
    IMSMQQueue * pQueue;
    BSTR bstrPathName;
    bstrPathName = SysAllocString(QUEUEPATHNAME);
    pQIInfo->put_PathName(bstrPathName);
    SysFreeString(bstrPathName);
    hr = pQIInfo->Open( MQ_SEND_ACCESS, MQ_DENY_NONE, &pQueue );
    pQIInfo->Release();

    //Check queue open result
    if ( FAILED( hr ) )
    {
        wprintf(L"Error opening queue object: %x\n\n",hr);
        return;
    }

    //Get an interface pointer to a message object
    IMSMQMessage * pMsg;
    hr = CoCreateInstance(    CLSID_MSMQMessage,
                              NULL,
                              CLSCTX_SERVER,
                              IID_IMSMQMessage,
                              (LPVOID *)&pMsg );

    //Check result
    if ( FAILED( hr ) )
    {
        wprintf(L"Error creating message object: %x\n\n",hr);
        pQueue->Release();
        return;
    }

    //Set up message label
    static int csMessageNumber = 0;             //Message label counter
    WCHAR wcsLabel[MSGLABELSIZE];               //Message label buffer
    swprintf(wcsLabel,L"Message number %d", ++csMessageNumber);
    BSTR bstrLabel = SysAllocString(wcsLabel);
    pMsg->put_Label(bstrLabel);
    SysFreeString(bstrLabel);

    //Set up message body
    WCHAR wcsBody[MSGBODYSIZE];
    wprintf(L"Enter message body: ");
    _getws(wcsBody);
    BSTR bstrBody = SysAllocString(wcsBody);
    VARIANT varBody;
    varBody.vt = VT_BSTR;
    varBody.bstrVal = bstrBody;
    pMsg->put_Body(varBody);

    //Send message
    VARIANT varTransactional;
    varTransactional.vt = VT_BOOL;
    varTransactional.boolVal = FALSE;
    hr = pMsg->Send( pQueue, &varTransactional );
    pQueue->Release();
    pMsg->Release();
    SysFreeString(bstrBody);

    //Check result
    if ( FAILED(hr) )
        wprintf(L"Error sending message: %x\n\n",hr);
    else
        wprintf(L"Message sent\n\n");

}

void ReceiveMessage()
{
    //Get an interface pointer to a QueueInfo object
    HRESULT hr;
    IMSMQQueueInfo * pQIInfo;
    hr = CoCreateInstance( CLSID_MSMQQueueInfo,
                           NULL,
                           CLSCTX_SERVER,
                           IID_IMSMQQueueInfo,
                           (LPVOID *) &pQIInfo );
        }
    else if ( NULL == pMsg )
    {
        wprintf(L"No messages in queue\n");
        return;
    }

    //Get and display message label
    BSTR bstrLabel;
    pMsg->get_Label( &bstrLabel );
    wprintf(L"Retrieved message label:\n\t%s\n",bstrLabel);
    SysFreeString(bstrLabel);

    //Get and display message body
    VARIANT varBody;
    pMsg->get_Body( &varBody );
    wprintf(L"Retrieved message body:\n\t%s\n", varBody.bstrVal );
    VariantClear(&varBody);

    //Release message object
    pMsg->Release();
}

void DestroyQueue()
{
    //Get an interface pointer to a QueueInfo object
    HRESULT hr;
    IMSMQQueueInfo * pQInfo;
    hr = CoCreateInstance( CLSID_MSMQQueueInfo,
                           NULL,
                           CLSCTX_SERVER,
                           IID_IMSMQQueueInfo,
                           (LPVOID *)&pQInfo );

    //Check result
    if ( FAILED( hr ) )
    {
        wprintf(L"Error creating queue info object: %x\n\n",hr);
        return;
    }

    //Setup queue info path & destroy queue
    BSTR bstrPathName;
    bstrPathName = SysAllocString(QUEUEPATHNAME);
    pQInfo->put_PathName(bstrPathName);
    SysFreeString(bstrPathName);
    hr = pQInfo->Delete();
    pQInfo->Release();
```

the imported elements to be imported into the MSMQ namespace. This is convenient if you have some potential name conflicts.

## .tlh Files

The mqoa.tlh file contains the C++ equivalent of the information in the type library. This, of course, means that you cannot include the pregenerated mqoa.h header used in the raw COM+ example because it contains the same information. The advantage of the #import directive here is that it will always generate matching type information, even as you upgrade your target code to newer versions. This is unlike the static header shipped with the latest version of Visual C++. You can, of course, use this approach to include interface and GUID definitions in your raw COM+ applications as well, and, as you might expect, this is the trend. The .tlh file also includes definitions for smart pointers to each COM+ class defined. The following are examples of the MSMQQueueInfo-related declarations generated in the mqoa.tlh header.

### Interface Declarations

Here is a line of code from the mqoa.tlh file that declares an MSMQ component interface:

```cpp
struct __declspec(uuid("d7d6e07b-dccd-11d0-aa4b-0060970debae"))
/* dual interface */ IMSMQQueueInfo;
```

This is the declaration of the IMSMQQueueInfo COM+ interface. The beautiful part about this declaration is the way the uuid declspec enables you to wire the GUID to the interface at the compiler level. Because this is not a preprocessor statement, you also avoid the potential duplicate GUID definitions that were discussed in the INTGUID scenario of the raw COM+ application.

### Class Declarations

Here is a line of code from the mqoa.tlh file that declares an MSMQ component class:

```cpp
struct /* coclass */ MSMQQueueInfo;
```

This is the declaration of the MSMQQueueInfo class. No surprises here.

### Smart Pointer Declarations

Here is a line of code from the mqoa.tlh file that declares an MSMQ component interface smart pointer:

```cpp
_COM_SMARTPTR_TYPEDEF(IMSMQQueueInfo, __uuidof(IMSMQQueueInfo));
```

If you were to unravel the nontrivial set of defines and templates that this line of code invokes, you would discover that it creates a powerful interface pointer wrapper. These smart pointer wrappers take care of most of the unknown issues involved with interface operations. Smart pointers also simplify the error-handling operations of the interface by generating exceptions for failed HRESULTs on standard methods. Note that the uuidof keyword is used to retrieve the GUID attached to the interface in the previous declaration. You will see several blocks of code that make use of smart pointers in this application.

There is one pitfall that comes up from time to time when using smart pointers. There are always dangers inherent in using a sophisticated set of pregenerated code below your actual source level; that is, code generated behind the scenes so that it is visible to the compiler but not to you. This danger exists especially in cases in which you haven't examined the macros and templates carefully. The most popular difficulty is that the source looks as if it does one thing, and the emitted code actually does something else. Because smart pointers implement the client side of a COM+ interface, attempting to override portions of the smart pointer behavior is not a particularly compelling solution. Smart pointers provide some dangerous operator overloads that might make the wrong assumptions in regard to IUnknown::AddRef() and IUnknown::Release() calls. This is one of the few prevailing arguments against smart pointers.

### Interface Definitions

The next block of code found in the .tlh file is the interface definitions block. Listing 24.6 is an example of the definition for the IMSMQQueueInfo interface.

### LISTING 24.6  The IMSMQQueueInfo Interface

```cpp
struct __declspec(uuid("d7d6e07b-dccd-11d0-aa4b-0060970debae"))
IMSMQQueueInfo : IDispatch
{
    //
    // Property data
    //

    __declspec(property(get=GetPathName,put=PutPathName))
    _bstr_t PathName;
    __declspec(property(get=GetFormatName,put=PutFormatName))
    _bstr_t FormatName;
    __declspec(property(get=GetIsTransactional))
    short IsTransactional;
    ...

    //
    // Wrapper methods for error-handling
    //

    _bstr_t GetPathName ( );
```

