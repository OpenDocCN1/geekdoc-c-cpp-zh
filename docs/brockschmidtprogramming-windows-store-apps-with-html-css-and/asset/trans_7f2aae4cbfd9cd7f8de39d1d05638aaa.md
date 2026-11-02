
`getCurrentDownloads[ForTransferGroup]Async` 和 `getCurrentUploads[ForTransferGroup]Async`，不完整的传输会自动重新启动。但那么你如何检索 `startAsync` 方法最初返回的 promise 呢？这些不是可以保存在应用状态中并在启动时重新加载的值，然而你需要它们以便在必要时取消这些操作，并附加你的完成、错误和进度处理程序。

因此，`DownloadOperation` 和 `UploadOperation` 对象都提供了一个名为 `attachAsync` 的方法，它为操作返回一个 promise，就像 `startAsync` 最初所做的那样。然后你可以调用 promise 的 `then` 或 `done` 方法来提供你的处理程序：

```
promise = download.attachAsync().then(complete, error, progress);
```

如果需要，调用 `promise.cancel()`。简而言之，当 Windows 重新启动后台传输并实质上代表你的应用调用 `startAsync` 时，它会在内部保存该 promise。`attachAsync` 方法只是返回该新的 promise。

## 身份验证、Microsoft 账户和用户配置文件

如果仔细想想，世界上几乎每个在线资源都与其关联着某种凭据或身份验证。当然，我们可以在没有凭据的情况下读取其中许多资源，但对网站上传数据的权限控制更为严格，对网站管理的数据库中个人账户或配置文件的访问也是如此。因此，在许多场景中，应用需要以某种方式使用服务特定的凭据，或许使用来自 Facebook、Twitter、Microsoft 等其他提供商的账户，对服务进行身份验证。

处理凭据有两种方法。首先，你可以直接通过自己的 UI 收集凭据，这意味着应用完全负责保护这些凭据。对于此，有针对不同登录场景的若干设计指南，例如应用需要登录才有用的情况以及登录仅为可选的情况。这些主题以及登录和账户/配置文件管理 UI 的放置位置，均在《登录控件的指南和检查清单》中讨论。

就存储而言，WinRT 中的 Credential Locker API 会在这里帮上忙——你可以在收集凭据时安全地保存它们，并在后续会话中检索它们，这样就不用再反复打扰用户。另一方面，将这些凭据传输到服务器则需要你进行加密工作，而且其中有很多细微之处可能变得复杂。有关 WinRT 中加密 API 的一些说明以及其他一些安全事项，请参阅附录 C。

更简单也更安全的方法——我们强烈推荐——是使用 Web Authentication Broker API。这允许用户直接在 broker 的 UI 中向服务器进行身份验证，将凭据完全保留在服务器上，之后应用会收到一个令牌以用于对服务的后续调用。Web Authentication Broker 可与任何已设置为主体的服务一起使用。这可以是你的服务，正如我们将看到的，也可以是 OAuth/OpenID 提供程序。

**Tip** 在思考可能用于身份验证的提供程序时，请记住，非域加入的用户最初是用 Microsoft 账户登录 Windows 的。如果你能利用该 Microsoft 账户与自己的服务一起使用，登录 Windows 就意味着他们无需输入任何额外凭据或为你的服务创建单独账户，提供了一种令人愉悦的透明体验。Microsoft 账户还可提供其他功能，正如我们稍后在“使用 Microsoft 账户”中将看到的那样。

Web Authentication Broker 的一个重要好处是，针对特定服务的身份验证可在应用之间以及网站之间转移，为用户提供非常强大的单点登录体验。也就是说，一旦用户在浏览器中或使用 broker 的应用中登录到某项服务，他们就已经登录到使用同一服务的其他应用和站点了（再次说明，使用 Microsoft 账户登录 Windows 也适用）。更妙的是，这些凭据还会漫游到用户的受信任设备上（除非他们选择退出），因此在切换机器时甚至无需再次进行身份验证。我个人发现这非常令人满意——例如在设置全新的设备时，所有这些凭据立即生效！

