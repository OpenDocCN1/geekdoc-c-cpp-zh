
该控件本身非常易于使用。在标记中，使用 WinJS.UI.SemanticZoom 构造函数声明一个 WinJS 控件。然后，在该元素中声明两个（且只能是两个）子元素：第一个定义缩小前的视图，第二个定义缩小后的视图——始终按照此顺序排列。下面是示例使用两个 ListView 控件的方式（另外还包括缩小后视图所使用的模板；这里展示的是本章配套内容中修改后的示例代码）：

```
<div id="semanticZoomTemplate" data-win-control="WinJS.Binding.Template" >
    <div class="semanticZoomItem">
        <h2 class="semanticZoomItem-Text" data-win-bind="innerText: groupTitle"></h2>
    </div>
</div>

<div id="semanticZoomDiv" data-win-control="WinJS.UI.SemanticZoom">
    <div id="zoomedInListView" class="win-selectionstylefilled"
        data-win-control="WinJS.UI.ListView"
        data-win-options="{ itemDataSource: myGroupedList.dataSource,
            itemTemplate: mediumListIconTextTemplate,
            groupDataSource: myGroupedList.groups.dataSource,
            groupHeaderTemplate: headerTemplate,
            selectionMode: 'none', tapBehavior: 'none', swipeBehavior: 'none',
            layout: { type: WinJS.UI.GridLayout } }">
    </div>

    <div id="zoomedOutListView" data-win-control="WinJS.UI.ListView"
        data-win-options="{ itemDataSource: myGroupedList.groups.dataSource,
            itemTemplate: semanticZoomTemplate,
            selectionMode: 'none', tapBehavior: 'invoke', swipeBehavior: 'none' }" >
    </div>
</div>
```

第一个子元素 `zoomedInListView` 与场景 1 中带有组标题和项目的 ListView 完全相同；第二个子元素 `zoomedOutListView` 则使用组作为项目，并使用不同的模板来呈现这些组。语义缩放控件会根据相应的输入手势，在两个视图之间进行切换。当缩放状态发生变化时，语义缩放控件会触发 `zoomchanged` 事件；当处于缩小状态时，`args.detail` 的值为 `true`，当处于放大状态时，该值为 `false`。你可以使用此事件，使应用栏中的某些命令在不同视图中可用，例如，在缩小后的视图中提供更改排序或筛选方式的命令，而这些更改随后会影响缩小前视图的显示方式。我们将在第 9 章介绍应用栏。

该控件还具有其他几个属性，例如 `enableButton`（用于控制叠加按钮可见性的布尔值；默认值为 `true`）、`locked`（用于禁用任意方向缩放的布尔值，也可以动态设置该属性来锁定当前缩放状态；默认值为 `false`），以及 `zoomedOut`（用于指示控件是否处于缩小状态的布尔值，因此你可以通过它来初始化控件；默认值为 `false`）。此外，还有一个 `forceLayout` 方法，其使用场景与 ListView 的 `forceLayout` 相同：移除 `display: none` 样式时使用。

`zoomFactor` 属性很有意思，它决定了控件在两个视图之间进行动画切换的方式；在视频 7-1 的慢放片段中，你可以更清楚地看到这一点。

该动画结合了缩放和交叉淡化效果，使缩小后的视图根据切换方向，仿佛从控件所在平面下方下降或从上方升起；同时，缩小前的视图则仿佛下沉到该平面下方，或从该平面下方升起。具体来说，缩小前的视图会在 1 和 `zoomFactor` 之间缩放，同时透明度会在 1 和 0 之间变化；缩小后的视图会在 1/`zoomFactor` 和 1 之间缩放，同时透明度会在 0 和 1 之间变化。`zoomFactor` 的默认值为 0.65，会产生适中的效果。较低的值（最小值为 0.2）会增强该效果，而较高的值（最大值为 0.8）会减弱该效果。

在样式设置方面，大多数情况下，你只需直接设置 Semantic Zoom 子元素的样式即可。不过，如果要设置 Semantic Zoom 控件本身的样式，可以重写 `win-semanticzoom`（用于整个控件）和 `win-semanticzoomactive`（用于活动视图）中的样式。`win-semanticzoombutton` 样式还允许你根据需要设置缩放控件按钮的样式。

