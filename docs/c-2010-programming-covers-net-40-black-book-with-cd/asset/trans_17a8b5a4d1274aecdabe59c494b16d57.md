

## 冒充身份与委派

我们已经讨论过，所有 ASP.NET 应用程序默认都在 NETWORK SERVICE 用户账户下运行。此内置 Windows 账户为 ASP.NET 应用程序所在的默认应用程序池提供身份。NETWORK SERVICE 账户在 Windows 计算机上具有有限的权限和特权。这意味着 ASP.NET 应用程序只能访问某些文件并在计算机上执行特定操作。例如，ASP.NET 应用程序可以读取和写入计算机上的数据库，但不能删除数据库日志。此外，通过这种对 ASP.NET 应用程序的低权限访问，在 Web 服务器遭到入侵的情况下，应用程序的安全性和可靠性得以保持。

可能存在这样的情况：你希望 ASP.NET 应用程序访问 Web 服务器上的文件、数据库或任何其他本地资源，但 NETWORK SERVICE 账户没有所需的权限。在这种情况下，你可以让 ASP.NET 应用程序冒充拥有所需特权的 Windows 用户。例如，你的 ASP.NET 应用程序可以冒充具有管理特权的用户来访问本地资源。

在 ASP.NET 中，冒充身份是指获取 ASP.NET 应用程序的匿名用户或经过身份验证的用户（Windows 身份验证）的身份，并以该用户身份执行应用程序。通过这种方式，ASP.NET 应用程序可以访问 Web 服务器上用户拥有权限的所有资源。你只能在应用程序中使用 Windows 身份验证时才可在 ASP.NET 应用程序中实现冒充身份。你可能还记得，当在 ASP.NET 应用程序中启用 Windows 身份验证时，身份验证仅在 IIS 级别需要；应用程序不执行任何身份验证，而是使用 IIS 提供的身份。在 IIS 中，你可以启用匿名、Windows、基本或摘要身份验证模式，以便在 ASP.NET 应用程序级别与 Windows 用户配合使用。这意味着基于 IIS 传递的身份，ASP.NET 应用程序可以冒充 Windows 用户。你可以通过以下三种方式实现冒充身份：

- 冒充匿名用户，其身份由 IIS 提供 — 当你在 ASP.NET 应用程序中实现冒充身份并在 IIS 中启用匿名身份验证时发生。在这种情况下，ASP.NET 应用程序以匿名用户身份运行，默认情况下为 IUSR。
- 冒充当前已登录的 Windows 用户，该用户由 IIS 进行身份验证 — 当你在 ASP.NET 应用程序中实现冒充身份并在 IIS 中启用 Windows、基本或摘要身份验证中的任意一种（且在 IIS 中禁用匿名身份验证）时发生。在这种情况下，ASP.NET 应用程序冒充用于登录应用程序的 Windows 用户的凭据。
- 为所有匿名用户和经过身份验证的用户冒充特定的 Windows 用户 — 当你在 ASP.NET 应用程序中实现冒充身份并提供特定 Windows 用户的凭据时发生。在这种情况下，无论在 IIS 和 ASP.NET 应用程序中启用了何种身份验证，应用程序始终以冒充的用户身份运行。请注意，对于这种情况，你需要使用访问控制列表（ACL）来确保被冒充的 Windows 用户具有写入位置为 C:\Windows\Microsoft.NET\Framework\v4.0.30319 的 Temporary ASP.NET Files 文件夹的权限。Temporary ASP.NET Files 文件夹是存储所有 ASP.NET 应用程序编译文件的[content]

## 冒充身份与委派

我们已经讨论过，所有 ASP.NET 应用程序默认都在 NETWORK SERVICE 用户账户下运行。此内置 Windows 账户为 ASP.NET 应用程序所在的默认应用程序池提供身份。NETWORK SERVICE 账户在 Windows 计算机上具有有限的权限和特权。这意味着 ASP.NET 应用程序只能访问某些文件并在计算机上执行特定操作。例如，ASP.NET 应用程序可以读取和写入计算机上的数据库，但不能删除数据库日志。此外，通过这种对 ASP.NET 应用程序的低权限访问，在 Web 服务器遭到入侵的情况下，应用程序的安全性和可靠性得以保持。

可能存在这样的情况：你希望 ASP.NET 应用程序访问 Web 服务器上的文件、数据库或任何其他本地资源，但 NETWORK SERVICE 账户没有所需的权限。在这种情况下，你可以让 ASP.NET 应用程序冒充拥有所需特权的 Windows 用户。例如，你的 ASP.NET 应用程序可以冒充具有管理特权的用户来访问本地资源。

在 ASP.NET 中，冒充身份是指获取 ASP.NET 应用程序的匿名用户或经过身份验证的用户（Windows 身份验证）的身份，并以该用户身份执行应用程序。通过这种方式，ASP.NET 应用程序可以访问 Web 服务器上用户拥有权限的所有资源。你只能在应用程序中使用 Windows 身份验证时才可在 ASP.NET 应用程序中实现冒充身份。你可能还记得，当在 ASP.NET 应用程序中启用 Windows 身份验证时，身份验证仅在 IIS 级别需要；应用程序不执行任何身份验证，而是使用 IIS 提供的身份。在 IIS 中，你可以启用匿名、Windows、基本或摘要身份验证模式，以便在 ASP.NET 应用程序级别与 Windows 用户配合使用。这意味着基于 IIS 传递的身份，ASP.NET 应用程序可以冒充 Windows 用户。你可以通过以下三种方式实现冒充身份：

