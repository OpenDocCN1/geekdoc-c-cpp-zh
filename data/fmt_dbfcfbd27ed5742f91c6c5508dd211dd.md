
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

在 `forms` 模式下，你可以看到 `<authentication>` 元素有一个 `mode` 属性。该属性指的是为 ASP.NET 应用程序指定的身份验证模式。`mode` 属性可以设置一组定义值。这些值如下所示：

你也可以从语法中注意到，`<authentication>` 元素可以有两个子元素，`<forms>` 和 `<password>`。当你使用 Forms 身份验证且 `<authentication>` 元素的 `mode` 属性设置为 Forms 时，就会使用 `<forms>` 元素。`<forms>` 元素有若干个属性，如表 30.16 所示。

表 30.16：`<forms>` 元素的属性
| 属性 | 描述 |
| --- | --- |
| name | 指用于用户身份验证的 HTTP cookie。此属性的默认值是 ASPCOOKIE |
| loginUrl | 指用户需要提供身份验证凭据的页面 URL。此属性的默认值是 login.aspx |
| defaultUrl | 指用户通过身份验证后重定向到的页面 URL。此属性的默认值是 default.aspx |
| protection | 指用于身份验证 cookie 的保护类型。此 cookie 可以具有以下任何一种： |
| All | 表示 cookie 同时被加密和验证使用。这是默认值。 |
| None | 表示应用程序不使用加密和验证来保护 cookie |
| Encryption | 表示应用程序使用 DES 或 3DES 加密 cookie。对 cookie 不进行验证。 |
| Validation | 表示应用程序使用验证机制来保护 cookie。 |
| timeout | 指身份验证 cookie 存在的时间（分钟）。cookie 在此属性指定的时间后过期。其默认值是 30（分钟）。 |
| path | 指存储身份验证 cookie 的路径。此属性的默认值是 /，指应用程序的根文件夹。 |
| requireSSL | 指定执行身份验证 cookie 是否必须使用安全 (SSL) 连接。此属性的默认值是 false。 |
| slidingExpiration | 指定身份验证 cookie 的过期时间是否在同一会话的每次请求中重置。默认值是 false。 |
| enableCrossAppRedirect | 指定身份验证的用户是否可以重定向到 web 应用程序的其他页面。此属性的默认值是 false。 |
| cookeless | 指身份验证 cookie 何时以及如何生成。此属性可以具有以下值之一： |
| UseUri | 表示完全不使用 cookie。 |
| UseCookies | 表示始终使用 cookie。 |
| AutoDetect | 表示仅在 Web 浏览器支持 cookie 时才使用 cookie。尝试使用 cookie 会触发探测机制。 |
| UseDeviceProfile | 表示仅对支持核心的 Web 浏览器使用 cookie。对于支持 cookie 的 Web 浏览器没有探测机制。此的默认值为空字符串。 |
| domain | 指传出的身份验证 cookie 的可选域名。此的默认值为空。 |

`<forms>` 元素可以包含一个 `<credentials>` 元素，允许你在使用表单进行身份验证时指定用户的凭据。`<credentials>` 元素有一个名为 `passwordFormat` 的属性。该属性指代以加密状态存储密码的格式。此属性可以具有以下值：

- * Clear - 表示密码未加密；相反，它们以明文形式存储
- * SHA1 - 表示密码使用 SHA1 哈希算法进行加密，这是默认值
- * MD5 - 表示密码使用 MD5 哈希算法进行加密

`<credentials>` 元素可以包含三个元素：`<clear>`、`<remove>` 和 `<user>`。表 30.17 列出了这三个元素及其语法：

表 30.17：`<credentials>` 元素的子元素
| 元素 | 描述 | 语法 |
| --- | --- | --- |
| <clear> | 允许清除对任何继承连接字符串的所有引用。这些元素允许你仅使用当前用户创建的连接字符串。 | <clear/> |
| <remove> | 允许删除特定用户的引用。 | <remove name=" |
| <user> | 允许定义用户。 | <user name=" |

## 深入探讨

### `<authorization>` 元素
如你所知，`<authorization>` 元素允许指定允许访问资源的用户。你可以在 `machine.config` 文件、根 `Web.config` 文件或 Web 应用程序或网站的 `Web.config` 文件中使用它。任何在子目录或页面层级的 `Web.config` 文件中使用它的尝试都会导致错误。

`<authorization>` 元素出现在 `<system.web>` 元素中，而该元素位于 `<configuration>` 元素中。`<authorization>` 元素的语法如下：

```xml
<authorization>
  <allow users="逗号分隔的用户列表" roles="逗号分隔的角色列表" verbs="逗号分隔的动词列表"/>
  <deny users="逗号分隔的用户列表" roles="逗号分隔的角色列表"/>
</authorization>
```

