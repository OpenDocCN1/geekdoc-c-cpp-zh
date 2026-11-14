

子文件夹，直到找到 **File\\CachingExample** 子文件夹。然后删除整个文件夹树。您应避免删除 **独立存储** 文件夹中的所有文件夹，因为这些文件夹可能包含其他应用程序使用的数据。

## 加密缓存的数据

默认情况下，缓存块不会加密其在内存或持久化后备存储中存储的数据。但是，您可以配置该块以使用加密提供程序，该提供程序将加密缓存管理器在后备存储中存储的数据——但请注意，内存缓存中的数据从未被加密。

要使用加密，只需将加密提供程序添加到后备存储的配置中。当您首次添加加密提供程序时，配置工具会自动将加密块添加到您的配置中。因此，您必须确保相关程序集 **Microsoft.Practices.EnterpriseLibrary.Security.Cryptography.dll** 已在您的项目中引用。

将加密提供程序添加到后备存储的配置后，通过添加新的对称提供程序来配置加密部分，并使用密钥向导生成新的加密密钥文件或导入现有密钥。然后，回到缓存块的配置中，为后备存储的对称加密属性选择您添加的新对称提供程序。有关配置加密块的更多信息，请参见第 7 章，“减轻加密复杂性”。

本章提供的示例包括一个名为 **加密后备存储中的缓存数据** 的示例，它演示了如何加密持久化数据。它实例化了应用程序配置中名为 **EncryptedCacheManager** 的缓存管理器：

```
' Resolve a CacheManager instance that encrypts the cached data.
Dim encryptedCache As ICacheManager _
    = EnterpriseLibraryContainer.Current.GetInstance(Of _
    ICacheManager)("EncryptedCacheManager")
...
CacheItemsAndShowCacheContents(encryptedCache)
```

代码随后执行您在第一个示例中看到的相同 **CacheItemsAndShowCacheContents** 例程，并将 **encryptedCache** 缓存管理器的引用传递给它。同样，当您运行此示例时看到的结果与您在本章第一个示例中看到的结果相同。

如果您在运行此示例时发现出现错误，可能是您未创建加密块可用的合适加密密钥，或 App.config 文件中密钥文件的绝对路径不正确。要解决此问题，请打开配置控制台，导航到加密应用程序块设置的对称提供程序部分，并选择 RijndaelManaged 提供程序。单击密钥属性中的“...”按钮以启动加密密钥向导。使用此向导生成新密钥，保存密钥文件，并自动更新 App.config 的内容。

## 使用数据库后备存储

如果您愿意，可以轻松快速地配置缓存块，以使用数据库作为缓存数据的持久化后备存储。企业库包含一个脚本和一个命令文件，您可以运行它们来创建数据库（位于企业库源代码的 \\Blocks\\Caching\\Src\\Database\\Scripts 文件夹中）。我们还将这些脚本与本章的示例一起提供。

这些脚本假设您将使用本地安装的 SQL Server Express 数据库，但您可以编辑 CreateCachingDb.cmd 文件以将目标更改为不同的数据库服务器。命令文件执行的 SQL 脚本会创建一个名为 Caching 的数据库，并向其中添加所需的表和存储过程。

但是，如果您只想运行我们为本章提供的示例应用程序，则无需创建数据库。项目包含一个预配置的数据库文件（位于 bin\\Debug 文件夹），它会自动附加到您的本地 SQL Server Express 实例。您可以使用 Microsoft® Visual Studio® 服务器资源管理器连接到此数据库以查看其内容，如图 3 所示。

![](img/d7009d38323c3b86f2dfbc5155fbf141_154_0.png)

图 3 查看数据库表中的缓存内容

要将缓存配置为使用数据库，只需使用配置控制台将数据库缓存存储提供程序添加到缓存管理器，并指定连接字符串和 ADO.NET 数据提供程序类型（默认值为 System.Data.SqlClient，但如果您使用的是不同的数据库系统，可以更改此设置）。

您还可以为缓存指定分区名称，方式与独立存储后备存储提供程序相同。这允许您为同一用户的不同应用程序（或不同缓存管理器）分离缓存数据，方法是有效地将每个数据隔离在数据库表中的不同分区内。

