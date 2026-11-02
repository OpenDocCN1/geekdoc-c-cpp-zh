
借助三个主要媒体库（以及文档库），你还可以通过编程方式将其他文件夹包含到这些库中。请注意，这与直接在该库中创建子文件夹不同——Windows 眼中的媒体文件夹是文件系统上任意数量其他文件夹的列表，这些文件夹随后被视为一个单一实体。你可以在 Windows 资源管理器的“库”下看到这一点（忽略旧版播客残留项）：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_591_0.png)

在 Windows 资源管理器中，如果右键单击某个文件夹并选择“包含到库中”，你将看到一个包含相同选项的弹出菜单：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_591_1.png)

`Windows.Storage.StorageLibrary` 对象让你可以从应用内访问这些功能。要获取 `StorageLibrary`，请使用 `Windows.Storage.KnownLibraryId` 枚举中的值调用静态方法 `Windows.Storage.StorageLibrary.getLibraryAsync`，如下面“库管理”示例的场景 1（js/S1_AddFolder.js）所示：

```js
Windows.Storage.StorageLibrary.getLibraryAsync(Windows.Storage.KnownLibraryId.pictures)
    .then(function (library) {
        // ...
    });
```

其中 `KnownLibraryId` 中的可用选项为 `pictures`、`music`、`videos` 和 `documents`。一旦获得 `StorageLibrary` 对象，你就可以使用以下成员：

- `folders` 库中文件夹的 `StorageFolder` 对象的只读但可观察向量。
- `saveFolder` 库默认保存位置的 `StorageFolder`（只读）。
- `requestAddFolderAsync` 调用文件夹选择器 UI，该 UI 自动仅显示有资格添加到库中的位置（例如排除其他应用和可移动存储，但包括 SkyDrive，因为它有一个至少包含占位文件的本地文件夹）。用户选择文件夹或取消后，API 将分别以选定的 `StorageFolder` 或 `null` 完成。
- `requestRemoveFolderAsync` 提示用户确认从库中移除给定的 `StorageFolder`，并以一个布尔值完成，指示用户是否同意该操作。
- `definitionChanged` 当文件夹集合的内容通过 Windows 资源管理器或其他应用发生更改时触发。应用使用它来根据需要更新自己的 UI。

“库管理”示例展示了除 `saveFolder` 之外的所有这些功能。为完成场景 1，它调用 `requestAddFolderAsync`（js/S1_AddFolder.js）：

```js
Windows.Storage.StorageLibrary.getLibraryAsync(Windows.Storage.KnownLibraryId.pictures)
    .then(function (library) {
        return library.requestAddFolderAsync();
    }).done(function (folderAdded) {
        // ...
    });
```

场景 3 使用 `requestRemoveFolderAsync` 执行相反操作（js/S3_RemoveFolder.js）：

```js
var folderToRemove =
    picturesLibrary.folders[document.getElementById("foldersSelect").selectedIndex];
picturesLibrary.requestRemoveFolderAsync(folderToRemove).done(function (folderRemoved) {
    // ...
});
```

其中 `foldersSelect` 控件由 folders 集合填充（js/S3_RemoveFolder.js）：

```js
function fillSelect() {
    var select = document.getElementById("foldersSelect");
    select.options.length = 0;
    picturesLibrary.folders.forEach(function (folder) {
        var option = document.createElement("option");
        option.textContent = folder.displayName;
        select.appendChild(option);
    });
}
```

场景 2（js/S2_ListFolders.js）中几乎相同的代码只是将当前文件夹列表输出到显示区域。

如果你在此示例中添加和移除文件夹，同时运行内置的“图片”应用，你会看到这些文件夹的内容出现和消失。这是因为“图片”应用使用 `definitionChanged` 事件来保持自身更新。“库管理”示例也这样做，只是为了在*场景 3*中刷新其下拉列表，并在*场景 2*（`js/S2_ListFolders.js`）中刷新其显示：

```js
Windows.Storage.StorageLibrary.getLibraryAsync(Windows.Storage.KnownLibraryId.pictures)
    .then(function (picturesLibrary) {
        picturesLibrary.addEventListener("definitionchanged", updateListAndHeader);
        updateListAndHeader(); // Refresh the display
    });
```

