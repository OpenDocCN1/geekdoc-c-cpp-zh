
1. 修改聊天页面，要求用户登录。
2. 使用已登录的用户对象设置聊天中消息的 user 字段，并从聊天消息输入表单中移除 user 字段。
3. 修改 POST 消息处理程序以使用已登录的用户。

我们已经在上一页的第 5.2 节 *让用户登录* 中了解了如何实现用户登录。将这一功能集成到聊天页面的请求处理程序中，只是同类代码的又一次应用。聊天页面请求处理程序中的另一项更改是从表单中移除 name 字段。更新后的请求处理程序如下所示：

下载 `long-chat/chat.py`

```python
class ChatRoomPage(webapp.RequestHandler):
    def get(self):
        user = users.get_current_user()
        if user is None:
            self.redirect(users.create_login_url(self.request.uri))
        else:
            self.response.headers["Content-Type"] = "text/html"
            self.response.out.write("""
                <html>
                <head>
                    <title>MarkCC’s AppEngine Chat Room</title>
                </head>
                <body>
                    <h1>Welcome to MarkCC’s AppEngine Chat Room</h1>
                    <p>(Current time is %s)</p>
                    """ % (datetime.now()))
            # Output the set of chat messages
            messages = db.GqlQuery("SELECT * FROM ChatMessage ORDER BY timestamp")

            for msg in messages:
                self.response.out.write("<p>%s</p>" % msg)

            self.response.out.write("""
                <form action="/" method="post">
                <p><b>Enter new message from: %s</p>
                <p><b>Message:</b></p>
                <div><textarea name="message" rows="5" cols="60"></textarea></div>
                <div><input type="submit" value="Send Chat Message"/></div>
                </form>
                </body>
                </html>
                """ % user.nickname())
```

登录代码位于 ① 处，完全遵循我们之前描述的模式。如果用户已经登录，聊天应用会为他们渲染聊天内容。如果用户未登录，它会重定向到登录页面，并在用户登录后将其带回聊天页面。

另一项更改位于 ② 处，我们从表单中移除了用户名输入字段，并将其替换为一行提示，该提示使用从当前已登录用户对象中获取的昵称。

修改 POST 处理程序的方法完全相同。我们只需要添加一行 get_current_user 的副本，并在创建 ChatMessage 的调用中使用它，如下所示：

下载 `login-chat/pchat.py`

```python
def post(self):
    user = users.get_current_user()
    if user is None:
        self.redirect(users.create_login_url(self.request.uri))
        return
    msgtext = self.request.get("message")
    if user.nickname() is None or user.nickname() == "":
        nick = "No Nickname"
    else:
        nick = user.nickname()
    msg = ChatMessage(user=nick, message=msgtext)
    msg.put()
    sys.stderr.write("****** Just stored message: %s" % msg)
    # Now that we've added the message to the chat, we'll redirect
    # to the root page,
    self.redirect('/')
```

既然我们已经能够提供登录功能，就可以开始让聊天应用变得更有趣了。我们可以构建多聊天、订阅以及其他功能，例如确定哪些用户已连接、用户之间的直接私信等等。当然，天下没有免费的午餐。当我们开始添加这类功能时，用于渲染用户界面的 HTML 会变得复杂，而且我们需要不断生成相同的样板 HTML 代码。这既费力又容易出错，还非常烦人。在下一章中，我们将了解如何向应用添加订阅和多聊天，以及如何使用一种称为模板的机制，轻松生成 UI 的 HTML，而不会出现错误、不一致或其他麻烦。

## 组织代码：分离 UI 与逻辑

到目前为止我们编写的所有代码中，都是通过编写打印 HTML 的 Python 代码来渲染用户界面。这样做既费力又笨拙，还容易出错。在本章中，你将了解模板，它通过将渲染用户界面的代码与实现应用逻辑的代码分离，来组织 Google App Engine 应用的代码。使用模板时，你不必再用 Python 打印语句渲染 HTML 用户界面代码，而是直接将其编写为带标记的 HTML 形式。你的应用逻辑仍保留在 Python 中，并在需要生成页面时调用模板。

### 6.1 模板入门

回到第 3 章 *第一个真正的云应用*（第 37 页），我们勾勒了一个相当高级的聊天系统。我们设计它来支持在不同聊天室中同时进行的多个聊天。用户可以通过订阅不同的聊天来同时参与多个聊天。

