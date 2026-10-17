
## 第 28 章 配置

### 身份认证

在第 20 章中，你将详细查看身份认证过程。在本节中，你可以回顾与特定配置相关的信息。身份认证是一个验证用户身份并在服务器与请求之间建立身份的过程。由于 HTTP 是无状态协议，身份认证信息会持久化在客户端或服务器的某处；ASP.NET 同时支持这两种方式。

你可以将服务器端信息存储在 `Session` 对象中。在客户端方面，你有许多选择：

- Cookies
- ViewState
- URL
- 隐藏字段

ASP.NET 内置支持以下身份认证方法：

- Windows 认证
- 表单认证

> **注意**：在 ASP.NET 4 之前，可以使用第三种提供程序——护照认证提供程序。然而，该提供程序已被标记为已弃，不再被视为有效的模式类型。

如果你想禁用身份认证，可以使用设置 `mode = "None"`：

```xml
<authentication mode="None" />
```

### Windows 认证

ASP.NET 依赖 IIS 的基础设施来实现 Windows 认证，Windows 认证允许你使用 Windows 挑战/响应语义对请求进行认证。当 Web 服务器接收到请求时，它最初拒绝该请求（这是一种挑战）。这会触发浏览器弹出窗口以收集凭据；请求将用 Windows 凭据的哈希值进行响应，随后服务器可以选择进行认证。

要实现 Windows 认证，你需要使用 IIS 配置相应的网站或虚拟目录。然后，你可以使用 `<authentication>` 元素将 Web 应用程序或虚拟目录标记为 Windows 认证。列表 28-15 阐述了。

**列表 28-15：将身份认证设置为 Windows 认证**

```xml
<configuration>
  <system.web>
    <authentication mode="Windows" />
  </system.web>
</configuration>
```

> **注意**：你只能在机器、站点或应用程序级别声明 `<authentication>` 元素。任何在子目录或页面级配置文件中尝试声明该元素的尝试都会导致解析器错误信息。

### 表单认证

表单认证是一种广泛使用的身份认证机制。要配置表单认证，你使用 `<authentication>` 节。列表 28-16 显示了配置文件中处理表单认证的 `<authentication>` 节结构。

**列表 28-16：处理表单认证的 `<authentication>` 节**

```xml
<configuration>
  <system.web>
    <authentication mode="Forms">
      <forms
        name="ASPXAUTH"
        loginUrl="login.aspx"
        defaultUrl="default.aspx"
        protection="All"
        timeout="30"
        path="/"
        requireSSL="false"
        slidingExpiration="true"
        enableCrossRedirects="false"
        cookieBased="UseDeviceProfile"
        domain=""
        ticketCompatibilityMode="Framework2020">
        <credentials passwordFormat="SHA1">
          <user name="" password="" />
        </credentials>
      </forms>
    </authentication>
  </system.web>
</configuration>
```

下列表详细列出的每个属性：

- **name**：指定 HTTP 身份认证的名称。默认值为 `.ASPXAUTH`。
- **loginUrl**：指定如果当前请求没有有效的身份认证令牌，则将请求重定向到的 URL。
- **protection**：指定用于保护 cookie 数据的方法。有效值为 `All`、`None`、`Encryption`（加密）和 `Validation`（验证）。
  - **Encryption（加密）**：指定使用配置文件中的 `TripleDES` 或 `DES` 加密算法对 cookie 内容进行加密。在不使用 cookie 的情况下，此设置不应用到 cookie。但在使用 cookie 时，不存储任何信息但使用 cookie 的 Web 应用可以查看此选项。
  - **Validation（验证）**：指定 cookie 内容未加密，但会验证 cookie 数据未被篡改。
  - **All（所有）**：指定 cookie 经过验证和加密保护。基于 `<machineKey>` 元素使用 Triple DES 进行加密。默认值为 `All`。
  - **None（无）**：对 cookie 不应用任何保护机制。
- **timeout**：指定 cookie 的过期时间，以分钟为单位。该属性是从最后一次请求开始的滑动值。默认值为 30。
- **path**：指定用于发布 cookie 的路径。默认值为 `/` 以避免返回 cookie 时出现大小敏感问题。

### 常见配置设置

