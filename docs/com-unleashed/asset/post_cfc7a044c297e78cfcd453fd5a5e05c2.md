
## LISTING 24.3 Continued

```c
aMsgPropId[1] = PROPID_M_BODY;
aMsgPropVar[1].vt = VT_VECTOR | VT_UI1;
aMsgPropVar[1].caub.pElems = (LPBYTE)(wcsBuf);
aMsgPropVar[1].caub.cElems = (wcslen(wcsBuf) + 1) * sizeof(WCHAR);

//Set up the body type
aMsgPropId[2] = PROPID_M_BODY_TYPE;
aMsgPropVar[2].vt = VT_UI4;
aMsgPropVar[2].ulVal = VT_BSTR;

//Set up message property struct
MsgProps.cProp = 3;                //Number of properties
MsgProps.aPropID = aMsgPropId;     //Ids of properties
MsgProps.aPropVar = aMsgPropVar;   //Values of properties
MsgProps.aStatus = NULL;           //No error reports

//Send message
MQSendMessage( hQueue,           //Queue handle
               &MsgProps,        //Message properties
               NULL );           //Transaction

//Check results
if ( FAILED(hr) )
    wprintf(L"Error sending message: %x\n\n",hr);
else
    wprintf(L"Message sent!\n\n");

//Close queue
MQCloseQueue(hQueue);
}

void ReceiveMessage()
{
    //Get the format name of the queue using the pathname
    HRESULT hr;                         //Return status
    WCHAR wcsFormatName[FORMATNAMESIZE]; //Queue format name
    DWORD dwFormatNameLen = FORMATNAMESIZE; //Size of format name
    hr = MQPathNameToFormatName( QUEUEPATHNAME,
                                 wcsFormatName,
                                 &dwFormatNameLen );

    //Check results
    if ( FAILED(hr) )
    {
        wprintf(L"Error looking up queue format name: %x\n\n",hr);
        return;
    }

    //Open the queue with send access
    QUEUEHANDLE hQueue;                 //Handle to queue
    hr = MQOpenQueue( wcsFormatName,       //Queue format name
                      MQ_RECEIVE_ACCESS,   //Access requested
                      MQ_DENY_NONE,        //Share mode
                      &hQueue);            //Queue handle

    //Check results
    if ( FAILED(hr) )
    {
        wprintf(L"Error opening queue: %x\n\n",hr);
        return;
    }

    //Allocate message property objects
    MQMSGPROPS MsgProps;                  //Message properties struct
    MSGPROPID aMsgPropId[4];              //Message property id array
    PROPVARIANT aMsgPropVar[4];           //Message property value array

    //Set up message label and length
    WCHAR wcsLabel[MSGLABELSIZE];          //Message label buffer
    aMsgPropId[0] = PROPID_M_LABEL;
    aMsgPropVar[0].vt = VT_LPWSTR;
    aMsgPropVar[0].pwszVal = wcsLabel;
    aMsgPropId[1] = PROPID_M_LABEL_LEN;
    aMsgPropVar[1].vt = VT_UI4;
    aMsgPropVar[1].ulVal = MSGLABELSIZE;

    //Set up message body and length
    WCHAR wcsBody[MSGBODYSIZE];            //Message body buffer
    aMsgPropId[2] = PROPID_M_BODY;
    aMsgPropVar[2].vt = VT_VECTOR | VT_UI1;
    aMsgPropVar[2].caub.pElems = (LPBYTE)wcsBody;
    aMsgPropVar[2].caub.cElems = MSGBODYSIZE * sizeof(WCHAR);
    aMsgPropId[3] = PROPID_M_BODY_SIZE;
    aMsgPropVar[3].vt = VT_UI4;
    aMsgPropVar[3].ulVal = MSGBODYSIZE;

    //Set up message property struct
    MsgProps.cProp = 4;                   //Number of properties
    MsgProps.aPropID = aMsgPropId;        //IDs of properties
    MsgProps.aPropVar = aMsgPropVar;      //Values of properties
    MsgProps.aStatus = NULL;              //No error reports

    //Get first message
    hr = MQReceiveMessage(    hQueue,      //Queue to receive from
                              0,           //Timeout
                              MQ_ACTION_RECEIVE, //Receive or peek
                              &MsgProps,   //Message properties
                              NULL,        //Overlapped structure
                              NULL,
                              NULL,
                              NULL );

    //Check results
    if ( FAILED(hr) )
    {
        wprintf(L"Error receiving message: %x\n\n",hr);
        MQCloseQueue(hQueue);
        return;
    }

    //Display message
    wcsBody[ (aMsgPropVar[3].ulVal)/sizeof(WCHAR) ] = L'\0';
    wprintf(L"Retrieved message label:\n\t%s\n",wcsLabel);
    wprintf(L"Retrieved message body:\n\t%s\n\n",wcsBody);

    //Close queue
    MQCloseQueue(hQueue);
}

void DestroyQueue()
{
    //Get the format name of the queue using the pathname
    HRESULT hr;                                //Return status
    WCHAR wcsFormatName[FORMATNAMESIZE];       //Queue format name
    DWORD dwFormatNameLen = FORMATNAMESIZE;    //Size of format name
    hr = MQPathNameToFormatName( QUEUEPATHNAME,
                                 wcsFormatName,
                                 &dwFormatNameLen );

    //Check results
    if ( FAILED(hr) )
    {
        wprintf(L"Error looking up queue format name: %x\n\n",hr);
        return;
    }

    //Destroy queue
    hr = MQDeleteQueue(wcsFormatName);

    //Check results
    if ( FAILED(hr) )
        wprintf(L"Error destroying queue: %x\n\n",hr);
    else
        wprintf(L"Queue destroyed\n\n");
}
```

