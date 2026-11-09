
用来命名许多不同的事物：文件、程序、人员、进程，或者几乎任何你能想到的东西。HTTP 中的每个请求要么请求从资源检索数据，要么向资源发送数据。

客户端发出的每个 HTTP 请求都会在服务器上调用一个*方法*。（不要让术语把你弄糊涂：尽管它们把这些称为“方法”，但 HTTP 实际上与面向对象毫无关系。）HTTP 中有四种基本方法（外加大约十几种扩展方法，我们不会讨论它们，因为 Web 应用不需要）：

- **GET** 要求服务器从资源中检索某些信息并将其发送给客户端。
- **HEAD** 要求服务器告知有关资源的信息。它基本上类似 GET 请求，只不过响应只包含元数据。你可以使用 HEAD 请求来做诸如“这个资源有多大？”之类的事情，而无需下载整个资源。一般来说，大多数 Web 应用不使用 HEAD 方法，但它偶尔很有用。
- **PUT** 将数据存储到资源中。客户端将信息发送给服务器，以便存储到目标资源中，服务器响应只说明数据是否成功存储。
- **POST** 将数据发送到服务器上的程序。POST 请求有些奇怪。PUT 和 POST 之间没有太多区别。这种区分实际上可以追溯到万维网的早期，当时人们在私人的单台机器上运行 Web 服务器。在早期 Web 服务器实现中，所有 GET 和 PUT 请求都被解释为获取或存储文件的请求。因此，要在 Web 服务器上运行程序，你需要一种不同的 HTTP 协议请求，它专门要求你运行程序。在现代系统中，我们使用 PUT 和 POST 几乎不加区分。

你使用 Web 浏览器生成的每个 HTTP 请求，以及你的 App Engine 服务将处理的每个 HTTP 请求，都包含三个部分：

- 请求行，由该请求的 HTTP 方法、随后是资源的 URL、再随后是协议版本说明组成。在你使用浏览器发出的大多数请求中，方法是 GET，版本说明通常是 HTTP/1.1。
- 一系列*头部*行，包含关于该请求的元数据（例如我们在第 2.3 节*使用 App 开始 Python 编程*的欢迎应用程序中使用的 Content-Type 说明）

### HTTP 状态码

HTTP 标准有一份很长的服务器结果消息状态码列表。以下是你最常遇到的几种：

- **200 OK（成功）** 请求已成功完成。消息正文将包含成功请求的结果。
- **301 永久移动（Moved Permanently）** 所请求的资源已被永久移动，针对该资源的本次及所有未来请求都应发送到新位置。
- **303 参见其他（See Other）** 对于此请求，可以通过对不同 URL 执行 GET 来找到结果。该 URL 可以在消息的 Location 头部中找到。这通常用于 PUT 请求的结果：在 PUT 成功处理后，服务器告诉客户端到哪里查看操作结果。
- **401 未授权（Unauthorized）** 请求是有效的，但用户未提供任何身份验证数据来表明其应被允许查看该资源。用户可以使用其他请求获取身份验证代码，然后重试该请求。
- **403 禁止访问（Forbidden）** 请求是有效的，但不允许用户访问指定的资源。这与 401 类似，但表示用户已经过身份验证但仍不能访问该资源，或者即使用户已经过身份验证，也不允许该用户访问它。
- **404 未找到（Not Found）** 在指定位置未找到资源。
- **500 内部服务器错误（Internal Server Error）** 服务器在处理请求期间发生任何错误最终都会生成 500 错误。特别是，对于你实现的 App Engine 服务，当你的请求处理程序崩溃和/或抛出异常时，客户端浏览器将收到 500。
- **501 未实现（Not Implemented）** 请求希望执行服务器不支持的操作。如果你做了诸如在 POST 请求中拼错 URL 之类的事情，最常看到这个错误。

你还希望能够发送消息，因此你需要浏览器能够作为一个活跃实体与聊天室通信，并告诉聊天室应用程序你有话要说。同样，聊天室就是资源，但这一次你想与它对话。这要么是 PUT，要么是 POST。我们本质上通过问一个问题来决定使用 PUT 还是 POST：你是想替换资源的内容，还是想与资源对话？向聊天室发布消息显然是后者。我们不想替换聊天室的内容；我们想与它对话，并告诉它有一条新消息要添加到对话中。所以发送新消息绝对是 POST。

这就为我们提供了应用所需的框架。我们将有一个资源，即聊天室。用户可以通过 GET 该资源来查看聊天的当前状态。我们还需要另一个资源，即一个活跃进程；当用户发送要添加到聊天中的新消息时，他们会向该资源发送 POST 请求。

现在我们需要稍微考虑一下 UI 问题。用户将如何能够向我们的应用 POST 数据？我们需要提供一种方式。最简单的方法是在用户请求查看聊天室时发送的页面中创建一个表单。因此，聊天页面顶部会有一个标题，然后会有房间内内容的聊天记录，最后在底部会有一个输入表单，用于接收用户名和用户想要发布的消息。

为了在 App Engine 中实现这一点，我们需要构建一个 RequestHandler，为聊天室内容实现 GET，然后构建另一个 RequestHandler，接收 POST 并将内容添加到聊天中。

聊天室主页几乎与我们在第 2 章*入门*第 20 页使用的代码相同。主要区别在于我们需要向其中添加一些动态内容；也就是说，我们需要为已发布的消息生成文本。因此，我们不能只使用带引号的 HTML；我们需要生成一些 HTML。作为第一次尝试，我们将创建一个包含消息列表的全局变量。当我们渲染页面时，将遍历该消息列表并将它们添加到页面中。

[下载 chatwo/chatwo.py](#)

```python
class ChatMessage(object):
    def __init__(self, user, msg):
        self.user = user
        self.message = msg
        self.time = datetime.datetime.now()

    def __str__(self):
        return "%s %s: %s" % (self.user, self.time, self.message)

Messages = []

class ChatRoomPage(webapp.RequestHandler):
    def get(self):
        self.response.headers["Content-Type"] = "text/html"
        self.response.out.write("""
            <html>
                <head>
                    <title>MarkCC's AppEngine Chat Room</title>
                </head>
                <body>
                    <h1>Welcome to MarkCC's AppEngine Chat Room</h1>
                    <p>(Current time is %s)</p>
                    """ % (datetime.datetime.now())
        # Output the set of chat messages
        global Messages
        for msg in Messages:
            self.response.out.write("<p>%s</p>" % msg)
        self.response.out.write("""
                    <form action="" method="post">
                    <div><b>Name:</b>
                    <textarea name="name" rows="1" cols="20"></textarea></div>
                    <p><b>Message:</b></p>
                    <div><textarea name="message" rows="5" cols="60"></textarea></div>
                    <div><input type="submit" value="Send ChatMessage"></input></div>
                    </form>
                </body>
            </html>
        """)
```

处理 POST 是一个全新的步骤，但 webapp 框架使它非常容易做到。在 GET 请求的处理程序中，我们实现 RequestHandler 的一个子类，该子类有一个 get 方法。对于 POST 请求，我们遵循相同的模式：我们实现 RequestHandler 的一个方法，在这里就是 post 方法。RequestHandler 超类确保当调用 post 时，对象的字段包含我们可能想从请求中查看的所有内容。要从产生 POST 的表单字段中获取数据，我们只需使用表单中指定的标签，在请求上调用 get 方法。在我们的代码中，我们将从 POST 请求中获取用户名和消息，并使用它们创建一个消息对象，并将其添加到全局消息列表。
