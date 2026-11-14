

为算法生成一个密钥。其他提供程序，例如 SHA 和 MD5，不需要密钥。作为一般建议，您应至少使用 SHA256 算法进行哈希处理，并尽可能使用更强大的版本，例如 SHA384 或 SHA512。

您可以在加密块中使用两种不同类型的 **对称加密提供程序**（您创建的自定义提供程序除外）。您可以选择 DPAPI 提供程序，或 AES 或 3DES 等知名对称算法之一。作为一般建议，您应尽量使用 AES (Rijndael) 算法进行加密。

> 关于许多不同加密和哈希算法的全面信息载于《应用密码学手册》（Menezes, Alfred J., Paul C. van Oorschot and Scott A. Vanstone, CRC Press, October 1996, ISBN: 0-8493-8523-7）。有关更多信息，请参见 http://www.cacr.math.uwaterloo.ca/hac/。您还可以在“加密的其他文档”（http://msdn.microsoft.com/en-us/library/aa375543(VS.85).aspx）中找到一份专注于加密的出版物列表。

## 配置加密提供程序

除了为添加到配置中的每个加密提供程序设置名称等明显属性外，某些提供程序还要求您指定加密密钥。如果您已为所选算法类型拥有 DPAPI 加密的密钥文件，可以使用该文件。或者，您可以复制适当大小的现有纯文本值，并将其用作密钥值。第三种方法是允许 Enterprise Library 配置为您生成新密钥。

当您将需要密钥的提供程序添加到配置中时，配置工具将启动加密密钥向导。这使您可以轻松选择或创建所需的密钥，将其保存到文件中，并在配置中设置适当的值。您可能会觉得令人困惑的唯一页面是最后一页，您必须在其中指定对密钥的机器模式或用户模式访问权限。

如果您的应用程序在不与其他应用程序共享的专用服务器上运行，或者您有多个在同一服务器上运行的应用程序并希望这些应用程序能够共享敏感信息，则应选择 **机器** 模式。

如果您在共享托管环境中运行应用程序，并希望确保应用程序的敏感数据不可被服务器上的其他应用程序访问，请选择 **用户** 模式。在这种情况下，每个应用程序应在单独的标识下运行，并且应用程序的资源（例如文件和数据库）应限制为该标识。

如果您将 DPAPI 对称加密提供程序添加到对称提供程序列表中，可以将保护范围指定为 **CurrentUser** 或 **LocalMachine**。当前用户意味着 DPAPI 使用加载的用户配置文件生成密钥，并且只有该用户帐户可以解密加密的数据。本地计算机意味着在计算机上运行的任何代码都可以访问受保护的密钥，并可以解密以相同模式加密的任何机密。

## 添加所需的引用

要在应用程序中使用加密块功能，必须引用所需的程序集，然后在代码中实例化要使用的对象。除了每个 Enterprise Library 项目所需的 Enterprise Library 程序集（在第 1 章“简介”中列出）之外，您还应引用或将以下程序集添加到 bin 文件夹中：

- Microsoft.Practices.EnterpriseLibrary.Security.Cryptography.dll
- Microsoft.Practices.EnterpriseLibrary.Security.Caching.dll

为了更轻松地在项目中使用加密块中的对象，您可以向项目添加相关命名空间的引用。然后您就可以开始编写代码了。以下部分演示了您可以完成的任务，并提供了有关块如何帮助您实现常见且可重用的加密策略的更多详细信息。

但是，在开始使用块中的对象之前，必须解析 CryptographyManager 类的实例。该类公开了用于在代码中与加密提供程序（对称提供程序和哈希提供程序）交互的 API。最简单的方法是使用 Enterprise Library 容器的 GetInstance 方法，如下所示。

```
' Resolve the default CryptographyManager object from the container.
Dim defaultCrypto As CryptographyManager _
    = EnterpriseLibraryContainer.Current.GetInstance(Of CryptographyManager)()
```

### 通过示例深入了解

您可以下载一个示例应用程序（一个简单的控制台应用程序），它演示了本章余下部分中您将看到的所有场景。您可以直接从 bin\debug 文件夹运行它，或在 Microsoft® Visual Studio® 中打开名为 Cryptography 的解决方案，以在运行示例时查看所有代码。

在尝试运行示例之前，必须为块创建新的加密密钥，以便在使用对称加密提供程序时加密数据。这是因为密钥与用户或计算机相关联，因此示例文件中包含的密钥无法在您的计算机上使用。在配置控制台中，选择 AesManaged 对称提供程序，并单击“密钥”属性中的“...”按钮以启动密钥向导。使用此向导生成新密钥，保存密钥文件，并自动更新 App.config 的内容。然后对 RijndaelManager 对称提供程序重复此过程。Rijndael 是 AES 算法的一种实现。但是，我们将在演示如何加密和解密值类型和对象时同时演示这两者。

## 使用对称提供程序加密和解密数据

要加密和解密信息，请使用对称加密提供程序。如前所述，加密块包含多个对称加密提供程序。我们提供的示例使用其中两个：AES 托管对称算法提供程序和 Rijndael 托管对称算法提供程序。示例演示了如何使用这些提供程序加密文本字符串和对象（在我们的示例中，这是一个名为 **Product** 的简单类），以及如何解密加密的项目。

加密管理器公开了用于处理对称加密提供程序的两个方法：

- **EncryptSymmetric** 方法的参数为应用程序中加密块配置的对称提供程序名称以及要加密的项目。此方法有两个重载。一个接受字符串并返回包含加密文本的 Base-64 编码字符串。第二个重载接受作为字节数组的要加密的数据，并返回包含加密数据的字节数组。

- **DecryptSymmetric** 方法的参数为应用程序中加密块配置的对称提供程序名称以及要解密的项目。此方法有两个重载。一个接受包含加密文本的 Base-64 编码字符串并返回解密后的文本。第二个重载接受包含加密数据的字节数组，并返回包含解密项目的字节数组。

### 加密和解密文本字符串

第一个示例 *使用对称算法加密和解密文本字符串* 使用 AES 托管对称算法提供程序来加密和解密文本字符串。

下面所示的代码创建一个文本字符串，然后调用加密管理器的 **EncryptSymmetric** 方法，向其传递应用程序配置中定义的 AES 托管对称算法提供程序的名称以及要加密的文本字符串。要解密生成的字符串，代码随后调用加密管理器的 **DecryptSymmetric** 方法，向其传递（如前所述）应用程序配置中定义的 AES 托管对称算法提供程序的名称以及加密的 Base-64 编码字符串。我们删除了仅将值写入控制台屏幕的某些代码行，以便更轻松地查看实际执行工作的代码。

```
' Define the text string instance to encrypt.
Dim sampleText As String = "This is some text to encrypt."

' Use the AES Symmetric Algorithm Provider.
' The overload of the EncryptSymmetric method that takes a
' string returns the result as a Base-64 encoded string.
Dim encrypted As String = defaultCrypto.EncryptSymmetric("AesManaged", sampleText)

' Now decrypt the result string.
```

