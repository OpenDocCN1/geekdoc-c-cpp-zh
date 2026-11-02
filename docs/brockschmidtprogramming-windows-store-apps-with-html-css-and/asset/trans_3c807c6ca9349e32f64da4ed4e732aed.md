
方法，当然，还有 `IItemPromise` 中找到的其它一些方法。这些 promise 随后返回的是带有 `IItem` 方法的项对象。需要跟踪的内容很多，所以让我们拆解一下。

`IListDataSource` 的成员，如下表所示，主要处理源中项的操纵。如果你使用过数据库，你会认识到该接口表达了典型的创建、更新和删除操作集合。接口背后的对象可以按其想要的方式实现这些操作。例如，`list.dataSource` 对象主要使用 `List` 方法，如 `move`、`splice`、`push`、`setAt` 等。但请再次注意，所有影响项内容（`change`、`getCount`、`item*`、`insert*`、`move*` 和 `remove`）的 `IListDataSource` 方法都是异步的，并为所讨论的结果返回项 promise（`IItemPromise`）。

| 成员（除非另行说明，否则为方法） | 描述 |
| --- | --- |
| `createListBinding` | 返回一个实现 `IListBinding` 方法的对象，这些方法允许按需枚举数据项并进行更改通知以满足数据绑定。 |
| `beginEdits`, `endEdits` | 在调用 `beginEdits` 和 `endEdits` 之间所做的更改将延迟通知（通过 `statusChanged` 事件），直到调用 `endEdits` 为止。 |
| `itemFromKey`, `itemFromIndex`, `itemFromDescription` | 使用键（字符串）、索引（数字）或描述（对象）进行项查找的方法。 |
| `change` | 使用新数据更新项。 |
| `insertAfter`, `insertAtEnd`, `insertAtStart`, `insertBefore` | 在源中相对于现有项或在源的开头或结尾插入新项。 |
| `moveAfter`, `moveBefore`, `moveToEnd`, `moveToStart` | 如果受支持，则将现有项移动到源中的其他位置（例如只读和不可排序的集合则不支持）。 |
| `remove` | 删除现有项。 |
| `statusChanged` (event) plus `addEventListener`, et al. | 当数据源以某种方式更改时触发，数据源不需要实现此功能（`list.dataSource` 未实现）。 |
| `getCount` | 返回数据源中项总数的 promise。这可以是估计大小，因为它被集合控件用于虚拟化。 |
| `invalidateAll` | 指示数据源清除并重置其可能维护的任何缓存。 |

你还会发现，所有引用现有项的操作，如 `change`、`move*`、`insertAfter` 等，都通过键而不是索引引用项。这是经过深思熟虑的设计决策，因为索引在不同的数据源中可能非常不稳定。另一方面，键，即源通常分配来唯一标识项的标识符，则非常稳定。

就其本身而言，`IListBinding` 的成员处理源中项的枚举。它的所有方法都是异步的，并返回带有 `IItemPromise` 方法的 promise：

| 成员（除非另行说明，否则为方法） | 描述 |
| --- | --- |
| `current` | 返回枚举中当前项的 promise。 |
| `jumpToItem` | 使给定项成为当前项并返回其 promise。 |
| `first`, `last`, `previous`, `next` | 返回枚举中相对于整体或当前项的项的 promise。 |
| `fromKey`, `fromIndex`, `fromDescription` | 根据键（字符串）、索引（数字）或描述（对象）返回项的 promise。这些方法都会使返回的项成为当前项。 |
| `releaseItem`, `release` | 如果向 `IListDataSource.createListBinding` 提供了通知处理程序，则停止对某项或所有项的更改请求。 |

要监听特定项上的更改通知，使用数据源的控件必须首先向 `createListBinding` 方法提供一个带有 `IListNotificationHandler` 的对象，如图 7-6 中所示。此步骤只是将处理程序提供给源，但实际上并未启动通知。那一步发生在控件请求项（通过其他任何方法）以获取项 promise 并调用 `ItemPromise.retain` 时。当控件完成监听时，它从 promise 中检索项（`ItemPromise.then` 或 `done`）并调用该项的 `release`。

这种按项的通知是为了支持虚拟化。如果你有一个可能包含数千项的数据源，但使用该源的控件一次只显示几十项，那么就没有理由保留源中的每个项：控件将改为对可见（或即将可见）的那些项调用 `retain`，并在它们完全移出视野后调用 `release`。这允许数据源高效地管理自己的内存。

