

```
)

void
MainForm::OnKeyReleased(const Control &source,
Osp::Ui::KeyCode keyCode)
{
    switch(keyCode)
    {
        // Handle the various keys however you need it
    }
    prevKeyCode = keyCode;
    prevKeyState = KEY_RELEASED;
}

void
MainForm::OnKeyLongPressed (const Control &source,
Osp::Ui::KeyCode keyCode)
{
    switch(keyCode)
    {
        // Handle the various keys however you need it
    }
    prevKeyCode = keyCode;
    prevKeyState = KEY_LONGPRESSED;
}
```

## Hints, Pitfalls, and Related Topics

当用户按下并释放硬键时，会生成两个事件：

- 1. KEY_PRESSED
- 2. KEY_RELEASED

当用户在释放硬键之前长按该键时，会额外生成一个长按事件：

- 1. KEY_PRESSED
- 2. KEY_LONGPRESSED
- 3. KEY_RELEASED（在键被释放时触发）

在设计应用程序时，必须考虑与硬键关联的功能是在按下时还是在释放时被调用。此外，还必须考虑是否要为硬键实现长按功能。这些因素将有助于确定按键事件处理方法的实现方式。

使用的命名空间：
Osp::Ui, Osp::Ui::Controls, Osp::Web::Controls

需要 #include 的头文件：
FUi.h, FUiControls.h, FWeb.h

所需库：
FUi, FUiControls, FWebControls

所需权限级别：
Normal

所需权限组：
WEB_SERVICE

Web 控件可用于在应用程序中添加网络浏览器以加载网页、下载内容并在浏览器内运行 JavaScript。Web 控件基于 Webkit（webkit.org）。本教程展示了使用 Web 控件的两种不同方式。每个示例都详细说明了创建和使用 Web 控件所需的步骤，并提供了一些示例代码片段。

本教程中的两个示例均假设已按照教程“Add a Form to a Frame-based App”中的方法 2 中详细说明的步骤将 Form 添加到应用程序的 Frame 中。

## Example 1: Loading a Web Page

本示例使用 Osp::Web::Controls::Web 类创建一个 Web 控件以显示网页，并以横向方向将其显示在表单中（见图 R2.14）。

![](img/a257d5fd53a79a244a20e587cd2f08f6_337_0.png)

图 R2.14 Web 控件。

在 MainForm 类中添加一个类型为 Web 的成员变量指针，以保存对创建的 Web 控件的引用：

```
Osp::Web::Controls::Web* pWeb;
```

Web 控件可以在 MainForm 初始化期间创建（OnInitializing()）：

- 1. 将 MainForm 的方向设置为横向。
- 2. 创建 Web 控件。
- 3. 使用可用屏幕区域的大小和位置初始化 Web 控件。
- 4. 将 Web 控件添加到 MainForm。
- 5. 在 Web 控件中加载指定的 URL。

以下代码片段是添加到 MainForm 的 OnInitializing() 方法中以创建 Web 控件的示例代码：

```
// Set the orientation of the Form to landscape
SetOrientation(ORIENTATION_LANDSCAPE);

// Create Web control object
pWeb = new Web();

// Initialise the Web control
pWeb->Construct(Rectangle(0, 0, GetClientAreaBounds().width, GetClientAreaBounds().height));

// Add the Web control to the Form
AddControl(*pWeb);

// Load the specified URL in the Web control
pWeb->LoadUrl(L"http://developer.bada.com");
```

## Example 2: Downloading a File

本示例使用 Osp::Web::Controls::Web 类创建 Web 控件并使用它从网络下载文件。文件保存到应用程序的 /Home 目录中，可由应用程序按需使用。

要从远程服务器下载文件，使用 Osp::Web::Controls::Web 控件在应用程序内嵌入浏览器。实现 Osp::Web::Controls::ILoadingListener 接口类以监听加载操作期间发生的事件并通知 Web 控件应用程序希望自行处理数据。Osp::Web::Controls::IWebDownloadListener 接口类用于将数据下载到应用程序。

以下代码片段显示了 MainForm 类定义的示例：

