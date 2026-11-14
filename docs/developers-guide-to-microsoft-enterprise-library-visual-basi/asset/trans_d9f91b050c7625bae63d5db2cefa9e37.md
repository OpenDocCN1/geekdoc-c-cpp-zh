

配置，除非您在本地配置中对其进行配置以覆盖它们。当某个设置在父源和本地配置中均指定时，将应用本地配置设置。

- 5. 要编辑共享父配置存储区的内容，必须在配置工具或文本编辑器中打开该配置；当本地应用程序的配置在配置工具中打开时，无法编辑父节的配置。如果在配置工具中打开父配置，请确保该配置的“所选源”属性设置为系统配置源。

配置设置的合并方式以及生成的配置中项目的顺序，遵循一组预定义的规则。这些规则在随 Enterprise Library 安装的文档中有详细说明，并可在线查阅：http://go.microsoft.com/fwlink/?LinkId=128874。

## 方案 7：在不同部署环境中管理配置

在此方案中，您希望能够为同一应用程序定义不同的配置设置，以便在将其部署到不同环境（例如测试环境和生产环境）时适用。在大多数情况下，差异较小，通常涉及数据库连接字符串或为某个块使用不同提供程序等设置。Enterprise Library 通过名为“环境覆盖”的功能实现此功能。其原理是，您为两个或多个环境中不同的设置指定覆盖值，并将差异保存为单独的增量配置文件。然后，管理员在每个环境中部署应用程序时，将这些差异应用到主配置文件中。要实现此目标：

- 1. 按照第 1 章“简介”中“使用配置工具”部分的逐步过程中的说明进行操作，该部分介绍了如何在配置工具中配置多个环境以及如何定义覆盖设置。

- 2. 单击环境标题右侧的箭头以打开添加到配置中的每个环境的属性窗格，并将“环境增量文件”属性设置为该环境的增量文件路径和名称。

- 3. 保存配置。配置工具会为每个环境生成一个普通 (.config) 文件和一个增量 (.dconfig) 文件。增量文件可以由管理员管理，并在需要时存储在单独的安全位置。例如，当生产环境设置不应对开发人员或测试人员可见时，这可能很合适。

- 4. 要创建运行时合并的配置文件（通常由管理员执行此操作）：
  - 打开本地配置 (config) 文件。
  - 从“环境”菜单中选择 **打开增量文件** 并加载适当的覆盖配置 (dconfig) 文件。
  - 将环境属性窗格中的 **环境配置文件** 属性设置为该环境的合并配置文件路径和名称。
  - 右键单击环境标题，然后单击 **导出合并的环境配置文件**。

- 5. 在目标环境中部署合并的配置文件。

Enterprise Library 还包含一个名为 MergeConfiguration.exe 的命令行实用程序，如果您没有在管理系统上部署配置控制台，可以使用它来合并配置文件和增量文件。如果您希望将配置合并作为部署过程的一部分进行自动化，也可以使用它。有关 MergeConfiguration.exe 的信息包含在随 Enterprise Library 安装的文档中。

> *您无法在重定向节或继承的配置设置中使用环境覆盖。仅当应用程序的整个配置在本地配置源中定义时，才能使用它们。*

有关此处介绍的所有方案的更多信息，请参阅随 Enterprise Library 安装的文档，并可在线查阅：http://go.microsoft.com/fwlink/?LinkId=188874。

## 附录 E 加密配置文件

Enterprise Library 支持加密配置信息。除非您的服务器完全免受物理入侵和网络远程入侵，否则应考虑加密包含敏感信息的任何配置文件，例如数据库连接字符串、密码和用户名或验证规则。

您可以选择系统 Machine.config 文件中包含的任何加密提供程序。通常，这些是使用 Microsoft® Windows® 数据保护 API (DPAPI) 的 **数据保护配置提供程序** 和使用 RSA 的 **RSA受保护配置提供程序**。这些提供程序的设置（例如密钥存储位置）也在 Machine.config 文件中。您无法使用配置工具编辑此文件；相反，必须使用文本编辑器或操作系统配置工具对其进行修改。

作为此选项效果的示例，以下是数据访问块的简单未加密配置。

