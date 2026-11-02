
大多数时候，你只会在选项字符串中使用字面量值，就像下面这个稍后还会再次看到的 WinJS.UI.Rating 控件示例：

```
<div id="rating1" data-win-control="WinJS.UI.Rating"
    data-win-options="{averageRating: 3.4, userRating: 4, onchange: changeRating}">
</div>
```

请注意 WinJS 控件事件如何使用 `on<event>` 形式的键名——这些键名就是控件对象上等效的 JavaScript 属性名。

不过，值还有其他可能性，其中许多都可以通过在 SDK JavaScript 示例中搜索“data-win-options”找到。总结如下：

- 值可以通过使用点表示法、方括号（[ ]）或两者兼用，来解引用对象、命名空间和数组。
- 值可以是数组字面量，也可以是用 { } 包围的对象，后者用于为复杂属性赋值。
- 值可以是 DOM 中另一个元素的 id，前提是该元素具有 `id` 属性。
- 值可以使用 `select('<selector>')` 语法以声明方式引用 DOM 中的元素。

让我们看一些示例。点表示法通常用于引用枚举或命名空间的成员。后者常见于 ListView 控件（见第 7 章），其中数据源在单独的命名空间中定义；也常见于应用栏（见第 9 章），其中事件处理程序在命名空间中定义：

```
data-win-options = "{ selectionMode: WinJS.UI.SelectionMode.multi,
    tapBehavior: WinJS.UI.TapBehavior.toggleSelect }"
```

```
data-win-options = "{ itemDataSource: DefaultData.bindingList.dataSource }"
```

```
data-win-options = "{ id: 'tenDay', label: 'Ten day', icon: 'calendarweek', type: 'toggle',
    onclick: FluidAppLayout.transitionPivot }"
```

html/app.html 中的 Adaptive layout with CSS 示例展示了同时使用点表示法和数组引用的情况。

```
data-win-options = "{ data: FluidAppLayout.Data.mountains[0].weatherData[0] }"
```

```
data-win-options = "{ data: FluidAppLayout.Data.mountains[0].weatherData }"
```

对象表示法通常与 ListView 一起使用来指定其布局对象，同时使用点表示法来标识该布局对象：

```
data-win-options = "{ layout: {type: WinJS.UI.GridLayout} }"
```

```
data-win-options = "{ selectionMode: 'none', tapBehavior: 'none', swipeBehavior: 'none',
    layout: { type: WinJS.UI.GridLayout, maxRows: 2 } }"
```

```
data-win-options = "{ itemDataSource: Data.list.dataSource,
    layout: {type: SDKSample.Scenario1.StatusLayout} }"
```

要以声明方式引用 DOM 中的另一个元素（当然，该元素必须在尝试引用它的控件之前完成实例化），你有两种选择。

第一种是使用该元素的 id——也就是该元素 `id` 属性中的同一名称。注意，你*不要*将该名称写成字符串字面量，而是直接将其指定为标识符。例如，如果我们在标记中较早的位置声明一个绑定模板（我们将在第 6 章看到）：

```
<div id="smallListItemTemplate" data-win-control="WinJS.Binding.Template"><!-- ... --></div>
```

然后我们可以在选项字符串中按如下方式引用该控件的根元素：

```
data-win-options = "{ itemTemplate: smallListItemTemplate }"
```

这之所以可行，是因为应用宿主会自动为具有 `id` 属性的元素在全局命名空间中创建变量，因此我们使用的值就是该变量。

另一种方式是使用 `select` 语法，这是一种将等同于 `document.querySelector` 的内容插入选项字符串的方法（严格来说是 `WinJS.UI.scopedSelect`，它会调用 `querySelector`）。因此，前面的选项字符串也可以写成这样：

```
data-win-options = "{ itemTemplate: select('smallListItemTemplate') }"
```

或者，如果我们用类而不是 `id` 声明模板：

```
<div class="templateSmall" data-win-control="WinJS.Binding.Template"><!-- ... --></div>
```

那么我们可以按如下方式引用它：

```
data-win-options = "{ itemTemplate: select('templateSmall') }"
```

`html/custom-content.html` 中的 `HTML AppBar control sample` 和 `html/appbar-flyout.html` 中的 `HTML flyout control sample` 还提供了几个示例：

```
data-win-options = "{ id: 'list', type: 'content', section: 'selection',
    firstElementFocus:select('.dessertType'), lastElementFocus:select('.dessertType') }"
data-win-options = "{ id: 'respondButton', label: 'Respond', icon: 'edit', type: 'flyout',
    flyout:select('#respondFlyout') }"
```

如果你想知道，`select` 是目前唯一能以这种方式使用的方法。

## WinJS 控件实例化

正如我们已经多次看到的，使用 `data-*` 属性在标记中声明的 WinJS 控件不会实例化，直到你对单个控件调用 `WinJS.UI.process(<element>)`，或对当前 DOM 中所有此类元素调用 `WinJS.UI.processAll`，或者可选地对给定元素中包含的所有元素调用它。对于 `processAll`，如果你刚刚向 DOM 添加了大量标记（例如通过 `innerHTML` 赋值或 `WinJS.UI.Pages.render`），你可以调用 `WinJS.UI.processAll` 来实例化该标记中的任何 WinJS 控件。

要理解此过程，以下是 WinJS.UI.process 对单个元素所做的事情：

- 将 `data-win-options` 字符串解析为选项对象，如果解析失败则抛出异常。
- 提取 `data-win-control` 中指定的构造函数，并对该函数调用 `new`，传入根元素和选项对象。
- 构造函数会在根元素内创建它所需的任何子元素。
- 构造函数返回的对象（即控件对象）会存储在根元素的 `winControl` 属性中。

显然，大部分工作实际上发生在构造函数中。完成此步骤后，其他 JavaScript 代码（例如应用激活方法或页面控件的 ready 方法中的代码）可以调用方法、操作属性，并为根元素和 winControl 对象上的事件添加监听器。

就 WinJS.UI.processAll 而言，它只是遍历 DOM（从文档根或给定的可选元素开始），查找 data-win-control 属性，并对每个属性执行 WinJS.UI.process。如何使用这两者完全取决于你：processAll 执行深度遍历，而 process 允许你在动态插入标记时一次实例化一个控件。请注意，在两种情况下返回值都是一个 promise，因此如果你需要在处理完成后采取额外步骤，请向该 promise 的 then 或 done 方法提供一个完成处理程序。

同样需要理解的是，process 和 processAll 实际上只是辅助函数。如有需要，你可以直接对控件构造函数调用 new，并传入元素和选项对象。这会创建控件并自动将其附加到给定元素。你也可以为元素传入 null，在这种情况下，WinJS 控件构造函数会创建一个新的 div 元素来容纳该控件，否则该控件不会附加到 DOM。例如，这允许你在屏幕外构建控件，并仅在需要时将其附加到 DOM。

另请注意，process 和 processAll 会检查任何给定控件是否已经实例化（该元素已具有 winControl 属性），因此你可以对同一根元素或整个文档反复调用任一方法而不会出现问题。

要了解所有这些的实际效果，我们稍后会看一些示例。不过首先，我们需要讨论一个称为严格处理的问题。

## 严格处理与 processAll 函数

WinJS 有三个 DOM 遍历函数：WinJS.UI.processAll、WinJS.Binding.processAll（我们将在第 6 章后面看到）和 WinJS.Resources.processAll（我们将在第 19 章“面向所有人的应用，第 1 部分”中看到）。其中每个函数都会查找特定的 `data-win-*` 属性，然后使用这些内容执行额外操作。不过，这些操作可能涉及调用多种不同类型的函数：
