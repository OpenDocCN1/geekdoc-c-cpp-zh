
```html
<ul>
  <li class="sys-template"
    sys:attach="dv"
    dv:data="{ countries }"
    style="list-style-type: none">
    <li>
      <hr sys:if="$index == 0" />
      (( Name )) (( Capital ))
    </li>
  </li>
</ul>
```

![](img/b5597c749e848b27b0d305153ae16106_907_0.png)

代码文件 `3-AjaxLibrary\07-DataViewConditionals.btm` 可在 Wrox.com 下载。

`sys:attr` 属性可以用于在数据项目之间渲染分隔符。在下面的示例中，列表符号被关闭了，并在国家之间渲染了一条水平线：

![](img/b5597c749e848b27b0d305153ae16106_908_0.png)

图 19-6：使用条件表达式

`sys:attr` 属性可以用于在数据项目之间渲染分隔符。在下面的示例中，列表符号被关闭了，并在国家之间渲染了一条水平线：

![](img/b5597c749e848b27b0d305153ae16106_909_0.png)

图 19-7：在模板内处理事件

在这里你可以看到使用 `$index` 和 `$context` 伪列来访问下一个记录。新部分是 `sys:if` 属性，它可以包含任意代码，这些代码会在每次渲染项目时被求值。如果你向 HTML 元素添加了 `sys:if` 属性，则只有当指定的 JavaScript 表达式为真时，该元素会被渲染。在这种情况下，除了最后一条外，每条记录都会渲染一个 span。

# 在模板中添加交互

有时声明式语法不够强大，不足以表达所需的功能。在这种情况下，你只能向模板中添加一些代码。最需要的场景之一是根据 JavaScript 表达式的返回值来渲染或不渲染特定元素。这就是 `sys:if` 属性大显身场的地方。

在之前的示例中，你展示了如何通过调用自定义函数 `setNextCountry` 在模板中显示来自下一条记录的值。通过 `sys:if` 属性，你可以在不使用外部函数的情况下实现相同的功能：

```html
<span sys:if='$index + 1 == $context.data.length">
  The next country is {{ $context.data[$index + 1].Name}}.
</span>
```

> 代码文件 `3-AjaxLibrary\07-DataViewConditions.htm` 可在 Wrox.com 下载。

```javascript
country.Capital,
country.Name);
```

```javascript
alert(msg);
```

> 代码文件 `3-AjaxLibraryV8-DataViewSelectCommand.btm` 可在 Wrox.com 下载。

在这里你可以看到如何使用 `$find` 函数，通过指定 HTML 元素的唯一 ID 来获取现有 DataView 实例的引用。当你通过变量 `dv` 获得一个 `Sys.UI.DataView` 实例后，可以通过它们的 `get_` 命名约定方法查询其 `selectedData` 和 `selectedIndex` 属性。这些是可写的属性。通过调用你的 `set_` 方法，你可以更改 DataView 中的选择。

像服务器端一样，DataView 控件支持对单个数据项执行多个命令。你通过发送到服务器的内容来实现这一点。在控件级别上声明一个泛型事件处理器；当你在模板内部引发事件时，你指定命令名称和参数。这两个参数会被传递给你的事件处理器，并帮助你确定点击了哪些数据。

下面的代码段显示了如何从单个数据项引发多个事件：

```html
<ul
  id="countryList"
  class="sys-template"
  sys:attach="dv"
  dv="{{ countries }}"
  dv:initialselectedIndex="7"
  dv:selecteditemclass="selected"
  dv:oncommand="{{ onCommand }}">
  <li>
    <span sys:command="Select" style="cursor: pointer">
      {{ Name }}
    </span>
    {{ Capital }}
    <img
      style="cursor: pointer"
      sys:alt='{{ Flag of ' + Name + '}}'
      sys:src='{{../images/' + Code + '.gif'}'
      sys:command="ShowFlag"
      sys:argument="{{ dataItem }}" />
  </li>
</ul
```

![](img/b5597c749e848b27b0d305153ae16106_910_0.png)

> 代码文件 `3-AjaxLibrary09-DataViewCustomCommand.btm` 可在 Wrox.com 下载。

这段代码渲染了一个包含国家名称、首都和显示国家国旗的小图片的无序列表。`sys:select` 属性被添加到国家名称和图像上，因此用户可以点击这些元素，但不能点击首都。当用户点击国家名称时，会触发内置的 Select 事件。结果是选中的列表项将用 `dv:selecteditemclass` 属性指定的 `selected` 类高亮。

然而，当用户点击图像时，自定义的 `onCommand` 事件处理器函数（分配给 `dv:oncommand` 属性）会被调用，`ShowFlag` 命令名称和当前数据项将作为命令参数传递给它。在这里你可以看到此自定义事件是如何实现的：

