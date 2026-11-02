
`setAccountPicturesAsync`（用于从 `StorageFile` 对象提供小图和大图以及视频），以及 `setAccountPictureFromStreamAsync` 和 `setAccountPicturesFromStreamAsync`（在给定 `IRandomAccessStream` 对象时执行相同操作）。在每种情况下，异步结果都是 `SetAccountPictureResult` 值：`success`、`failure`、`changeDisabled`（`accountPictureChangeEnabled` 为 false）、`largeOrDynamicError`（图片过大）、`fileSizeError`（文件过大）或 `videoFrameSizeError`（视频帧尺寸过大）。

-   `accountPictureChanged` 事件在用户图片被更改时发出信号。
-   请记住，由于此事件源自 WinRT，如果您不是在应用生命周期内监听此事件，则应调用 `removeEventListener`。

这些功能在账户图片名称示例中进行了演示。场景 1 检索显示名称，场景 2 检索名字和姓氏（如果可用），场景 3 检索账户图片和视频，场景 4 更改账户图片和视频并监听图片更改。

该示例演示的另一点是其清单中的 Account Picture Provider 声明，这会导致应用出现在 PC 设置 > 账户 > 你的账户 下的“创建账户图片”中：

![](img/0e8e4a2b6f953d339e14e88cd5d8b4d_224_0.png)

在这种情况下，示例实际上并未直接提供图片，而是启动到场景 4。像默认也在 PC 设置中出现的相机应用这样的真实应用，当通过其 UI 获取图片时会自动设置账户图片。它是如何知道这样做的？答案在于应用被激活时使用的特殊 URI 方案。也就是说，当你在清单中声明 Account Picture Provider 声明时，应用将以 `protocol` 的激活类型被激活（参见第 15 章“Contracts”），其中 URI 方案 specifically 以 `ms-accountpictureprovider` 开头。你可以在示例的 `js/default.js` 文件中看到这是如何处理的：

```js
if (eventObject.detail.kind === Windows.ApplicationModel.Activation.ActivationKind.protocol) {
    // Check if the protocol matches the "ms-accountpictureprovider" scheme
    if (eventObject.detail.uri.schemeName === "ms-accountpictureprovider") {
        // This app was activated via the Account picture apps section in PC Settings.
        // Here you would do app-specific logic for providing the user with account
        // picture selection UX
    }
}
```

回到 *UserInformation* 类，如果应用在其清单中声明了 *Enterprise Authentication* 功能，它还为域账户提供一些更多详细信息：

-   `getDomainNameAsync` 提供用户的完全限定域名作为字符串，格式为 `<domain>\<user>`，其中 `<domain>` 是域控制器的全名，例如 `mydomain.corp.ourcompany.com`。
-   `getPrincipalNameAsync` 以字符串形式提供主体名称。在 Active Directory 用语中，这是一个 Internet 风格的登录名（称为用户主体名称或 UPN），比域名更短更简单，将电子邮件和登录命名空间合并。通常，这是一个类似 `user@ourcompany.com` 的电子邮件地址。
-   `getSessionInitiationProtocolUriAsync` 提供一个 *session initiation protocol URI*，可与该用户连接；有关背景信息，请参阅 *Session Initiation Protocol*（Wikipedia）。

这些方法的使用在 *User domain name sample* 中进行了演示。

## 我们刚刚学到的内容

