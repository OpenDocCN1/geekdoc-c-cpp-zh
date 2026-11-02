
## 应用数据位置

现在我们已经了解构成应用状态的信息类型，让我们更深入地探讨“状态存储在哪里？”这个问题。回顾一下，当 Windows 为用户安装应用时（并且所有 Windows Store 应用只能由安装它的用户访问），它会在当前用户的 AppData 文件夹中自动为该应用创建一个文件夹（卸载应用时会被删除的文件夹）。然后在该应用文件夹内创建 LocalState、TempState 和 RoamingState 文件夹。在文件系统中，如果你在 Windows 资源管理器中打开 %localappdata%\packages，你会看到系统中不同应用的一堆文件夹。如果你进入其中任何一个，你会看到这些文件夹以及一个名为“Settings”的文件夹，如内置 Sports 应用的图 10-2 所示。该图还显示了这些文件夹的不同内容。

图 10-2 中的 LocalState 文件夹里可以看到一个名为 _sessionState.json 的文件。这就是 WinJS 保存和加载 WinJS.Application.sessionState 对象内容的文件，正如我们在第 3 章中所看到的。由于它只是一个 JSON 格式的文本文件，你可以轻松地用记事本或其他 JSON 查看器打开它来检查其内容。事实上，如果你查看 Sports 应用的此文件，如图所示，你会看到类似 {"lastSuspendTime":1340057531501} 的值。Sports 应用（以及 News、Weather 等）显示时间敏感的内容，因此它们在被挂起时保存，并在恢复时检查经过的时间。如果该时间超过了它们的刷新间隔，它们就可以去从相关服务获取新数据。对于 Sports 应用而言，其设置之一专门允许用户设置刷新周期。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_514_0.png)

**图 10-2** Sports 应用的 AppData 文件夹及其内容。

**注意** 如果你仔细查看图 10-2，你会看到所有与应用数据相关的文件夹，包括 RoamingState，都位于用户的整体 AppData/Local 文件夹中。还有一个同级的 AppData/Roaming 文件夹，但这仅适用于内网上的漫游用户账户设置，例如域加入的用户登录企业网络上的另一台机器时。这个 AppData/Roaming 文件夹与 Windows Store 应用的 AppData/Local/.../RoamingState 文件夹没有任何关系。

在编程上，你可以通过几种方式引用这些位置。首先，你可以使用我们在第 3 章中看到的 `ms-appdata:///` URI 方案，其中 `ms-appdata:///local`、`ms-appdata:///roaming` 和 `ms-appdata:///temp` 引用各个文件夹及其内容。（注意三条斜杠：它是一种简写，允许你省略包名。）你也可以使用 `Windows.Storage.ApplicationData.current` 方法返回的对象，其中包含操作状态所需的所有 API，我们稍后会看到。

顺便说一下，你的应用包中可能有一些直接以文件形式存在的只读状态。你可以用以 / 开头的 URI 引用它们（意思为 `ms-appx:///`）。你也可以通过 `Windows.ApplicationModel.Package.current.installedLocation` 属性中的 `StorageFolder` 对象访问它们。我们稍后会再讨论 `StorageFolder` 类。

### 应用数据 API（WinRT 和 WinJS）

我们已经回答了“我们需要关注哪些类型的状态？”和“状态存储在哪里？”这两个问题。现在我们可以回答第三个问题，“什么影响和修改了该状态？”——这将占据接下来的 25 页！

答案的很大一部分始于从 `Windows.Storage.ApplicationData.current` 属性获取的 `ApplicationData` 对象，该对象已完全为你的特定应用配置。该对象包含以下内容，其中其他对象类型也位于 `Windows.Storage` 命名空间中：

