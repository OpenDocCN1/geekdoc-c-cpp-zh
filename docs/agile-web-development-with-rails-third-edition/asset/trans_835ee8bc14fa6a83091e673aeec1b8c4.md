

```
config.action_mailer.perform_deliveries = true | false
```

如果 perform_deliveries 为 true（默认值），邮件将正常投递。如果为 false，投递邮件的请求将被静默忽略。这在测试时可能有助于禁用电子邮件。

```
config.action_mailer.raise_delivery_errors = true | false
```

如果 raise_delivery_errors 为 true（默认值），则在最初发送电子邮件时发生的任何错误都会向你的应用程序抛出一个异常。如果为 false，错误将被忽略。请记住，并非所有电子邮件错误都是立即发生的——一封邮件可能在发送三天后被退回，而你（希望）到那时应用已经继续处理其他事情了。

使用以下设置用于新电子邮件的字符集：

```
config.action_mailer.default_charset = "utf-8"
```

与所有配置更改一样，如果你对环境文件做了任何更改，都需要重新启动你的应用程序。

## 发送邮件

既然我们已经完成了所有配置，让我们编写一些代码来发送电子邮件。

到目前为止，你不应对 Rails 有一个生成邮件器的脚本感到惊讶。可能令人惊讶的是它创建它们的位置。在 Rails 中，邮件器是存储在 app/models 目录中的一个类。它包含一个或多个方法，每个方法对应一个电子邮件模板。为了创建电子邮件的正文，这些方法反过来使用视图（就像控制器操作使用视图来创建 HTML 和 XML 一样）。因此，让我们为我们的商店应用创建一个邮件器。我们将用它来发送两种不同类型的电子邮件：一种是在订单下达时，另一种是在订单发货时。generate mailer 脚本接受邮件器类的名称，以及电子邮件操作方法的名称：

```
depot> ruby script/generate mailer OrderMailer confirm sent
exists  app/models/
exists  app/views/order_mailer
exists  test/unit/
create  test/fixtures/order_mailer
create  app/models/order_mailer.rb
create  test/unit/order_mailer_test.rb
create  app/views/order_mailer/confirm.erb
create  test/fixtures/order_mailer/confirm
create  app/views/order_mailer/sent.erb
create  test/fixtures/order_mailer/sent
```

注意，我们在 app/models 中创建了一个 OrderMailer 类，并在 app/views/order_mailer 中创建了两个模板文件，每种邮件类型一个。（我们还创建了一个

当指定了 headers ‘return-path’ 时，该值将用作“信封发件人”地址。当你希望将投递通知发送到与 from 中不同的地址时，设置此值非常有用。

```
headers "Organization" => "Pragmatic Programmers, LLC"
```

recipients 数组或字符串
一个或多个收件人电子邮件地址。这些可以是简单的地址，如 dave@pragprog.com，也可以是某个标识短语后跟尖括号中的电子邮件地址。

```
recipients [ "andy@pragprog.com", "Dave Thomas <dave@pragprog.com>" ]
```

reply_to 数组或字符串
在回复你的邮件时，这些地址将被列为默认收件人。设置电子邮件的 Reply-To: 头。

sent_on 时间
一个 Time 对象，用于设置电子邮件的 Date: 头。如果未指定，将使用当前日期和时间。

subject 字符串
电子邮件的主题行。

body 接受一个哈希，用于向包含电子邮件的模板传递值。我们很快将了解它是如何工作的。

## 邮件模板

generate 脚本在 app/views/order_mailer 中创建了两个电子邮件模板，分别对应 OrderMailer 类中的每个操作。这些是常规的 .erb 文件。我们将用它们来创建纯文本电子邮件（稍后我们会看到如何创建 HTML 电子邮件）。与我们用来创建应用网页的模板一样，这些文件包含静态文本和动态内容的组合。我们可以自定义 confirm.erb 中的模板；这是用于确认订单的电子邮件：

```
Download e1/mailer/app/views/order_mailer/confirm.erb
```

```
Dear <%= @order.name %>

Thank you for your recent order from The Pragmatic Store.

You ordered the following items:

<%= render(:partial => "/line_item", :collection => @order.line_items) %>

We'll send you a separate e-mail when your order ships.
```

这个模板中有一个小问题。我们必须为 render 提供模板的显式路径（开头的 ./），因为我们不是从真正的控制器调用视图，Rails 无法猜测默认位置。

create_confirm 调用会调用我们的 confirm 实例方法来设置电子邮件的详细信息。我们的模板用于生成正文文本。正文和头信息一起被添加到一个新的电子邮件对象中，create_confirm 会返回该对象。该对象是 TMail::Mail 类的一个实例。² email.encoded 调用返回我们刚刚创建的电子邮件的文本。我们的浏览器将显示类似下面的内容：

