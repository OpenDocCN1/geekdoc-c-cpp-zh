
请注意，`DynamicForms.dll` 是在加载它的 `DynamicLoading.exe` 项目之后才创建并编译的。只要 `DynamicLoading.exe` 知道程序集的位置以及要从该程序集加载的类型，就不需要重新编译，甚至不需要重启 `DynamicLoading.exe` 即可动态加载新程序集。

### 将程序集投入使用

前面的代码示例将程序集的位置和类型标识以硬编码字符串的形式写入代码。这类技术有其用途，例如某些类型的应用程序 Internet 部署。但是，在使用动态加载时，这些值通常是从代码外部获取的。例如，可以使用数据库表或基于 XML 的配置文件来存储这些信息。

这样，你便可以在应用程序运行时即时添加新功能。可以编写一个具有新功能的新程序集，然后将该程序集的位置以及要从该程序集加载的类型的标识添加到配置文件或数据库表中。

与由 CLR 自动定位、必须位于应用程序目录或其子目录中的应用程序程序集不同，动态加载的程序集可以位于应用程序知道如何访问的任何位置。可能的位置包括：

- 网站
- 本地计算机上的目录
- 共享网络计算机上的目录

代码可用的安全权限会因程序集加载位置的不同而有所不同。如前所示，与从本地目录加载的代码相比，通过 HTTP 从 URL 加载的代码默认情况下拥有的权限非常有限。第 32 章详细介绍了代码访问安全性、默认安全策略，以及如何更改默认策略。

## 总结

程序集是 .NET 中部署和版本控制的基本单元。即使你对程序集了解不多，也可以编写和安装简单的应用程序。更复杂的应用程序则需要深入了解程序集的结构、它们包含的元数据，以及 CLR 如何定位和加载程序集。

你已经了解了程序集的标识如何用于允许同一程序集的多个版本安装在一台计算机上并并行运行。本章解释了程序集如何设定版本、CLR 解析外部程序集引用的过程，以及如何通过配置文件修改这一过程。

你还了解了程序集如何存储有关它所引用的任何外部程序集的信息（例如版本号、强名称和区域性），以及运行时如何检查这些信息以确保引用的是正确版本的程序集。你看到了在程序集存在缺陷时，如何使用版本策略来覆盖这一行为。程序集是减少 DLL 地狱可能导致的错误、并帮助简化部署的最大助力。

你还了解了如何检查程序集，以发现其中包含的类型以及这些类型的成员。你甚至可以利用反射功能对某个类型调用方法。

本章还讨论了基于运行时确定的位置动态加载程序集的能力。这种能力对于某些特殊的部署方案（例如简单的 Internet 部署）很有用。理解所有这些要素有助于你理解如何构建应用程序、何时以及如何使用共享程序集，以及你对程序集所做的选择在部署方面的影响。

简单的应用程序通常不使用强名称，也不使用共享程序集，应用程序的所有程序集都部署到应用程序目录中。只要类接口保持一致，版本问题就很少出现。

复杂的应用程序可能需要将共享程序集放入全局程序集缓存（GAC）中，这意味着这些程序集必须具有强名称，并且你必须控制版本号。你还需要了解各种选项：允许应用程序加载与默认加载版本不同的程序集版本，或者使用应用程序特定的技术来确定程序集的位置并动态加载程序集。本章已涵盖了满足所有这些需求的基础知识。

## 32 .NET Framework 中的安全性

### 本章你将学到什么

- 概念和定义
- 权限
- 角色
- 主体
- 代码访问权限
- 基于角色的权限
- 身份权限
- 用户访问控制 (UAC)
- 加密
- 哈希
- 对称密钥加密
- 非对称密钥加密
- 数字签名
- X.509 证书
- SSL

本章涵盖安全性和加密的基础知识。它首先简要讨论了 .NET Framework 的安全架构，因为这会影响你可能选择实现的所有解决方案。

.NET Framework 为你提供了有关安全的最佳实践、工具和核心功能。你拥有 `System.Security.Permissions` 命名空间，它使你能够控制代码访问权限以及基于角色和身份的权限。通过你的代码，你可以以编程方式控制对对象的访问，以及获取有关对象当前权限的信息。此安全框架将帮助你确定是否有权限运行你的代码，而不是在执行进行到一半时才不得不处理基于权限的异常。

