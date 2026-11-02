
```
https://www.facebook.com/dialog/oauth?client_id=<client_id>&redirect_uri=<redirectUri>&
scope=read_stream&display=popup&response_type=token
```

```
https://accounts.google.com/o/oauth2/auth?client_id=<client_id>&redirect_uri=<redirectUri>&
response_type=code&scope=http://picasaweb.google.com/data
```

其中 `<client_id>` 和 `<redirectUri>` 会替换为特定于应用的值。就 Twitter 和 Flickr 而言，它们改用 OAuth 1.0a 协议，因此创建要包含在传给 `authenticateAsync` 的 `requestUri` 参数中的冗长 OAuth 令牌时，需要繁琐得多的流程。这些细节我留给示例代码展示。

## 单一登录

到目前为止，我们所看到的凭据保险箱和 Web 身份验证代理配合得非常好，能够最大限度地减少应用反复要求用户提供凭据的次数。就单个应用而言，理想情况下它只要求提供一次凭据，直到用户显式注销为止。但如果有多个应用呢？设想随着时间推移，你从 Windows 应用商店获取了几十个甚至几百个应用，而这些应用使用的服务全都要求身份验证。即使这些服务只使用众所周知的 OAuth 提供程序，也仍然意味着你必须在每一个应用中输入你的 Facebook、Twitter、Google、LinkedIn、Tumblr、Yahoo 或 Yammer 凭据。到那时，每个应用只需验证一次这一事实，早已淹没在整体的繁琐之中！

从用户的角度来看，一旦他们在某个应用中通过给定的提供程序完成了身份验证，那么其他应用在可能的情况下也应当受益于该身份验证，这是合理的。是的，有些应用可能需要提示获取额外权限，有些提供程序可能不支持该过程，但理想情况仍然是尽可能减少麻烦和打扰。

*单一登录* 的概念正是如此：在一个应用中对用户进行身份验证（对于 Microsoft 帐户则是登录系统），实际上会让用户登录到使用同一提供程序的其他应用。为实现这一点，Web 身份验证代理会将每项服务的持久登录 Cookie 保存在一个特殊的应用容器中，该容器与应用完全隔离，但又允许这些 Cookie 在应用之间共享（就像浏览器中 Cookie 在网站之间共享一样）。与此同时，每个应用通常必须获取自己的访问密钥或令牌，因为这些不应在应用之间共享。因此，真正的诀窍在于有效执行我们已见过的同一种身份验证，只是除非确实必要，否则不显示任何 UI。

这正是 `authenticateAsync` 的一种变体的用途：该变体只接受 `options` 和 `requestUri` 参数（不接受显式的 `callbackUri`）。在这种情况下，`options` 通常设置为 `WebAuthenticationOptions.silentMode`，以防止代理的 UI 出现（但这不是必需的）。可是，代理如何知道身份验证何时完成？也就是说，它使用哪个 `callbackUri` 进行比较，提供程序本身又如何知道这一点？听起来情况会是：代理一直隐藏在那里，而提供程序则耐心等待一个同样不可见的网页的输入！

实际发生的情况是，`authenticateAsync` 会监视提供程序是否导航到一种特殊形式的 `callbackUri`，即 `ms-app://<SID>`，其中 `<SID>` 是唯一标识调用应用的安全标识符。这个 SID URI（我们姑且这样称呼）可通过两种方式获得。在代码中，调用静态方法 `WebAuthenticationBroker.getCurrentApplicationCallbackUri`。它会返回一个 `Windows.Foundation.Uri` 对象，其 `absoluteUri` 属性就是你需要的字符串。第二种方式是通过 Windows 应用商店仪表板。查看相关应用的信息时，转到“服务”部分。在那里你会看到一个指向“Live 服务站点”的链接（根地址为 https://account.live.com）。在该站点上，单击“验证你的服务”链接，你会看到此 URL 列在“包安全标识符 (SID)”下。

为了理解它的用法，让我们跟随静默身份验证过程的完整流程：

