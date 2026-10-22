

这段代码假设 before 过滤器已在 `@user` 实例变量中设置了当前用户的信息：

```
def show
  @order = Order.find(params[:id], :conditions => [ "user_id = ?", @user.id])
rescue
  redirect_to :action => "index"
end
```

更好的是，考虑使用新的基于集合的查找方法，它们将结果限制为仅属于该集合的行。例如，如果我们假设 user 模型 has_many :orders，那么 Rails 允许我们将之前的代码写成这样：

```
def show
  id     = params[:id]
  @order = @user.orders.find(id)
rescue
  redirect_to :action => "index"
end
```

此解决方案不仅限于 find 方法。基于表单返回的 id（或 ids）删除或销毁行的操作同样危险。养成使用类似以下方式限制对 delete 和 destroy 的调用的习惯：

```
def destroy
  id     = params[:id]
  @order = @user.orders.find(id).destroy
rescue
  redirect_to :action => "index"
end
```

## 27.4 不要暴露控制器方法

一个 action 只是控制器中的一个公共方法。这意味着如果不小心，你可能会将本意仅在应用程序内部调用的方法暴露为 action。例如，控制器可能包含以下代码：

```
class OrderController < ApplicationController

  # Invoked from a webform
  def accept_order
    process_payment
    mark_as_paid
  end

  def process_payment
    @order = Order.find(params[:id])
    CardProcessor.charge_for(@order)
  end
```

```
def mark_as_paid
  @order = Order.find(params[:id])
  @order.mark_as_paid
  @order.save
end
end
```

好吧，这不是很好的代码，但它说明了一个问题。显然，accept_order 方法 intended 用于处理来自表单的 POST 请求。开发人员决定通过将其两个职责封装在两个独立的控制器方法 process_payment 和 mark_as_paid 中来对其进行拆分。

不幸的是，开发人员将这两个辅助方法保留为 public 可见。这意味着任何人都可以在其浏览器中输入以下内容：

http://unlucky.company/order/mark_as_paid/123

并且订单 123 将神奇地被标记为已付款，绕过了所有信用卡处理。每天都是 Unlucky Company 的免费赠送日。

基本规则很简单：控制器中唯一的公共方法应该是可以从浏览器调用的 action。

此规则也适用于你添加到 application.rb 中的方法。这是所有控制器类的父类，其公共方法也可以作为 action 调用。

## 27.5 跨站脚本攻击 (CSS/XSS)

许多 Web 应用程序使用 session cookie 来跟踪用户的请求。cookie 用于识别请求并将其连接到 session 数据（Rails 中的 session）。通常此 session 数据包含当前登录用户的引用。

跨站脚本是一种“窃取”网站另一位访客的 cookie 的技术，从而可能窃取该人的登录信息。

cookie 协议具有少量内置安全功能；浏览器仅向 cookie 最初创建的域发送 cookie。但这种安全性可以被绕过。获取他人 cookie 的最简单方法是向网站放置一段精心制作的 JavaScript 代码；脚本可以读取访客的 cookie 并将其发送给攻击者（例如，通过将数据作为 URL 参数传输到另一个网站）。

### 典型的攻击

任何显示来自应用程序外部的数据的站点，除非应用程序注意过滤该数据，否则都容易受到 XSS 攻击。有时攻击的路径很复杂且微妙。例如，考虑一个允许用户为

## 27.6 避免 Session Fixation 攻击

如果你知道某人的 session id，那么你就可以创建使用它的 HTTP 请求。当 Rails 收到这些请求时，它认为它们与原始用户相关联，因此会让你做该用户能做的任何事情。

Rails 在很大程度上防止人们猜测他人的 session id，因为它使用安全哈希函数构造这些 id。实际上，它们是非常大的随机数。然而，仍有办法实现几乎相同的效果。

在 session fixation 攻击中，坏人从我们的应用程序获取一个有效的 session id，然后以这样的方式将其传递给第三方，即第三方将使用相同的 session。如果该人使用该 session 登录我们的应用程序，坏人也会登录，因为他也有访问该 session id 的权限。⁴

有几种技术有助于消除 session fixation 攻击。首先，你可能会发现将创建 session 的请求的 IP 地址保存在 session 数据中很有帮助。如果此地址发生变化，你可以取消该 session。这将惩罚在网络间移动笔记本电脑的用户以及在 PPPOE 租约到期时 IP 地址发生变化的家庭用户。

其次，你应该考虑每次有人登录时通过 reset_session 创建一个新 session。这样，合法用户将继续使用应用程序，而坏人将被留下一个孤立的 session id。

## 27.7 文件上传

一些面向社区的网站允许其参与者上传文件供其他参与者下载。除非你小心，否则这些上传的文件可能会被用来攻击你的站点。

例如，想象有人上传一个文件名以 .rhtml 或 .cgi 结尾的文件（或与站点上可执行内容关联的任何其他扩展名）。如果你在下载页面直接链接到这些文件，当选择该文件时，你的 Web 服务器可能会被诱惑执行其内容，而不是简单地下载它。这将允许攻击者在你的服务器上运行任意代码。

解决方案是永远不要允许用户上传随后直接对其他用户可访问的文件。相反，将文件上传到 Web 服务器无法访问的目录（在 Apache 术语中，位于 DocumentRoot 之外）。然后提供一个 Rails action 允许人们查看这些文件。

> 4. Session fixation 攻击在 ACROS Security 的一份文档中有详细描述，可在 http://www.secinft.net/uplarticle/11/session_fixation.pdf 获取。

## 输入验证很难

Johannes Brodwall 在对本章的评论中写道：

当你验证输入时，重要的是要记住以下几点：

- *使用白名单进行验证*：有许多编码点和斜杠的方法可能会逃避你的验证，但会被底层系统解释。例如，../、\、%2e%2e%2f、%2e%2e%5c 和 ..%c0%af（Unicode）可能会使你上升一个目录级别。接受非常小的字符集（从 [a-zA-Z][a-zA-Z0-9_]* 开始）。
- *不要尝试通过替换、剥离等来从奇怪的路径中恢复*：例如，如果你剥离字符串 ../，像 ....// 这样的恶意输入仍然会通过。如果发生任何奇怪的事情，有人正在尝试一些聪明的手段。只需用简短、无信息的消息将其踢出，例如 “检测到入侵尝试。事件已记录。”

我们经常检查 dirname(full_file_name_from_user) 是否与预期目录相同。这样我们就知道文件名是卫生的。

在此 action 中，请确保执行以下操作：

- 验证请求中的名称是一个简单的、有效的文件名，与目录中的现有文件或表中的行匹配。不要接受诸如 ../../../etc/passwd 之类文件名（参见侧边栏 输入验证很难）。你甚至可能想将上传的文件存储在数据库表中，并使用 id 而不是名称来引用它们。
- 当你下载将在浏览器中显示的文件时，请确保转义其中包含的任何 HTML 序列，以消除 XSS 攻击的可能性。如果你允许下载二进制文件，请确保设置适当的 Content-Type HTTP 头，以确保文件不会意外地在浏览器中显示。

从第 469 页开始的描述说明了如何从 Rails 应用程序下载文件，而从第 544 页开始的关于上传文件的部分展示了一个示例，该示例将图像文件上传到数据库表并提供一个 action 来显示它们。

## 27.8 不要明文存储敏感信息

你可能正在编写受外部法规管辖的应用程序（在美国，如果你处理信用卡数据，CISP 规则可能适用，如果你处理医疗数据，HIPAA 可能适用）。这些法规对你处理信息的方式施加了一些严重的限制。即使你