需要理解的是，语义缩放的设计目的是在同一数据的两个视图之间进行切换，*而不是*在完全不同的数据集之间进行切换（另请参阅“语义缩放控件指南和检查清单”）。此外，该控件不支持嵌套，也就是说，不能多次缩小到不同的层级。不过，这并不意味着两个视图必须使用相同类型的控件：缩小前的视图可以是列表，而缩小后的视图可以是图表、日历，或任何其他合理的可视化形式。换句话说，缩小后的视图非常适合显示摘要数据，而这些数据通常很难从缩小前的视图中推导出来。例如，使用我们在场景 1 中为组数据添加项目计数时所做的相同更改（请参阅上面的“快速入门 #4”），我们只需对缩小后项目的模板稍作扩展即可（本章配套内容中的修改后示例就是这样做的）：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_343_0.png)

你还需要了解，语义缩放控件不能与任意子元素配合使用。如果出现关于缺少 `zoomableView` 属性的异常，就说明了这一点！每个子控件都必须通过名为 `zoomableView` 的属性，提供 `WinJS.UI.IZoomableView` 接口的实现。在所有内置 HTML 和 WinJS 控件中，只有 ListView 和 Hub 实现了该接口（请参阅第 8 章“布局和视图”），这就是为什么你通常会在这些场景中看到语义缩放。不过，你当然可以在自定义控件中提供此接口：此时，构造函数返回的对象应包含一个 `zoomableView` 属性，该属性是一个包含该接口方法的对象。这些方法包括用途显而易见的 `beginZoom` 和 `endZoom`，以及 `getCurrentItem` 和 `setCurrentItem`；后两者使语义缩放控件能够在用户点击缩小后的视图中的某个组时，缩放到正确的组。

如需了解更多详细信息，请查看 [用于自定义控件的 HTML SemanticZoom 示例]，它也可以作为自定义控件的另一个示例。文档中还有一个名为 [SemanticZoom 模板] 的主题，其中提供了一些额外的缩小后视图模板设计。

## 模板如何与集合控件配合使用

在介绍集合控件时，我曾提到，对于 `template`（Repeater）、`itemTemplate`（FlipView 和 ListView）以及 `groupHeaderTemplate`（ListView）等属性，你可以使用函数来代替声明式模板。这是一项重要的功能，因为它允许你根据集合中每个项目的具体内容，分别动态呈现项目并自定义其视图；而声明式模板则会对每个项目进行相同的呈现。呈现函数还允许你以声明式形式无法实现的方式初始化项目元素，例如，使用延迟加载的图像，分阶段以异步方式构建元素。这种控制程度为性能优化提供了许多机会；在深入了解 ListView 后，我们将在本章末尾重新讨论这一主题。

目前，了解声明式模板究竟是如何工作的，以及它与自定义模板函数之间的关系，会很有帮助。理解其工作方式后，你可能会开始设想出许多用途！

**正在为模板设计而苦恼？** 文档中有两个页面，包含各种预定义模板（包括 HTML 和 CSS）。这些模板主要围绕 ListView 控件设计，但在任何需要模板的地方都能派上用场。这两个页面分别是 [网格布局的项目模板] 和 [列表布局的项目模板]。

### 引用模板

正如我之前所说，在 Repeater、FlipView 或 ListView 控件中引用声明式模板时，你实际引用的是一个*元素*。你可以使用元素 ID 作为快捷方式，因为应用宿主会为元素所标识的元素创建同名变量。不过，我们实际上并不推荐这种做法，尤其是在页面控件中（你可能会经常使用页面控件）。首先，一个 ID 只能对应一个元素，这意味着如果你恰好在同一个 DOM 中两次呈现页面控件，就会得到非常奇怪的行为。

第二个问题与时序有关。应用宿主提供的元素 ID 变量，只有在包含该元素的 HTML 片段添加到 DOM 后才会创建。对于页面控件，`WinJS.UI.processAll` 会在此之前调用，这意味着该页面中模板对应的元素 ID 变量届时还不可用。因此，任何使用 ID 指定模板的控件，要么会抛出异常，要么只显示空白。无论是哪种情况，都会令人极其困惑。

要避免声明式模板出现此问题，请将模板名称放在其 `class` 属性中（并确保该名称具有唯一性且描述性明确）：

