
图 24-44 显示了此简单页面的结果。

![](img/67a6707ff505c052edb96c0128fb3096_1004_0.png)

图 24-44

## 总结

`Ajax Control Toolkit` 让为 Web 应用程序添加丰富的动画和交互变得简单。除了可以使用 `UpdatePanel` 控件来实现页面内容的异步更新外，你还可以使用 `UpdatePanelAnimation` 向用户显示后台正在处理。该工具包有助于模糊桌面应用程序与 Web 应用程序之间的区别。模态对话框和弹出对话框开始让 Web 应用程序超越用户对在浏览器中工作的预期。

如你所见，许多此类控件供你选择。最棒的一点是，这是与微软的社区努力，可用控件列表将随着时间的推移不断增长。

本章探索了 `Ajax Control Toolkit` 的许多控件以及如何在 ASP.NET 应用程序中使用它们。请经常访问 Microsoft Ajax 页面和 `Ajax Control Toolkit` 站点，以利用最新的发布功能。

# 25

# jQuery

本章内容包括：

- 下载并引入 jQuery
- 访问和操作文档对象模型 (DOM)
- 处理事件
- 向服务器触发 Ajax 调用
- 使用 UI 组件

## 本章 WROX.COM 下载

请注意，本章中的所有代码示例均作为本章代码下载的一部分，可以在书籍网站 www.wrox.com 的 `Download Code` 选项卡获取。

开源 JavaScript 库 jQuery 是当今现代 JavaScript 开发的事实标准。根据 http://trends.billwith.com/javascript 的统计（截至 2013 年 1 月），在使用了知名 JavaScript 库的前 1,000,000 个顶级网站中，有超过 40% 选择了 jQuery。因此，微软也采用 jQuery 并不令人意外。

此前，微软开发了自己的 JavaScript 项目：`Microsoft Ajax Library` 仍然是 ASP.NET Web Forms 的一部分（如果在页面上添加了 `ScriptManager` 控件，它会自动加载，如第 23 章所述），但它在非微软对象并不流行。因此，微软决定转而支持市场领导者。随 Visual Studio 2010 及更高版本提供的许多 Web 模板带有 jQuery。

