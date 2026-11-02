
这两类命令的放置位置（在这里使用任何其他随机值都会默认归为 selection）。这会训练用户的眼睛，在一侧寻找最固定的命令，在另一侧寻找特定于选择的命令。请注意，每个区域中的命令都按照它们在标记中出现的顺序从左到右（或从右到左）排列。

- firstElementFocus、lastElementFocus 对于 content 类型的命令，分别在使用 Home 键和 End 键以及方向键时，获取或设置该命令的 DOM 树中应接收焦点的元素。
- onclick 可用于以声明方式指定单击处理程序；请记住，在标记中此处命名的任何函数都必须标记为可安全处理。（参见第 5 章“控件和控件样式”中的“严格处理和 processAll 函数”一节。）也可以通过 addEventListener 以编程方式分配单击处理程序，在这种情况下不需要该标记。
- disabled 如果为 true，则设置命令的禁用状态；默认值为 false。
- extraClass 指定附加到命令的一个或多个 CSS 类。这些类可用于单独设置命令控件的样式，也可用于创建可以轻松显示和隐藏的集合，如后文“显示、隐藏、启用和更新命令”一节所述。

如果要在运行时生成命令（不使用 content 类型），可以在应用栏不可见时（即其 hidden 属性为 true 时），通过将应用栏的 commands 属性设置为一个 JSON AppBarCommand 描述符数组来实现。示例中场景 1 应用栏的此类描述符数组如下所示（本章附带的修改后示例中提供了该数组；参见 js/create_appbar.js）：

```
//Set the app bar commands property to populate it
var commands = [
  { id: 'cmdAdd', label: 'Add', icon: 'add', section: 'global', tooltip: 'Add item' },
  { id: 'cmdRemove', label: 'Remove', icon: 'remove', section: 'global',
    tooltip: 'Remove item' },
  { type: 'separator', section: 'global' },
  { id: 'cmdDelete', label: 'Delete', icon: 'delete', section: 'global',
    tooltip: 'Delete item' },
  { id: 'cmdCamera', label: 'Camera', icon: 'camera', section: 'selection',
    tooltip: 'Take a picture' }
];
appBar.commands = commands;
```

创建应用栏时，它将遍历 commands 数组，并为每一项创建 AppBarCommand 控件。如果未指定 type，或者将其设置为 button、flyout 或 toggle，则该命令是一个 button 元素。separator 类型会创建一个 hr 元素。content 类型会创建一个空的 div。请注意，你应该本地化每个命令声明中的 label、tooltip 以及可能的 icon 字段，而不是像这里所示的那样使用显式文本。

你也可以直接在声明性标记中使用这样的数组，但这种形式无法本地化，因此不推荐使用（不过我在修改后的示例中加入了注释来说明如何实现）。同时，由于标记中 commands 的值只是一个字符串，你可以通过数据绑定，在应用栏元素中使用如下属性来分配其值：

```
data-win-bind="{ winControl.commands: Data.commands }"
```

其中 Data.commands 可以引用本地化的数据源。在这种情况下，Data 必须是一个全局变量（类似于命名空间），并且你必须在 WinJS.UI.processAll 的 completed 处理程序中，对应用栏元素（不指定特定上下文）调用 WinJS.Binding.processAll，以确保应用栏已首先创建。或者，你可以将 Data 作为第二个参数传递给 Binding.processAll，并在 data-win-bind 字符串中仅使用 commands 作为源。

另请注意，这种方法不适用于 data-win-res 属性（我们将在第 19 章看到，示例的场景 8 中也展示了这一点），因为资源字符串在资源查找过程中不会转换为 JSON。无论如何，尝试玩这种把戏会得不偿失，因此最好在运行时使用 HTML 声明形式或本地化的 commands 数组。

另外，请注意，commands 是只写属性的一个罕见示例：你可以设置它，但无法从应用栏中检索该数组。应用栏仅使用此数组来配置自身，一旦所有元素都在 DOM 中创建完毕，该数组就会被丢弃。不过，在运行时，你可以使用应用栏的 getCommandById 方法来检索特定的命令元素。

