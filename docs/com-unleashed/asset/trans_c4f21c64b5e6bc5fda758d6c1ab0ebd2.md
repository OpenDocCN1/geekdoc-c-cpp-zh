
```cpp
BSTR bstrPathName;
bstrPathName = SysAllocString(L".\\BasicQueue");
pQInfo->put_PathName(bstrPathName);
SysFreeString(bstrPathName);
hr = pQInfo->Open( MQ_SEND_ACCESS, MQ_DENY_NONE, &pQueue );
pQInfo->Release();
```

### 发送消息

为了向队列发送消息，你需要获取三个独立对象的接口指针。一个用于打开队列的 MSMQQueueInfo 对象，一个用于发送消息的 MSMQMessage 对象，以及一个用于表示消息的 MSMQMessage 对象。你的应用程序需要创建一条带有标签和文本正文的消息来发送。正如你可能猜到的，这是通过创建消息对象并设置其属性来完成的。下面是一个示例：

```cpp
//Get an interface pointer to a message object
IMSMQMessage * pMsg;
    hr = CoCreateInstance( CLSID_MSMQMessage,
                           NULL,
                           CLSCTX_SERVER,
                           IID_IMSMQMessage,
                           (LPVOID *)&pMsg );
```

```cpp
//Set up message label
static int s_cMessageNumber = 0;                 //Message label counter
WCHAR wcsLabel[MSGLABELSIZE];                     //Message label buffer
swprintf(wcsLabel,L"Message number %d", ++s_cMessageNumber);
BSTR bstrLabel = SysAllocString (wcsLabel);
pMsg->put_Label (bstrLabel);
SysFreeString(bstrLabel);
```

```cpp
//Set up message body
WCHAR wcsBody[MSGBODYSIZE];
wprintf(L"Enter message body: ");
_getws(wcsBody);
BSTR bstrBody = SysAllocString(wcsBody);
VARIANT varBody;
varBody.vt = VT_BSTR;
varBody.bstrVal = bstrBody;
pMsg->put_Body(varBody);
```

最后一步是将消息传输到目标队列。IMSMQMessage::Send() 方法需要一个指向目标队列的接口指针和事务信息。在下一章之前，你不会使用事务，因此可以简单地传入一个 FALSE 布尔类型变体。请注意，在使用 C++ 进行原生 COM+ 级别编程时，即使 COM+ 在更高级编程环境中支持可选参数，你也必须提供所有方法参数。下面是 IMSMQMessage::Send() 调用的示例：

```cpp
//Send message
VARIANT varTransactional;
varTransactional.vt = VT_BOOL;
varTransactional.boolVal = FALSE;
hr = pMsg->Send( pQueue, &varTransactional );
    pQueue->Release();
    pMsg->Release();
    SysFreeString(bstrBody);
```

### 接收消息

接收消息总是比发送消息稍微困难一些，因为可能存在未知的缓冲区大小等情况。与 IMSMQMessage::Send() 方法不同，Receive() 方法是 IMSMQQueue 接口的成员。检索消息的第一步是打开一个用于接收访问的队列：

```cpp
//Setup queue info path & get interface pointer to queue
IMSMQQueue * pQueue;
BSTR bstrPathName;
bstrPathName = SysAllocString(L".\\BasicQueue");
pQInfo->put_PathName(bstrPathName);
SysFreeString(bstrPathName);
hr = pQInfo->Open( MQ_RECEIVE_ACCESS, MQ_DENY_NONE, &pQueue );
pQInfo->Release();
```

IMSMQQueue::Receive() 方法接受多个参数。第一个参数指定事务状态，你同样会将其设置为 false。第二个参数设置一个 IMSMQQueueInfo 接口指针，用于描述返回的消息对象中原始消息的目标队列。这样就能确定从死信队列或其他此类队列中检索到的消息的原始目标。第三个参数指定是否检索消息正文。第四个参数是超时值，它指定函数是等待消息还是立即返回。最后但同样重要的是，必须提供返回消息对象的接口指针。

消息对象提供各种有用的属性。接收调用超时严格来说并不被视为错误。如果没有可用消息，IMSMQMessage 接口指针参数将被设置为 NULL。因此，在使用消息接口指针之前，应检查其值是否为 NULL。清单 24.4 是一个简单的非阻塞同步接收场景示例。

![](img/112c2326f49d26b8d59aa054e14c5747_634_0.png)