密码学是 .NET Web Services 安全模型的基石，因此本章的后半部分讨论了密码学的基础以及如何实现它。具体涵盖以下内容：

- 哈希算法
- SHA
- MD5
- 密钥加密
- 公钥密码学标准
- 数字签名
- 认证
- 安全套接字层通信

让我们先来看一些安全概念和定义。

> 一如既往，本章的代码可从 www.wrox.com 下载，以便你跟随学习。

### 安全概念和定义

表 32-1 描述了本章中介绍的不同类型的安全性，以及它们如何与现实世界场景相关。

表 32-1：安全类型

| 安全类型 | 与 `System.Security.Permissions` 命名空间中的相关概念 | 目的 |
|---|---|---|
| NTFS | 无 | 允许详细的文件系统权限，例如锁定特定文件 |
| 加密 | 强名称和程序集生成，`SignCode.exe` 实用工具 | 使用公钥基础设施和证书 |
| 编程 | 组和权限集 | 用于被调用的代码片段。为防止调用代码的用户违反程序中未在机器级别提供安全措施，提供额外安全保障。 |
| 用户访问控制 | 用户在没有管理员权限的情况下运行 | 由操作系统提供，帮助用户保护其系统免受使用机器管理员账户登录时可能发生的意外更改。 |

在托管你共享代码的机器上提供安全性的方式有很多。如果一台机器上有多個共享代码应用程序，每个共享代码片段都可能被许多前端应用程序调用。每个共享代码片段在访问其运行所在机器上的环境变量——例如注册表、文件系统和其他项目——时都有自己的安全要求。从 NTFS 角度来看，你的服务器管理员只能锁定那些不需要被该机器上运行的任何共享代码片段访问的项目。因此，一些应用程序需要在内部构建额外的安全措施，以防止任何调用代码执行其不应该执行的操作。

.NET 4 中安全性的一个更显著的变化是移除了代码访问安全策略。与旧的 `Permview.exe` 类似，`CasPol.exe` 现在是一个已过时的实用工具，因此本主题的介绍已被省略。此外，`PermCalc.exe` 工具在 .NET 4 中也已被弃用。

为了限制你的 Internet 应用程序对本地文件系统的访问，你创建一个限制该访问的权限集，并将 Internet 应用程序组与此权限集关联。默认情况下，.NET 环境提供一个名为 `All Code` 的代码组，它与 `FullTrust` 权限集关联。

权限集是安全配置的组合。此集合定义了每个授权用户可以访问的内容以及该用户可以在该机器上执行的操作——例如，用户是否可以读取环境变量或文件系统，或执行其他代码。

在编程环境中使用的安全措施也使用权限集。通过代码你可以控制对文件系统中的文件、环境变量、文件对话框、隔离存储、反射、注册表、套接字和 UI 的访问。隔离存储和虚拟文件系统是新的操作系统级存储位置，可供程序使用并受机器安全策略管辖。这些文件系统通过为文件存储指定受监管区域，从设计上使机器免受文件系统入侵。主要对这些项目的访问是通过代码访问权限控制的。

尽管我们在 Visual Basic 中使用的许多方法都提供可识别的返回值，但我们从安全方法获得返回值的时间仅限于方法失败时。当安全方法成功时，它不会提供返回值。如果失败，则返回反映所发生的特定错误的异常对象。

### `System.Security.Permissions` 命名空间中的权限

`System.Security.Permissions` 命名空间是用于在代码中建立和使用与对象相关联的权限的命名空间，包括文件系统、环境变量和注册表。该命名空间控制对操作系统级对象以及代码对象的访问。为了在你的项目中使用此命名空间，你需要导入它。使用此命名空间可让你访问 `CodeAccessPermission` 和 `PrincipalPermission` 类，用于使用基于角色的权限和身份权限提供的信息。`CodeAccessPermission` 控制对操作系统级对象的访问。基于角色的权限和身份权限根据运行程序的用户身份授予对对象的访问权限（用户上下文）。