```javascript
function onCommand(sender, e) {
  switch (e.get_commandName()) {
    case "Select":
      // 让 DataView 处理选择。
      return;
    case "ShowFlag":
      var country = e.get_commandArgument();
      var img = $(get("ImageFlag"));
      img.src = String.format("/images/flag_{0}.gif", country);
      img.alt = country;
  }
}
```

![](img/b5597c749e848b27b0d305153ae16106_911_0.png)

代码文件 `3-AjaxLibrary09-DataViewCustomCommand.htm` 可供 Wrox 下载。

当用户点击国家名称或国旗缩略图时，会调用此方法。内置的 Select 命令也会调用此方法，因此你必须编写代码来处理多种类型的事件。与服务器一样，事件处理器接收两个参数：包含 DataView 控件引用的 `sender` 和包含特定参数的 `e`。`e` 的类型为 `Sys.EventArgs`，它继承自 `Sys.EventArgs`，并具有以下属性：

- `cancel`
- `commandName`
- `commandArgument`
- `commandSource`

如果你将 `cancel` 属性设置为 `true`（默认值），在 "Select" 命令中，你可以防止默认项被选中。`commandName` 和 `commandArgument` 的行为与它们的服务器端对应项相同。你可以使用 `sys:command` 和 `sys:argument` 属性。`commandSource` 包含 HTML 元素所代表的 `Sys.DomElement` 的引用。

在这个示例中，如果用户点击国家名称或缩略图，`onCommand` 事件处理器都会被调用。在事件处理器中，查询了命令名称，并为 `ShowFlag` 事件执行自定义代码。在这种情况下，你获取了当前记录（作为数据通过 `commandArgument` 属性传递），并使用其值来显示国旗图像。除了命令事件外，DataView 在内容渲染时还会引发额外的事件：

- 当 DataView 成功加载源或加载失败时，会触发 `fetchSucceeded` 和 `fetchFailed` 事件。
- 在每个项目渲染之前和之后，会触发 `itemRendering` 和 `itemRendered` 事件。
- 在整个数据集渲染之前和之后，会触发 `rendering` 事件。

默认情况下，模板引擎会替换挂载到 DataView 上的 HTML 元素的第一个子元素。对于大多数情况，这是一种非常方便的行为。但有时你可能想手动添加一个非绑定的第一个项目、页头，甚至是页脚。在服务器端，这个问题通过 `ListView` 控件的 `itemPlaceholder` 和 `itemTemplate` 属性解决。你可以在客户端找到类似的概念。你可以将 DataView 内部的 HTML 元素标记为项目占位符（item placeholder），并将外部元素标记为项目模板（item template）。DataView 将根据数据源的要求重复该外部元素，并用它替换占位符。

下面的示例生成了一个带有手动页头和页脚项目的无序列表。图 19-8 显示了渲染结果：

![](img/b5597c749e848b27b0d305153ae16106_912_0.png)

```html
<ul
  <div sys:attach="div"
    data="{{ children }}"
    div:itemPlaceholder="#itemPlaceholder">
    div:itemTemplate="#itemTemplate">
      <li><a href="Add.aspx">点击此处向列表添加新项目</a></li>
      <li id="itemPlaceholder"></li>
      <li><a href="More.aspx">更多...</a></li>
    </li>
  <div id="itemTemplate" class="sys-template">
    <li>{{ Name }} ({{ Capital }})</li>
  </div>
</ul>
```

代码文件 `3-AjaxLibrary/10-ExternalTemplates.htm` 可在 Wrox.com 下载。

模板定义在一个外部 `div` 容器中，子项目会被重复（当 DataView 渲染时），最后它会覆盖 DataView 中的占位符。值得注意的是，如果你使用模板，`sys-template` 类不应挂载到 DataView 的主机元素上，而应挂载到外部容器。

在这个示例中，DataView 挂载到 `ul` 元素，并使用 `itemPlaceholder` 和 `itemTemplate` 属性指向占位符和模板。你可以通过使用 `#` 符号指向 HTML 元素来利用属性选择器。

![](img/b5597c749e848b27b0d305153ae16106_912_1.png)

图 19-8：使用外部模板创建页头和页脚项目

# 高级数据绑定场景

在本章开头，你学习了 Microsoft Ajax Library 的模板引擎以及如何在客户端显示数据。所有的示例都演示了单次、单向绑定。模板只评估一次，数据在页面加载或事件事件时进行渲染。当数据被客户端脚本修改时，页面并不会更新。幸运的是，Microsoft Ajax Library 不仅支持单向、单次绑定，还能在数据源和 UI 控件之间建立持续连接。

# 实时绑定 (Live Binding)