- 1. 应用向服务注册其 SID URI。在代码中，这可以通过为此目的设置的某个服务 API 或其他终结点来完成。服务可以有一个页面（如 Facebook），你作为开发者在该页面上直接注册应用，并在该过程中提供 SID URI。
- 2. 为 `authenticateAsync` 构造 `requestUri` 参数时，应用将其 SID URI 插入为 `&redirect_uri=` 参数的值。当然，SID URI 需要像其他 URI 参数一样，使用 `encodeURIComponent` 进行适当编码。
- 3. 应用使用 `silentMode` 选项调用 `authenticateAsync`。
- 4. 当提供程序处理 `requestUri` 参数时，它会检查 `redirect_uri` 值是否已注册；如果未注册，则返回失败。
- 5. 验证应用后，提供程序随后会（如果可能）静默进行身份验证，并导航到 `redirect_uri`，同时确保在响应数据中包含访问密钥和令牌等内容。
- 6. Web 身份验证代理会检测到这一导航，并将其与应用 SID URI 匹配。找到匹配项后，代理便可完成异步操作，并将响应数据提供给应用。

尽管如此，身份验证仍可能因其他原因失败。例如，如果用户尚未为相关应用设置权限（如 Facebook 的情况），就无法进行静默身份验证。因此，尝试使用单一登录的应用会先调用这种形式的 `authenticateAsync`；如果失败，再回退到调用其较长的形式（带 UI），如上一节所述。

## 使用 Microsoft 帐户

由于各种 Microsoft 服务都是 OAuth 提供程序，因此可以将 Web 身份验证代理与 Hotmail、Live 和 MSN 等 Microsoft 帐户一起使用。（我仍然保留着同一个 @msn.com 电子邮件帐户 [我从 1996 年就拥有了！]。）详细信息可在 Live Connect 开发者中心的 OAuth 2.0 页面上找到。

Live Connect 帐户（也称为 Microsoft 帐户）处于更有利的地位，因为它们还可用于登录 Windows，或可连接到用于同一目的的域帐户。许多内置应用（如邮件、日历、SkyDrive、人脉以及 Windows 应用商店本身）都使用同一个帐户。因此，许多其他应用可能希望利用这一点。此类应用会自动受益于单一登录，并可访问与内置应用自身所依赖的相同 Live 服务（包括已取代 Live Messenger 的 Skype）。

可用功能的完整范围可在 Live Connect 文档中找到。46 你可以直接通过 Live Connect 的 REST API 访问其功能，也可以通过 Live SDK 的客户端库访问。安装 SDK 并向项目添加适当的引用后，你将在 JavaScript 中拥有可用的 WL 命名空间。例如，登录通过 `WL.login` 方法完成。

为了稍微探索一下 Live 服务，我们先走一遍这里适用的用户体验，然后再转向本章配套内容中的 LiveConnect 示例，该示例演示如何使用 Live SDK 库。请注意，使用 Live 服务时，应用清单中的包信息必须与你的应用在 Windows 应用商店仪表板中的信息匹配。为确保这一点，请在仪表板中创建应用配置文件（尽可能创建），转到 Visual Studio，选择“商店 > 将应用与应用商店关联”菜单命令，登录到应用商店，然后选择你的应用。

## WinRT 中的 OnlineId API

`Windows.Security.Authentication.OnlineId` 命名空间包含一个与 Live SDK 存在一定冗余的 API，提供了另一条登录并获取访问令牌的途径。Windows 帐户授权示例演示了这一点：在直接向 Live REST API 发出 HTTP 请求时使用该令牌。尽管该示例包含 JavaScript 版本，但此 API 主要面向用 C++ 编写的应用，因为这类应用没有 Live SDK 之类的其他选择。不过，当用户使用 Microsoft 帐户以外的方式（例如域帐户）登录 Windows 时，此 API 也很有用。例如，如果 Microsoft 帐户不是主登录帐户，则 `OnlineIdAuthenticator.canSignOut` 属性会设置为 true，因此使用该属性的应用应提供注销方式。OnlineId API 还支持将多个帐户一起进行身份验证（例如多个 SkyDrive 帐户），并且可与 Windows Azure Active Directory 和 SkyDrive Pro 之类的提供程序配合使用。

## Live Connect 用户体验

每当应用首次尝试登录 Live Connect 时，都会自动出现一个如图 4-9 所示的同意对话框，以确保用户了解该应用可能访问的信息类型。如果用户拒绝同意，登录当然会失败。因此，应用应提供一种让用户能够再次登录的方式。（另请参阅“Microsoft 帐户登录体验指南”以了解其他要求。）

46 其他有用的参考资料包括 Live Connect（Windows 应用商店应用）、应用和网站的单一登录、使用 Live Connect 个性化应用，以及 Microsoft 帐户登录体验指南。另请参阅 Windows 8 开发者博客（在 Windows App Builder 博客之前）上的“使用 Live SDK 为 Windows 应用带来单一登录”和“使用 Live SDK 向应用添加单一登录时的最佳实践”。
