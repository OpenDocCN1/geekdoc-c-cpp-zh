
## 分组

当 ListView 除了项数据源之外还提供组数据源时，自定义布局的变化在于 layout 方法的 tree 参数将包含多个项。当然，tree 中的每个项都是一个单独的组，包含属于该组的任意项。也就是说，我们一直使用如下代码来查看这些项：

```
var container = tree[0].itemsContainer;
```

但现在我们需要改为处理整个 tree 数组。HTML ListView 自定义布局示例（同样是 SDK 示例）的场景 3 和场景 4 就是这样做的，如下所示，摘自 js/scenario3.js：

```javascript
layout: function (tree, changedRange, modifiedElements, modifiedGroups) {
    var offset = 0;

    var treeLength = tree.length;
    for (var i = 0; i < treeLength; i++) {
        this._layoutGroup(tree[i], offset);
        offset += tree[i].itemsContainer.items.length;
    }

    return WinJS.Promise.wrap();
},

// Private function that is responsible for laying out just one group
_layoutGroup: function (tree, offset) {
    var items = tree.itemsContainer.items;

    var itemsLength = items.length;
    for (var i = 0; i < itemsLength; i++) {
        // Get CSS class by item index
        var cssClass = this._itemInfo(i + offset);
        WinJS.Utilities.addClass(items[i], cssClass);
    }
}
```

所有这些仍然是为各种元素添加 CSS 样式的问题；组标题本身的布局由 html/scenario3.html 中的 headerTemplate 元素以及 css/scenario3.css 中的适用样式定义。如下所示，每个组只是一个较大的字符（各组垂直排列；这里我横向展示每个组的部分内容）：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_726_0.png)

简而言之，对分组的支持并不与特定 ILayout2 方法的实现绑定——它主要取决于你如何实现 layout 方法本身。

当然，你可以通过包含 itemsFromRange 来同时实现分组和虚拟化，正如我们在上一节看到的那样。示例的场景 4 基本上通过组合场景 2 和场景 3 的代码演示了这一点。

## 其他内容

现在让我们看看 ILayout2 的其余方法，其中大部分在 Custom Layout Extras 示例的场景 4 中演示，该示例是场景 2 中最小水平布局的扩展。

其中一些方法必须返回一个对象，该对象包含项索引和类型（来自 WinJS.UI.ObjectType 的值）。这个对象没有指定的类型，但看起来像这样：

```
return { type: WinJS.UI.ObjectType.item, index: itemIndex };
return { type: WinJS.UI.ObjectType.groupHeader, index: headerIndex };
```

hitTest 方法还应包含一个 insertAfterIndex，它表示被移动项的实际插入点。

### 键盘支持：getAdjacent

ListView 会响应方向键以及 Page Up 和 Page Down 调用 getAdjacent，因为布局对象才知道各项之间如何相对排列。如果没有此方法，默认行为（如你在场景 2 中所见）是：右箭头、下箭头和 Page Down 将焦点移到列表中的下一项，左箭头、上箭头和 Page Up 移到上一项。（Home 和 End 始终按预期转到第一项和最后一项。）

然而，在这个网格布局中，我们希望上、下、Page Up 和 Page Down 按行工作（一次一行或三行）。于是我们实现 getAdjacent，它接受一个项对象（包含如返回对象中的 index 和 type 属性）和一个 WinJS.Utilities.Key，并返回一个描述下一个要获得焦点的项的对象。（如果你只是返回一个对象，对于前进键和后退键分别将 index 设置为 item.index + 1 或 item.index - 1，并设置 type: WinJS.UI.ObjectType.item，你将复制默认行为。）

在我们的例子中，需要确定一行有多少项。这相当直接。还记得我们通过 initialize 获得的 site 对象吗？它包含一个 viewportSize 属性，其宽度告诉我们 ListView 的宽度。如果将其除以项宽度——最好在布局对象上有一个属性，让应用可以将其指定为固定大小——我们就得到每行的项数。由于此值只会在重新计算布局时改变，我们可以在 layout 方法中这样做：

