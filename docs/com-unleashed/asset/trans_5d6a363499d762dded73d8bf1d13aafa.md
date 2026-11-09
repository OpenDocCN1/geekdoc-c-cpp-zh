

## 使用原始 COM+ 接口构建 MSMQ 应用程序

使用原生 COM+ 调用构建 COM+ 应用程序，可以带来许多此前已有文档记载的强大 COM+ 优势。当然，它也会带来维护 COM+ 接口通用性、必需的 IUnknown 特性以及各种初始化和关闭问题的开销。好处在于，你只需学习一次 COM+，而它所应对的问题会在无数编程场景中反复出现。因此，不再赘述，你将使用原生 COM 构建一个 MSMQ 应用程序。

你的 COM+ 应用程序版本不需要在项目设置中进行任何显式链接调整。毕竟，COM+ 编程的标志之一就是动态接口解析。接下来注意，你需要根据打算如何解决问题，向编译器提供不同的支持。在低级 COM+ 示例中，你需要包含由 MSMQ 组件类型库生成的头文件。该头文件是 MQOA.H，随 Visual C++ 提供。该头文件定义了访问 MSMQ COM+ 对象所需的各种接口和类 ID。

### 定义接口和 GUID

有一个“陷阱”。MQOA.H 头文件可以独立使用，因为它包含了其他必要的 COM+ 元素。这些间接包含的头文件中最重要的之一是 objbase.h。问题在于，MQOA.H 中定义的 GUID 看起来像这样：

```cpp
DEFINE_GUID(IID_IMSMQMessage, 0xD7D6E07B,
  0x0CCD, 0x11D0, 0xA0, 0x48, 0x00, 0x60, 0x97, 0x0D, 0xEB, 0x0A);
```

在头文件中通过语句定义内容——也就是实际分配存储空间——可能导致多种链接器问题。预编译头文件的使用使问题有些复杂。因此，objbase.h 使用以下语句定义 DEFINE_GUID：

```cpp
#ifndef INITGUID
#define DEFINE_GUID(name, l, w1, w2, b1, b2, b3, b4, b5, b6, b7, b8) \
    EXTERN_C const GUID FAR name
#else

#define DEFINE_GUID(name, l, w1, w2, b1, b2, b3, b4, b5, b6, b7, b8) \
    EXTERN_C const GUID name = { l, w1, w2, { b1, b2, b3, b4, b5, b6, b7, b8 } }
#endif // INITGUID
```

如你所见，必须恰好定义一次 INITGUID 才能生成实际的 GUID。如果未能定义 INITGUID，最终会出现对所有 MSMQ GUID 的未解析引用。如果在多个模块中定义它，最终会出现重复的 GUID 和更多链接器错误。你的简单应用程序位于单个源文件中，这使你能够使用以下简化的包含方式：

```cpp
// MSMQ ActiveX component header
// ( We need to define INITGUID to force the definition
//   of the MSMQ GUIDs )
#define INITGUID
#include <mqoa.h>
```

### 初始化 COM

任何超出 CoGetMalloc() 的 COM+ 使用都需要正确初始化。以下代码行设置并关闭单线程应用程序的单线程套间。除了这些新增内容外，main() 例程在其他方面与前一示例相同。调用 CoInitialize() 的效果与调用 CoInitializeEx() 相同。

```cpp
// Initialize COM
CoInitializeEx(NULL, COINIT_APARTMENTTHREADED);

//body of main function
...

//Uninitialize COM+ and return success
CoUninitialize();
```

不过，在现代 COM+ 开发中，CoInitialize() 已被弃用。如果编译对 CoInitializeEx() 的调用时遇到问题，可以尝试定义符号 _WIN32_DCOM。CoInitializeEx() 的条件声明基于 _WIN32_DCOM 符号，或基于 _WIN32_NT 中大于等于 0x0400 的值。例如，NT 5 beta 2 在 CoInitializeEx() 方面存在问题，只需将 _WIN32_DCOM 加入项目符号列表（Project[Settings] 的 C/C++ 选项卡）即可解决。

### 创建队列

要创建队列，需要获取指向 MSMQQueueInfo 对象的 IMSMQQueueInfo 接口的指针。MSMQQueueInfo 接口提供 Create() 方法，用于创建新队列。由于你已从函数式 API 迁移到面向组件的接口，属性和对象亲和性将在本应用程序所需的代码中发挥重要作用。特别是，值通常作为各种对象类型的属性来设置和检索，而不是使用查询函数调用。以下是对 CoCreateInstance() 的示例调用，它将为你提供所需的对象和接口：