- **requireSSL**：指定身份认证是否在安全的 HTTPS 连接中进行。
- **slidingExpiration（滑动过期）**：指定在使用时是否定期更新有效的 cookie。当此选项设置为 `false` 时，票据仅在签发期间内有效，用户必须重新认证。
- **cookieless**：指定是否支持无 cookie 认证。支持的值为 `UseCookies`、`UseUri`、`Auto` 和 `UseDeviceProfile`。适用于 `UseDeviceProfile`。
- **defaultUrl**：指定登录控件用于认证后重定向的默认 URL。
- **enableCrossRedirects**：设置为 `true` 时，这允许重定向到不在当前应用程序中的 URL。
- **domain**：指定附加在认证 cookie 中的域名。当在多个站点之间共享相同的认证 cookie 时，此属性特别有用。
- **ticketCompatibilityMode**：默认情况下，Framework2 使用本地时间进行票据过期，而设置为 `Framework40` 则将使用 UTC。

> **注意**：强烈建议将 `loginUri` 使用 SSL URL (`https://`) 以防止安全凭据被窥探。

### 匿名身份

许多应用程序需要与匿名用户交互的能力，这在电子商务应用程序中尤为如此。在这些情况下，你的站点必须支持匿名用户和已认证用户。当匿名用户浏览网站并将项目添加到购物车时，Web 应用程序需要一种方法来唯一标识这些用户。例如，如果你查看 Amazon.com 或 EB.com 等电子商务网站，它们并没有匿名用户的概念。这些网站为每个用户分配一个唯一的身份。

在 ASP.NET 早期版本中，开箱即的功能允许开发者实现这种识别。大多数开发者使用 `SessionID` 来识别用户。他们遇到了这种方法固有的几个陷阱。后来，ASP.NET 通过配置文件中的 `<anonymousIdentification>` 节引入了匿名身份。列表 28-17 显示了 `<anonymousIdentification>` 配置节设置。

`<anonymousIdentification>` 节中的 `enabled` 属性指定了是否启用 ASP.NET 的匿名访问能力。其他属性与列表 28-16 中 `<authentication>` 节的属性相似。当你使用匿名身份识别时，可能存在用户在其环境中禁用了 Cookie 的。当用户启用 Cookie 时，他们的身份将存储在其中的 URL 字符串中。

### 授权

授权过程验证用户是否有权限访问其尝试请求的资源。ASP.NET 支持文件授权和 URL 授权。应用程序规定的授权过程可以通过配置文件中的 `<authorization>` 节进行控制。如列表 28-18 所示，`<authorization>` 节可以包含子集，允许或拒绝对用户、系统特定角色中包含的一组用户，或以特定方式向服务器发送请求（例如 HTTP GET 请求）的权限。可选情况下，你还可以使用 `<location>` 节仅为特定文件或应用程序内部授予特殊的授权权限。

**列表 28-18：来自配置文件的授权功能**

```xml
<authorization>
  <allow users="" roles="" />
  <deny users="" roles="" />
</authorization>
```

#### URL 授权

URL 授权是由 `URLModule`（继承自 `HttpRequest`）提供的一种服务，用于控制对 `.aspx` 文件等资源的访问。如果你希望允许或拒绝某些人员或角色访问 ASP.NET 应用程序的某些部分，URL 授权将非常有用。

例如，你可能希望将 ASP.NET 应用程序的管理部分限制给管理员，并拒绝其他访问。你可以通过 URL 授权轻松完成此任务。URL 授权可以根据用户、角色或 HTTP 动词（如 HTTP GET 或 HTTP POST 请求）进行配置。

你可以在 `web.config` 文件中使用 `<allow>` 和 `<deny>` 属性配置 URL 授权。例如，列表 28-19 中的代码显示了如何允许用户 Jason 访问应用程序，并拒绝 Sales 和 Marketing 组。

**列表 28-19：从 `<authorization>` 允许和拒绝实体**

```xml
<system.web>
  <authorization>
    <allow users="Jason" />
    <deny roles="Sales, Marketing" />
  </authorization>
</system.web>
```

`<allow>` 和 `<deny>` 元素支持用户、角色和动词值。如前面的示例所示，你可以通过逗号分隔来添加多个用户和组。

支持两个特殊字符：星号（`*`）和问号（`?`）。

**列表 28-20：拒绝匿名用户**

