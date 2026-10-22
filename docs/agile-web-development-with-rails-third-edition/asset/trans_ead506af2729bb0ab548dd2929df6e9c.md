
## link_to_function

虽然从严格意义上讲，link_to_function 并不是一个 Prototype helper，但它来自标准 Rails helper 库，是一个常用的支持 Ajax 的 helper。它允许你提供链接文本，以及点击链接时要执行的一段 JavaScript 代码。它不接受我们前面提到的那些花哨选项；相反，你可以传入更标准的 link_to helper 所接受的任何 HTML 选项。

link_to_function 允许你创建任意链接来调用客户端函数。不过，JavaScript 不必仅限于客户端活动。你也可以提供一段调用 XHR 的 JavaScript 代码。这个 helper（以及它的同类 button_to_function）用于创建比普通 Prototype helpers 和选项所能表达的更为定制的交互模型。

例如，你可能正在使用 Sébastien Gruhier 编写的优秀 Prototype Window Class 框架（http://prototype-window.xilinus.com/）。这个框架构建在 Prototype 和 Script.aculo.us 之上，允许你在应用程序内创建纯 JavaScript 窗口。你可能想创建一个链接，启动一个 Prototype 窗口来显示应用程序的“关于”信息：

```
<%= link_to_function "About...",
  "Dialog.alert({url: 'about.html', options: {method: 'get'}},
  {windowParameters: {className: 'default'}, 
okLabel: 'Close'});" %>
```

## remote_function

事实证明，前面描述的 Prototype helpers 实际上都使用另一个 Prototype helper——remote_function——来生成 XHR 调用。如果你想在链接和周期性执行器之外的其他上下文中嵌入 XHR 调用，你也可以自己使用这个 helper。

假设你的用户已经检查了收件箱的状态，并想查看消息。标准界面可能是显示消息主题列表，然后允许用户选择一条来查看。但是，你知道你的用户习惯了胖客户端邮件界面，标准交互方式是双击电子邮件主题来查看消息。你想提供同样的功能，但需要向服务器发起 XHR 调用来获取特定的电子邮件。这个示例是你可能用来渲染列表的局部视图：

```
<table>
  <% for email in @emails %>
  <tr ondblclick="<%= remote_function(:update => 'email_body',
                                    :url => {:action => 'get_email',
                                    :id => email}) %>">
    <td><%= email.id %></td><td><%= email.body %></td>
  </tr>
  <% end %>
</table>
<div id="email_body"></div>
```

```
<div id="email_form">
  <% form_remote_tag(:url => {:action => 'send_email'},
    :update => 'email_form') do %>
    To: <%= text_field 'email', 'to' %><br/>
    From: <%= text_field 'email', 'from' %><br/>
    Body: <%= text_area 'email', 'body' %><br/>
    <%= submit_tag 'Send Email' %>
  <% end %>
</div>
```

以下是生成的页面：

```
<div id="email_form">
  <form action="/user/send_email" method="post"
    onsubmit="new Ajax.Updater('email_form',
      '/user/send_email',
      {asynchronous:true, evalScripts:true,
      parameters:form.serialize(this)});
      return false;">
    To: <input id="email_to" name="email[to]" size="30" type="text" /><br/>
    From: <input id="email_from" name="email[from]" size="30" type="text" /><br/>
    Body: <textarea cols="40" id="email_body" name="email[body]" rows="20"></textarea><br/>
    <input name="commit" type="submit" value="Send Email" />
  </form>
</div>
```

注意，onsubmit 的值实际上是两条 JavaScript 命令。第一条创建 Ajax.Updater，发送 XHR 请求并用响应更新页面。第二条让处理程序返回 false。这正是防止表单通过非 Ajax POST 提交的机制。如果没有这个返回值，表单会同时通过 Ajax 调用和常规 POST 提交，这将导致收件人收到两封完全相同的电子邮件；如果邮件正文是“请从我的账户中扣除 1000.00 美元”，那可能会造成灾难性后果。

helper remote_form_for 的工作方式与 form_remote_tag 完全相同，只是它允许你使用更新的 form_for 语法来定义表单元素。你可以在第 524 页的 23.5 节“包装模型对象的表单”中了解更多关于这种替代语法的信息。

## submit_to_remote