表 32-2 列出了适用于 Windows 应用程序编程的 `System.Security.Permissions` 命名空间的成员。虽然每个成员都有相应的描述，但以 `Attribute` 结尾的类，例如 `EnvironmentPermissionAttribute`，是使你能够修改你的代码被允许以何种安全级别与每个相应对象交互的类。这些对象创建了可用于多种不同实现模型的声明式安全设置模型。

默认环境将提供给定的访问级别。通过代码访问安全无法授予超出此级别的访问权限；然而，使用这些类时，你可以指定在给定情况下应允许或不允许的内容。此外，这些类已被标记为防止继承。如果可以从这些类之一继承，那将不是一个非常安全的系统。代码可以编写来覆盖关联的安全方法并授予无限权限。

表 32-2 还涉及与软件发布者的安全问题。软件发布者是使用数字签名在基于 Web 的场景中识别自己的特定实体。

表 32-2：`System.Security.Permissions` 的成员

| 类 | 描述 |
|---|---|
| `CodeAccessSecurityAttribute` | 代码访问安全属性类的基类 |
| `DataProtectionPermission` | 控制对数据保护 API 的访问，T |
| `DataProtectionPermissionAttribute` | 允许通过代码以声明方式控制 `DataProtectionPermission` |
| `EnvironmentPermission` | 控制查看和修改系统和用户环境变量的能力 |

**表 32-2（续）**

| CLASS | DESCRIPTION |
|---|---|
| `EnvironmentPermissionAttribute` | 允许通过代码为环境变量添加安全操作 |
| `FileDialogPermission` | 控制通过文件对话框打开文件的能力 |
| `FileDialogPermissionAttribute` | 允许通过代码为文件对话框添加安全操作 |
| `FileIOPermission` | 控制在文件系统中读写文件的能力 |
| `FileIOPermissionAttribute` | 允许通过代码为文件访问尝试添加安全操作 |
| `GacIdentityPermission` | 定义来自全局程序集缓存（GAC）的文件的身份权限 |
| `GacIdentityPermissionAttribute` | 允许为源自 GAC 的文件添加安全操作 |
| `HostProtectionAttribute` | 允许使用安全操作来确定主机保护要求 |
| `IsolatedStorageFilePermission` | 控制对应用程序隔离存储区域内的私有虚拟文件系统的访问 |
| `IsolatedStorageFilePermissionAttribute` | 允许通过代码为私有虚拟文件系统添加安全操作 |
| `IsolatedStoragePermission` | 控制对应用程序隔离存储区域的访问 |
| `IsolatedStoragePermissionAttribute` | 允许通过代码为应用程序的隔离存储区域添加安全操作 |
| `KeyContainerPermission` | 控制对密钥容器的访问 |
| `KeyContainerPermissionAccessEntry` | 定义特定密钥容器的访问权限 |
| `KeyContainerPermissionAccessEntryCollection` | 表示 `KeyContainerPermission-AccessEntry` 对象的集合 |
| `KeyContainerPermissionAccessEntryEnumerator` | 表示 `KeyContainerPermissionAccessEntryCollection` 对象中包含的对象的枚举器 |
| `KeyContainerPermissionAttribute` | 允许为密钥容器添加安全操作 |
| `MediaPermission` | 与访问音频、视频和图像的能力相关联的权限集。WPF 利用此功能。 |
| `MediaPermissionAttribute` | 允许代码设置与 `MediaPermission` 集相关的权限 |
| `PermissionSetAttribute` | 允许为权限集添加安全操作 |
| `PrincipalPermission` | 控制验证活动主体的能力 |
| `PrincipalPermissionAttribute` | 允许验证特定用户。安全主体是用于建立安全身份的用户和角色组合。 |
| `PublisherIdentityPermission` | 允许基于软件发布者的身份进行访问 |
| `PublisherIdentityPermissionAttribute` | 允许为软件发布者定义安全 |
| `ReflectionPermission` | 控制对给定类型的非公共成员的访问 |
| `ReflectionPermissionAttribute` | 允许为给定类型的公共和非公共成员定义安全 |
| `RegistryPermission` | 控制对注册表项和值的访问 |
| `RegistryPermissionAttribute` | 允许为注册表定义安全 |
| `ResourcePermissionBase` | 控制使用代码访问安全权限的能力 |
| `ResourcePermissionBaseEntry` | 允许您定义代码访问安全权限集的最小部分 |
| `SecurityAttribute` | 控制代表代码的安全属性；用于在创建程序集时控制安全 |
| `SecurityPermission` | 此集合用于在代码中指定一组权限以定义访问。 |
| `SecurityPermissionAttribute` | 允许对安全权限标志进行安全操作 |
| `StorePermission` | 控制对包含 X.509 证书的存储的访问 |
| `StorePermissionAttribute` | 允许为包含 X.509 证书的访问存储添加安全操作 |
| `StrongNameIdentityPermission` | 定义创建强名称的权限级别 |
| `StrongNameIdentityPermissionAttribute` | 允许在 `StrongNameIdentityPermission` 集合上定义安全 |
| `StrongNamePublicKeyBlob` | 与强名称关联的公钥信息 |
| `TypeDescriptorPermission` | 控制对 `TypeDescriptor` 类的部分信任访问的权限集 |
| `TypeDescriptorPermissionAttribute` | 允许在 `TypeDescriptorPermission` 集合上定义安全 |
| `UIPermission` | 控制对用户界面的访问和使用 Windows 剪贴板 |
| `UIPermissionAttribute` | 允许为 UI 接口和使用剪贴板添加安全操作 |
| `UrlIdentityPermission` | 与代码源自的 URL 的身份和相关权限关联的权限集 |
| `UrlIdentityPermissionAttribute` | 允许在 `UrlIdentityPermission` 集合上定义安全 |
| `WebBrowserPermission` | 控制创建 WebBrowser 控件的能力 |
| `WebBrowserPermissionAttribute` | 允许在 `WebBrowserPermission` 集合上定义安全 |
| `ZoneIdentityPermission` | 定义代码源自的区域的身份权限 |
| `ZoneIdentityPermissionAttribute` | 允许在 `ZoneIdentityPermission` 集合上定义安全 |

