
```javascript
dropTarget.addEventListener("drop", function (eventArgs) {
    var indexSelected = JSON.parse(eventArgs.dataTransfer.getData("Text"));
    var listview = document.querySelector("#listView").winControl;
    var ds = listview.itemDataSource;

    ds.itemFromIndex(indexSelected[0]).then(function (item) {
        WinJS.log && WinJS.log("You dropped the item at index " + item.index + ", "
            + item.data.title, "sample", "status");
    });
});
```

当然，你可以对拖放的数据做任何想做的事。如你所见，示例只是在 ListView 的数据源中查找该项。如果你想将该项移出源列表，可以使用该索引调用数据源的 `remove` 方法。

接下来看场景 3 和 4，它们使 ListView 成为拖放目标。场景 3 通过将 `itemsReorderable` 设置为 true，允许将数据放到控件中的特定位置。另一方面，场景 4 将 `itemsReorderable` 保留为 false，但随后为 `HTML5` 拖放事件实现处理程序。这是一个关键区别：只有当 ListView 可重新排序时，才使用 ListView 的 `itemdragdrop` 事件，这意味着你会获得特定插入点的索引；否则，你可以使用 `HTML5` 拖放事件，并在合理的位置插入数据。例如，如果数据源已排序，你只需将新项追加到集合中，让它的排序项目确定位置。

当然，在这两种情况下，数据源都必须支持插入；否则你会看到异常。

现在在场景 3 中，当 `itemsReorderable`: true 时，将某物拖放到 ListView 上会触发 `itemdragdrop` 事件。这里的 `eventArgs.detail` 对象将包含拖放位置的索引、插入点的 `insertAfterIndex`，以及 `HTML5` `dataTransfer` 对象（js/scenario3.js）：

```javascript
listView.addEventListener("itemdragdrop", function (eventArgs) {
    var dragData = eventArgs.detail.dataTransfer &&
        JSON.parse(eventArgs.detail.dataTransfer.getData("Text"));

    if (dragData && dragData.sourceId === myDragContent.id) {
        var newItemData = { title: dragData.data,
            text: ("Source id: " + dragData.sourceId), picture: dragData.imgSrc };
        // insertAfterIndex tells us where in the list to add the new item. If we're
        // inserting at the start, insertAfterIndex is -1. Adding 1 to insertAfterIndex
        // gives us the nominal index in the array to insert the new item.
        myData.splice(eventArgs.detail.insertAfterIndex + 1, 0, newItemData);
    }
});
```

场景 4 中，`itemsReorderable`: false，只是使用几乎相同的代码实现了一个拖放处理程序，只不过它始终将拖放的项插入列表开头（js/scenario4.js）：

```javascript
listView.addEventListener("drop", function (eventArgs) {
    var dragData = JSON.parse(eventArgs.dataTransfer.getData("Text"));

    if (dragData && dragData.sourceElement === myDragContent.id) {
var newItemData = { title: dragData.data,
    text: ("id: " + dragData.sourceElement), picture: dragData.imgSrc };
var dropIndex = 0;
myData.splice(dropIndex, 0, newItemData);
});
```

请注意，这两种情况下的 myData 对象都是 Binding.List；如果你在 ListView 后面使用不同的数据源，请改用 IListDataSource 方法来插入一项或多项。

示例中的最后一个场景展示了如何将数据拖放到 ListView 中的特定项上，而不是拖放到整个控件中；这仅仅意味着向项本身添加 HTML5 拖放事件处理程序。场景 5 在项模板中实现了这一点（html/scenario5.html）：

```html
<div id="smallListIconTextTemplate" data-win-control="WinJS.Binding.Template">
  <div class="smallListIconTextItem" ondragover="Scenario5.listItemDragOverHandler(event)"
       ondrop="Scenario5.listItemDropHandler(event)"
       ondragleave="Scenario5.listItemDragLeaveHandler(event)">
    <!-- Other content omitted -->
  </div>
</div>
```

