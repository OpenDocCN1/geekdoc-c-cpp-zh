
### **LISTING 24.6** Continued

```cpp
void PutPathName (
    _bstr_t bstrPathName );
_bstr_t GetFormatName ( );
void PutFormatName (
    _bstr_t bstrFormatName );
short GetIsTransactional ( );

...

HRESULT Create (
    VARIANT * IsTransactional = &vtMissing,
    VARIANT * IsWorldReadable = &vtMissing );
HRESULT Delete ( );
IMSMQQueuePtr Open (
    long Access,
    long ShareMode );
HRESULT Refresh ( );
HRESULT Update ( );

//
// Raw methods provided by interface
//

virtual HRESULT __stdcall get_PathName (
    BSTR * pbstrPathName ) = 0;
virtual HRESULT __stdcall put_PathName (
    BSTR bstrPathName ) = 0;
virtual HRESULT __stdcall get_FormatName (
    BSTR * pbstrFormatName ) = 0;
virtual HRESULT __stdcall put_FormatName (
    BSTR bstrFormatName ) = 0;
virtual HRESULT __stdcall get_IsTransactional (
    short * pisTransactional ) = 0;

...

virtual HRESULT __stdcall raw_Create (
    VARIANT * IsTransactional = &vtMissing,
    VARIANT * IsWorldReadable = &vtMissing ) = 0;
virtual HRESULT __stdcall raw_Delete ( ) = 0;
virtual HRESULT __stdcall raw_Open (
    long Access,
    long ShareMode,
    struct IMSMQQueue ** ppq ) = 0;
virtual HRESULT __stdcall raw_Refresh ( ) = 0;
virtual HRESULT __stdcall raw_Update ( ) = 0;
};
```

Note that raw property accessors take the form get_PathName() and put_PathName(). The generated header also provides for equivalent wrapper methods taking the names GetPathName() and PutPathName(), respectively. As you can see, the wrapper routines look more like standard functions than low-level COM+ calls.

Another advantage provided by smart pointers is the introduction of optional call parameters. Raw COM+ interfaces do not present default or named parameters in C++. Smart pointer method declarations reintroduce optional parameters. The following IMSMQQueuePtr::Receive() method example demonstrates this:

```cpp
IMSMQMessagePtr IMSMQQueuePtr::Receive(
    VARIANT * Transaction = &vtMissing,
    VARIANT * WantDestinationQueue = &vtMissing,
    VARIANT * WantBody = &vtMissing,
    VARIANT * ReceiveTimeout = &vtMissing );
```

Also note that the VARIANT vtMissing, which has a runtime type of VT_ERROR, is defined to represent fields that you are not interested in supplying.

## .tli Files

The big difference between raw MSMQ COM+ programming and ATL-style MSMQ COM+ programming revolves around the use of smart pointers and the wrapper functions previously declared. Wrapper functions are defined in .tli files. The mqoa.tli file contains wrapper routines similar to the following:

```cpp
inline _bstr_t IMSMQQueueInfo::GetLabel () {
    BSTR _result;
    HRESULT _hr = get_Label(&_result);
    if (FAILED(_hr)) _com_issue_error(_hr, this, __uuidof(this));
    return _bstr_t(_result, false);
}
```

One of the strengths of these wrapper routines is that they reduce the functional error-management overhead by converting failed HRESULTs into exceptions that can be managed in a structured way. The smart pointers implement similar behavior for stock COM+ calls like CoCreateInstance(), which is invoked by the smart pointer constructor method among others.

## ATL Dependencies

Although the smart pointer templates and generated wrappers fall under the blanket of ATL technology, they don’t really make use of the official ATL template library. ATL is, in general, the preferred mechanism for COM+ application construction in C++. You’re really just writing a COM+ client application in these examples, but if you’re going to buy into the smart pointer thing, you’ll find other efficiencies in ATL proper that complement the approach. In order to simplify the application, I’ll make use of the ATL CComBSTR class instead of using raw BSTRs. Basic ATL dependencies are resolved by including `atlbase.h` as follows.

```cpp
#include <atlbase.h>
```

## Creating a Queue

You’ll need to get an interface pointer to a MSMQQueueInfo object in order to create a queue. In the current example, you’ll use smart pointers for this task. Smart pointers have the same name as the interface that they wrap, with the addition of a Ptr suffix. Smart pointers encapsulate various basic COM+ behaviors such as calls to CoCreateInstance() as well as error management. You can also do away with the several Release() calls of the previous example because the smart pointer destructors handle it for you. Furthermore, you can avoid some of the BSTR allocation and free business by using the CComBSTR ATL class.