但从那以后，我们一直在构建只有一个聊天的应用。在上一章中，我们处理了完整聊天应用的一个方面：识别已登录用户。我们需要这个功能，既是为了让用户不必每次发言都输入用户名，也是为了跟踪谁参与了哪个聊天。我们能够跟踪用户，但到目前为止，这只是为用户提供便利。我们并没有管理多个聊天；也没有需要跟踪或保护的用户信息。

我们想开始实现一些更有趣的功能。为此，我们将引入几个新视图。正如在前几章中所见，添加新视图可能很痛苦，因为编写生成 HTML 的代码既笨拙又容易出错。

为了让事情既更简单又更易维护，我们将学习使用一种称为*模板*的机制。模板提供了一个灵活、易用的系统，用于创建描述用户界面的 HTML 代码。它通过允许我们将系统的逻辑与外观分离来实现这一点。逻辑我们仍将用 Python 编写。外观我们将用带注释的 HTML 模板文件编写。

模板语言有很多种。Google App Engine webapp 框架包含一种来自开源 Django 项目的模板语言，所以我们将使用它。如果你更喜欢另一种，尽管使用它：只需将所需的 Python 文件放入项目中，它应该就能工作。

### 为什么还要学另一种语言？

像所有 Web 应用一样，云应用通过生成将由浏览器渲染的 HTML 来构建用户界面。这很方便，因为它使得动态创建各种吸引人的界面变得容易。Web 浏览器为创建用户界面提供了一个非常灵活、一致且令人愉悦的平台，你可以通过使用 HTML 来利用浏览器提供的一切。尤其是在即将到来的 HTML5 标准下，你可以使用 HTML 创建漂亮的界面。

问题在于，正确生成 HTML 可能很艰巨，而且很容易出错。HTML 的语法非常冗长，并且使用与大多数编程语言相同的一些引号字符。这意味着你在编写代码时必须非常小心——而且无论你多么小心，仍然很容易出错。

模板有助于解决这个问题。它们让你将代码程序分成两部分：计算和界面。计算部分是你完成工作并生成想要在网页中渲染的数据的地方。在计算部分，你主要是在处理数据——有时你可能会将其中的一部分渲染为 HTML，但大多数情况下，计算部分并不进行渲染。

界面则完全是为了生成 HTML。它接收计算部分产生的数据，并将其渲染为 HTML。在大多数应用中，很大一部分 HTML 是固定的。在我们的聊天应用中，每次页面渲染都必须生成基本的 HTML 结构、页面标题、消息输入表单等等。只有消息列表的内容会变化：其他一切都完全相同。这意味着有大量打印语句除了输出构成页面 HTML 一部分的固定字符串之外什么也不做。HTML 被嵌入在代码中，而这种嵌入充其量是笨拙的。

使用模板时，你用 Python（或你正在使用的任何语言）编写代码的计算部分。如果你需要在计算过程中进行任何 HTML 渲染，则使用嵌入在 Python 中的 HTML 字符串来完成。对于代码的界面部分，你用 HTML 编写，并使用特殊的元语法来嵌入在 HTML 文件中插入动态内容所需的任何计算。

事实上，你可以使用模板编写整个应用。但正如从标准 Python 代码渲染 HTML 既笨拙、痛苦又容易出错一样，尝试在模板内部使用复杂的编程逻辑也同样笨拙、痛苦且容易出错。

### 模板基础：使用模板渲染聊天

使用模板，我们可以做的第一件事是将从数据存储中检索聊天消息的逻辑，与渲染包含这些聊天消息的页面以显示聊天的逻辑分开。为此，我们将把应用的聊天页面编写为模板，然后修改 Python 代码以使用该模板。下面展示了聊天显示页面的一个非常简单的模板版本：

下载 `template-chat/chat-template.html`

```html
<html>
  <head>
    <title>{{ title }}</title>
  </head>
  <body>
    <h1>Welcome to {{ title }} </h1>
    <p> Current time is {% now "F j Y h:i" %}</p>

    {% for m in msg_list %}
      <p> {{ m.user }} ( {{ m.timestamp }} ): {{ m.message|escape }} </p>
    {% endfor %}
    <form action="/talk" method="post">
      <p><b>Message</b></p>
      <div><textarea name="message" rows="5" cols="60"></textarea></div>
      <div><input type="submit" value="Send Message"/></div>
    </form>
  </body>
</html>
```
