
- 2. 身份验证遵循“使用bada SNS网关访问Facebook等社交网络服务”方法中所示的步骤，除了构造SnsGateway实例时作为参数提供的预期监听器方法的位置。要上传图像，监听器是ISnsContentListener，它在函数调用中作为第二个参数提供（作为this，因为我们从ISnsContentListener派生类进行调用）：

    ```
    pSnsGateway->Construct(*this, this, null, null);
    ```

- 3. 身份验证成功后，使用以下代码上传照片：

    ```
    r = pSnsGateway->UploadPhoto(serviceProvider, null, *pContentInfo, reqId);
    ```

    其中serviceProvider是指定Facebook的String，pContentInfo是SnsUploadContentInfo*的一个实例，它封装了要上传的内容——在本例中是通过文件路径指定的照片。

    ```
    void
    MyFacebookClass::UploadPhotos(void)
    {
        RequestId reqId = INVALID_REQUEST_ID;
        result r = E_SUCCESS;

        String filepath = "~/Home/upload/1.jpg";

        String serviceProvider = pSNSAuthResult->GetServiceProvider();
        SnsUploadContentInfo* pContentInfo = new
            SnsUploadContentInfo(SNS_UPLOAD_CONTENT_PHOTO, filepath);

        r = pSnsGateway->UploadPhoto(serviceProvider, null, *pContentInfo,
            reqId);

        delete pContentInfo;
        pContentInfo = null;
    }
    ```

    > 注意：SnsUploadContentInfo类提供了设置标题、标签和其他内容详细信息的方法，但并非所有这些当前都支持Facebook。有关哪些功能支持哪些服务的更多详细信息，请参阅developer.bada.com上的文档。

- 4. 完成后，SnsGateway::OnSnsPhotoUploaded()是包含上传请求结果的回调方法。实现此方法以处理任何错误。`result r`中的值包含更新请求的结果，`errorCode`和`errorMsg`字符串提供有关任何错误的进一步信息：

    ```
    void
    MyFacebookClass::OnSnsPhotoUploaded(RequestId reqId, Osp::Base::String &serviceProvider, Osp::Base::String *pPhotoId, result r, const Osp::Base::String &errorCode, const Osp::Base::String &errorMsg)
    {
        if (!IsFailed(r))
        {
            AppLog("Successfully uploaded the photo with photoId as %ls",pPhotoId->GetPointer());
        }
    }
    ```

## 提示、陷阱和相关主题

请注意，在第2步中将监听器实例ISnsContentListener传递给SnsGateway构造函数时的参数位置；ISnsContentListener应为第二个参数，第三个和第四个参数应为null。

作为使用SNS网关的替代方案，您可以使用bada的HTTP API直接从应用程序中使用Facebook的RESTful API。使用SNS网关要简单得多，但直接使用Facebook API可提供更大的灵活性。有关更多信息，请参阅“使用RESTful API从Facebook获取笔记”方法。

请注意，如果您没有在UploadPhoto()中设置目标相册，上传的照片将进入默认相册；该相册使用应用程序名称创建，即Facebook为其提供API密钥和API秘密的名称。

在撰写本文时，您无法通过SNS网关设置上传照片的标题和其他属性，但您可以设置说明。

## 相关方法

- 使用bada SNS网关访问Facebook等社交网络服务
- 从Twitter发送推文
- 使用RESTful API从Facebook获取笔记

## 7.5 使用RESTful API从Facebook获取笔记

### 问题描述

您想从Facebook帐户获取笔记并在应用程序中使用它们。

### 方法

此方法需要以下配置：

- **使用的命名空间：** Osp::Social::Services, Osp::Base, Osp::Base::Collection, Osp::System, Osp::Security, Osp::Security::Crypto, Osp::Base::Utility, Osp::Net::Http
- **要#include的头文件：** FUI.h, FSocial.h, FSecurity.h, FNet.h
- **所需库：** FSocial, FSocialServices, FSocialServicesSnsAuth, FSecurity, FNet, FSystem
- **所需权限级别：** System
- **所需权限组：** SNS_SERVICE, HTTP

有些时候，您需要使用SNS网关不支持的服务功能。从Facebook获取笔记就是一个例子。

在这种情况下，您必须直接使用Facebook的RESTful API。本方法描述了执行此操作的步骤。概括如下：

- 1. 按照“使用bada SNS网关访问Facebook等社交网络服务”方法获取令牌密钥和秘密。
- 2. 使用bada HTTP服务请求Facebook的“Notes”URL。
- 3. 您需要使用bada Crypto服务，因为Facebook要求URL请求参数进行MD5Hash签名。
- 4. HTTP响应返回XML数据。
- 5. 按照“解析XML内容”方法解析XML并提取您想要的内容。