-   网络有多种不同的形式，清单中的单独功能专门指出了 *Internet (Client)*、*Internet (Client & Server)* 和 *Private Networks (Client & Server)*。这些中的本地环回通常对应用被阻止，但在具有开发者许可证的机器上可用于调试目的。
-   通过 `Windows.Networking.Connectivity.NetworkInformation` API 可获得丰富的网络信息，包括跟踪连接性、感知网络成本以及获取连接配置文件详细信息的能力。
-   可以通过使用 `networkStateChange` 触发器以及诸如 `InternetAvailable` 和 `InternetNotAvailable` 之类的条件从后台任务监控连接性。
-   离线运行的能力可能是一个重要考虑因素，可以使应用对客户更具吸引力。应用需要自行设计和实现此类功能，使用本地或临时应用数据文件夹来存储必要的缓存。
-   根据需求，Web 内容可以在应用中托管在 webview 和 `iframe` 元素中。使用 `iframe` 元素的本地和 Web 上下文为托管内容提供不同的功能，而 webview 可以托管本地动态生成的内容（使用 `ms-appdata` URI）和不受信任的 Web 内容。
-   要发出 HTTP 请求，你可以在 `XMLHttpRequest`、`WinJS.xhr` 和 `Windows.Web.Http.HttpClient` 之间选择，后者是最强大的。在所有情况下，`resuming` 事件通常用于在适当时刷新在线内容。
-   Windows.Networking.BackgroundTransfer 提供了预取在线内容以及在应用未运行时管理传输的功能。它包括成本感知、凭据、分组和多部分上传，对于较大的传输，建议使用它而不是自己的 HTTP 请求。
-   Credential Locker 是安全存储应用可能收集的任何凭据或敏感令牌的地方。
-   为了理想地将凭据完全保留在客户端设备之外，应用可以通过 Web Authentication Broker API 登录服务，该 API 还为使用相同身份提供者的应用提供单点登录。
-   通过用户的 Microsoft 账户和 Live SDK，应用可以访问 Live Services 中可用的所有信息，包括 SkyDrive、联系人和日历。
-   应用可以获取和管理用户个人资料数据的某些部分，包括用户图像或视频以及锁屏图像和视频。

## 第 5 章

### 控件和控件样式

控件是你似乎无法摆脱的东西之一，尤其是在像我们周围许多人那样的技术成瘾文化中。即使是自行车和各种园艺工具等低技术设备也有控件。但这不是问题——实际上这是必要的。控件是人类意图转化为机械和电子领域的手段，并且完全是为了邀请交互而设计的。我在写这篇文章时，实际上正坐在飞机上，注意到视野中的所有控件。前排的小男孩似乎也在做同样的事情，他头顶上那个大大的“呼叫乘务员”按钮似乎在恳求被按下！

控件对于 Windows Store 应用来说绝对是必不可少的，它们会邀请用户戳、探、触摸、点击和滑动它们。（它们也会邀请许多小幼儿经常弄脏的小手；有人制造过可洗碗机清洗的平板电脑吗？）Windows 当然为用 HTML、CSS 和 JavaScript 编写的应用提供了丰富的控件。在这种情况下最值得注意的是，从设计的早期阶段开始，Microsoft 就希望避免强迫 HTML/JavaScript 开发者使用与这些开发者已知的东西不一致的控件——即使用像 `<button>` 这样的 HTML 控件元素，这些元素可以用 CSS 样式化，并通过使用 addEventListener 和 `on<event>` 属性等函数在 JavaScript 中连接起来。

当然，你可以在 Store 应用中使用这些固有的 HTML 控件，因为这些应用运行在与 Internet Explorer 相同的 HTML/CSS 渲染引擎之上。没问题。甚至还有特殊的类、伪类和伪元素，可以提供精细的样式功能，我们稍后会看到。但真正的问题是如何实现 Windows 特定控件，如切换开关和列表视图，使你能够以相同的方式使用它们——即在标记中声明它们，用 CSS 样式化，并在 JavaScript 中使用 addEventListener 和 `on<event>` 属性连接它们。

所有这些的结果是，对于你这个 HTML/JavaScript 开发者来说，你会寻找 WinJS 中的这些控件而不是 WinRT。换句话说：如果注意到 Windows.UI.Xaml 命名空间中庞大的 API 集合（约占 WinRT 的 40%），猜猜怎么着？你可以完全忽略它们！相反，你将使用支持声明式标记、用 CSS 样式化等的 WinJS 控件，这意味着 Windows 控件（以及遵循相同模型的自定义控件）最终会与所有其他内容一起出现在 DOM 中，使它们可以通过你已知的和理解的所有方式访问。

Windows 控件的故事实际上比一章内容更大。我们已经在第 4 章“Web Content and Services”中探讨了 webview 控件。在这里，我们现在主要关注那些表示或处理简单数据（单个值）并且作为 DOM 中的元素参与页面布局的控件。参与 DOM，事实上正是你可以通过标准机制样式化和操作所有控件（HTML 和 WinJS 均可）的确切原因，本章的很大一部分是
