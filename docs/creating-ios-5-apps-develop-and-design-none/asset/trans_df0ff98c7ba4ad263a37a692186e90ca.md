
## iCloud 键值存储

iCloud 键值存储为在云端保存数据提供了更简单的接口。不幸的是，它受到的约束也更多。键值存储旨在保存非关键配置数据。在许多方面，它与 NSUserDefaults 类似。它只能存储有限数量的数据——每个应用最多 64 KB——并且只能存储简单的属性列表数据类型：数字、日期、字符串、数组、字典等。最后，它没有任何冲突解决机制——总是以最后一次保存为准。

与 iCloud 文档存储类似，我们需要在应用的授权（entitlements）中设置键值存储标识符。一旦完成，我们只需访问共享的 NSUbiquitousKeyValueStore。然后调用该存储的实例方法来读写数据。所有更改最初都缓存在内存中。我们必须调用 synchronize 来将这些更改保存到磁盘。之后，系统会自动将本地容器中的数据与 iCloud 同步。

> **注意：** 同步 NSUbiquitousKeyValueStore 并不会强制系统立即将更改上传到 iCloud。实际上，系统可能会故意延迟上传，尤其是当我们的应用频繁更改时。更新越频繁，延迟越长。

![](img/fe9fea534a8e7868f811f7cd33da015f_300_0.png)

一般来说，我们不应该使用 iCloud 键值存储来保存用户生成的数据。它真正的用途是同步用户偏好设置。事实上，我们也不应该用它来替代 NSUserDefaults。相反，我们的应用仍应使用 NSUserDefaults 在本地管理偏好设置。我们只是使用键值存储来跨多台设备同步这些偏好设置。

在本章后面的“保存用户默认设置”一节中，我们将看到 NSUserDefaults 和 iCloud 键值存储如何协同工作。

## 准备应用程序

在 Health Beat 中，用户通常会打开应用并输入新的体重。我们希望让这个过程尽可能快速简便。因此，与其保存并恢复用户上次所在的位置，我们应始终打开体重输入视图。幸运的是，这意味着我们不需要保存界面状态；我们可以专注于模型。

不幸的是，在开始之前，我们必须准备好应用以支持 iCloud。

在开始使用 iCloud 存储之前，我们必须确保描述文件（provisioning profile）已启用 iCloud 支持。在大多数情况下，Xcode 会自动处理此事。自 iOS 5 发布以来，通用应用 ID（以及 Xcode 创建的默认描述文件）都会启用 iCloud。但是，如果你是在 iOS 5 发布之前设置开发工具的，则可能需要刷新描述文件。

下一步，我们需要为应用设置授权。如前所述，我们需要一个包含两个 iCloud 标识符的授权文件。第一个用于文档存储，第二个用于键值存储。授权为你的应用提供了一定程度的安全性，确保只有你自己的应用才能访问你的文档。此外，系统会使用授权来识别你应用的文档，并将它们与 iCloud 存储中的其他文档区分开。

授权文件包含许多键值对。对于文档存储，`com.apple.developer.ubiquity-container-identifiers` 键应包含一个字符串数组，表示我们团队创建的应用的包标识符。所有包标识符采用以下格式：`<DEVELOPER_ID>.<BUNDLE_IDENTIFIER>`。其中 `<DEVELOPER_ID>` 是与你的个人或团队帐户关联的唯一十字符标识符。你可以通过查看 Apple 开发者成员中心（<http://developer.apple.com/membercenter>）中的帐户信息找到它。`<BUNDLE_IDENTIFIER>` 是目标应用的标识符。

我们不必使用当前应用的包标识符。例如，精简版应用可以使用专业版应用的包标识符，从而保证用户升级后仍能继续访问文件。我们还可以使用多个标识符，以访问多个不同的容器。虽然第一个包标识符必须显式定义，但任何次要标识符都可以使用通配符。这让我们可以隐式地引用多个应用，而无需逐一列出它们。

**图 6.1** 设置授权

![](img/fe9fea534a8e7868f811f7cd33da015f_303_0.png)