```
Date: Thu, 12 Oct 2006 12:17:36 -0500
From: orders@pragprog.com
To: dave@pragprog.com
Subject: Pragmatic Store Order Confirmation
Mime-Version: 1.0
Content-Type: text/plain; charset=utf-8

Dear Dave Thomas

Thank you for your recent order from The Pragmatic Store.

You ordered the following items:

1 x Programming Ruby, 2nd Edition
1 x Pragmatic Project Automation

We'll send you a separate e-mail when your order ships.
```

如果我们想发送电子邮件，而不是仅仅创建一个电子邮件对象，我们可以调用 OrderMailer.deliver_confirm(order)。

## 发送 HTML 格式的电子邮件

创建 HTML 电子邮件的一种方法是创建一个为电子邮件正文生成 HTML 的模板，然后在投递消息之前将 TMail::Mail 对象的内容类型设置为 text/html。

我们将从在 OrderMailer 中实现 sent 方法开始。（实际上，这个方法与最初的 confirm 方法之间有太多共同之处，以至于我们很可能会将两者重构为使用一个共享的辅助方法。）

```
Download e1/mailer/app/models/order_mailer.rb

class OrderMailer < ActionMailer::Base
  def sent(order)
    subject    'Pragmatic Order Shipped'
    recipients order.email
    from       'orders@pragprog.com'
    sent_on    Time.now

    body       :order => order
  end
end
```

2. TMail 是 Minero Aoki 编写的优秀电子邮件库；Rails 附带了一个版本。

接下来，我们将编写 sent.erb 模板：

```
Download e1/mailer/app/views/order_mailer/sent.erb
<h3>Pragmatic Order Shipped</h3>
<p>
This is just to let you know that we've shipped your recent order:
</p>
<table>
<tr><th colspan="2">Qty</th><th>Description</th></tr>
<%= render(:partial => "html_line_item", :collection => @order.line_items) %>
</table>
```

我们将需要一个生成表格行的新局部模板。该模板放在文件 _html_line_item.erb 中：

```
Download e1/mailer/app/views/order_mailer/_html_line_item.erb
<tr>
<td><%= html_line_item.quantity %></td>
<td>&times;</td>
<td><%= html_line_item.product.title %></td>
</tr>
```

最后，我们将使用一个操作方法对其进行测试，该方法渲染电子邮件，将内容类型设置为 text/html，并调用邮件器来投递它：

```
Download e1/mailer/app/controllers/test_controller.rb
class TestController < ApplicationController
  def ship_order
    order = Order.find_by_name("Dave Thomas")
    email = OrderMailer.create_sent(order)
    email.set_content_type("text/html")
    OrderMailer.deliver(email)
    render(:text => "Thank you...")
  end
end
```

生成的电子邮件将类似于下一页的图 25.1。

## 发送多种内容类型

有些人更喜欢接收纯文本格式的电子邮件，而另一些人则喜欢 HTML 电子邮件的外观。Rails 允许你轻松发送包含备用内容格式的电子邮件消息，允许用户（或其电子邮件客户端）决定他们更愿意查看哪种格式。

在上一节中，我们通过生成 HTML 内容然后将内容类型设置为 text/html 来创建 HTML 电子邮件。事实证明，Rails 有一个约定可以自动完成这一切，甚至更多。

![](img/a160fc3a330a0b3b2a764d41d614e688_616_0.png)

## 图 25.1：一封 HTML 格式的电子邮件

我们的 sent 操作的视图文件被称为 sent.erb。这是标准的 Rails 命名约定。但是，对于电子邮件模板，还有更多的命名魔法。如果你像这样命名模板文件：

```
name.content.type.erb
```

那么 Rails 将自动将电子邮件的内容类型设置为文件名中的内容类型。对于之前的示例，我们可以将视图文件名设置为 sent.html.erb，Rails 会自动将其作为 HTML 电子邮件发送。但还有更多。如果你创建多个同名但文件名中嵌入不同内容类型的模板，Rails 将在一封邮件中发送所有模板，并安排内容，以便电子邮件客户端能够区分每个模板。因此，通过创建 sent.text.plain.erb 和 sent.text.html.erb 模板，我们可以让用户选择以文本或 HTML 格式查看电子邮件。

让我们试试这个。我们将设置一个新的操作：

```
Download e1/mailer/app/controllers/test_controller.rb

def survey
  order = Order.find_by_name("Dave Thomas")
  email = OrderMailer.deliver_survey(order)
  render(:text => "E-Mail sent")
end
```