```
<dataConfiguration defaultDatabase="Connection String" />
<connectionStrings>
  <add name="Connection String"
    connectionString="Database=TheImportantOne; Server=WEHAVELIFTOFF;
    User ID=secret; Password=DontTellNE1"
    providerName="System.Data.SqlClient" />
</connectionStrings>
```

当您指定 **数据保护配置提供程序** 选项时，生成的配置节如下所示。

```
<dataConfiguration
  configProtectionProvider="DataProtectionConfigurationProvider">
  <EncryptedData>
    <CipherData>
      <CipherValue>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAAbCHTvqG8QbuQI1BYa0uH
yTm50vQjNdSiohA5Fo6bXQh0R5VsvUxdcFNuGkHuhUaH15RZSN5WDM2CDmiQg
...
JyEadytIBvTbCmxXefuWNSMT/ T
</CipherValue>
</CipherData>
</EncryptedData>
</connectionStrings>
<connectionStrings
configProtectionProvider="DataProtectionConfigurationProvider">
<EncryptedData>
<CipherData>
<CipherValue>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAcHVgTvQb80uQiB1ya0uH
..
zBjP7SQXVAsA<=</CipherValue>
</CipherData>
</EncryptedData>
</connectionStrings>
```

如果您只打算将加密的配置文件部署到加密文件所在的服务器，可以使用 **数据保护配置提供程序**。但是，如果您要将加密的配置文件部署到不同的服务器，或部署到 Web 场中的多个服务器，则应使用 **RSA受保护配置提供程序**。您需要导出解密数据所需的 RSA 私钥。然后，可以将配置文件和导出的密钥部署到目标服务器，并重新导入密钥。有关更多信息，请参阅 http://msdn.microsoft.com/en-us/library/ywx286t2(VS.80).aspx 上的“导入和导出受保护配置 RSA 密钥容器”。

当然，接下来的显而易见的问题是“我如何解密配置？”幸运的是，您不需要这样做。只要加密文件是在该计算机上创建的，或者您已导入 RSA 密钥文件，就可以在配置工具中打开加密文件。此外，只要满足相同条件，Enterprise Library 块就能自动解密和读取配置。

- A
- 访问器 另请参阅 数据访问应用程序块
- ACID 原则, 53
- AddInParameter 方法, 27
- AddOutParameter 方法, 27
- AddParameter 方法, 27
- 高级配置方案, 237-242
- AndCompositeValidator 验证器, 174
- AnnotatedProduct 类, 170-171
- 附录, 233-242
  - 高级配置方案, 237-242
  - 应用程序的常见配置结构, 240-241
  - 多个应用程序的配置, 238
  - 默认应用程序配置文件, 237
  - 在不同环境中, 241-242
  - 非默认配置, 237-238
  - 跨多个应用程序共享, 239-240
  - 在多个应用程序之间共享, 238
- 配置方案, 235-242
  - 流式接口, 236
  - 编程支持, 234
- Enterprise Library 中的依赖项注入, 227-232
- 备用服务定位器或容器, 231-232
- 基于请求的应用程序中的容器引用, 230-231
- 将配置信息加载到 Unity 容器中, 227-228
- 在应用程序启动时填充对象图, 229-230
- 容器中的注册, 228-229
- 使用 Unity 进行依赖项注入, 233-244
- 加密配置文件, 243-244
- Enterprise Library 中的策略注入, 233-234
- 应用程序块, 2
- 可选依赖项, 6-7
- 在 WCF 应用程序边界应用异常屏蔽示例, 81
- 面向切面编程 (AOP) 范式, 233
- ASP.NET 用户界面验证, 180-181
- 程序集
- 数据访问应用程序块, 28-29 和参考概述, 7-8
- 基于属性的技术, 216
- AttributeValidatorFactory, 173
- 验证用户并缓存标识示例, 204-205
- 授权
- 授权规则提供程序, 198
- 授权规则, 202
- 授权管理器 (AzMan), 198-199, 210-211
- AuthorizationProvider 类, 212
- 使用存储规则为进程授权用户示例, 209-210
- 使用 AzMan 规则为进程授权用户示例, 210-211