这就是整个关系的要点。大多数情况下，你不必处理所有这些细节。对于自定义数据源，`VirtualizedDataSource` 提供了核心实现，我们稍后会看到。当你的数据源是 `List` 时，你只需通过 `List` 方法操纵该源。同时，你也可以直接通过 `ListItemDataSource/ListItemBinding` 方法进行更改。当数据源不是 `List` 时这是必要的，如果你正在创建支持任意源的自定义集合控件，则变得很重要。

一个例子可以在 *HTML ListView 使用数据源示例* 中找到。场景 2 和 3 使用 ListView 显示字母瓦片，如许多字游戏中常见的那样：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_364_0.png)

然后一系列按钮让你洗牌列表、添加瓦片、移除瓦片或交换瓦片。在场景 2 中，这些操作是通过 ListView 绑定的 `Binding.List` 完成的。例如，添加瓦片只需使用 `List.push`（js/scenario2.js）：

```js
function addTile() {
    var tile = generateTile();
    lettersList.push(tile);
}
```

场景 3 则做了所有相同的事情，仍然使用 `List`，但通过 `ListItemDataSource` 方法执行操作。例如，添加瓦片是通过 `insertAtEnd`（js/scenario3.js）：

```js
function addTile() {
    var ds = document.getElementById("listView3").winControl.itemDataSource;
    var tile = generateTile();
    ds.insertAtEnd(null, tile);
}
```

洗牌操作更为复杂，因为它必须首先调用 `createListBinding` 以获取可用于枚举集合的 `IListBinding` 方法。这会产生一个项 promise 数组，可以用 `WinJS.Promise.join` 完成。然后它调用源的 `beginEdits` 批量更改，使用 `moveToStart` 随机将项移动到列表顶部，然后调用 `endEdits` 收尾。代码有点长，你可以在 js/scenario3.js 中查看。

## 使用图片库的 FlipView

对于我们在 FlipView 示例中已经看到的一切，它真的很需要能够做一件完全明显的事情：在文件夹中翻阅图片。我们该如何实现呢？我们已经有一个包含 `img` 标签的项模板，所以也许我们只需要这些文件的 URI。我们可以使用 `Windows.Storage.KnownFolders.picturesLibrary` 文件夹和该库的 `StorageFolder.getFilesAsync` 方法（当然需要在清单中声明 `Pictures Library` 能力）来制作这些 URI 的数组。这将为我们提供一批 `StorageFile` 对象，我们可以为其调用 `URL.createObjectURL`。我们可以将这些 URI 存储在数组中并创建一个 `List`，其 `dataSource` 属性我们可以分配给 FlipView 的 `itemDataSource`：

```js
var myFlipView = document.getElementById("pictures_FlipView").winControl;
```

```js
Windows.Storage.KnownFolders.picturesLibrary.getFilesAsync()
    .done(function (files) {
        var pixURLs = [];

        files.forEach(function (item) {
            var url = URL.createObjectURL(item, { oneTimeOnly: true });

            pixURLs.push({ type: "item", title: item.name, picture: url });
        });

        var pixList = new WinJS.Binding.List(pixURLs);
        myFlipView.itemDataSource = pixList.dataSource;
    });
```

尽管这种方法有效，但对于大量高分辨率图片，它会消耗相当多的内存，因为每张图片都必须完全加载到内存中。我们可以通过加载缩略图而不是完整图像来减轻内存需求，但仍然存在一个显著的缺点：图像只是被拉伸或压缩以适应 FlipView，而不考虑纵横比，除非每张图像大小相同，否则会产生糟糕的结果。

更好的方法是使用 `WinJS.UI.StorageDataSource` 对象，其演示可在本章配套内容中修改的 HTML FlipView 示例的场景 8 中找到。另一个例子可以在 StorageDataSource 和 GetVirtualizedFilesVector 示例中找到，它也在 Pictures 文件夹上创建了一个 ListView。

`StorageDataSource` 当然提供了所有必要的接口，并直接将文件系统用作数据源，而不是内存中的数组。它还提供自动更改检测，因此如果你向文件夹添加文件或修改现有文件，它将触发必要的更改通知