```cpp
//Get an interface pointer to a QueueInfo object
HRESULT hr;
IMSMQQueueInfo *pQInfo;
hr = CoCreateInstance(
                         CLSID_MSMQQueueInfo,
                         NULL,
                         CLSCTX_SERVER,
                         IID_IMSMQQueueInfo,
                         (LPVOID *) &pQInfo );
```

### VARIANTS

如前所述，队列可以带有事务和/或全局属性创建。你的基本需求不需要特殊功能，因此只需设置所需路径名，并向 MSMQQueueInfo::Create() 调用传入 false 队列属性。由于 MSMQ 接口旨在支持高级应用程序编程环境，大多数方法参数将采用 BSTR 和 VARIANT 的形式。VARIANT 因支持无类型脚本环境而被自动化大量使用。VARIANT 有一个 vt 字段用于标记所存储的类型，还有一个由所有受支持的变体类型组成的联合字段。以下是设置所需变体并创建队列的代码：

```cpp
//Create a default queue
VARIANT varTransactional;
    varTransactional.vt = VT_BOOL;
    varTransactional.boolVal = FALSE;
VARIANT varWorldReadable;
    varWorldReadable.vt = VT_BOOL;
    varWorldReadable.boolVal = FALSE;
pQInfo->put_PathName(L"BasicQueue");
hr = pQInfo->Create( &varTransactional, &varWorldReadable );
```

### BSTRs

成功创建队列后，所创建队列的格式名称将作为队列信息对象的属性存储。检索格式名称需要使用 BSTR。BSTR 是 Basic（Visual Basic）格式的字符串，并且始终使用 Unicode 字符存储。BSTR 基本上是 WCHAR 指针，但有一个特别之处：所指向的第一个字符之前的两个字节用于存储字符串长度。在 COM+ 中使用 BSTR 的一个重要方面是，服务器通常为 BSTR 分配内存，而客户端应释放该内存。需要指向 BSTR 的指针的 COM+ 方法通常希望将 BSTR 缓冲区传回客户端，从而移交缓冲区的控制权。由于 BSTR 带有前缀的特性，使用系统 SysAllocString() 和 SysFreeString() 调用分配和释放它们更容易。以下是检索新创建队列格式名称的代码：

```cpp
    //Display format name
    BSTR bstrFormatName;
    pQInfo->get_FormatName(&bstrFormatName);
    wprintf(L"Queue created with format name: %s\n\n", bstrFormatName);
    SysFreeString(bstrFormatName);
```

请注意前两个代码块中用于操作 MSMQ COM+ 对象属性的 get_ 和 put_ 方法。这些是低级 COM+ 属性访问器。在你的智能指针示例中，将使用这些相同例程的包装版本，其前缀为 get 和 put。务必区分这两者，因为低级版本返回 HRESULT，而包装器抛出异常。意外异常从来都不是好事。

与许多其他更高级形式的 COM+ 编程不同，在这种底层细节中，你需要确保在完成使用后释放所有接口指针。释放 IMSMQQueueInfo 接口指针即可完成 CreateQueue() 函数：

```cpp
    //Release the QueueInfo object
    pQInfo->Release();
```

### 销毁队列

销毁队列在过程上几乎与创建队列完全相同。只需创建一个 MSMQQueueInfo 对象，设置目标队列路径名，然后调用 MSMQQueueInfo::Delete() 方法。下面是一个示例。

```cpp
    //Setup queue info path & destroy queue
    BSTR bstrPathName;
    bstrPathName = SysAllocString(L".\\BasicQueue");
    pQInfo->put_PathName(bstrPathName);
    SysFreeString(bstrPathName);
    hr = pQInfo->Delete();
    pQInfo->Release();
```

### 打开队列

为了发送和接收消息，需要打开目标队列。给定路径名，MSMQQueueInfo 对象将为你提供获取队列接口指针的方法。队列将表示为 MSMQQueue 对象。创建 MSMQQueueInfo 对象后，调用 IMSMQQueueInfo::Open() 方法；如果成功，该方法会将其最后一个参数作为队列接口指针返回。MSMQQueue 类提供了一个方便的 Handle 属性，可以方便地脱离 COM+ 世界，以便使用仅通过 MSMQ API 函数可用的功能。下面是一个示例：

```cpp
    //Setup queue info path & get interface pointer to queue
    IMSMQQueue * pQueue;
```

