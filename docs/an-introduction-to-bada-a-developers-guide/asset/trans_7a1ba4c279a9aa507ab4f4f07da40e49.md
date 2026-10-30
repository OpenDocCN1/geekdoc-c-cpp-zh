
本配方与第5章介绍的内容服务类似，但更为详细。bada平台上的内容指的是图像、音乐、视频或开发者指定的任何其他类型的数据。创建内容需要两个步骤。第一步是将物理内容文件传输到工作区，第二步是在bada服务器上创建内容元信息。这些元信息对于bada平台能够搜索和操作工作区上的物理内容至关重要。

在使用Amazon S3工作区之前，应用程序必须在Amazon服务器上进行身份验证。我们此前在第5章中已经解释过这一过程。因此，在本配方中我们不再重复这部分内容，而是专注于内容传输本身。在本配方的所有示例代码中，我们假设您已经使用Amazon服务器对应用程序进行了身份验证。下面的代码片段展示了我们类的声明，该类包含了所需的方法和成员。

我们将类命名为`YourClassName`，它派生自`Osp::App::IAppControlEventListener`、`Osp::Content::IContentTransferListener`和`Osp::Content::IRemoteContentManagerListener`这些接口。

```cpp
class YourClassName :
    public Osp::App::IAppControlEventListener,
    public Osp::Content::IContentTransferListener,
    public Osp::Content::IRemoteContentManagerListener
{
private:
    Osp::Content::ContentTransfer* pContentTransfer;
    Osp::Content::RemoteContentInfo* pRemoteContentInfo;
    Osp::Content::RemoteContentManager* pRemoteContentManager;
    Osp::Base::Utility::Uri uri;

public:
    // 这里我们只提及相关的方法

    // 登录AppControl的回调函数
    void OnAppControlCompleted(const Osp::Base::String& appControlId,
        const Osp::Base::String& operationId,
        const Osp::Base::Collection::IList* pResultList);

    // 内容传输到工作区的回调函数
    void OnContentUploadCompleted(RequestId reqId, result r,
        const Osp::Base::String& errorCode,
        const Osp::Base::String& errorMessage);

    void OnContentTransferCanceled(RequestId reqId, result r,
        const Osp::Base::String& errorCode,
        const Osp::Base::String& errorMessage);

    void OnContentCreated(RequestId reqId,
        const Osp::Base::String& contentId, result r,
        const Osp::Base::String& errorCode,
        const Osp::Base::String& errorMessage);
};
```

在这个头文件中，`IContentTransferListener`和`IRemoteContentManagerListener`接口类中还定义了其他纯虚函数。为简洁起见，我们在此不一一列出。但在您的代码项目中，您必须实现它们，否则项目将无法构建。

在本配方中，我们只关注内容创建部分，因此我们只实现上述头文件中定义的相关回调函数。

```cpp
void
YourClassName::OnAppControlCompleted(
    const Osp::Base::String& appControlId,
    const Osp::Base::String& operationId,
    const Osp::Base::Collection::IList* pResultList)
{
    if (appControlId.Equals(APPCONTROL_SIGNIN) && operationId.Equals(
        OPERATION_SIGNIN))
    {
        AppLog("SignIn AppControl Completed");
    }
}
```

上述代码是一个检查登录步骤的示例实现。当用户首次启动应用程序并完成登录流程后，该函数会被调用。我们也可以检查登录过程的结果，以验证其是否成功。

成功登录后，我们现在可以开始将物理内容信息传输到Amazon服务器。为此，您只需要创建一个`ContentTransfer`类的实例：

```cpp
pContentTransfer = new ContentTransfer();

result r = E_SUCCESS;

// 将YourClassName作为指向IContentTransferListener的指针传递
r = pContentTransfer->Construct(*this);

if (IsFailed(r))
{
    AppLog("Failed to construct ContentTransfer: %s",
        GetErrorMessage(r));
    // 处理错误条件
}

RequestId reqId;
pContentTransfer->Upload(L"/Media/Images/sample.jpg",
    L"/Image/sample.jpg", true, uri, reqId);
```

`Upload()`方法需要五个参数：

- 设备上内容文件的源路径；
- Amazon工作区上内容文件的目标路径；
- 一个`bool`原始类型，指示是否应替换已有文件；
- URI；
- 请求ID。

```cpp
void
YourClassName::OnContentCreated(RequestId reqId,
    const Osp::Base::String& contentId, result r,
    const Osp::Base::String& errorCode,
    const Osp::Base::String& errorMessage)
{
    if (IsFailed(r))
    {
        AppLog("OnContentCreated[%s]", GetErrorMessage(r));
        AppLog("Error code: %s", errorCode.GetPointer());
        AppLog("Error message %s", errorMessage.GetPointer());
    }
    else
    {
        // 正常继续，并在此处实现您的“检查”...
    }
}
```

## 提示、陷阱及相关主题

之前我们介绍了`Osp::Content::IContentTransferListener`接口。另一个有用的方法是`OnContentTransferInProgress()`，其定义如下：

```cpp
virtual void
Osp::Content::IContentTransferListener::OnContentTransferInProgress
(RequestId reqId, int totalTransferredSize);
```

该方法被声明为纯虚函数，这意味着它必须被实现。在数据上传或下载时，这是一个非常实用的方法，可用于查询进度信息。

在bada平台上创建内容相当直接。其优势在于，您的内容由bada服务器进行虚拟管理，而物理内容则存储在工作区提供商（如Amazon）处。由于内容托管在独立的第三方平台上，因此能保证内容的最大安全性。

目前，Amazon是唯一允许使用bada内容服务（即搜索和共享）的存储提供商。因此，Amazon会对此服务收取费用，尽管费用很小。不过，预计不久后将建立一系列类似的存储服务提供商。

bada SDK提供了一些代码示例，这些示例更详细地说明了如何与远程内容交互并利用bada平台的这一功能。例如，可以查看RemoteContent示例，它提供了有关（远程）内容管理功能的更多细节。

## 7.2 使用bada SNS网关访问Facebook等社交网络服务

## 问题描述

您需要一种简便的方式从bada应用中使用Facebook等社交网络服务。您可以使用bada SNS网关。

## 配方

本配方需要以下配置：

**使用的命名空间：**  
Osp::Social::Services, Osp::Base::Collection

**需要`#include`的头文件：**  
FSocial.h, FBase.h

**所需库：**  
FSocial, FSocialServices, FSocialServicesSnsAuth

**所需权限级别：**  
System

**所需权限组：**  
SNS_SERVICE

bada SNS网关提供了统一的API，使应用程序能够轻松访问Facebook、Twitter和MySpace等社交网络服务（SNS）。该网关支持许多基本用例，并且提供简单的身份验证，可用于后续与服务自身的RESTful API交互，如果您需要更复杂的交互。

该API是异步的，使用接口类的监听器方法来接收框架在感兴趣事件发生时发出的回调。要使用监听器，应用程序需要从相应的接口类派生一个合适的对象（例如`Form`），并实现一个监听器方法来处理感兴趣的事件。

SNS网关为四种不同类型的事件提供了监听器：

- `ISnsActivityListener`：接收发送到网关的活动请求的响应。
- `ISnsGatewayListener`：接收与客户端应用登录状态相关的事件。