- 冒充匿名用户，其身份由 IIS 提供 — 当你在 ASP.NET 应用程序中实现冒充身份并在 IIS 中启用匿名身份验证时发生。在这种情况下，ASP.NET 应用程序以匿名用户身份运行，默认情况下为 IUSR。
- 冒充当前已登录的 Windows 用户，该用户由 IIS 进行身份验证 — 当你在 ASP.NET 应用程序中实现冒充身份并在 IIS 中启用 Windows、基本或摘要身份验证中的任意一种（且在 IIS 中禁用匿名身份验证）时发生。在这种情况下，ASP.NET 应用程序冒充用于登录应用程序的 Windows 用户的凭据。
- 为所有匿名用户和经过身份验证的用户冒充特定的 Windows 用户 — 当你在 ASP.NET 应用程序中实现冒充身份并提供特定 Windows 用户的凭据时发生。在这种情况下，无论在 IIS 和 ASP.NET 应用程序中启用了何种身份验证，应用程序始终以冒充的用户身份运行。请注意，对于这种情况，你需要使用访问控制列表（ACL）来确保被冒充的 Windows 用户具有写入位置为 C:\Windows\Microsoft.NET\Framework\v4.0.30319 的 Temporary ASP.NET Files 文件夹的权限。Temporary ASP.NET Files 文件夹是存储所有 ASP.NET 应用程序编译文件的位置。

要有效地在 ASP.NET 应用程序中实现冒充身份，你需要在 IIS 中以及在应用程序中启用冒充身份。要在 IIS 中启用冒充身份，双击身份验证功能选项，即可打开身份验证窗格。右键单击 ASP.NET 冒充身份选项并选择启用。

你还需要启用 ASP.NET 冒充身份，因为默认情况下它是禁用的。你可以通过在 ASP.NET 应用程序的 web.config 文件中使用 <identity> 元素来实现。 <identity> 元素允许你指定是否在 ASP.NET 应用程序中启用或禁用冒充身份。例如，要在 ASP.NET 应用程序中启用冒充身份，你可以使用以下代码中的 <identity> 元素：

```
<identity impersonate="true"/>
```

如果希望 ASP.NET 应用程序始终冒充特定用户，则可以使用以下代码中的 <identity> 元素：

```
<identity impersonate="true" userName="testuser" password="testuser"/>
```

在此代码中，ASP.NET 应用程序冒充具有相同用户名和密码的 Windows 用户，在此例中为 testuser。

当你想在应用程序中禁用冒充身份时，可以使用以下代码中的 <identity> 元素：

```
<identity impersonate="false"/>
```

> NOTE
> 你将在本章后面了解更多关于 <identity> 元素的信息。

你也可以通过代码在 ASP.NET 应用程序中使用冒充身份。这在你希望 ASP.NET 应用程序暂时冒充 Windows 用户访问特定资源，然后再更改回应用程序的原始账户时特别有用。你可以通过使用 WindowsIdentity 类的 Impersonate() 方法在 ASP.NET 中实现编程冒充身份。如前所述，WindowsIdentity 类表示 Windows 用户的身份。因此，你可以使用当前 Windows 用户的 WindowsIdentity 对象以及该对象的 Impersonate() 方法，允许特定的 ASP.NET 代码冒充 Windows 用户。与 web.config 文件类似，你也可以指定特定用户的用户名和密码，以使代码在该用户的安全上下文下为所有请求运行。

通过冒充身份，ASP.NET 应用程序可以使用 Windows 用户的身份并访问 Web 服务器上的资源。现在，假设 ASP.NET 应用程序需要访问网络上其他客户端（计算机）或远程计算机上的资源，例如需要访问网络共享的应用程序。在这种情况下，你可以使用同一 Windows 用户的身份并访问远程计算机上的资源。此过程称为委派，它只是冒充身份的扩展形式。在委派中，ASP.NET 应用程序冒充 Windows 用户并访问另一台计算机上的资源，即被冒充 Windows 用户的凭据被委派给存在预期资源的那台其他计算机。请注意，委派仅在基本和 Windows（Kerberos）身份验证下才可能。

> NOTE
> 在 ASP.NET 应用程序中实现委派时，你需要谨慎行事，因为委派的不当使用可能会损害网络安全。

现在，让我们学习 web.config 文件中的各个元素。

## 通过 ASP.NET 配置文件实现安全

如前所述，你可以通过使用 ASP.NET 应用程序的配置文件在应用程序本身中实现 ASP.NET 应用程序的安全性。如你所知，ASP.NET 应用程序有一个名为 web.config 的配置文件。它包含文件所在目录的设置。应用于一个目录的设置会应用于其子目录，前提是子目录没有自己的 web.config 文件。请注意，除了不同 ASP.NET 应用程序各自的 web.config 文件外，你的计算机上 C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config 文件夹中还有一个根 web.config 文件。此根 web.config 文件具有适用于所有 ASP.NET 应用程序的通用配置设置。其中一些设置与 machine.config 文件中的设置相同。

web.config 文件具有某些 XML 元素，你可以使用它们为 ASP.NET 应用程序提供安全性。涉及 ASP.NET 应用程序安全的 XML 元素包括 <authentication>、<authorization>、<identity> 和 <location>。你也可能在 machine.config 文件中找到这些元素。请注意，这些元素的设置仅适用于 ASP.NET 资源。因此，你将了解这四个元素所代表的含义以及如何使用它们在 ASP.NET 应用程序中实现安全性。

### <authentication> 元素

<authentication> 元素定义为 ASP.NET 应用程序指定的身份验证模式或方案。你可以在 machine.config 文件、根 web.config 文件或 Web 应用程序或站点的 web.config 文件中使用此元素。任何尝试在子目录或页面级 web.config 文件中使用它的尝试都会导致错误。 <authentication> 元素出现在 <system.web> 元素内，而 <system.web> 元素本身位于 <configuration> 元素内。 <authentication> 元素的语法如下：