- `localFolder`、`temporaryFolder` 和 `roamingFolder` 每个这些属性都是一个 `StorageFolder` 对象，允许你在这些位置创建任意文件和额外的文件夹结构（但请注意下面的 `roamingStorageQuota`）。
- `localSettings` 和 `roamingSettings` 这些属性是 `ApplicationDataContainer` 对象，提供管理键值设置对层级或此类对的复合组的机制。所有这些都存储在 `AppData\Settings` 文件夹中的 `settings.dat` 文件里。
- `roamingStorageQuota` 此属性包含 Windows 将自动漫游的应用数据量（以千字节为单位，通常为 100）；如果存储在 `roamingFolder` 和 `roamingSettings` 中的总数据超过此数量，漫游将被暂停，直到数量降至配额以下。如果你认为可能超出配额，你必须自行跟踪存储的数据量。
- `dataChanged` 一个事件，表示 `roamingFolder` 或 `roamingSettings` 的内容已从云端同步，在这种情况下应用应重新读取其漫游状态。它还表示应用的另一部分（正在运行的代码或后台任务）已调用了 `signalDataChanged` 方法。（注意：`dataChanged` 是一个 WinRT 事件，你需要使用第 3 章“WinRT Events and removeEventListener”部分中描述的 `removeEventListener`。）
- `signalDataChanged` 一个触发 `dataChanged` 事件的方法。这允许你将本地和漫游更新合并到 `dataChanged` 事件的单个处理程序中，包括在后台任务中发生的更改（也就是说，如果应用当前未被挂起，从后台任务调用此方法将触发应用中的事件。）
- `version` 属性和 `setVersionAsync` 方法 这些用于管理应用状态上的版本戳。此版本适用于你的整个应用状态（本地、临时和漫游一起）；没有为每个单独设置版本。请再次注意，状态版本与应用版本是分开的，因为应用的多个版本都可以使用其状态的同一版本（也就是说，相同的状态结构）。
- `clearAsync` 一个清除所有 AppData 文件夹和设置容器内容的方法。当你想重新初始化默认状态时使用它，如果你因状态损坏而重新启动应用，这尤其有帮助。
- `clearAsync(<locality>)` `clearAsync` 的一个变体，限制为一个位置（local、temp 和 roaming）。位置由 `ApplicationDataLocality` 枚举中的值标识，例如 `ApplicationDataLocality.local`。对于本地和漫游，文件夹和设置容器两者的内容都会被清除；temp 仅影响 `TempState` 文件夹。

现在让我们看看如何使用这里的 API 来管理不同种类的应用数据，其中包括一些用于相同目的的 WinJS 助手。

> **提示** 如果你已按第 3 章“Debug Output, Error Reports, and the Event Viewer”部分所述启用了通道，应用状态 API 会在事件查看器中生成事件。总结一下，确保已勾选 View > Show Analytics and Debug Logs 菜单项。然后导航到 Application and Services Log，展开 Microsoft/Windows/AppModel-State，你会找到 Debug 和 Diagnostic 组。右键单击其中一个或两个并选择 Enable Log 以记录这些事件。

### 设置容器

首先，让我们看看 `localSettings` 和 `roamingSettings` 属性，它们通常被称为设置容器。你通过相对简单的 `ApplicationDataContainer` API 与它们交互。

每个容器都有四个只读属性：一个 `name`（字符串）、一个 `locality`（再次来自 `ApplicationDataLocality`，这里只有 `local` 和 `roaming` 两个值），以及名为 `values` 和 `containers` 的集合。

顶级设置容器具有空名称；使用 `createContainer` 方法创建（并使用 `deleteContainer` 删除）的子容器将设置该属性。这些子容器也可以有其他容器，从而允许你创建整个设置层级。尽管如此，这些设置容器旨在用于少量数据，如用户配置；任何单个设置限制为 8K，任何复合设置（见下文）限制为 64K。在这些限制下，超过约一兆字节的设置意味着一个相当复杂的层级，这将难以管理并且肯定会减慢访问速度。因此不要被诱惑去认为应用