在上述语法中，你可以看到 `<authorization>` 元素没有任何属性，但可以有两个子元素，`<allow>` 和 `<deny>`。`<allow>` 元素允许你指定拥有 Web 应用程序权限的用户、角色和 HTTP 传输方法。另一方面，`<deny>` 元素允许你拒绝访问 Web 应用程序的用户、角色和 HTTP 传输方法。这两个元素都可以具有三个属性，如表 30.18 所示：

表 30.18：authorization 元素的属性
| 属性 | 描述 |
| --- | --- |
| users | 允许你指定一个逗号分隔的用户列表，以授予/拒绝访问 Web 应用程序的权限。此属性的默认值是星号 (*)，表示所有身份验证的用户都无法访问 Web 应用程序。你可以使用问号 (?) 仅拒绝匿名用户的访问。 |
| roles | 允许你指定一个逗号分隔的角色列表，以授予/拒绝访问 Web 应用程序的权限。空字符串 ("") 表示对没有角色的用户授予/拒绝。 |
| verbs | 允许你指定一个逗号分隔的 HTTP 传输方法列表，这些方法拥有/不拥有访问 Web 应用程序的权限。你指定的 HTTP 传输方法包括 GET、POST、DEBUG 和 HEAD。 |

> 如果你想引用用户或计算机，可以使用点 (.) 来表示当前计算机。这仅适用于 Windows 用户账户。

不建议将 `<deny>` 元素置于 `<allow>` 元素之前，因为访问的允许或拒绝取决于元素在 `<authorization>` 元素中指定的顺序。例如，如果你按如下方式指定 `<deny>` 元素：

```xml
<authorization>
  <deny users="*"/>
  <allow users="Testuser"/>
</authorization>
```

`<allow>` 元素将失效且无法访问 Testuser 用户。

## 深度解析

## `<location>` 元素

你已经知道在 `Web.config` 文件中使用 `<authentication>` 和 `<authorization>` 元素（位于根节点、应用程序或目录级别）如何帮助你保护 ASP.NET Web 应用程序。现在，考虑一种情况：你想保护 Web 应用程序中特定范围的 Web 页面。在这种情况下，你可以使用 `<location>` 元素而不是使用 `<authentication>` 和 `<authorization>` 元素。`<location>` 元素允许你对特定的 Web 应用程序或页面（或一组 Web 页面）应用任何配置设置。你还可以使用 `<location>` 元素来保护特定的 Web 资源，例如虚拟目录或图像。

在 `Web.config` 文件中，`<location>` 元素可以出现在 `<configuration>` 元素内部。`<location>` 元素包含任何子元素，以指定 Web 应用程序、页面或资源的设置。`<location>` 元素的语法如下：

```xml
<location path="/" overrideMode="true">
  <!-- child elements -->
</location>
```

在以下语法中，`<location>` 元素有两个属性：

- `path`—引用你想要保护或应用任何其他配置设置的特定 Web 应用程序、页面或资源。如果省略此属性或将其设置为空字符串，则安全（或配置）设置将应用于当前目录及其所有子目录。
- `overrideMode`—引用是否可以在 `Web.config` 文件中重写安全（或配置）设置。它的值可以是 true 或 false。如果为 true，则可以在子目录中重写设置；如果为 false，则设置不能被重写。该属性的默认值为 true。

注意：

你可以在 `path` 属性中使用 `/~` 来表示当前应用程序根目录。例如，考虑以下代码：

```xml
<location path="~/Customers/Customer.xls">
  <system.web>
    <authorization>
      <deny users="TestUser"/>
    </authorization>
  </system.web>
</location>
```

在前面的代码中，TestUser 被拒绝访问位于当前应用程序根目录下的 Customer 目录中的 Customer.xls 文件。

## `<identity>` 元素

`<identity>` 元素允许你指定 Web 应用程序的标识。这在你想要实现冒充（impersonation）时很有帮助。你可以在 `Web.config` 文件的根应用程序级别或目录级别使用 `<identity>` 元素。`<identity>` 元素可以出现在根或目录级别的 `Web.config` 文件的 `<system.web>` 内部。`<identity>` 元素的语法如下：

```xml
<identity impersonate="true" username="domain\username" password="secure"/>
```

在以下语法中，`<identity>` 元素有三个属性：

- `impersonate`—引用是否使用客户端冒充。该属性的值可以是 true 或 false。该属性的默认值为 false，这意味着不使用冒充。如果你将该属性设置为 true，则在每个请求上都会使用冒充。
- `username`—引用在启用冒充时使用的用户名。
- `password`—引用在启用冒充时使用的密码。

