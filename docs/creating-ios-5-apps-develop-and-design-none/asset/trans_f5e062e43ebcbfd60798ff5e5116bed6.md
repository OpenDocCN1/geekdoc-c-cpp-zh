
我们可以完整地使用 NSString 的比较方法。我们甚至可以融入我们自己的 Objective-C 代码（通过为排序描述符提供自定义选择器或 NSComparator 块，或者使用 predicateWithBlock: 方法创建谓词）。

然而，当使用 SQLite 存储时，谓词和排序描述符会被转换为 SQL 并在数据库中执行。我们不能使用包含自定义 Objective-C 代码的谓词或排序描述符。SQLite 只支持以下 NSString 排序选择器：compare:、caseInsensitiveCompare:、localizedCompare:、localizedCaseInsensitiveCompare: 和 localizedStandardCompare:。最后，谓词中的键路径只能包含一个对多关系。但是，你可以将任意数量的对一关系和属性与该对多关系串联在一起（表 7.2）。

**表 7.2 示例键路径模式**

| 有效 | 无效 |
|---|---|
| `<to_one>.<to_one>.<to_many>` | `<to_many>.<to_one>.<to_many>` |
| `<to_one>.<to_many>.<to_one>` | `<to_many>.<to_many>.<to_one>` |
| `<to_many>.<to_one>.<to_one>` | `<to_one>.<to_many>.<to_many>` |
| `<to_one>.<to_one>.<to_one>` | `<to_many>.<to_many>.<to_many>` |

请记住，如果你需要额外的功能，你总是可以先执行一个更通用的获取请求，然后对结果数组执行自定义排序和过滤。这会浪费内存，但有时候你不得不这么做。

> **注意：** iOS 5 还允许创建自定义增量存储，让我们能够将 Core Data 连接到任意数据存储。这需要创建 NSIncrementalStore 抽象类的子类，并重写一些方法来支持数据访问。这使我们能够将 Core Data 连接到我们选择的数据存储技术。这也是将 Core Data 连接到 Web 服务的首选方式。

![](img/fe9fea534a8e7868f811f7cd33da015f_403_0.png)

## 使用 SQLite 存储以减少内存使用

请记住，对于 SQLite 存储，谓词和排序描述符会被转换为 SQL 并在数据库中执行。虽然这可能会有点麻烦，但这也意味着我们可以基于关系进行过滤和排序，而这些关系仍然以故障（fault）的形式返回。我们永远不必将相应的托管对象实例化到内存中。

如果我们想在 Objective-C 中执行相同的排序或过滤，我们就需要同时实例化所有这些关系——然后执行排序描述符和谓词。这只是基于 SQLite 的存储帮助提高性能并减少应用程序内存占用的一种方式。

## 数据保护

对于 iOS 5 应用程序，持久化存储现在会对磁盘上的数据进行加密。持久化存储支持一系列加密选项：

- NSFileProtectionNone 关闭加密。
- NSFileProtectionComplete 提供最严格的安全性。只有在设备通过认证并且处于解锁状态时，才能访问文件。不幸的是，这可能会阻止你的应用在后台运行时访问数据。
- NSFileProtectionCompleteUnlessOpen 阻止访问文件，除非设备已认证并解锁。你的应用在设备锁定后仍然可以继续访问已打开的文件；但是，你不能打开新文件。
- NSFileProtectionCompleteUntilFirstUserAuthentication 在设备启动期间以及用户使用密码认证之前，阻止访问文件。但是，一旦用户完成认证，即使设备之后被锁定，这些文件仍然可以访问。

Core Data 默认会使用 NSFileProtectionCompleteUntilFirstUserAuthentication。我们可以通过在为持久化存储配置 NSPersistentStoreFileProtectionKey 时赋值来更改保护级别。

## iCloud 支持

Core Data 提供了与 iCloud 的轻松集成。iCloud 支持侧重于管理第 6 章中处理的许多细节。如果你使用的是单一集中式 Core Data 存储，那么设置很简单：在设置持久化存储时设置几个偏好选项，然后监听更新。其他一切都会自动处理。无需使用 NSMetadataQuery 来搜索文件。我们不再需要担心合并冲突。我们甚至不需要告诉应用程序如何保存和加载数据。所有这些都会自动为我们处理。

当将 Core Data 与 SQLite 存储一起使用时，每个应用程序都管理自己的本地数据库，并且该数据库实际上永远不会上传到 iCloud 存储中。相反，每个数据库会保存事务日志文件并将日志文件上传到 iCloud。应用程序的其他副本随后可以识别并下载这些日志文件，使用它们来更新本地数据库。这也意味着文件只会上传增量（delta）——即基于每个条目的文件差异。这大大减少了 Core Data 在应用程序与 iCloud 之间传输的数据量。

iCloud 还使用三方合并来自动解决基于每个条目的冲突。在这里，系统会将两个冲突的副本与原始版本进行比较。这使得合并更加准确和自主。

例如，看看我们在第 6 章中实现的双向合并。想象一种情况：一个 WeightEntry 实例存在于版本 A 中，但在版本 B 中缺失。我们的双向合并无法判断该条目是被添加到 A，还是从 B 中删除。因此，我们宁可谨慎行事，始终选择保留不匹配的条目。

另一方面，三方合并则能够明确地识别该条目是被添加还是被删除，并在合并时采取相应的操作。如果它被添加到 A，则应包含在合并后的版本中。如果它从 B 中被删除，则应将其移除。

要设置集中式 Core Data 存储，我们只需在创建持久化存储时，将 NSPersistentStoreUbiquitousContentNameKey 和 NSPersistentStoreUbiquitousContentURLKey 键设置到传递给 addPersistentStoreWithType:configuration:URL:options:error: 的选项字典中。然后，我们注册 NSPersistentStoreDidImportUbiquitousContentChangesNotification 通知（这可能是 Objective-C 历史上最长的常量名），

我们可以对 UIManagedDocument 进行子类化以修改其默认行为。例如，我们可以更改文档包中持久化存储的名称。我们可以更改持久化存储的类型，或者修改文档模型或存储的创建方式。我们甚至可以启用对 Core Data 之外的数据进行保存和加载的支持。有关更多信息，请查看 UIManagedDocument 类参考。

### iCloud 限制

现在来说说坏消息。目前，在 iCloud 上使用 Core Data 会受到以下限制：

- 不支持有序关系。
- 我们不能使用映射模型来迁移我们的模式。轻量级迁移仍然可以。
- 在创建新存储时，我们不应该用预先存在的数据库文件来填充它。如果我们需要设置一些初始数据，我们应该在代码中以编程方式创建数据，或者使用 `NSPersistentStoreCoordinator's migratePersistentStore:toURL:options:withType:error:` 从现有文件加载数据。

有关更多信息，请务必查看最新的发行说明。

## Core Data 性能

Core Data 是一个成熟、高效的对象图管理框架。它的类已经过高度优化。例如，NSManagedObject 实例使用反射来检查其内部数据。然后，托管对象会利用这些信息来优化对这些数据的访问。因此，从 NSManagedObject 访问值通常比访问通用 Objective-C 对象上的类似访问器更快。

基于 SQLite 的持久化存储帮助我们最大限度地减少活动内存中持有的对象数量，让我们只获取并持有需要的对象。这对于 iOS 应用尤其重要，因为内存管理仍然是我们关注的关键问题之一。

尽管如此，仍有一些关键点需要记住，以避免性能不佳。