```cpp
try
{
    //Set up queue information using a smart pointer
    IMSMQQueueInfoPtr pQIInfo(L"MSMQ.MSMQQueueInfo");
    pQIInfo->PutPathName(L"\\BasicQueue");

    //Create the queue
    pQIInfo->Create();

    //Display format name
    CComBSTR FormatName;
    FormatName.Attach( pQIInfo->GetFormatName() );
    wprintf(L"Queue created with format name: ");
    wprintf(L"%s\n", BSTR(FormatName));
}
catch (_com_error &e)
{
    wprintf(L"Error creating queue: %x\n\n", e.Error());
}
```

Notice the way the preceding code distills the essence of the CreateQueue() function behavior presented in the previous raw COM+ example. All the error management is handled in a structured fashion using a catch block and the _com_error class. All the routines discussed in the following paragraphs operate within a similar try block, although the code has been omitted for brevity. As you are working with COM+ at a higher level of abstraction, you will also migrate to ProgIDs, MSMQ.MSMQQueueInfo, from the previous usage of CLSIDs. This is simply a preference as opposed to a requirement.

## Destroying a Queue

As in previous examples, the destroy behavior is pretty straightforward:

```cpp
//Setup queue information using a smart pointer
IMSMQQueueInfoPtr pQInfo(new MSMQQueueInfo);
pQInfo->PutPathName(L"\\\\.\\Private$\\BasiqueQueue");

//Destroy the queue
pQInfo->Delete();
wprintf(L"Queue destroyed\n\n");
```

## Opening a Queue

Opening a queue with smart pointers is almost as easy as opening a queue with the MSMQ Library API. All you need to do is get an interface pointer to a MSMQQueueInfo object, set the pathname in the Info object, and call the IMSMQQueueInfo::Open() method. An IMSMQQueuePtr smart pointer object receives the interface pointer returned by the open call.

```cpp
//Setup queue information using a smart pointer
IMSMQQueueInfoPtr pQInfo(new MSMQQueueInfo);
pQInfo->PutPathName(L"\\\\.\\Private$\\BasiqueQueue");

//Open the queue
IMSMQQueuePtr pQueue =
             pQInfo->Open(MQ_SEND_ACCESS, MQ_DENY_NONE);
```

## Sending a Message

Sending a message with smart pointers involves setting up a MSMQMessage object and sending it to the target MSMQQueue object. Listing 24.7 demonstrates sending a message with standard label and body properties.

### **LISTING 24.7** Sending a Message with Standard Label and Body Properties

```cpp
//Set up message label
static int s_MessageNumber = 0;      //Message label counter
WCHAR wcsLabel[MSGLABELSIZE];         //Message label buffer
swprintf(wcsLabel,L"Message number %d", s_MessageNumber);

//Set up message body
WCHAR wcsBody[MSGBODYSIZE];
CComBSTR MessageBody;
VARIANT vtBody;
wprintf(L"Enter message body: ");
_getws(wcsBody);
MessageBody.Attach(SysAllocString(wcsBody));

vtBody.vt = VT_BSTR;
vtBody.bstrVal = BSTR(MessageBody);

//Set up the message and send it
IMSMQMessagePtr pMsg("MSMQ.MSMQMessage");
pMsg->PutLabel(wcsLabel);
pMsg->PutBody(vtBody);
pMsg->Send( pQueue );
wprintf(L"Message sent!\n\n");
```

## Receiving a Message

Receiving a message with smart pointers is actually easier than sending one. Once again, you will need to create a MSMQMessage object. In receive mode, you use the IMSMQQueue::Receive() method to retrieve the message:

```cpp
//Set up the message and receive it
IMSMQMessagePtr pMsg("MSMQ.MSMQMessage");
VARIANT vtTimeout;
vtTimeout.vt = VT_I4;
vtTimeout.lVal = 0;
pMsg = pQueue->Receive( &vtMissing,
                        &vtMissing,
                        &vtMissing,
                        &vtTimeout );
wprintf(L"Retrieved message label:\n\t%s\n",
        (const wchar_t *)pMsg->Label);
wprintf(L"Retrieved message body:\n\t%s\n\n",
        (pMsg->Body).bstrVal );
```

Notice that you can use vtMissing to take the place of ignored arguments leading up to our field of interest, which is the timeout value. Because you want nonblocking behavior, you supply a four-byte integer variant with a value of zero. Note that C++ allows you to completely leave out trailing parameters that you're not interested in. As you can see, the smart pointer property accessors make this block of code very easy to put together. I should mention the fragile nature of your last print statement. You are making the strong assumption that the message body is a BSTR. You could avoid the danger inherent in assumptions by simply checking the variant type to be sure that it is a BSTR.

![](img/112c2326f49d26b8d59aa054e14c5747_650_0.png)

## Closing a Queue

As you might expect, there's nothing to do here, but I'm a fan of symmetry. The smart pointer destructors handle the entire shutdown behavior involved with releasing interface pointers.