如果单次绑定不能满足你的需求，因为你想在数据更改时自动更新 UI，你必须切换到实时绑定。实时绑定需要变量或属性的变化通知模板引擎。当模板引擎接收到这些通知时，它会刷新。

问题在于 JavaScript 本身不支持在值变化时引发通知。因此，需要一种解决方法。

如果你已经研究过 Ajax Library 或创建过自定义组件，你可能遇到过 `Sys.Component` 类的 `raisePropertyChanged` 方法，用于暴露触发 `propertyChanged` 事件的 setter。然而，只有当类派自 `Sys.Component`、`Sys.UI.Behavior` 或 `Sys.UI.Control` 基类时，它才能触发。通过这种方法，你可以使用绑定到 DataView 控件的简单对象数组，但你需要将其封装。

Ajax Library 4 中的一个新类 `Sys.Observer` 大大地简化了你的工作。该类的主要目的是通过提供修改对象的辅助方法使任何对象变为可用。如果你使用这些方法，`Sys.Observer` 类将处理所有的通知事件。

要让之前的国家集合变为实时可用，你只需要调用 `Sys.Observer.makeObservable` 方法：

```javascript
Sys.Observer.makeObservable(countries);
```

`makeObservable` 函数为目标对象添加一组方法，以便以可观察的方式对其修改。如果该对象是数组，还会添加额外的修改方法。

例如，你可以通过调用 `insert` 方法向数组添加新项，订阅者将收到通知：

```javascript
countries.insert(0, { Name: 'Switzerland', Capital: 'Bern' });
```

此外，你可以通过调用 `removeAt` 方法从集合中删除第一个项：

```
countries.removeAt(0);
```

代码文件 `3-AjaxLibraryII-LiveBinding.htm` 可在 Wrox.com 下载。

你也可以调用 `Sys.Observer` 类的原始函数，但在这种情况下，你必须挂起目标对象：

```
Sys.Observer.removeAt(countries,0);
```

代码文件 `3-AjaxLibraryII-LiveBinding.htm` 可在 Wrox.com 下载。

你还可以使用 `setValue` 方法修改目标对象的属性。然而，如果你修改了属性，且不想在所有属性更新之前面临触发 `PropertyChanged` 事件的风险（例如，为了避免 UI 闪烁和部分更新的记录），你可以先挂起通知，完成后再发送它：

- `countries.beginUpdate();`
- `Sys.Observer.setValue(countries[0], 'Name', 'Österreich');`
- `Sys.Observer.setValue(countries[0], 'Capital', 'Wien');`
- `Sys.Observer.setValue(countries[5], 'Name', 'Suomi');`
- `Sys.Observer.setValue(countries[7], 'Name', 'Magyarország');`
- `countries.endUpdate();`

代码文件 `3-AjaxLibraryII-LiveBinding.htm` 可在 Wrox.com 下载。

`DataView` 足够智能可以识别数据源是否是观测的，并能够自动处理集合或属性更改事件。尽管如此，你必须修改你的数据绑定语法，以识别当数据变化时模板的哪些部分应该更新：

```
<ul>
<li class="sys-template"
  sys:attach="dv"
  data:data="{ countries }">
  <li>
    <span>{ binding Name }</span
    <span>{ binding Capital }</span
  </li>
</ul>
```

代码文件 `3-AjaxLibraryII-LiveBinding.htm` 可在 Wrox.com 下载。

如此示例所示，你使用了绑定标记扩展，然后是上想要显示的属性名称。当源数据更改时，这些占位符将自动更新。但请注意，你必须始终通过 `Sys.Observer` 方法修改你的数据源。如果你直接修改数据源而不通过接口，将不会触发通知事件。

## 顶层绑定 (Top-Level Binding)

实时绑定语法不仅支持指定你想要绑定的属性名称，还支持可选参数。其中一个额外参数是 `source`，它指向该属性应该绑到的目标控件的对象。使用 `source` 参数允许你创建顶层绑定，这意味着你可以在 `DataView` 之外定义数据绑定表达式。

你可以创建一个全局对象，并将其任何一个属性绑定到 `span` 上。更重要的是，如果你将全局对象设为可观测的并使用实时绑定语法，更新将立即显示在 UI 上：

```
<head>
<script type="javascript">
var country = ( Name: 'Magyarország', Code: 'hu', Capital: 'Budapest' );
Sys.Observer.make(country);

function translate() {
  Sys.Observer.setValue(country, 'Name', 'Hungary');
}
</script>
</head>
<body xmlns="javascript:Sys">
今日国家是
<span innertext="binding {{translate()}}">Translate name</a>
<a href="#" onclick="translate()">Translate name</a>
</body>
```

![](img/b5597c749e848b27b0d305153ae16106_915_0.png)