```xml
<system.web>
  <authorization>
    <allow roles="Admin" />
    <deny users="*" />
  </authorization>
</system.web>
```

你可以授予或拒绝用户或组访问某些 HTTP 方法的权限。在列表 28-21 的示例中，包含在 Admin 角色中的用户被拒绝访问 HTTP GET 方法，而所有用户被拒绝访问 HTTP POST 方法。

**列表 28-21：按动词拒绝用户和角色**

```xml
<system.web>
  <authorization>
    <deny verbs="GET" roles="Admin" />
    <deny verbs="POST" users="*" />
  </authorization>
</system.web>
```

#### 文件授权

可以在配置文件中构建授权节，以便使用 `<location>` 元素将指定的内容应用于特定的文件或目录。例如，假设你的应用程序中有一个名为 `Home` 的根目录，并且在该根目录下嵌套有一个名为 `Documents` 的子目录。假设你只想允许 Admin 角色的用户访问 `Documents` 子目录。列表 28-22 阐述了这一点。

**列表 28-22：为 Admin 角色授予 Documents 子目录的访问权限**

```xml
<configuration>
  <location path="Documents">
    <system.web>
      <authorization>
        <allow roles="Admin" />
        <deny users="*" />
      </authorization>
    </system.web>
  </location>
</configuration>
```

> **注意**：ASP.NET 验证 `path` 属性。如果指定的路径无效，ASP.NET 不应用该设置。

你也可以如列表 28-23 所示为单个文件设置安全性。

**列表 28-23：为 Admin 角色授予特定文件的访问权限**

```xml
<configuration>
  <location path="Documents/Default.aspx">
    <system.web>
      <authorization>
        <allow roles="Admin" />
        <deny users="*" />
      </authorization>
    </system.web>
  </location>
</configuration>
```

![](img/67a0ff505c05edb961fb30png)

### 锁定配置

ASP.NET 的配置系统在将配置应用于特定应用程序或文件夹方面非常灵活。尽管配置系统是灵活的，但在某些情况下，你可能希望限制特定应用程序可以控制的配置选项。例如，你可以决定存储信息的的方式。这种锁定过程可以使用 `machine.config` 文件中的 `<location>` 节来实现，它识别 "Default/ExampleApplication" 并允许该应用程序覆盖 `<trace>` 节。

**列表 28-4：在底层文件中允许覆盖 `<trace>` 节**

```xml
<configuration>
  <location path="Default/ExampleApplication" allowOverride="true">
    <trace enabled="false"/>
  </location>
</configuration>
```

如果 `allowOverride` 属性设置为 `true`，则可以覆盖 `trace` 属性。但是，如果你在 `machine.config` 文件的 `<location>` 节中写了 `allowOverride="false"`，则 ExampleApplication 的 `web.config` 将无法覆盖该设置。

### ASP.NET 页面配置

当部署 ASP.NET 页面时，配置文件的 `<pages>` 节允许你控制每个 ASP.NET 页面的默认行为。这些行为包括在发送输出之前是否应该缓冲，或者为整个页面启用会话状态。列表 28-25 显示 `<pages>` 节的示例。

**列表 28-25：配置 `<pages>` 节**

```xml
<configuration>
  <system.web>
    <pages
      buffer="true"
      enableSessionState="true"
      enableViewState="true"
      enablePageEvents="true"
      smartNavigation="false"
      autoWireUp="true"
      mainScrollPositionOnPostBack="false"
      pageBaseType="System.Web.UI.Page"
      userControlBase="System.Web.UI.UserControl"
      parserFilterType=""
      validateRequest="true"
      masterFile=""
      theme=""
      styleTheme=""
      maxPageLength="-1"
      compilation="Always"
      viewStateEncryptionModes="Auto"
      asyncTimeout="45"
      renderAllHiddenFieldsAtTopOfForm="true"
      clientMode="Predictable"
      renderingCompatibilityVersion="4.0">
      <namespaces autoImportNamespace="true">
        <add namespace="String, Required, CollectionKey" />
      </namespaces>
      <controls>
        <tagMapping />
        <ignoreDeviceFilters />
      </controls>
    </pages>
  </system.web>
</configuration>
```

以下列表详细提供了一些 ASP.NET 页面配置元素：

- **buffer**：指定请求在发送到客户端之前必须在服务器上进行缓冲。