jQuery 是一个非常强大的库，让无数常见的 JavaScript 任务变得非常简单。关于 jQuery 有整本书著作，包括 Cesar Otero 和 Rob Larsen 编写的 336 页的《Professional jQuery》(John Wiley & Sons, 2012)。显然，本章只能触及表面，并在使用 JavaScript 库时引导你完成最常见的任务。欲需更深入的信息，请参考上述书籍或 jQuery 站点 (http://api.jquery.com/)上的丰富文档。

## jQuery 简介

jQuery 首页是 http://jquery.com/（见图 25-1），并于 2013 年 1 月进行了重新设计。它突出了该库的三个主要卖点：

- 它是轻量级的：如果使用 HTTP 的 Gzip 压缩，整个库的大小约为 32KB。
- 它兼容 CSS3：支持大多数 CSS3 标准，即使在不支持 CSS3 的浏览器中也是如此（例如版本 6 的 Internet Explorer）。
- 它是跨浏览器的：jQuery 对最常用的浏览器进行了彻底测试，包括 Internet Explorer、Firefox、Chrome、Opera 和 Safari。

![](img/67a6707ff505c052edb96c0128fb3096_1007_0.png)

图 25-1

要在 ASP.NET 应用程序中使用 jQuery，你需要将该库添加到当前网站或项目中。如果你想手动下载该库，只需点击 jQuery 首页上的下载链接；然而，代码看起来非常难以读（见图 25-2）。原因是代码已针对性能进行了优化：删除了空格，并重命名了标识符使其更短。

![](img/67a6707ff505c052edb96c0128fb3096_1008_0.png)

图 25-2

如果你点击 `Download Un-minified Copy` 链接，可以下载一个更易读且带有注释的代码版本。图 25-3 显示了该文件中部分 JavaScript。

![](img/67a6707ff505c052edb96c0128fb3096_1008_1.png)

图 25-3

任选你需要的的文件版本（提示：通常，较小的版本对于开发足够了，这也是你应该部署到任何地方的版本），并将其添加到站点或 Web 项目中。

向项目添加当前版本 jQuery 的更方便方法是使用 NuGet 包管理器。在包管理器控制台中，执行列表 25-1 中的命令。

### 列表 25-1：通过 NuGet 安装 jQuery

```powershell
Install-Package jQuery
```

过了一会儿，你的网站将包含一个新的 `Script` 文件夹，其中至少包含以下文件（假设 jQuery 1.9.0 是最新版本——你尝试此处时的最新版本可能会不同）：

- `jquery-1.9.0.js`：带有注释、易读的 jQuery 版本
- `jquery-1.9.0.min.js`：压缩后的 jQuery 版本
- `jquery-1.9.0-vsdoc.js`：Visual Studio IntelliSense 的提示

取决于你如何安装 jQuery 以及当前哪个版本，路径和文件名可能与本章使用的有所不同。请确保根据你的系统调整文件名。

上述列表中的第三个文件具有特定的意义，因为它可以方便使用 jQuery。为了演示这一点，请查看列表 25-2。你会看到 jQuery 库已添加到带有 `<script>` 标签的页面。

### 列表 25-2：加载 jQuery

```html
<!DOCTYPE html>
<html>
<head>
  <title>jQuery</title>
  <script src="jquery.min.js"></script>
  <script type="text/javascript">
    $(function () {
      // DOM ready
    });
  </script>
</head>
<body>
  <div>
  </div>
</body>
</html>
```

## 选择元素

> **注意**：规范当前版本 (http://www.w3.org/TR/css3-selectors/) 包含了标准的完整列表，jQuery 支持其大部分内容。实际上，jQuery 非常智能。在旧版浏览器中，JavaScript 库有自己的选择器引擎 `Sizzle`，它也可以作为一个独立项目使用 (http://sizzle.com/)。该选择器解析 CSS 选择器并返回一组元素。
>
> 更现代的浏览器内置了 JavaScript API 用于 CSS 选择。如果遇到此类客户端，jQuery 会将复杂的解析和选择工作交给浏览器。

与 jQuery 一样，CSS 是一个复杂的话题。Richard York 写的《Work's Beginning CSS》(John Wiley & Sons, 2004) 有 648 页！然而，在许多场景下，一种 CSS 选择器就能完成工作。CSS 元素选择通用的三种：

- **标签选择器**：例如，选择器 `p` 匹配页面上所有的 `<p>` 元素；`p a` 匹配 `<p>` 元素内所有的 `<a>` 元素。结果是 HTML，而不是使用的 ASP.NET 控件。例如，选择器 `Calendar` 将无法工作。
- **类选择器**：这些以点为开头。例如，选择器 `.class` 会选择所有具有 HTML 属性 `class="class"` 的元素。你也可以混合使用：`a.class` 会匹配所有带有 class 的 `<a>` 标签，但不匹配 `<p>` 标签。使用 ASP.NET 时，请记住 Web 控件的 `Class` 属性变为生成的 HTML 中的 `class`。
- **ID 选择器**：如果一个 HTML 元素有一个 ID，例如 `id="myID"`，则选择器 `#myID` 将匹配该元素。

> **警告**：与 ASP.NET Web Forms 工作时通常是危险的，因为 ASP.NET 会重写某些 ID。使用 `ClientID="Static"` 可能有所帮助，或者通过控件的 `ClientID` 属性动态确定客户端 ID。在大多数情况下，标签和选择器的组合是最佳方法。

如果你用 CSS 选择器作为参数调用 `$()` 函数，你将获得页面上所有匹配该选择器的列表。为了进行选择，你将接收到一个代表所选元素的 jQuery 对象。区别在于，jQuery 对象拥有方法，因此你可以对这些元素进行进一步处理。你将在章的后面部分经常用到此功能。

现在，你只需要使用 jQuery 对象的一个方法，例如 `size()` 返回元素的数量。列表 25-4 显示了一个包含几个元素的简单页面。jQuery 代码使用 JavaScript 的 `alert()` 输出结果，结果也显示在图 25-6 中。

### 列表 25-4：使用 jQuery 选择元素

```html
<%@ Page Language="C#" %>
<!DOCTYPE html>
<html>
<head>
<title>jquery</title>
<script type="text/javascript" src="Scripts/jquery.js"></script>
<script type="text/javascript">
$(function () {
  var divs = $("div").size();
  var spans = $("span").size();
  alert(divs + " <div> elements\n" + spans + " <span>elements</span>");
});
</script>
</head>
<body>
<form runat="server">
  <div>
    <span>First label</span>
  </div>
  <asp:Panel ID="Panel" runat="server">
    <asp:Label ID="Labell" runat="server" Text="Second label" />
  </asp:Panel>
</form>
</body>
</html>
```

![](img/67a6707ff505c052edb96c0128fb3096_1013_0.png)

图 25-6

图 25-6 中的结果可能有点令人惊讶。然而，请考虑 `<asp:Panel>` 默认渲染为 `<div>` 元素，而 `<asp:Label>` 变为 `<span>` 元素。此外，查看生成的 HTML 标记可以发现，隐藏的 ViewState 被封装在另一个 `<div>` 元素中，因此结果是正确的。记住：重要的是 HTML，而不是 ASP.NET 标记。

## 修改元素

仅仅统计你选择了多少元素是罕见的；通常你确切知道自己正在获取多少个元素。重要的是你对它们做了什么。通过 jQuery 你拥有完整的增、读、改、删 (CRUD) 功能，但大多数时候，你要么从元素读取或写入元素，要么向你的页面添加新元素。

### 修改内容

jQuery 提供了四个方法从所选元素中读取信息，取决于元素的类型：

- `attr("属性名称")`：所选元素 HTML 属性的值
- `html()`：所选元素的内部 HTML 内容
- `text()`：所选元素的内部内容，仅限文本（已剥离 HTML）
- `val()`：大多数表单元素的值，对应于元素的 value HTML 属性

更改这些值也是可能的。提供了以下四个方法：

- `attr("属性名称", "属性值")`
- `html("新的 HTML 内容")`
- `text("新文本内容")`
- `val("新值")`

如你所见，获取 (getter) 和设置 (setter) 方法是相同的——仅仅是参数的数量帮助 jQuery 确定要做什么。从 API 的角度来看，这看起来可能很奇怪，但列表 25-5 显示了 `html()` 的两个用途。

### 列表 25-5：使用 html() 读取和写入内容

```html
<%@ Page Language="C#" %>
<!DOCTYPE html>
<html>
<head>
<title>jquery</title>
<script type="text/javascript" src="Scripts/jquery.js"></script>
<script type="text/javascript">
$(function () {
  var divs = $("div").size();
  var spans = $("span").size();
  alert(divs + " <div> elements\n" + spans + " <span>elements</span>");
});
</script>
</head>
<body>
<form runat="server">
  <div>
    <span>First label</span>
  </div>
  <asp:Panel ID="Panel" runat="server">
    <asp:Label ID="Labell" runat="server" Text="Second label" />
  </asp:Panel>
</form>
</body>
</html>
```

![](img/67a6707ff505c052edb96c0128fb3096_1014_0.png)

如果你用 CSS 选择器作为参数调用 `$()` 函数，你将获得页面上所有匹配该选择器的列表。为了进行选择，你将接收到一个代表所选元素的 jQuery 对象。区别在于，jQuery 对象拥有方法，因此你可以对这些元素进行进一步处理。你将在章的后面部分经常用到此功能。

现在，你只需要使用 jQuery 对象的一个方法，例如 `size()` 返回元素的数量。列表 25-4 显示了一个包含几个元素的简单页面。jQuery 代码使用 JavaScript 的 `alert()` 输出结果，结果也显示在图 25-6 中。

如你所见，获取 (getter) 和设置 (setter) 方法是相同的——仅仅是参数的数量帮助 jQuery 确定要做什么。从 API 的角度来看，这看起来可能很奇怪，但列表 25-5 显示了 `html()` 的两个用途。

演示 25-7：

- `css("property")`：读取属性
- `css("property", "value")`：写入属性
- `css({"property1": "value1", "property2": "value2"})`：写入多个属性

### 列表 25-7：使用 append() 添加元素

```html
<!DOCTYPE html>
<html>
<head>
<meta name="server">
<title>Query</title>
<script type="text/javascript" src="Scripts/jquery.js"></script>
<script type="text/javascript">
$(function () {
  $("body").append(
    $("<a>").attr("href", "http://jquery.com/").html("Query")
  );
});
</script>
</head>
<body>
</body>
</html>
```

在列表 25-8 中，使用了类似的方法。这次，你使用的是新创建的元素的 `appendTo()` 方法。同样地作为参数，你必须选择一个 CSS 选择器，这次是针对你想要将新 HTML 元素追加其上的现有元素。

### 列表 25-8：使用 appendTo 添加元素

```html
<!DOCTYPE html>
<html>
<head>
<meta runat="server">
<title>Query</title>
<script type="text/javascript" src="Scripts/jquery.js"></script>
<script type="text/javascript">
$(function () {
  $("<a>").attr("href", "http://jquery.com/")
    .html("Query")
    .appendTo("body");
});
</script>
</head>
<body>
</body>
</html>
```

![](img/67a6707ff505c052edb96c0128fb3096_1016_0.png)

列表 25-7 和 25-8 都导致图 25-9 所示的结果。

如果你想移除元素，删除它们很容易。一种粗暴的方法是选择一个周围元素并执行 `html("")`。更简洁的方法是选择你想删除的元素，然后如列表 25-9 所示调用 `remove()` 方法。

图 25-9

### 列表 25-9：使用 remove() 移除元素

```javascript
$(function () {
  $("p.myClass").remove();
});
```