此处与相关方法中关于SNS身份验证所需密钥以及所需bada权限的说明相同。有关这两个主题的更多信息以及针对Facebook的指导，请参阅developer.bada.com上的文档。

图R7.3显示了下载后显示的Facebook笔记。

![](img/a257d5fd53a79a244a20e587cd2f08f6_463_0.png)

图R7.3 从Facebook检索到的笔记。

让我们看看它在代码中是什么样子。

- 1. 对于初始身份验证，您可以使用SNS网关`SnsAuthenticator`。按照“使用bada SNS网关访问Facebook等社交网络服务”方法中的步骤1-7进行设置并使用SNS网关进行身份验证。为此，您的请求类应继承自`ISnsAuthenticatorListener`和`ISnsGatewayListener`。
- 2. 身份验证成功后，`OnSnsAuthenticated()`回调返回一个`SnsAuthResult`对象，该对象包含一个密钥令牌和一个秘密令牌。您可以使用这些令牌进一步直接与SNS站点（此处为Facebook）的RESTful API通信。
- 3. 继承`Osp::Net::Http::IHttpTransactionEventListener`接口以接收HTTP事务事件。注意，您需要查看Facebook API文档以了解如何使用Notes接口；它提供了要调用的方法和所需参数的详细信息。

```
#include <FNet.h>
#include <FSecurity.h>

class MyClass :
    public Osp::Net::Http::IHttpTransactionEventListener
{
public:

    MyClass();
    ~MyClass();

private:
    Osp::Net::Http::HttpSession* pSession;
    Osp::Base::String authToken;
    Osp::Base::String authTokenSecret;

    void GetNotes(void);

    void SendRequest(Osp::Base::String reqString);

    Osp::Base::String MakeRequestUrl(const Osp::Base::String& method);

    Osp::Base::String GenerateSignature(const Osp::Base::String&
        requestStr);
    //Generates the MD5Hash signature

    //HTTP functions
    void OnReadyToRead
    (Osp::Net::Http::HttpSession& httpSession,
    Osp::Net::Http::HttpTransaction& httpTransaction,
    int availableBodyLen);

    void OnTransactionAborted(Osp::Net::Http::HttpSession& httpSession,
        Osp::Net::Http::HttpTransaction& httpTransaction, result r);

    void OnTransactionReadyToWrite
    (Osp::Net::Http::HttpSession &httpSession,
    Osp::Net::Http::HttpTransaction& httpTransaction,
    int recommendedChunkSize);

    void OnTransactionHeaderCompleted
    (Osp::Net::Http::HttpSession& httpSession,
    Osp::Net::Http::HttpTransaction& httpTransaction,
    int headerLen, bool rs);

    void OnTransactionCompleted
    (Osp::Net::Http::HttpSession& httpSession,
    Osp::Net::Http::HttpTransaction& httpTransaction);

    void OnTransactionCertVerificationRequiredN
    (Osp::Net::Http::HttpSession& httpSession,
    Osp::Net::Http::HttpTransaction& httpTransaction,
    Osp::Base::String* pCert);
};
```

- 4. GetNotes()方法封装了构造URL请求字符串和发送HTTP请求所需的步骤。调用的Facebook API方法是facebook.notes.get。

```
void
MyClass:: GetNotes(void)
{
String url = L"http://api.facebook.com/restserver.php?";
String method = L"facebook.notes.get";
String requestString = MakeRequestString(method);
String requestUrl = url + requestString;
SendRequest(requestUrl);
}
```

- 5. MakeRequestString()方法封装了创建我们将发送到facebook.notes.get API的参数字符串所需的步骤。我们必须提供API密钥、指定Open API（必须为版本1.0）、会话密钥、方法名称等。
- 6. 会话密钥是网关身份验证过程生成的密钥（见步骤2）。
- 7. 我们构造字符串，然后按字母顺序对参数列表排序，最后使用网关身份验证过程中生成的秘密令牌生成MD5Hash签名。
- 8. 最后，我们将此签名附加到请求字符串。

```
String
MyClass:: MakeRequestString()
{
String apiKey = L"api_key=";
String callId = L"call_id=";
String version = L"v=";
String signature = L"sig";
String sessionKey = L"session_key=";
String methodParam = L"method=";
String paramString;
String requestString;
String signatureStr;
long long secTimeStamp = 0;
```