你可以在示例运行时，在 Windows 资源管理器中向“图片”库添加和移除文件夹来测试这一点。

**提示** 请记住，`definitionChanged` 是 WinRT 事件，因此务必适当地移除其侦听器。我要指出，“库管理”示例并没有正确执行此操作。

## 可移动存储

与媒体库一样，对用户可移动存储设备的编程访问由功能声明加上一个或多个文件类型关联控制。这意味着你不能直接枚举这些文件夹的内容，也不能在那里随意写入文件。换句话说，直接访问 `Windows.Storage.KnownFolders.removableDevices` 只适用于你在查找特定文件类型的时候。例如，照片管理应用可以在这里查找相机或 USB 驱动器，以便从中导入其支持的图像文件。

如果你只是想允许用户在可移动设备上打开或保存文件，那么功能和 `removableDevices` 文件夹并不是你需要的：请改用文件选择器。你不想做的是创建你并不真正支持的文件类型关联，因为用户会尝试通过这些关联启动你的应用，并把他们的失望反映在你的商店评分中！

话虽如此，我们假设该功能适合你要做的事情。如果你在 Visual Studio 中加载[可移动存储示例](#)并运行它，你可以看到它将自己与 gif、jpg 和 .png 文件关联的效果。因此，它会出现在“打开方式”列表中，例如 Windows 资源管理器的上下文菜单和默认程序选择器中。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_593_0.png)

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_593_1.png)

如何创建适当的声明并处理文件激活，是我们稍后将在“文件激活与关联”一节中回头讨论的主题。现在，假设你已经正确完成了所有这些，你的应用将能够访问 `removableDevices` 文件夹。该示例（场景 1）只是使用 `StorageFolder.getFoldersAsync` 方法列出连接的设备。场景 2 和 3 随后向选定设备发送图像并从中检索图像，其中设备名称本身来自 `Windows.Devices` 命名空间中的 API，正如我们将在第 17 章“设备和打印”中看到的那样。不过，你不必做到那种程度，因为 `removableDevices` 文件夹已经为你提供了相同用途所需的 `StorageFolder` 对象。

然后场景 4 演示处理自动播放激活，我们也将在“文件激活与关联”中回头讨论。在这种情况下，你可能会查询相关可移动设备的内容，以创建你关心的文件列表，为此我们需要查看文件查询。

## 简单枚举与常见查询

对文件夹内容的简单或浅层枚举通过 `StorageFolder` 对象中 `getFilesAsync`、`getFoldersAsync` 和 `getItemsAsync` 的变体进行，这些变体不接受参数。每个方法都会生成相应项类型的向量：`getFilesAsync` 仅枚举文件，并提供 `StorageFile` 对象的向量；`getFoldersAsync` 仅枚举直接子文件夹，返回 `StorageFolder` 对象的向量；`getItemsAsync` 提供两者合并的向量，每一项都由 `StorageItem` 对象表示。请注意，`getItemsAsync` 有一个变体 `getItemsAsync(<startIndex>, <maxItemsToRetrieve>)`，可以用它进行部分枚举。当处理包含数百个或更多项的文件夹时，这尤其有用，这样你可以仅在项进入视图时才将其带入内存。

收到其中一个向量后，你可以像遍历数组一样遍历它，因为向量会以这种方式投影到 JavaScript 中。借助 `StorageFile`、`StorageFolder` 和 `StorageItem` 对象，你可以提取它们的显示名称和缩略图，以创建画廊视图、向用户呈现更紧凑的列表，或者做任何其他你想做的事情。请注意，各种权限和清单功能不会影响枚举：如果你能够获取根 `StorageFolder`，你就拥有枚举其内容的编程权限。（但是，对于文档库和可移动存储，枚举会自动限制为你在清单中声明的文件类型。）

`Folder_enumerationsample` 向我们展示了这些简单用例。场景 1 在“图片”库上调用 `getItemsAsync`：

```javascript
picturesLibrary.getItemsAsync().done(function (items) {
    // Output all contents under the library group
    outputItems(group, items);
});
```

其中 `outputItems` 函数只是遍历结果列表并创建一些 DOM 元素来显示它们的名称（`group` 变量只是带有计数的标题元素）：
