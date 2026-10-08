

```javascript
var authors = eval('+' + executor_responseData + ' ');
var msg = String.format('This sample is written by (0) (1).',
authors[0].FirstName, authors[0].LastName);
}
get(divResult).innerHTML = msg;

request.invoke();
```

代码文件 [3-AjaxLibrary01-Basics.htm] 可在 Wrox.com 下载。

如果你想进行管理，了解客户端生命事件的顺序至关重要。整个页面的生命周期不在本书的讨论范围内。然而，让我们接触一下这个话题，因为该领域有一些细微（但重要）的变化。

触发的第一个事件是 `init` 事件，它在所有脚本加载后、任何对象创建并初始化之前被起——这是生命周期中一个可以向页面添加自定义组件的切入点。要处理此事件，你必须使用 `Sys.Application.add_init` 方法对其进行订阅。

如果你不是开发者，应该使用 `load` 事件，它在所有脚本加载完毕且所有对象都创建并初始化后触发。你不需要为该事件实现处理程序。相反，你可以创建一个保留名称 `pageLoad` 的函数。在 ASP.NET 4 中，你也可以使用 `Sys.onload` 来注册一个函数，该函数会在 DOM 准备绪且所有所需资源已加载时被调用。

在早期的 Ajax 库版本中，如果你使用 `pageLoad` 方法在 `window.onload` 事件之前被调用，你必须手动调用页面的 `Sys.Application.initialize` 方法。从 ASP.NET 4.0 开始，这不再需要，因为 `pageLoad` 方法会在 DOM 内容加载完成后、`window.onload` 事件之前立即调用。

## 操作 DOM 元素

在此之前，你可以看到使用 `get` 函数通过 ID 获取 DOM 元素引用示例。虽然 `get` 函数非常有用，但现代 Web 2.0 应用对 DOM 元素的选择方式需要更大的灵活性。Microsoft Ajax Library 4 引入了一个新函数 (`Sys.get`)，它允许不仅通过 ID，还通过名称或 CSS 类来选择元素。`Sys.get` 同样能够返回 Ajax Library 组件的引用。

`Sys.get` 函数期望两个参数：

- selector — 用于定义你正在寻找的内容。
- context — 这本质上是搜索的范围。

如果你省略第二个参数，函数将搜索整个 DOM。

格式（或者更准确地说，`selector` 参数的第一个字符）决定了函数如何执行搜索。`selector` 可以采用以下格式之一：

- $component - 如果你使用 `$` 前缀，函数将查找指定名称的组件（例如 DataView）。在这种情况下，`$get` 函数的行为类似于 `$find` 方法。
- #id - 如果你使用 `#` 前缀，该方法的行为类似于 `$get` 函数。在内部，`$get` 函数将调用委托给 `Sys.get` 函数，并在 ID 前加上 `#` 前缀。
- .class - 如果你使用 `.` 前缀，`Sys.get` 函数将返回具有指定名称的元素（例如，

例如，要在页面上静态无序列表，你可以使用以下代码：

```html
<ul id="continents" class="list">
  <li class="item">Asia/</li>
  <li class="item">Africa/</li>
  <li class="item">North America/</li>
  <li class="item">South America/</li>
  <li class="item">Antarctica/</li>
  <li class="item">Europe/</li>
  <li class="item">Australia/</li>
</ul>
```

![](img/b5597c749e848b27b0d305153ae16106_894_0.png)

代码文件 [3-AjaxLibrary\02-Selector.htm] 可在 Wrox.com 下载。

要使用文档中 ID 为 "continents" 的第一个元素的引用，你可以使用以下函数：

```javascript
Sys.get('#continents')
```

![](img/b5597c749e848b27b0d305153ae16106_894_1.png)

代码文件 [3-AjaxLibrary\02-Selector.htm] 可在 Wrox.com 下载。