### 凭据库

应用可能会反复要求用户提供凭据的一个原因，仅仅是因为它们没有一个真正安全且与其他应用隔离的地方来存储和检索这些凭据。这完全就是凭据库的目的，其功能也从这个特定 API 的名称中一目了然：Windows.Security.Credentials.PasswordVault。它当然是设计用来存储凭据的，但你也可以用它来存储诸如令牌之类的其他内容。

使用该库时，任何给定凭据本身都由 PasswordCredential 对象表示，正如我们在后台传输 API 中简要看到的那样。你可以按如下方式创建一个已初始化的凭据：

```
var cred = new Windows.Security.Credentials.PasswordCredential(resource, userName, password);
```

另一个选项是创建一个未初始化的凭据并单独设置其属性：

```
var cred = new Windows.Security.Credentials.PasswordCredential();
cred.resource = "userLogin";
cred.userName = "userName";
cred.password = "password";
```

凭据对象还包含一个名为 properties 的 IPropertySet 值，可通过它管理相同的信息。

无论如何，当你从用户处收集凭据并希望保存它们时，创建一个 PasswordCredential 并将其传递给 PasswordVault.add：

```
var vault = new Windows.Security.Credentials.PasswordVault();
vault.add(cred);
```

请注意，如果你使用已存在的 `resource` 和 `userName` 将凭据添加到库中，新凭据将替换旧凭据。如果在任何时候你想从库中删除凭据，请使用该凭据调用 `PasswordVault.remove` 方法。

此外，尽管 `PasswordCredential` 对象以用户名和密码为视角，但该密码可以是你需要安全存储的任何内容，例如访问令牌。正如我们将在下一节看到的，通过 OAuth 提供程序进行身份验证可能会返回此类令牌，在这种情况下，你可能会将 `"Facebook_Token"` 存储在凭据的 `resource` 属性中，将你的应用名称存储在 `userName` 中，并将令牌存储在 `password` 中。这是一种完全合法且预期的用法。

一旦凭据进入库，它将保留在后续的应用启动中，直到你调用 `remove` 方法或用户通过控制面板 > 用户账户和家庭安全 > 凭据管理器显式删除它。在受信任的 PC 上（需要使用 Microsoft 账户登录），Windows 还会安全地自动将库的内容漫游到用户的其他设备（除非在 PC 设置 > SkyDrive > 同步设置 > 其他设置 > 密码中关闭）。这有助于在用户在设备之间移动时为你的应用创建无缝体验。<sup>44</sup>

因此，当你启动应用时——即使是首次启动——也应始终检查库中是否保存了凭据。`PasswordVault` 类提供了几种方法来执行此操作：

- `findAllByResource` 返回给定资源标识符的凭据对象数组（向量）。这是你获取从另一设备漫游而来的用户名和密码的方式，因为应用会在另一台机器上在同一资源下将这些凭据存储到库中。
- `findAllByUserName` 返回给定用户名的凭据对象数组（向量）。如果已知用户名并希望检索应用连接的多个资源的全部凭据，这很有用。
- `retrieve` 根据资源标识符和用户名返回单个凭据。再次说明，对于任何给定的资源和用户名，库中永远只有一个凭据。
- `retrieveAll` 返回此应用在库中的所有凭据的向量。该向量包含库的快照，不会随着库中凭据的后续更改而更新。

上面列表中 `findAll` 和 `retrieve` 方法之间有一个细微差别。`retrieve` 方法会为你提供完全填充的凭据对象。而 `findAll` 方法则会给出 `password` 属性仍为空的对象。这避免了对可能大量凭据执行密码解密。要为任何单个凭据填充该属性，请调用 `PasswordCredential.retrievePassword` 方法。

有关凭据库的进一步演示——代码非常简单——请参阅 `Credential_locker sample`。它展示了单用户/单资源（方案 1）、单

44 然而，如果凭据*首先*存储在加入域的机器的库中，则不会发生此类漫游。这可以防止域凭据泄露到云端。