## The MSMQ ActiveX Control API

ActiveX components are a distribution mechanism for COM+ class behavior operating behind COM+ interfaces in the context of dynamically constructed COM+ objects. That means the behavior of MSMQ ActiveX components is well encapsulated, and the way it was developed has nothing to do with the way it is used. In Visual C++ alone, there are several ways to make use of the MSMQ components, including raw COM+ interfaces, Class Wizard dispatch wrappers, and ATL-style smart pointers. A multitude of additional techniques is available in other languages. For example, you’ll try three different approaches: raw COM, smart pointers with ATL, and finally a Visual Basic script to ensure low-level programming humility.

The first example using the MSMQ ActiveX components will use raw COM+ interfaces. All COM+ components expose COM+ interfaces. COM+ consumers, on the other hand, can use any level of abstraction available in programming against COM+ objects. The lowest and, often, the most powerful approach is to use the COM+ interfaces directly. This usually means quite a bit of work for the developer, along with several easy-to-step-into snares. For example, a script using an object doesn’t have to remember to release the object; the scripting engine takes care of that. A low-level COM+ interface developer who fails to release an interface pointer has a resource leak on his hands.

As you’ve probably determined by now, this is a hard-core COM+ book, so of course it looks at the bottom layer of things. Even if you decide to adopt one of the other styles of MSMQ development presented here, the ensuing discussion of what’s going on beneath the covers will probably make your high-level efforts that much easier.

Your second COM+ cut at the “Hello World” MSMQ application will be with the Active Template Library–derived smart pointer technique. C++ developers have always enjoyed the power of their language but at the same time have envied the ease with which many applications, especially those related to COM, could be constructed in higher-level environments like Visual Basic. ATL has made serious inroads in simplifying the C++ COM+ programming model. ATL has also become more than just a set of templates you can use for common coding tasks. Visual C++ 5 featured the #import statement, which provided the capability to generate “compilable” (is that a word?) type information directly from a COM+ component on-the-fly. Visual C++ 6 improves the studio and debugging tools that work with ATL. Perhaps the most exciting ATL-derived technology is the attribute COM+ programming technique to be introduced with Visual C++ 7. Attributes such as coclass (for automatically turning a C++ class into a COM+ class by generating ATL-based code during the build process) are quite enticing. In the second MSMQ ActiveX component example, you’ll take a look at how much easier COM+ programming can be using smart pointers and a bit of ATL.

In the final example, you'll write a Visual Basic script that performs the same behavior as the previous applications. No, it isn't there to depress you. You know that it's well worth typing a few extra lines of code to gain performance in a critical application with an extended life span. But what about a system administrator who needs to glue some ad hoc stuff into his enterprise? Or how about presenting a scriptable message-based interface to your server-side application without writing any client proxies? In these contexts, a Visual Basic script would make the most sense. This final example will complete our high-level view of MSMQ programming.

### MSMQ ActiveX Classes

There are 10 different COM+ classes in the MSMQ ActiveX component set. There are also 10 additional objects dedicated to the MSMQ email support. This might seem like a lot compared to the meager 26 total functions in the MSMQ library API. The important thing to remember about a good COM+ programming model is that it simplifies the process of development by modeling the entities in the system, not necessarily by reducing the total object count. It's much easier to understand and work with a set of objects that map directly to the mechanisms in the problem domain rather than work with a smaller set of arbitrarily reduced components with nonintuitive interfaces. This is especially the case when working with high-level programming systems that have trouble dealing with more than one interface per object, such as VBScript. In fact, the MSMQ ActiveX component set has been tailored to fit well into any programming environment, particularly those at higher levels.

MSMQ COM+ classes all begin with the MSMQ prefix. Each MSMQ COM+ class supplies one dual interface named for the class with the traditional I prefix. A basic application like yours will require the use of three of the MSMQ classes and their subordinate interfaces:

- `MSMQQueueInfo` — `IMSMQQueueInfo`
- `MSMQQueue` — `IMSMQQueue`
- `MSMQMessage` — `IMSMQMessage`

The first class is MSMQQueueInfo. This object type is used to create and destroy queues and also to open existing queues. The next class you will work with is the MSMQQueue class. The queue class is used to represent actual queues (instances of queues) in the MSMQ system providing support for browsing and retrieving messages from queues. The final class in the introductory suite is the MSMQMessage class. MSMQMessage instances are used to represent individual messages that are sent or received through the queue objects.