除了将缓存管理器配置为使用数据库后备存储之外，您用于缓存和检索数据的代码是相同的。示例“在数据库后备存储中缓存数据”使用名为 DatabaseCacheManager 的缓存管理器，该管理器配置了数据缓存存储后备存储。与先前的示例一样，代码通过在调用当前企业库容器的 GetInstance 方法时指定名称来检索此缓存管理器的引用。

```
' Retrieve a CacheManager instance that uses a Database Backing Store.
Dim databaseCache As ICacheManager _
= EnterpriseLibraryContainer.Current.GetInstance(Of _
ICacheManager)("DatabaseCacheManager")
...
CacheItemsAndShowCacheContents(databaseCache)
```

代码随后执行您在第一个示例中看到的相同 CacheItemsAndShowCacheContents 例程，并将 databaseCache 缓存管理器的引用传递给它。如您所料，当您运行此示例时看到的结果与您在本章第一个示例中看到的结果相同。

我们为本示例提供的数据库的连接字符串如下：

```
Data Source=.\SQLEXPRESS; AttachDbFilename=|DataDirectory|\Caching.mdf;
Integrated Security=True; User Instance=True
```

如果您使用示例提供的脚本配置了不同的数据库，则运行此示例时可能会出现错误。这可能是因为您的 App.config 文件中数据库的连接字符串无效。此外，请使用管理工具文件夹中的服务小应用程序检查 SQL Server (SQLEXPRESS) 数据库服务（服务名为 MSSQL$SQLEXPRESS）是否正在运行。

## 从缓存中删除项和刷新缓存

在了解了如何向缓存添加项以及使用各种后备存储选项和加密之后，现在是时候了解如何操作缓存以删除项，或通过刷新将其完全清除了。缓存中的项会根据其过期时间或依赖关系自动删除，但您也可以删除单个项或删除所有项。

示例“删除和刷新缓存的项”实际上演示的内容不仅仅是删除和刷新项——它展示了如何使用依赖项从缓存中删除相关项、如何创建扩展时间过期，以及如何使用过期数组。此示例中有大量代码，因此我们将逐步讲解并依次解释每个部分。

### 使用文件依赖项和扩展时间过期

该示例首先创建一个 NeverExpired 过期实例，然后在当前执行文件夹中写入一个文本文件。接着，它针对该文件创建一个 FileDependency。这是一个典型场景：您从文件（例如文本文件或 XML 文档）读取数据，并在代码中频繁访问该数据。但是，如果原始文件被更改或删除，您希望相应的缓存项从缓存中删除。

```
' Create an expiration that never expires
Dim never As New NeverExpired()
' Create a text file to use in a FileDependency
File.AppendAllText("ATextFile.txt", "Some contents for the file")
' Create an expiration dependency on the new text file
Dim fileDep As New FileDependency("ATextFile.txt")
```

接下来，代码创建 ExtendedFormatTime 类的一个实例。该类允许您根据重复计划为缓存项指定过期时间。与您迄今所见的更常见的 SlidingTime 和 AbsoluteTime 过期类型相比，它提供了更多机会。

ExtendedFormatTime 类的构造函数接受一个字符串值，将其解析为分钟、小时、天、月和星期（其中零表示星期日）的单独值，这些值共同指定缓存项过期的频率。每个值由空格分隔。星号表示格式字符串的该部分没有值，并有效地意味着该项的每次出现都会过期。这一切听起来非常复杂，因此一些示例无疑会很有用（请参见表 2）。

| 扩展格式字符串 | 含义 |
| :--- | :--- |
| * * * * * | 每分钟过期。 |
| 5 * * * * | 每小时的第 5 分钟过期。 |
| * 21 * * * | 每天第 21 小时的每分钟过期。 |
| 31 15 * * * | 每天下午 3:31 过期。 |
| 7 4 * * 6 | 每个星期六凌晨 4:07 过期。 |
| 15 21 4 7 * | 每年 7 月 4 日晚上 9:15 过期。 |

该示例生成一个在每小时第 30 分钟过期的 ExtendedFormatTime。然后，它创建一个 ICacheItemExpiration 类型的数组，其中包含先前创建的文件依赖项和新的 ExtendedFormatTime 实例。

```
' Create an extended expiration for 30 minutes past every hour
Dim extTime As New ExtendedFormatTime("30 * * * *")
' Create array of expirations containing the file dependency and extended format
Dim exp As ICacheItemExpiration() = _
    New ICacheItemExpiration() {fileDep, extTime}
```

