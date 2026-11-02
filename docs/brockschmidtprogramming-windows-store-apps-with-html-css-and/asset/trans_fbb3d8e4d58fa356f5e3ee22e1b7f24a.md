
以便绑定控件能够自行更新。

StorageDataSource 会与一种称为查询的东西配合工作，但我们要到第 11 章“状态的故事，第 2 部分”⁶⁷才会学习它。幸运的是，WinJS 允许你简化媒体库的处理过程，只需传入像 "Pictures" 这样的字符串（js/scenario8.js）：

```js
myFlipView.itemDataSource = new WinJS.UI.StorageDataSource("Pictures");
```

这将在 Pictures 库的内容之上创建一个 StorageDataSource（当然，前提是你已声明相应功能）。

StorageDataSource 的注意事项是，它不直接支持单向绑定：如果你尝试在声明性模板中直接引用项属性，就会遇到异常。为绕过此问题，必须为每个属性显式使用 WinJS.Binding.oneTime 作为初始化函数（或在 Binding.processAll 中将其设为默认值）。该模板位于 html/scenario8.html：

```html
<div id="pictures_ItemTemplate" data-win-control="WinJS.Binding.Template">
<div class="overlayItemTemplate">
<img class="image" data-win-bind="src: thumbnail InitFunctions.thumbURL; alt: name WinJS.Binding.oneTime" />
<div class="overlay">
<h2 class="ItemTitle" data-win-bind="innerText: name WinJS.Binding.oneTime"></h2>
</div>
</div>
</div>
```

对于 img.src 属性，查询会向我们提供类型为 Windows.Storage._BulkAccess.FileInformation 的项（下面代码中的变量 s），其中包含缩略图图像，而不是 URI。要将该图像数据转换为 URI，我们需要使用自己的绑定初始化器：

```js
WinJS.Namespace.define("InitFunctions", {
  thumbURL: WinJS.Binding.initializer(function (s, sp, d, dp) {
    var thumb = WinJS.Utilities.getMember(sp.join("."), s);
    if (thumb) {
      var lastProp = dp.pop();
      var target = dp.length ? WinJS.Utilities.getMember(dp.join("."), d) : d;
      dp.push(lastProp);
      target[lastProp] = URL.createObjectURL(thumb, { oneTimeOnly: true });
    }
  })
});
```

请注意，缩略图并不总是立即存在于 FileInformation 对象中，这就是为什么在为其创建 URI 之前，我们必须验证确实已有缩略图。这意味着快速翻阅图像时可能会显示一些空白。要解决这个特定问题，我们可以监听 FileInformation.onthumbnailupdated 事件，并在此时更新项。完成此目的的最佳方式是使用 StorageDataSource.loadThumbnail 辅助方法，它会确保为此 WinRT 事件调用 removeEventListener。（参见第 3 章中的“WinRT 事件与 removeEventListener”。）你可以在绑定初始化器中使用此方法，如前面提到的 StorageDataSource 和 GetVirtualizedFilesVector 示例的场景 1 所示，也可以在取代声明性模板的渲染函数中使用此方法。修改后的 FlipView 示例的场景 9 就是这样做的。

### 自定义数据源与 WinJS.UI.VirtualizedDataSource

创建自定义数据源，归根结底意味着要提供我们先前在“数据源的结构（接口多多！）”中看到的所有接口的实现。显然，那将涉及大量编码工作，还会牵涉变更检测以及缓存和虚拟化等大量优化。为了让整个工作更轻松，WinJS 相应地提供了 WinJS.UI.VirtualizedDataSource 类，它承担了大部分繁重工作，并提供所有 IListDataSource 和 IListBinding 方法。你需要提供的部分是一个无状态适配器——一个实现 IListDataAdapter 接口的部分或全部方法的对象——用于将 VirtualizedDataSource 定制或适配到你的特定数据存储。

**提示** 文档中的“使用 ListView”主题包含许多此处未涵盖的、针对自定义数据源的性能提示。如其中所述，IListDataAdapter 接口和 VirtualizedDataSource 对象是创建异步数据源的最佳手段。

