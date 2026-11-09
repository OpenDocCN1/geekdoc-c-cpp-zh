
## 清单 24.5 续

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

这些导入元素将被导入到 MSMQ 命名空间。如果你存在一些潜在名称冲突，这会很方便。

## .tlh 文件

mqoa.tlh 文件包含类型库中信息的 C++ 等价内容。当然，这意味着你不能包含原始 COM+ 示例中使用的预生成 mqoa.h 头文件，因为它包含相同的信息。此处 #import 指令的优点是，即使你将目标代码升级到较新版本，它也始终会生成匹配的类型信息。这与最新版 Visual C++ 随附的静态头文件不同。当然，你也可以使用这种方法在原始 COM+ 应用程序中包含接口和 GUID 定义；正如你所预料的，这是一种趋势。.tlh 文件还包含指向每个已定义 COM+ 类的智能指针的定义。以下是 mqoa.tlh 头文件中生成的与 MSMQQueueInfo 相关的声明示例。

### 接口声明

下面这行代码来自 mqoa.tlh 文件，它声明了一个 MSMQ 组件接口：

```cpp
struct __declspec(uuid("d7d6e07b-dccd-11d0-aa4b-0060970debae"))
/* dual interface */ IMSMQQueueInfo;
```

这是 IMSMQQueueInfo COM+ 接口的声明。这个声明的精妙之处在于，uuid declspec 让你能在编译器层面把 GUID 关联到接口。由于这不是预处理器语句，你还可以避免原始 COM+ 应用程序的 INTGUID 场景中讨论过的潜在重复 GUID 定义。

### 类声明

下面这行代码来自 mqoa.tlh 文件，它声明了一个 MSMQ 组件类：

```cpp
struct /* coclass */ MSMQQueueInfo;
```

这是 MSMQQueueInfo 类的声明。这里没有意外之处。

### 智能指针声明

下面这行代码来自 mqoa.tlh 文件，它声明了一个 MSMQ 组件接口智能指针：

```cpp
_COM_SMARTPTR_TYPEDEF(IMSMQQueueInfo, __uuidof(IMSMQQueueInfo));
```

如果展开这行代码所调用的一整套并不简单的定义和模板，你会发现它创建了一个功能强大的接口指针包装器。这些智能指针包装器处理了接口操作中涉及的大多数未知问题。智能指针还会为标准方法上失败的 HRESULT 生成异常，从而简化接口的错误处理操作。请注意，uuidof 关键字用于检索前一个声明中附加到接口的 GUID。在本应用程序中，你将看到若干使用智能指针的代码块。

使用智能指针时，偶尔会遇到一个陷阱。使用位于实际源代码层之下的一套复杂预生成代码，始终存在固有风险；也就是说，这些代码在幕后生成，因此编译器可见，而你不可见。这种危险在你没有仔细检查宏和模板的情况下尤其明显。最常见的困难是，源代码看起来做一件事，而生成的代码实际上做另一件事。由于智能指针实现的是 COM+ 接口的客户端一侧，试图覆盖智能指针的部分行为并不是一个特别有吸引力的解决方案。智能指针提供了一些危险的运算符重载，它们可能在 IUnknown::AddRef() 和 IUnknown::Release() 调用方面做出错误假设。这是反对使用智能指针的少数常见论据之一。

### 接口定义

.tlh 文件中的下一个代码块是接口定义块。清单 24.6 是 IMSMQQueueInfo 接口定义的示例。

### 清单 24.6  IMSMQQueueInfo 接口

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