对于键值存储，我们需要定义 `com.apple.developer.ubiquity-kvstore-identifier` 键。该键接受单个包标识符——我们不能使用多个容器。大多数情况下，它应与我们的主文档存储键匹配。

如你所见，查找和设置包标识符可能需要做一些工作。幸运的是，有一种非常简单的方法可以自动生成授权文件，并同时设置文档存储和键值存储。在项目导航器中，选择 Health Beat 应用图标。然后，在编辑器区域中，确保同时选中 Health Beat 目标和 Summary 选项卡。向下滚动，找到 Entitlements 设置，然后选中 Enable Entitlements 复选框。这将自动用当前目标的包标识符填充 iCloud Key-Value Store 和 iCloud Containers 设置（图 6.1）。

接下来，我们要设置文档类型和导出的统一类型标识符（UTI）。这让我们可以为应用定义唯一的 UTI。不幸的是，目前这对我们帮助不大。然而，当我们使用 iTunes Connect 提交应用时，它将使我们能够正确标记应用的 iCloud 数据。

![](img/fe9fea534a8e7868f811f7cd33da015f_304_0.png)

**图 6.2** 设置文档类型

在仍然选中应用图标和 Health Beat 目标的情况下，点击 Info 选项卡。现在，点击 Add 图标，并从弹出菜单中选择 Add Document Type。这将创建一个未命名的文档类型。展开该文档类型并进行以下更改。在“名称”字段中输入 **Health Beat History**。在“类型”字段中输入 `com.freelancemadscience.hhistory`。接下来，展开“其他文档类型属性”，添加一个 `CFBundleTypeExtensions` 键，并将其类型设置为 **Array**。然后，添加一个 `LSHandlerRank` 键，并将其值设置为 **Owner**。最后，展开 `CFBundleTypeExtensions` 并添加一个名为 `hhistory` 的字符串子项。

我们无需担心创建文档图标。iOS 会根据我们的应用图标自动创建图标（参见第 9 章）。如果你想了解有关创建文档特定图标的更多信息，请参阅 Apple 的《iOS 人机界面指南》中的“自定义图标和图像创建指南”一节。

该条目现在应与**图 6.2** 匹配。

由于我们已经定义了自定义文档类型，现在必须将其导出。再次点击 Add 按钮，并选择 **Add Exported UTI**。然后展开未命名的 UTI。在“描述”字段中输入 **Health Beat History**，在“标识符”字段中输入 `com.freelancemadscience.hhistory`。现在展开“其他导出的 UTI 属性”，添加一个 `UTTypeTagSpecification` 键，并将其类型设置为 **Dictionary**。展开该字典，添加一个 `public.filename-extension` 子键，并将其类型设置为 **Array**。最后，展开该数组并添加一个条目。将该条目的值设置为 `hhistory`。导出后的 UTI 现在应与**图 6.3** 匹配。

![](img/fe9fea534a8e7868f811f7cd33da015f_305_0.png)

在提交应用到 iTunes Store 之前，我们仍然需要创建一个 iCloud 显示集（display set）。这将定义当用户在“设置”应用中查看文档时，文档的呈现方式。遗憾的是，这超出了本书的范围，但更多信息请参阅 iTunes Connect 开发者指南中的“iCloud 显示集”一节。现在，让我们继续创建 UIDocument 子类。

## 创建 UIDocument 子类

就我们而言，保存模型实际上就是保存 WeightHistory 对象。显然，我们想要利用 iCloud 存储——而最简单的方法就是使用 UIDocument。幸运的是，我们可以毫不费力就让 WeightHistory 成为 UIDocument 的子类。

打开 WeightHistory.h，并按如下所示修改接口声明：

```
@interface WeightHistory : UIDocument
```

在这里，我们只需将 WeightHistory 的父类从 NSObject 改为 UIDocument。趁此机会，继续移除 defaultUnits 属性。毕竟，我们最终要将它迁移到 NSUserDefaults 中。就这样。当然，实现文件还需要做更多工作。

打开 WeightHistory.m，稍微清理一下。我们需要移除 defaultUnits 属性的所有痕迹。删除 `@synthesize defaultUnits` 这一行，并删除整个 `setDefaultUnits:` 方法。