### 代码访问权限

代码访问权限通过 `System.Security` 命名空间中的 `CodeAccessPermission` 类进行控制。代码访问权限被通用语言运行时（CLR）广泛使用，以管理和保护操作系统环境。

代码访问权限授予和拒绝对操作系统各部分的访问，例如文件系统，但尽管您的代码可以请求权限更改，但存在一个关键限制。使用此 API 的代码可以请求降低当前执行代码的用户权限，但 API 不会授予用户在其当前上下文中或基于 CLR 可用的权限所不拥有的权限。

当代码从网站下载，并且用户随后尝试运行该代码时；CLR 可以选择限制该代码的权限，因为默认情况下不应信任它。例如，如果操作系统不信任该代码，则请求访问系统注册表将被拒绝。因此，应用程序开发人员使用代码访问安全的主要用途是根据用户当前所做的事情的上下文限制用户已有的权限。代码访问安全利用了各种安全类别中使用的许多相同的核心安全方法，其中许多在表 32-3 中进行了描述。

#### 表 32-3：`CodeAccessPermission` 的方法

| 方法 | 描述 |
|---|---|
| `Assert` | 将权限设置为完全访问，以便即使调用方未被授予访问该资源的权限，也可以访问特定资源 |
| `Copy` | 复制权限对象 |
| `Demand` | 除非调用链中的所有调用方都被授予以特定方式访问资源的权限，否则返回异常 |
| `Deny` | 在 .NET 的早期版本中，您会使用此方法明确拒绝访问。这仍然有效，但它变得过时，应避免使用。 |
| `Equals` | 确定给定对象是否是当前对象的同一实例 |
| `FromXml` | 根据特定的 XML 编码建立权限集。此方法接受的参数是 XML 编码。 |
| `Intersect` | 返回两个权限对象共有的权限 |
| `IsSubsetOf` | 返回指示当前权限对象是否是指定权限的子集的结果 |
| `PermitOnly` | 指定只有此权限集内的权限可以被访问，即使程序集的用户已被授予对底层对象的额外权限。这是使用自定义权限集时最常见的权限级别之一。 |
| `RevertAll` | 逆转所有先前的 `assert`、`deny` 或 `permit-only` 方法 |
