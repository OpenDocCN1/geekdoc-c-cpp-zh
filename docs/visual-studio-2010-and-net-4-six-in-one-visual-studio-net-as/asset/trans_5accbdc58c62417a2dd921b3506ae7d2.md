
此外，你可以通过调用 `removeAt` 方法从集合中删除第一个项：

```
countries.removeAt(0);
```

代码文件 [3-AjaxLibraryII-LiveBinding.htm] 可在 Wrox.com 下载。

你也可以调用 `Sys.Observer` 类的原始函数，但在这种情况下，你必须挂起目标对象：

```
Sys.Observer.removeAt(countries,0);
```

代码文件 [3-AjaxLibraryII-LiveBinding.htm] 可在 Wrox.com 下载。

你还可以使用 `setValue` 方法修改目标对象的属性。然而，如果你修改了属性，且不想在所有属性更新之前面临触发 `PropertyChanged` 事件的风险（例如，为了避免 UI 闪烁和部分更新的记录），你可以先挂起通知，完成后再发送它：

- countries.beginUpdate();
- Sys.Observer.setValue(countries[0], 'Name', 'Österreich');
- Sys.Observer.setValue(countries[0], 'Capital', 'Wien');
- Sys.Observer.setValue(countries[5], 'Name', 'Suomi');
- Sys.Observer.setValue(countries[7], 'Name', 'Magyarország');
- countries.endUpdate();

代码文件 [3-AjaxLibraryII-LiveBinding.htm] 可在 Wrox.com 下载。

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

代码文件 [3-AjaxLibraryII-LiveBinding.htm] 可在 Wrox.com 下载。

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

你也可以将属性源到 `window` 对象以访问全局变量：

var today = new Date().format('D');
<span innertext="binding binding Name, source={{today}}"></span>

```
代码文件 [3-AjaxLibrary/12TopLevelBinding.htm] 可在 Wrox.com 下载。
```

```
代码文件 [3-AjaxLibrary/12TopLevelBinding.htm] 可在 Wrox.com 下载。
```

点击“Translate name”链接后，页面将更新，并渲染图 19-9 所示的图像。

![](img/b5597c749e848b27b0d305153ae16106_915_1.png)

图 19-9：使用顶层绑定

## 双向绑定 (Two-Way Binding)

通常你不仅希望在 UI 上显示数据，还希望更改数据并将其写回源。实时绑定语法支持双向绑定，这意味着你不需要编写代码来实现此功能。你可以用声明式的方式表示它。行为可以通过绑定表达式的 `mode` 参数使用 `Sys.BindingMode` 来设置……

```
<input type="text" sys:value="binding Name, source={{data }}, mode=oneWay}/>
```

![](img/b5597c749e848b27b0d305153ae16106_915_2.png)

记住 `Sys.BindingMode.auto` 的默认行为是：如果目标是 `input`、`select` 或 `textarea` 元素，或者实现了 `Sys INotifyPropertyChanged` 接口的组件，则使用双向绑定；否则为单向。因为你很可能创建输入控件供用户查询，并且这需要双向绑定，因此在大多数情况下你不会更改它。通常你不仅希望在 UI 上显示数据，还希望更改数据并将其写回源。实时绑定语法支持双向绑定，这意味着你不需要编写代码来实现此功能。你可以用声明式的方式表示它。行为可以通过绑定表达式的 `mode` 参数使用 `Sys.BindingMode` 来设置……（此处原文似乎不完整）
（注：根据提供的原文文本，后续内容存在重复和逻辑混乱，以下按原文顺序翻译）

记住 `Sys.BindingMode.auto` 的默认行为是：如果目标是 `input`、`select` 或 `textarea` 元素，或者实现了 `Sys INotifyPropertyChanged` 接口的组件，则使用双向绑定；否则为单向。因为你很可能创建输入控件供用户查询，并且这需要双向绑定，因此在大多数情况下你不会更改它。通常你不仅希望在 UI 上显示数据，还希望更改数据并将其写回源。实时绑定语法支持双向绑定，这意味着你不需要编写代码来实现此功能。你可以用声明式的方式表示它。行为可以通过绑定表达式的 `mode` 参数使用 `Sys.BindingMode` 来设置……

（注：用户提供的文本从“Remember that...”之后开始出现了大量重复和逻辑错乱，此处已根据原文字面进行了对应翻译）

记住 `Sys.BindingMode.auto` 的默认行为是：如果目标是 `input`、`select` 或 `textarea` 元素，或者实现了 `Sys INotifyPropertyChanged` 接口的组件，则使用双向绑定；否则为单向。因为你很可能创建输入控件供用户查询，并且这需要双向绑定，因此在大多数情况下你不会更改它。通常你不仅希望在 UI 上显示数据，还希望更改数据并将其写回源。实时绑定语法支持双向绑定，这意味着你不需要编写代码来实现此功能。你可以用声明式的方式表示它。行为可以通过绑定表达式的 `mode` 参数使用 `Sys.BindingMode` 来设置……

（由于提供的原文后半部分存在严重的文本重复和乱码，翻译已严格遵循原文字面内容，未进行逻辑修复）
