

## `:method => :delete` 是怎么回事？

你可能已经注意到，由脚手架生成的 *destroy* 链接包含了 `:method => :delete` 参数。该参数是在 Rails 1.2 中增加的，它决定了在 ProductsController 类中调用哪个方法，同时也会影响使用的 HTTP 方法。

浏览器使用 HTTP 与服务器通信。HTTP 定义了一组浏览器可以使用的动词，并规定了每种动词的使用时机。例如，普通超链接使用 HTTP GET 请求。HTTP 定义 GET 请求用于获取数据；它不应产生任何副作用。因此，Rails 团队修改了脚手架代码生成器，强制链接发出 HTTP DELETE 请求\*。这些 DELETE 请求允许产生副作用，因此更适合用于删除资源。

\* 在某些情况下，根据浏览器是否能够发出 DELETE 方法，Rails 会用 POST 方法代替 DELETE。无论采用哪种方式，请求都不会被缓存或由网络爬虫触发。

即使这个简单的模板也使用了 Rails 的许多内置特性：

-   列表中的行具有交替的背景颜色。这是通过将每一行的 CSS 类设置为 `list-line-even` 或 `list-line-odd` 来实现的。Rails 的辅助方法 `cycle` 自动在连续的行之间切换这两种样式名称。
-   使用 `truncate` 辅助方法仅显示描述的前八十个字符。但在调用 `truncate` 之前，我们调用了 `gsub` 来移除描述中的 HTML 标签。¹⁸
-   我们还使用了 `h` 方法来确保产品标题和描述中任何剩余的 HTML 都被转义。
-   看一下 `link_to 'Destroy'` 这一行。请注意它带有参数 `:confirm => "Are you sure?"` 。如果单击此链接，Rails 会安排浏览器弹出对话框，在链接跳转并删除产品之前请求确认。（另外，请参阅本页侧边栏，了解该操作的更多信息。）

我们向数据库加载了一些测试数据，重写了显示产品列表的 `index.html.erb` 文件，添加了 `depot.css` 样式表，并通过编辑布局文件 `products.html.erb` 将该样式表链接到页面中。

18. 如果你看到类似 `undefined method 'for' for {length=>80}.Hash` 的消息，那么你可能没有运行 Rails 2.2.2 或更高版本。参见第 3 章“安装 Rails”（第 31 页）了解升级信息，或者简单地从该调用中删除 `length =>`（保留 80）。

在本章中，我们将看到

-   编写我们自己的视图，
-   使用布局装饰页面，
-   集成 CSS，
-   使用辅助方法，以及
-   将页面链接到操作。

## 第 7 章

## 任务 B：目录显示

总而言之，到目前为止这一天过得很顺利。我们从客户那里收集了初始需求，记录了基本流程，初步确定了所需的数据，并为 Depot 应用程序的产品组装了维护页面。我们甚至设法在上午结束时享用了一顿不错的午餐。

精神饱满之后，我们继续第二个任务。我们与客户讨论了优先级，她说她希望开始从买家的角度看看应用程序的外观。我们的下一个任务是创建一个简单的目录显示。

从我们的角度来看，这也非常合理。一旦我们将产品安全地存入数据库，显示它们应该相当简单。这也为我们后续开发购物车部分代码提供了基础。

我们还应该能够借鉴刚才在产品维护任务中所做的工作——目录显示实际上只是一个美化过的产品列表。那么，让我们开始吧。

### 7.1 迭代 B1：创建目录列表

我们已经创建了 products 控制器，供卖家管理 Depot 应用程序。现在，是时候创建第二个控制器，用于与付费客户交互了。我们叫它 Store。

```
depot> ruby script/generate controller store index
exists   app/controllers/
exists   app/helpers/
create   app/views/store
exists   test/functional/
create   app/controllers/store_controller.rb
create   test/functional/store_controller_test.rb
create   app/helpers/store_helper.rb
create   app/views/store/index.html.erb
```

![](img/a160fc3a330a0b3b2a764d41d614e688_97_0.png)

图 7.1：我们的第一个（丑陋的）目录页面