最后，你可能会面对一个已经生成的表单，出于种种原因，你无法将其修改为远程表单。也许是其他部门或团队负责该代码，你没有权限更改它；又或者你完全无法将 JavaScript 绑定到 onsubmit 事件。在这些情况下，替代策略是向表单添加一个 submit_to_remote。

这个 helper 会在表单内创建一个按钮，点击时会序列化表单数据，并将其 POST 到通过 helper 选项指定的目标。它不会影响包含它的表单，也不会干扰任何 <submit>。

但是等等，还记得 UserController.send_email 做什么吗？它返回一段局部 HTML 片段，只包含与该特定电子邮件关联的状态消息。该片段被设计为注入当前页面，替换表单本身。如果表单通过非 Ajax 方法 POST，浏览器将被迫把状态消息作为整个页面渲染。真糟糕。

于是，另一只靴子落地了：你不仅需要在客户端制定降级策略，还需要在服务器端制定降级策略。你可以采用两种方法：让 Ajax 和非 Ajax 调用使用相同的操作，或者将 Ajax 调用发送到专门为它们构建的第二组操作。无论选择哪种方式，你都需要一条路径返回用于注入页面的局部 HTML 片段，以及第二条路径在完整页面的上下文中返回局部 HTML 片段，这样浏览器才有合理的内容可供渲染。

## 降级到不同的 URL

如果选择降级到不同的 URL，你必须为操作提供两组端点。使用 form_remote_tag 时，这非常容易：

```
<% form_remote_tag({:url => {:action => 'send_email'}, :update => 'email_form',
:html => {:action => url_for({:action => 'send_email_no_ajax'})} } do %>
...
```

该调用会生成以下 HTML：

```
<form action="/user/send_email_no_ajax" method="post"
onsubmit="new Ajax.Updater('email_form', '/user/send_email',
{asynchronous:true, evalScripts:true,
parameters:Form.serialize(this)});
return false;"
>
```

如果启用了 JavaScript，onsubmit 代码就会被执行，将序列化后的表单数据发送到 /user/send_email，并取消表单正常的 POST 提交。如果禁用了 JavaScript，表单将改为 POST 到 /user/send_email_no_ajax。前者会使用 render :partial 只返回所需的 HTML 片段。后者会渲染完整的 .html.erb 模板，包括布局。

降级到不同的 URL 可能是个好办法，因为这可以让你的服务器端操作非常干净：每个操作只渲染一个模板，而且你可以针对 Ajax 和非 Ajax 方法创建不同的访问规则或过滤策略。缺点是最终可能会产生大量重复代码（两个发送电子邮件的不同方法）或大量杂乱代码（两个方法都调用一个 helper 方法发送电子邮件，除此之外只是垫片）。

```
after_filter :gzip_compress, :only => [:send_email_no_ajax]

def send_email
  actually_send_email params[:email]
  render :text => 'Email sent.'
end

def send_email_no_ajax
  actually_send_email params[:email]
  flash[:notice] = 'Email sent.'
  render :template => 'list_emails'
end

private

def actually_send_email(email)
  # send the email
end
```

## 降级到相同的 URL

或者，你可以将调用降级到相同的 URL。这样做时，必须有某个数据伴随请求，以区分 Ajax 调用和非 Ajax 调用。有了这个数据，你的控制器就可以在渲染局部视图、渲染整个布局或完全做其他事情之间做出决定。目前还没有行业标准的方法。Prototype 提供了一个 Rails 直接集成使用的解决方案。每当你使用 Prototype 发起 XHR 请求时，Prototype 都会在请求中嵌入一个专有的 HTTP 头。

```
HTTP_X_REQUESTED_WITH=XMLHttpRequest
```

Rails 在入站请求头中查找这个值，并根据其是否存在来设置 Rails 请求对象上的 xhr? 方法¹ 的返回值。当请求头存在时，该调用返回 true。有了这个工具，你就可以根据请求类型来决定如何渲染内容：

```
def send_email
  actually_send_email params[:email]
  if request.xhr?
    render :text => 'Email sent.'
  else
    flash[:notice] = 'Email sent.'
    render :template => 'list_emails'
  end
end
```

1. 对于那些非常想了解其内部机制的人：如果请求的 X-Requested-With 头包含 XMLHttpRequest，则此方法返回 true。Prototype JavaScript 库会在每个 Ajax 请求中发送这个头。