起初，这似乎比使用 `$get` 长一点，但你会很快习惯的，因为这个函数强大得多。例如，你可以获取第一个带有 "item" CSS 类的元素：

```javascript
Sys.get('.item')
```

![](img/b5597c749e848b27b0d305153ae16106_894_2.png)

代码文件 [3-AjaxLibrary\02-Selector.htm] 可在 Wrox.com 下载。

或者，你可以获取文档中的第一个 `li` 元素：

```javascript
Sys.get('li')
```

> 代码文件 [3-AjaxLibrary/02-Selector.htm] 可在 Wrox.com 下载。

你也可以使用 `context` 参数来限制搜索范围，并获取 ID 为 "continents" 的父元素内的第一个元素：

```javascript
Sys.get('li').Sys.get('#continents')
```

> 代码文件 [3-AjaxLibrary/02-Selector.htm] 可在 Wrox.com 下载。

正如你可能注意到的，该方法始终返回单个元素（第一个匹配项）或元素集。另一个需要注意的是，不同类型的搜索（按组件名称、按 ID、按类或按元素名称）不会合并在一个选择器中。这两种情况似乎都是 `Sys.get` 方法的一个非常严格的限制，特别是如果你熟悉 jQuery Library 的功能。好消息是，如果 jQuery Library 已加载到页面中，且选择器不是之前提到的格式之一，则调用将自动转发到 jQuery。这意味着你不需要知道 Microsoft Ajax Library 或 jQuery Library 如何解析查询；你只需要使用你喜的任何语法，并处理结果即可。

继续上一个示例，如果你使用 jQuery，你可以通过 `Sys:` 不仅获取第一个，还可以获取最后一个大洲：

```javascript
Sys.get('#continents .item:last()')
```

> 代码文件 [3-AjaxLibrary/02-Selector.htm] 可在 Wrox.com 下载。

或者你也可以获取第四个：

```javascript
Sys.get('#continents .item:eq(3)')
```

> 代码文件 [3-AjaxLibrary/02-Selector.htm] 可在 Wrox.com 下载。

或者你甚至可以获取 "America"：

```javascript
Sys.get('#continents .item:contains("America")')
```

> 代码文件 [3-AjaxLibrary/02-Selector.htm] 可在 Wrox.com 下载。

## 脚本加载器

在本章早期，你看到了 Microsoft 如何拆分文件以优化页面加载时间。相同的拆分脚本文件在 ways ASP.NET 时也可以用于客户端代码。由于 Microsoft Ajax Library 由 JavaScript 文件组成，将其引入页面的自然方式是使用声明式脚本标签：

```html
<script type="text/javascript" src="MicrosoftAjax.js"></script>
```

然而，Ajax 允许使用命令式代码下载外部文件，而 Microsoft Ajax Library 的脚本加载器封装了这一功能并扩展了额外功能。脚本加载器实现在非常小的 `Start.js` 文件中。`Start.js` 文件被设计为整个库的引导，它是唯一需要在脚本标签中引用的文件。由于 Microsoft Ajax Library可以通过 Microsoft CDN 获取，你也可以从这里加载：

```html
<script src="http://ajax.microsoft.com/ajax/beta/0911/Start.js" type="text/javascript"></script>
```

在 `Start.js` 文件在客户端下载并解析后，你可以使用 `Sys.require` 方法定义你的代码依赖的标准脚本文件。例如，如果你需要历史记录和 jQuery 支持，可以这样加载它们：

```html
<script src="Start.js" type="text/javascript"></script>
<script type="text/javascript">
Sys.require([
  Sys.scripts.History, Sys.jQuery],
  function() {
    // History 和 jQuery 在此处可用
  }
});
</script>
```

`Sys.require` 方法接受三个参数，但在大多数情况下，你可能只调用两个。在第一个参数中，你可以定义应该加载的功能。表 19-1 显示了可用的拆分脚本文件功能（类似于枚举）值，用于引用它们。