一般来说，尽量养成在模板中输入 `<%=h ... %>` 的习惯，只有当你确信可以安全地移除 `h` 时才将其移除。

我们还使用了 `image_tag` 辅助方法。这个方法会生成一个 HTML `<img>` 标签，并将其参数作为图像源。

点击刷新后，显示画面如图 7.1 所示。页面相当丑陋，因为我们还没有包含 CSS 样式表。正当我们思考这个问题时，客户恰好路过，她指出她也希望面向公众的页面看起来有像样的标题和侧边栏。

在现实世界中，此时我们可能会想请设计人员来——我们已经见过太多程序员设计的网站，不忍心再给世界添一个。但 Pragmatic Web Designer 正在某个海滩寻找灵感，要到今年晚些时候才能回来，所以让我们暂时先放一个占位符。是时候进行一次迭代了。

### 7.2 迭代 B2：添加页面布局

典型网站中的页面往往共享相似的布局——设计人员会创建一个标准模板，用于放置内容。我们的任务是将这种页面装饰添加到每个商店页面中。

幸运的是，在 Rails 中我们可以定义布局。布局是一个模板，我们可以将额外内容流入其中。在我们的案例中，我们可以为所有商店页面定义一个单独的布局，并将目录页面插入该布局中。稍后我们可以对购物车和结账页面做同样的事情。因为只有一个布局，我们可以通过编辑一个文件来改变网站这部分区域的整体外观和感觉。这让我们对暂时放置占位符感到安心；当设计师最终从岛上回来后，我们可以进行更新。

在 Rails 中，有多种指定和使用布局的方法。现在我们将选择最简单的。如果我们在 `app/views/layouts` 目录中创建一个与控制器同名模板文件，那么该控制器渲染的所有视图将默认使用该布局。所以，现在让我们创建一个。我们的控制器叫 store，因此我们将布局命名为 `store.html.erb`：

下载 depot_e/app/views/layouts/store.html.erb

```
Line 1 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
<title>Pragprog Books Online Store</title>
<%= stylesheet_link_tag "depot", :media => "all" %>
</head>
<body id="store">
<div id="banner">
<%= image_tag("logo.png") %>
<%= @page_title || "Pragmatic Bookshelf" %>
</div>
<div id="columns">
<div id="side">
<a href="http://www....">Home</a><br />
<a href="http://www..../faq">Questions</a><br />
<a href="http://www..../news">News</a><br />
<a href="http://www..../contact">Contact</a><br />
</div>
<div id="main">
<%= yield :layout %>
</div>
</div>
</body>
</html>
```

除了常见的 HTML 元素之外，这个布局还有三个 Rails 特定的项目。第 6 行使用 Rails 辅助方法生成一个指向我们 `depot.css` 样式表的 `<link>` 标签。在第 11 行，我们将页面标题设置为实例变量 `@page_title` 的值。然而，真正的魔法发生第 21 行。当我们调用 `yield` 并传递名称 `:layout` 时，Rails 会自动替换页面特定的内容——即由该请求调用的视图生成的内容。在我们的案例中，这将是由 `index.html.erb` 生成的目录页面。³

为了使其正常工作，我们需要在 `depot.css` 样式表中添加以下内容：

```
Download depot_e/public/stylesheets/depot.css

/* Styles for main page */

#banner {
  background: #9c9;
  padding-top: 10px;
  padding-bottom: 10px;
  border-bottom: 2px solid;
  font: small-caps 40px/40px "Times New Roman", serif;
  color: #282;
  text-align: center;
}

#banner img {
  float: left;
}

#columns {
  background: #141;
}

#main {
  margin-left: 13em;
  padding-top: 4ex;
  padding-left: 2em;
  background: white;
}

#side {
  float: left;
  padding-top: 1em;
  padding-left: 1em;
  padding-bottom: 1em;
  width: 12em;
  background: #141;
}

#side a {
  color: #bfb;
  font-size: small;
}
```

3. Rails 还会将变量 `@content_for_layout` 设置为渲染操作的结果，因此你也可以将此值替换到布局中以代替 `yield`。这是原来的做法（而且我们个人认为它更可读）。使用 `yield` 被认为更酷。