## 第 3 章：.NET 4.5 安全

> 注意
> `<identity>` 元素的 `username` 和 `password` 属性的值以明文形式存储在 `Web.config` 文件中。然而，你可能选择加密这些值并将它们保存在注册表中。若要在存在注册表中存储 `username` 和 `password` 属性的加密值，你首先需要将这些值加密为 REG_BINARY 格式，然后使用 `Aspnet_reg.exe` 工具将这些值添加到注册表中。之后，你需要使用来自 `<identity>` 元素的注册表项来指定读取值的键。

## 成员功能 (Membership Feature)

ASP.NET 功能提供了一种在数据存储中存储授权用户凭据的方法。使用成员功能存储用户凭据两个主要优势是：

- 抽象用户凭据
- 减少基于表单身份验证中验证用户凭据的复杂性

现在，让我们如何在使用 ASP.NET 创建的应用程序中实现成员功能。

成员功能通过以下两个提供程序来实现：

- `ActiveDirectoryMembershipProvider`
- `SqlMembershipProvider`

你可以在 ASP.NET 应用程序中使用这两种，你也可以创建自定义的提供程序，以在 Active Directory 和 SQL Server 以外的数据存储中存储用户凭据，例如轻级目录访问协议 (LDAP) 数据。

除了这两个提供程序之外，你还需要使用 `Membership` 和 `MembershipProvider` 类来在 ASP.NET 应用程序中实现成员功能。现在，让我们逐个查看这两个类的详细信息。

## ActiveDirectoryMembershipProvider

`ActiveDirectoryMembershipProvider` 允许你在 Active Directory（活动目录）或 Active Directory Mode (ADAM) 数据存储中存储用户凭据。在本主题中，我们学习为 Web 应用程序配置 `ActiveDirectoryMembershipProvider`。

你需要在 `Web.config` 文件的 `<connectionStrings>` 元素中定义连接字符串以配置 `ActiveDirectoryMembershipProvider`。

定义到 Active Directory 数据存储的语法如下：

```
LDAP://server/userdn
```

在前面的语法中，`server` 是存放 Active Directory 数据存储的计算机名称，`userdn` 是要存储用户凭据的 Active Directory 数据名称。

```xml
<connectionStrings>
<add name="ActiveDirectoryCS" connectionString="LDAP://server/userdn" />
</connectionStrings>
```

在前面的语法中，`server` 是存放 Active Directory 数据存储的计算机名称，`userdn` 是要存储用户凭据的 Active Directory 数据名称。

## 深度解析

现在，让我们查看 `<provider>` 元素的一些属性，你在定义 `<provider>` 时需要设置。表 30.19：`<provider>` 属性

| 属性 | 描述 |
| :--- | :--- |
| connectionPassword | 指定用于访问 Active Directory 的密码。 |
| connectionStringName | 指定位于 `<connectionStrings>` 元素中的连接字符串名称。 |
| connectionUsername | 指定用于访问 Active Directory 的用户名。 |

以下代码说明了 `ActiveDirectoryMembershipProvider` 的配置：

```xml
<membership provider="ActiveDirectoryProvider">
  <provider>
    name="ActiveDirectoryMembershipProvider"
    type="System.Web.ActiveDirectoryMembershipProvider, System.web, Version=0.0.0, Culture=neutral, PublicKeyToken=b0f5ff71d5ua3a"
    connectionString="domain=domain"
    username="administrator"
    connectionPassword="pass"
  </provider>
</membership>
```

## SqlMembershipProvider

`SqlMembershipProvider` 用于在 SQL Server 数据存储中存储凭据。你需要先安装 SQL Server 数据存储，然后配置 `SqlMembershipProvider` 在 ASP.NET 应用程序中使用。SQL Server 数据存储是用于存储凭据的。我们将在后续主题中查看安装 SQL Server 数据存储和配置 `SqlMembershipProvider` 的详情。

## 安装 SQL Server 数据存储

登录到具有管理权限的计算机（例如管理员），以便计算机上安装 SQL Server 数据存储。登录系统后，在 VS2012 开发人员命令提示符上以管理员身份运行 `aspnet_regsq.exe` 工具。`aspnet_regsq.exe` 工具用于为 ASP.NET 的各种功能安装数据存储，如下（使用 `aspnet_regsq` 工具）：

- E - 促进当前使用 sql 的凭据创建
- S - 指定要安装 SQL Server 数据存储的计算机名称
- A - 由 `SqlMembershipProvider` 生成表和存储过程

例如，使用以下命令在计算机上安装 SQL Server 数据存储：

```
aspnet_regsq.exe -E -S server -A m
```