```
layout: function() {
    this._itemsPerRow = Math.floor(this._site.viewportSize.width / this._itemWidth);
    this._totalRows = Math.floor(this._site.itemCount._value / this._itemsPerRow);

    //We don't need to do anything else.
    return WinJS.Promise.as();
},
```

假设布局上有一个已针对实际项大小（内容大小 + 边框等）适当设置的 itemWidth 属性，我们可以如下实现 getAdjacent。这里，Page Up 和 Page Down 一次移动三行，上/下箭头移动一行：

```
getAdjacent: function (item, key) {
    var Key = WinJS.Utilities.Key;
    var index = item.index;
    var curRow = Math.floor(index / this._itemsPerRow);
    var curCol = index % this._itemsPerRow;
    var newRow;

    //The ListView is gracious enough to ignore our return index if it's out of bounds,
    //so we don't have to check for that here.

    switch (key) {
        case Key.rightArrow:
            index = index + 1;
            break;

        case Key.downArrow:
            index = index + this._itemsPerRow;
            break;

        case Key.pageDown:
            //If we page down past the last item, this will go to the last item
            newRow = Math.min(curRow + 3, this._totalRows);
            index = curCol + (newRow * this._itemsPerRow);
            break;

        case Key.leftArrow:
            index = index - 1;
            break;

        case Key.upArrow:
            index = index - this._itemsPerRow;
            break;

        case Key.pageUp:
            newRow = Math.max(curRow - 3, 0);
            index = curCol + (newRow * this._itemsPerRow);
            break;
    }

    return { type: WinJS.UI.ObjectType.item, index: index };
},
```

这样，我们就能在布局内获得良好的键盘导航。请注意注释：ListView 会忽略无效的索引值，因此我们不必费心验证返回的内容。

将列表内拖动的项移动到该索引。注意，应将 `insertAfterIndex` 设置为 -1，以便插入到列表开头。

有了 `hitTest` 之后，每当 `hitTest` 返回的索引发生变化时，就会调用 `dragOver` 方法。它接收拖动操作的 x/y 坐标（以及一个名为 *`dragInfo`* 的对象，该对象供 ListView 内部使用，因为其所有成员都以 `_` 开头，表示“不要碰”）。该方法没有返回值，因此其全部目的是让你的布局有机会以视觉方式指示放置结果。例如，你可以高亮插入点，在布局中显示一点抖动空间（内置布局会将命中测试的项移动 12px），或者任何其他你想要的效果。当然，随后使用 `dragLeave` 重置该指示器。（如果你想查看内置布局对 `dragOver` 做了什么，请查看 WinJS 的 `ui.js` 文件中的 `_layoutCommon_dragOver` 函数。）

在示例中（仍在场景 4 中），我只是将放置点处的项稍微旋转（见视频 8-3），并确保在 `dragLeave` 时清除该变换：

```js
dragOver: function (x, y, dragInfo) {
    //Get the index of the item we'd be dropping on
    var index = this._indexFromCoordinates(x, y);

    console.log("dragOver on index = " + index);

    //Get the element and scale it a little (like a button press)
    var element = this._site.tree[0].itemsContainer.items[index];
    element && this._addAnimateDropPoint(element);
    this._lastRotatedElement && this._clearAnimateDropPoint(this._lastRotatedElement);
    this._lastRotatedElement = element;
},

dragLeave: function () {
    console.log("dragLeave");
    if (this._lastRotatedElement) {
        this._clearAnimateDropPoint(this._lastRotatedElement);
        this._lastRotatedElement = null;
    }
},

_addAnimateDropPoint: function (element) {
    element.style.transition = "transform ease 167ms";
    element.style.transform = "rotate(-20deg)";
},

_clearAnimateDropPoint: function (element) {
    element.style.transition = "";
    element.style.transform = "";
}
```

这样，ListView 将自动处理数据源中项的移动，无需任何其他特殊处理。在示例中，我为列表中的每个项添加了标识号，以便你可以看到效果。