**演练** 要了解有关自定义数据源概念的更多信息，以及使用适配器的演练，请观看 Sam Spencer 在 //build 2011 上的演讲 Build data-driven collection and list apps using ListView，特别是 31:16 到 48:48 之间的部分。有趣的是，他在 WCF 数据服务（OData）之上构建了一个数据源，该数据服务与托管在 Windows Azure 上的 SQL Server 数据库通信。适配器也适用于其他云服务、与数据相关的 WinRT API 和本地数据库。

如果查看 IListDataAdapter，你会发现它有许多与 IListDataSource 相同的方法，因为它处理许多相同的功能。不过，务必不要混淆二者，因为它们存在差异，甚至同名方法也可能具有不同的参数。

| 成员（除非另有说明，否则为方法） | 说明 |
| --- | --- |
| `change` | 异步修改项。 |
| `getCount` | 返回一个 Promise，其兑现结果为数据源中项的估计计数。与 IListDataSource 一样，计数不必准确；它主要用于帮助控件管理其分页或虚拟化。 |
| `insertAfter`、`insertAtEnd`、`insertAtStart`、`insertBefore` | 将项添加到源中。所有方法都返回一个针对所添加项的 Promise。 |
| `itemsFromDescription`、`itemsFromEnd`、`itemsFromIndex`、`itemsFromKey`、`itemsFromStart` | 返回一个 Promise，其兑现结果为一个或多个项，具体取决于位置（开头、结尾）、索引（数字）、键（字符串）或描述（对象）。可以要求所有这些方法检索多个项（例如，主项前后若干项），以高效支持分页和虚拟化。Promise 交付的项组具体是一个具有 IFetchResult 接口的对象。 |
| `moveAfter`、`moveBefore`、`moveToEnd`、`moveToStart` | 在源中移动项，并返回一个针对该项的 Promise。 |
| `remove` | 从源中删除项，并返回一个针对该项的 Promise。 |
| `setNotificationHandler` | 注册通知处理程序。在这种情况下，该处理程序应实现 IListDataNotificationHandler 接口的方法。 |
| `compareByIdentity`（属性） | 指示是否使用对象的标识（而不是其值）来检测更改。 |
| `itemSignature` | 返回用于比较的项的字符串表示形式。 |

当你查看这些方法，并结合不同类型的数据源来思考它们时，应该会清楚其中一些方法并不合理。例如，只读源不需要 `insert*` 或 `move*` 方法。幸运的是，适配器接口和 `VirtualizedDataSource` 被设计得很灵活，允许你按下表所述只实现那些适配器方法。

| 源能力 | 适用方法 |
| --- | --- |
| 只读、基于索引 | `getCount`、`itemsFromIndex` |
| 只读、基于键 | `getCount`、`itemsFromKey`、`itemsFromStart`、`itemsFromEnd` |
| 读写、无排序 | 上述方法加上 `change`、`remove`、`insertAtEnd` |
| 读写、有排序 | 上述方法加上 `insertAtStart`、`insertBefore`、`insertAfter`、`insertAtEnd`、`moveAfter`、`moveBefore`、`moveToEnd` 和 `moveToStart` |
| 更改通知 | 添加 `setNotificationHandler` |

现在来看一些示例！首先，如果你一直在留意，可能会注意到除了场景 6 之外，我们已经讨论了 HTML FlipView 示例（修改后的那个）中的每个场景。这是因为这个特定场景实现了一个自定义数据源，以处理来自 Bing 搜索的图像。这里将需要我在本章开头提到的 Bing 搜索 API 密钥，所以如果你还没有获取密钥，现在就去做。

场景 6 如图 7-7 所示，使用的是修改后的示例；在该示例中，我将默认搜索字符串从 Seattle 和 New York 改为几项更贴近我内心的内容（我儿子最喜欢的火车和我居住的社区）。你可以在这个场景中做很多事情。控件让你可以选择不同的项渲染形式（我们将在本章后面讨论），并选择带有可配置延迟时间的虚拟化在线数据源——正如我们将在这里讨论的那样——或选择增量加载到 `Binding.List` 中的在线源。
