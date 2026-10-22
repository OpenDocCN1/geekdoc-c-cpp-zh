

现在我们需要注册处理器。这可以放在你的环境文件中，或者你可以在 app/controllers 目录下的 application.rb 中设置它。

Download e1/views/app/controllers/application.rb

```
require "rdoc_template"
```

```
ActionView::Template.register_template_handler("rdoc", RDocTemplate)
```

注册调用表示任何以 .rdoc 结尾的模板文件都将由 RDocTemplate 类处理。我们可以通过创建一个名为 example.rdoc 的模板并通过一个新生成的测试控制器访问它来测试这一点：

![](img/a160fc3a330a0b3b2a764d41d614e688_560_0.png)

## Making Dynamic Templates

html.erb 和 xml.builder 模板与控制器共享其环境：它们可以访问控制器实例变量。它们也可以在作为 partials 调用时传入局部变量。我们可以赋予自己的模板同样的权限。你实现这一点的方式取决于你希望模板做什么。这里我们构造一个相当人为的东西：一个 reval 模板，其中包含 Ruby 代码行。渲染时，每一行都会显示出来，并附带其值。以下代码展示了一个名为 test.reval 的模板：

```
a = 1
3 + a
@request.path
```

这可能会产生以下输出：

```
a = 1 => 1
3 + a => 4
@request.path => /text/example1
```

注意模板如何访问 @request 变量。我们通过创建一个 Ruby binding（基本上是变量值的范围）并用控制器设置到视图中的实例变量和局部变量的值来填充它来实现这种魔术。请注意渲染器还将响应内容类型设置为 text/plain；我们不希望我们的结果被解释为 HTML。我们可以

本章由 Justin Gehtland（http://relevancellc.com）撰写，他是一名软件开发者、演讲者和作家，居住在北卡罗来纳州达勒姆市。他是 Streamlined 项目的创始人，该项目用于 Rails 上的高级 CRUD 应用（http://streamlinedframework.org）。它基于他和 Relevance 的 Stuart Halloway 为 RailsConf '06 所写的作品。

## Chapter 24

## The Web, v2.0

我们已经了解了 Action View 如何用于将模板渲染到浏览器。我们已经看到了如何通过布局和 partials 的组合创建页面；大多数情况下，我们的操作都是向浏览器返回整个页面并强制浏览器刷新当前屏幕。这是 Web 的一个核心基础原则：对服务器的请求返回整个页面，浏览器必须完整显示。这章是关于打破 Web 的这一核心原则，并允许你的应用程序处理更小的粒度单元，在浏览器和服务器之间传输数据、部分页面和代码，以提供更具响应性和交互性的用户体验。

Rails 的 Ajax 支持可以分为三个主要领域：

- Prototype 支持 DOM 交互和远程对象调用
- Script.aculo.us 支持视觉效果
- RJS 模板用于以代码为中心的 Ajax

对于前两者，我们必须记住我们学到的关于 helpers 的所有内容，因为几乎所有对 Prototype 和 Script.aculo.us 的支持都可以在 ActionView::Helpers::PrototypeHelper 和 ActionView::Helpers::ScriptaculousHelper 中找到。RJS 模板则完全是另一种生物，结合了一点 Action View 模板和一种全新的调用 render 的方式。

### 24.1 Prototype

Prototype，由 Sam Stephenson 编写的开源 JavaScript 框架，主要用于简化 JavaScript 中的两个任务：

- 使用 XMLHttpRequest（及其朋友）进行 Ajax 调用
- 与页面 DOM 交互

Ajax 是在浏览器背后进行操作。浏览器只是受训的猴子：发出请求，重新加载页面；提交表单，重新加载页面。如果你