换句话说，处理 ListView 中某项上的拖放——或者就此而言，任何其他集合控件或自定义控件——仅仅是在项上处理 HTML5 事件的问题，与集合控件本身无关。ListView 参与其中只是充当 HTML5 事件上的薄代理，以便它可以添加少量额外信息来支持重新排序和选择信息。

## 布局

ListView 的 layout 属性包含一个用于从视觉上组织列表项的对象。你作为选项提供给 ListView 构造函数的任何布局，都会决定控件的初始外观。在运行时更改布局会告诉 ListView 使用新结构重新渲染自身，这就是 ListView 如何轻松地在一维和二维布局之间、水平和垂直方向之间等进行切换。示例可以在 HTML ListView 基础示例的场景 3 中找到。

WinJS.UI 包含若干预置布局，每个布局本身都是一个对象类，遵循用于呈现集合的推荐设计准则：

- **GridLayout** 一种二维布局，可以基于 CSS 网格水平或垂直平移。如果你不指定布局，这是 ListView 的默认布局。
- **ListLayout** 一种一维布局，可以基于 CSS flexbox 水平或垂直平移。
- **CellSpanningLayout** GridLayout 的派生布局，支持不同大小的项——也就是说，项可以跨行和跨列。

你也可以创建自定义布局，附录 B 和 [HTML ListView 自定义布局示例](#) 中对此进行了介绍。

如何指定布局取决于你是在标记中还是在代码中执行。在标记中，`data-win-options` 字符串内的 `layout` 选项具有以下语法：

```
layout: { type: <layout> [, <options>] }
```

`<layout>` 是布局构造函数的名称，例如 `WinJS.UI.GridLayout`、`WinJS.UI.ListLayout`、`WinJS.UI.CellSpanningLayout` 或自定义类；然后 `<options>` 为该构造函数提供选项。例如，以下配置了一个左侧带组标题、最多四行的 GridLayout：

```
layout: { type: WinJS.UI.GridLayout, groupHeaderPosition: 'left', maximumRowsOrColumns: 4 }
```

如果你在 JavaScript 中通过使用 `new` 直接调用构造函数并将结果赋给 `layout` 属性来创建布局对象，则直接将此类选项提供给构造函数：

```
listView.layout = new WinJS.UI.GridLayout({ groupHeaderPosition: "left", maximumRowsOrColumns: 4 });
```

如果你愿意采用这种方法，也可以在 JavaScript 中创建 ListView 的 `layout` 对象后设置其属性。更改属性通常会导致布局更新。

无论如何，每个布局都有自己独特的选项，如下表所述；这些选项在运行时也可以作为布局对象上的属性访问。与 ListView 选项的枚举一样，你可以使用字符串值（例如 `'horizontal'`），或使用枚举中的完整标识符（例如 `WinJS.UI.Orientation.horizontal`）。

| GridLayout 选项/属性 | 描述 |
|---|---|
| `groupHeaderPosition` | 使用 `HeaderPosition` 枚举中的值控制标题相对于其组的位置：`top`（默认）或 `left`（在从右到左的语言中变为右侧）。 |
| `maximumRowsOrColumns` | 控制布局在开始另一列之前垂直放置的项数（当 `orientation` 设置为 `horizontal` 时），或在开始另一行之前水平放置的项数（当 `orientation` 设置为 `vertical` 时）。 |
| `orientation` | 使用 `Orientation` 枚举中的值控制布局的平移方向：`horizontal`（默认）或 `vertical`。 |

| ListLayout 选项/属性 | 描述 |
|---|---|
| `groupHeaderPosition` | 使用 `HeaderPosition` 枚举中的值控制标题相对于其组的位置：`top`（默认）或 `left`（在从右到左的语言中变为右侧）。 |
| `orientation` | 使用 `Orientation` 枚举中的值控制布局的平移方向：`horizontal` 或 `vertical`（默认）。 |

⁶⁹ 你在文档中看到的其他属性要么在 WinJS 1.0 中已弃用，要么供内部使用。你还会在这些对象上看到许多方法，这些方法是 ListView 与布局通信的方式；应用不会直接调用这些方法。
