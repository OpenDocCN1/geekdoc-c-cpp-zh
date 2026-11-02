
事件参数还包含一个名为 `neighboringFilesQuery` 的属性，它是一个现成的 `StorageFileQueryResult`，使你能够检索同级文件，即使这些文件实际上并未被选中或激活。这有助于为包含已激活文件的文件夹创建图库视图，并且这是调用查询的 `findStartIndexAsync` 的好地方，尤其是在使用语义缩放控件且希望缩放到该索引时。在这种情况下，`findStartIndexAsync` 的参数是 `eventArgs.detail.files` 中的某个 `StorageFile` 对象，而不是关键字。

**注意** 使用 `neighboringFilesQuery` 时，应用仍需要以编程方式访问相关文件夹，例如通过库功能，否则会遇到访问被拒绝的异常。因此，该查询主要适用于这些库，而不适用于任意文件夹。

声明了可移动存储功能并至少声明一种文件类型的应用，也可以通过 `ActivationKind.device` 启动，这意味着当设备（如相机）连接到系统时，用户选择响应 AutoPlay 事件来启动该应用。例如，应用通常会随后执行从该设备导入图像等操作。[可移动存储示例](https://github.com/microsoft/Windows-universal-samples/tree/main/Samples/RemovableStorage)的场景 4 就是为此启动类型激活的。这里的 eventArgs 是 WebUIDeviceActivatedEventArgs，其关键属性是 eventArgs.detail.deviceInformationId，用于标识所连接的设备。此示例将该值传递到 js/s4_autoplay.js 中的页面控件（作为 arg），然后通过 `Windows.Devices.Portable.StorageDevice.FromId` 获取虚拟 `StorageFolder`，并运行文件查询来查找图像：

```javascript
var storage = (typeof arg === "string") ?
    Windows.Devices.Portable.StorageDevice.fromId(arg) : arg;
if (storage) {
    var storageName = storage.name;

    // Construct the query for image files
    var queryOptions = new Windows.Storage.Search.QueryOptions(
        Windows.Storage.CommonFileQuery.orderByName, [".jpg", ".png", ".gif"]);
    var imageFileQuery = storage.createFileQueryWithOptions(queryOptions);

    // Run the query for image files
    imageFileQuery.getFilesAsync().done(function (imageFiles) {
        // process results
    });
```
```

## 刚刚学到的内容

- 用户数据可以位于应用自身应用数据文件夹（以及包）之外的任何位置。用户数据位置涵盖本地文件系统、可移动存储设备、本地网络和云，而 `StorageFile` 和 `StorageFolder` 对象隐藏了有关这些位置如何被引用及其访问模型的细节。
- 对用户数据文件夹（如媒体库、文档和可移动存储）的访问由清单功能控制。仅当应用需要以文件选取器之外的方式访问文件系统时，才需要声明此类功能。
- 文件选取器是用户从文件系统中任何安全位置选择文件的方式，也是选择其他应用提供的文件的方式（这些文件可能位于远程、存储在数据库中，或者以其他方式不作为本地文件系统上的文件实体存在）。能够直接从其他应用选择文件——包括另一个应用可能按需生成的文件——是 Windows 应用商店应用最便捷、最强大的功能之一。
- 应用应始终使用 `Windows.Storage.AccessCache` 来保留对文件和文件夹的编程访问权限，以便后续会话使用。该缓存维护两个独立列表：一个用于最近使用的项（限制为 25 个），另一个用于通用目的（限制为 1000 项）。
- SkyDrive 已深度集成到 Windows 中，因此始终至少有一个本地占位文件；当该文件打开时，它会自动下载其内容（如果当前网络允许）。`StorageFile.isAvailable` 标志指示文件内容当前是否可访问。
- `StorageFile` 对象提供对丰富元数据的访问，包括缩略图和媒体特定属性。
- 在浏览场景中，应用应始终使用缩略图显示图像内容，以避免加载完整图像数据。只有在编辑和全图平移视图中才需要加载图像。
- `StorageLibrary` 对象提供管理用户媒体库中包含哪些文件夹的能力。
- `StorageFolder` 对象提供非常丰富且广泛的能力，可用于枚举其内容并查询符合特定条件的项。WinRT 为典型场景提供常见的文件和文件夹查询，但你也可以使用高级查询语法 (AQS) 字符串构建自定义查询。自定义查询还提供属性和缩略图的预提取功能。
- `WinJS.UI.StorageDataSource` 对象提供内置方式，并支持查询，以在 ListView 控件中创建图库体验。图库应始终对图像使用缩略图，并使用 `isAvailable` 标志在其 UI 中区分各项。
- 为支持文件激活，应用会在其清单中将自己与一种或多种文件类型关联，然后监视 `ActivationKind.File`；该激活类型的事件参数将包含已启动文件对应的 `StorageFile` 对象，以及一个可访问文件夹中其他文件的 `neighboringFilesQuery`。
- 支持可移动存储的应用还可以将自己与一种或多种文件类型关联，并通过 `ActivationKind.device` 为 Auto Play 事件启动。

## 第 12 章

### 输入与传感器

触摸显然是与终于成熟起来的计算机进行交互的最令人兴奋的方式之一。当然，我们拥有触敏设备已经很多年了：我记得大学时代用过一块支持触摸的屏幕，不得不承认，那已经是久到令人尴尬的过去了！在那种情况下，触摸传感器是一系列嵌入屏幕上方塑料片中的透明导线，整体触摸分辨率大约为宽 60、高 40……而且，真正暴露我年龄的是，那台显示器本身只是一个文本终端！

幸运的是，近年来触摸屏取得了巨大进步。它们响应足够灵敏，可用于通用目的（也就是说，你不必用力戳它们才能登记一个点），被集成到高分辨率显示器中，价格相对低廉，并且能够做的不只是复制鼠标——也就是说，支持多点触控和复杂手势。

因此，出色的触摸交互如今已成为优秀应用的一项基本特性，而为触摸进行设计意味着在许多方面重新思考 UI 相关问题。例如，在布局中，这意味着让点击目标的大小适合各种手指。在内容导航中，这意味着利用轻扫和捏合等直接手势，而不是仅依赖项选择和导航控件。同样，为触摸进行设计意味着思考手势如何丰富用户体验——以及如何提供通常依赖悬停等仅鼠标事件的可见性和用户反馈。

总而言之，请把触摸当作用户可能拥有的唯一交互方式来设计。同时，务必记住，新的输入方法很少会让现有方法过时。当然，打孔卡最终确实消失了，但鼠标的出现并没有让键盘过时。语音识别或手写的可用性既没有让鼠标过时，也没有让键盘过时。我认为触摸也是如此：它确实是一种补充性输入方法，有其自身的独特优点，但不太可能完全取代其他方法。正如 Microsoft Research 的 Bill Buxton 所说：“每一种模式，包括触摸，都有最适合它的地方，也有最不适合它的地方。”我预计，随着时间的推移，我们会看到自己同时使用键盘、鼠标和触摸，就像我们曾经学会在只有键盘的现实环境中整合鼠标一样。

Windows 旨在与所有形式的输入良好配合——与触摸良好配合、与鼠标良好配合、与键盘良好配合，并且，嗯，在多样化的硬件上也能良好运行！（Windows 应用商店认证也要求应用做到这一点。）因此，Windows 提供统一的基于指针的输入模型；在其中，如果你确实需要，可以区分不同的输入，否则可以将它们同等对待。你也可以更多地关注更高级别的手势，这些手势可以来自任何输入源，而完全不必担心原始指针事件。事实上，我们直到本书进行到一半的现在才提起这个话题，这本身就证明了使用各种指针输入而不必考虑它是多么自然：控件和