```
class MainForm :
    public Osp::UI::Controls::Form,
    public Osp::UI::Controls::ILoadingListener,
    public Osp::Web::Controls::IWebDownloadListener
{
public:
    MainForm(void);
    ~MainForm(void);
    bool Initialize(void);

protected:
    Osp::Io::File* pFile;
    Osp::Web::Controls::Web* pWeb;

    String serverFilePath;
    String fileName;
    String localFilePath;

    void WriteDownloadFile(Osp::Io::File* file,
        const Osp::Base::ByteBuffer& chunk);
    void CloseDownloadFile(Osp::Io::File* file);

public:
    result OnInitializing(void);
    result OnTerminating(void);

    void OnEstimatedProgress(int progress) {};
    void OnHttpAuthenticationCanceled(void) {};
    bool OnHttpAuthenticationRequestedN(
        const Osp::Base::String &host,
        const Osp::Base::String &realm,
        const Osp::Web::Controls::AuthenticationChallenge &authentication) { return false; };
    void OnLoadingCanceled(void) {};
    void OnLoadingCompleted(void) {};
    void OnLoadingErrorOccurred
        (Osp::Web::Controls::LoadingErrorType error,
        const Osp::Base::String &reason) {};
    bool OnLoadingRequested(const Osp::Base::String &url,
        Osp::Web::Controls::WebNavigationType type)
        { return false; };
    void OnLoadingStarted(void) {};
    void OnPageTitleReceived(const Osp::Base::String &title) {};
    Osp::Web::Controls::DecisionPolicy OnWebDataReceived
        (
        const Osp::Base::String &mime,
        const Osp::Net::Http::HttpHeader &httpHeader);

    void OnWebChunkedDataReceived
        (
        const Osp::Base::ByteBuffer& chunk);
    void OnWebDataDownloadCompleted(void);
    void OnWebDownloadFailed
        (
        Osp::Web::Controls::LoadingErrorType error);
};
```

Web 控件的创建和监听器的注册应在 OnInitializing() 方法中完成：

- 1. 定义文件名、要从中下载文件的服务器文件路径以及要存储文件的本地文件路径。
- 2. 创建 Web 控件并将其初始化为客户端区域的大小。
- 3. 将 Web 控件添加到 MainForm。
- 4. 注册 ILoadingListener。
- 5. 注册 IWebDownloadListener。

以下代码片段是添加到 MainForm 的 OnInitializing() 方法中的示例代码：

```
fileName.Append(L"somefile");
serverFilePath.Append(L"http://www.somewebsite.com/");
serverFilePath.Append(fileName);

localFilePath.Append(L"/Home/");
localFilePath.Append(fileName);

// Create web control and add to form
pWeb = new Web();
pWeb->Construct(GetClientAreaBounds());
AddControl(*pWeb);

// Register loading & download listeners with the web control
pWeb->SetLoadingListener(this);
pWeb->SetDownloadListener(this);

// Load the URL
pWeb->LoadUrl(serverFilePath);
```

ILoadingListener 接口类提供了多个方法来监控加载操作期间发生的事件。本示例仅实现了其中一个方法：OnWebDataReceived()。OnWebDataReceived() 方法在接收到第一块数据时立即被调用，并通知应用程序要下载的数据的内容类型。

在本示例中，而不是由 Web 引擎处理数据，应用程序自行处理数据。OnWebDataReceived() 方法应返回 WEB_DECISION_DOWNLOAD，以便将数据路由到由应用程序注册的 IWebDownloadListener：

```
Osp::Web::Controls::DecisionPolicy
MainForm::OnWebDataReceived(const Osp::Base::String &mime,
    const Osp::Net::Http::HttpHeader &httpHeader)
{
    return WEB_DECISION_DOWNLOAD;
}
```

CloseDownloadFile() 销毁对本地文件的引用，以便无法再向其写入数据：

```
void
MainForm::CloseDownloadFile(Osp::Io::File* file)
{
    if(file)
    {
        delete file;
        file = null;
    }
}
```

文件成功下载后，可由应用程序按需使用。

## Hints, Pitfalls, and Related Topics

必须在应用程序的清单文件中设置 WEB_SERVICE 组权限才能使用 Web 控件。

## Related Recipe

- Add a Form to a Frame-based App