## 命令事件

说到命令元素，应用栏的 AppBarCommand 控件（分隔符除外）都只是 button 元素，因此会响应常规事件。由于每个命令元素都被分配了你指定的 id，你可以像往常一样使用 getElementById 作为 addEventListener 的前奏，但更直接的方法是应用栏的 getCommandById 方法。例如，在 HTML AppBar 控件示例的场景 1 中，以下代码出现在页面的 ready 方法中（js/create-appbar.js）：

```javascript
var appBar = document.getElementById("createAppBar").winControl;
appBar.getCommandById("cmdAdd").addEventListener("click", doClickAdd, false);
appBar.getCommandById("cmdRemove").addEventListener("click", doClickRemove, false);
appBar.getCommandById("cmdDelete").addEventListener("click", doClickDelete, false);
appBar.getCommandById("cmdCamera").addEventListener("click", doClickCamera, false);
```

当然，如果你在标记中为每个命令的 onclick 属性指定处理程序（并且每个处理程序的 supportedForProcessing 属性都为 true），就可以完全避免所有这些操作！

同样显而易见的是，你可以在应用中的任何位置这样连接事件，当然也可以监听你想要的任何其他事件，尤其是在使用其他 UI 进行自定义布局时。另外，要知道 click 事件可以方便地处理触摸、鼠标和键盘输入，因此你无需在那里做任何额外工作。顺便说一下，对于键盘，应用栏允许你使用 Tab 键和方向键在命令之间移动；Enter 或空格键将调用单击处理程序。

## 应用栏事件和方法

除了我们刚刚看到的应用栏 `getCommandById` 方法之外，应用栏还有其他几个方法和少量事件。首先是方法：

- `show` 在应用栏的 `disabled` 属性为 `false` 时显示应用栏；否则忽略该调用。
- `hide` 关闭应用栏。
- `showCommands`、`hideCommands` 和 `showOnlyCommands` 用于管理命令集，如下一节“显示、隐藏、启用和更新命令”所述。

至于事件，WinJS 中的覆盖式 UI 控件（即不参与布局的控件）共有四个常见事件：

- `beforeshow` 在浮出控件变为可见之前发生。对于应用栏，此时可以根据应用当前状态设置 `commands` 属性，或者启用/禁用特定命令。
- `aftershow` 在浮出控件变为可见后立即发生。对于应用栏，如果其 `sticky` 属性为 `true`，并且你有一个否则可能被部分覆盖的滚动元素，则可以使用此事件调整应用的布局——见下文。
- `beforehide` 在浮出控件隐藏之前发生。对于应用栏，你可以使用此事件隐藏随应用栏创建的任何补充 UI，并重新调整 `sticky` 应用栏周围的布局。
- `afterhide` 在浮出控件隐藏后立即发生。对于应用栏，如果必要，这同样可以是重新调整应用布局的时机。

你可以在 HTML AppBar 控件示例的场景 5 中找到结合使用 `show` 方法以及 `aftershow` 和 `beforehide` 事件的示例。

上面提到的应用布局问题（也是我在本章引言中保密的内容）之所以出现，是因为应用栏会覆盖并遮挡页面底部。如果该页面包含滚动元素，那么对于鼠标用户而言，将 `sticky` 设置为 `true` 的应用栏会部分覆盖垂直滚动条，并使水平滚动条完全无法访问。如果你要在这样的页面上使用粘性应用栏，那么——而且由于 Windows Store 策略不赞成歧视鼠标用户！——你应该使用 `aftershow`，将滚动元素的高度减少应用栏控件的 `offsetHeight` 或 `clientHeight` 值，从而保持滚动条可访问。当应用栏隐藏并触发 `afterhide` 时，你可以重新调整布局。在这些计算中也应始终使用像 `clientHeight` 这样的运行时值，因为它能适应不同的视图大小，并且应用栏的高度可能会随命令数量和视图大小而变化。