```
<% for user in @users %>
<tr>
<td><%=h user.username %></td>
<td><%=h user.favorite_language %></td>
<td><%= link_to 'Show', :action => 'show', :id => user %></td>
<td><%= link_to 'Edit', :action => 'edit', :id => user %></td>
<td><%= link_to 'Destroy', { :action => 'destroy', :id => user },
:confirm => 'Are you sure?', :method => :post %></td>
</tr>
<% end %>
</table>

<%= link_to 'Previous page',
{ :page => @users.previous_page } if @users.previous_page %>
<%= link_to 'Next page',
{ :page => @users.next_page } if @users.next_page %>

<br />

<%= link_to 'New user', :action => 'new' %>
```

我们希望允许用户通过在文本字段中输入来过滤当前列表。应用程序应监视字段的变化，将字段的值提交到服务器，并更新列表以仅显示与当前过滤条件匹配的程序员。

与非 Ajax 页面一样，第一步是添加一个表单来收集用户的输入。然而，与标准表单不同，我们将添加一个所谓的 no-op 表单；这是一个本身无法提交到服务器的表单。旧的做法是创建一个 action 属性设置为 # 的表单。这可以防止请求发布到服务器，但它有一个不幸的副作用，即在地址栏中通过在 URL 末尾添加 # 字符来破坏 URL。现代的方法是将 action 设置为 javascript:void(0)：

```
<% form_tag('javascript:void(0)') do %>
```

其次，我们需要用一个命名元素包装渲染的 partial，以便我们可以轻松地用更新后的数据替换它。在我们的例子中，我们添加一个简单的 <div> 标签，id='ajaxWrapper'，以便为新数据提供一个位置：

```
<div id='ajaxWrapper'>
<%= render :partial=>'search' %>
</div>
```

如果返回的数据很复杂，你也可以选择注册一个回调函数来按你希望的方式处理数据。在我们的例子中，服务器将返回一个包含匹配过滤条件的用户的表格，我们只想将该数据显示在名为 ajaxWrapper 的元素内部。

在第 4 行和第 5 行，我们克服了 Ajax 的主要问题之一。用户可能很敏感。如果他们点击链接或提交表单，或者其他什么，唯一阻止他们无意识地疯狂点击链接或按钮的东西就是浏览器窗口东北角的喷火蜥蜴或旋转地球仪。这告诉用户正在发生有用的事情，请等待其完成。这是在每个浏览器中内置的功能，用户期望这种对否则透明过程的通知。

使用 XHR 时，你必须提供自己的进度指示器。before 选项在向服务器发送请求之前调用一个 JavaScript 函数。在这种情况下，我们使用 Prototype 的 Element.show 来显示一个图形，该图形已在初始化时加载到页面上（但其 style 属性设置为 display:none）。complete 回调同样在响应完全接收后触发。在这种情况下，我们再次使用 Element.hide 隐藏进度指示器。还有其他潜在的回调函数钩子，我们将在第 24.1 节 Callbacks，第 572 页中讨论。（这个 spinner 在哪里？我们一会儿就会看到。）

最后，在第 6 行和第 7 行，我们定义 Ajax 调用将针对的服务器端点以及要发送给它的数据。在第 6 行，我们指定 url 参数并告诉它调用当前控制器的 search action。发送到 url 的选项与 url_for helper 方法相同。

在第 7 行，我们使用 with 参数提供了将发送到服务器的数据。此参数的值是一个包含一个或多个名称/值对的字符串。仔细查看提供的字符串文字：

```
"search=' + encodeURIComponent(value)"
```

该字符串是一段可执行的 JavaScript 代码，将在目标字段的值发生变化时运行。encodeURIComponent 是一个 JavaScript 方法，它接受一个值并用其 UTF-8 对应字符转义某些字符，以使其成为有效的 URL 组件。在这种情况下，value 将是目标字段的当前值，结果是一个名称/值对，其中名称为 search，值为目标字段值的 UTF-8 编码值。

还记得我们用作进度指示器的 spinner 吗？我们还没有编写显示它的代码。通常你会直接将其放在包含引用它的字段的页面上。事实证明，在我们的示例代码中，我们会在各处使用它，所以与其在每个页面上都包含它，我们将改为将其一次添加到布局中。