**清单 24.4** 一个简单的非阻塞同步接收

**清单 24.4** 续

```cpp
//Receive message using nonblocking synchronous call
IMSMQMessage * pMsg;
VARIANT varTransaction;
varTransaction.vt = VT_BOOL;
varTransaction.boolVal = FALSE;
VARIANT varWantDestQueue;
varWantDestQueue.vt = VT_BOOL;
varWantDestQueue.boolVal = FALSE;
VARIANT varWantBody;
varWantBody.vt = VT_BOOL;
varWantBody.boolVal = TRUE;
VARIANT varTimeout;
varTimeout.vt = VT_I4;
varTimeout.lVal = 0;
hr = pQueue->Receive(
                    &varTransaction,
                    &varWantDestQueue,
                    &varWantBody,
                    &varTimeout,
                    &pMsg );

pQueue->Release();

//Get message label
BSTR bstrLabel;
pMsg->get_Label( &bstrLabel );
wprintf(L"Retrieved message label: \n\t%s\n", bstrLabel);
SysFreeString(bstrLabel);

//Get message body
VARIANT varBody;
pMsg->get_Body( &varBody );
wprintf(L"Retrieved message body:\n\t%s\n", varBody.bstrVal );
VariantClear(&varBody);

//Release message object
pMsg->Release( );
```

### 关闭队列

正如你在前面的示例中可能已经注意到的，MSMQ 并没有定义显式机制来关闭队列或任何其他对象。当然，这种行为已经以 IUnknown::Release() 的形式内置到 COM+ 中。MSMQ ActiveX 对象接口的最终释放会使其执行任何必要的关闭操作。因此，从 COM+ 的角度来看，关闭队列就像这样简单：

```cpp
pQueue->Release();
```

如你所见，与直接使用 MSMQ API 相比，原生 COM+ 的 MSMQ 编程方法可能略显繁琐。直观的编程模型是这种方法最重要的优势。随着应用程序变得更大、更分布式，COM+ 提供的好处将会增加。当你沿着 COM+ 客户端食物链向上移动时，COM+ MSMQ 角度在编程上也会显著更容易。

在清单 24.5 中，你会注意到大量错误处理代码。API 开发的函数式方法通常要求检查每个返回值。此应用程序也不例外，但我在操作属性的 put 和 get 方法方面做了一个例外。这些确实是函数调用，可能会失败，但添加额外检查会损失清晰性，因此我将它们省略了，因为整个代码的其他地方有许多 HRESULT 检查示例。在进程内对象上获取和设置属性是相当可靠的事情，但真正的生产系统绝不应采取这种捷径。清单 24.5 展示了原生 COM+ MSMQ “Hello World” 应用程序的完整代码。

**清单 24.5** MSMQ 原生 COM+ 编程示例

**清单 24.5** 续

```cpp
// HelloMsmq.cpp
//
// Simple MSMQ Raw COM+ application


//MSMQ ActiveX component header
// ( We need to define INITGUID to force the definition
//    of the MSMQ GUIDs )
#define INITGUID


//Standard Dependencies
#include <windows.h>
#include <stdio.h>
#include <conio.h>
#include <mqoa.h>


//Symbols
#define MSGBODYSIZE       128
#define MSGLABELSIZE      64
#define QUEUEPATHNAME     L".\\BasicQueue"


//Prototypes
void CreateQueue();
void SendMessage();
void ReceiveMessage();
void DestroyQueue();


//Application entry point

int main()
{
    int iChoice;                  //User input buffer

    //Initialize COM
    CoInitializeEx(NULL, COINIT_APARTMENTTHREADED);

    //User command processing loop
    do
    {
        //Display menu
        wprintf(L"Choose a command:\n");
        wprintf(L"0 - Exit\n");
        wprintf(L"1 - Create the Queue\n");
        wprintf(L"2 - Send a Message\n");
        wprintf(L"3 - Receive a Message\n");
        wprintf(L"4 - Destroy the Queue\n");
        wprintf(L"\n>> ");

        //Get selection
        iChoice = getch();
        wprintf(L"%c\n", iChoice);

        //Execute command
        switch ( iChoice )
        {
        case '0':
            break;

        case '1':
            CreateQueue();
            break;

        case '2':
            SendMessage();
            break;

        case '3':
            ReceiveMessage();
            break;

        case '4':
            DestroyQueue();
            break;

        default:
            wprintf(L"Bad choice.\n\n");
            break;
        }
```

