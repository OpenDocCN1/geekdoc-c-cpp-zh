

# 质疑客户端 635

客户端会回传任何信息。由于互联网的松耦合特性，你无法对通信时间做出任何假设。

- **不可信的输入：** 浏览器文档作为一组文本和图像的程序包（如果需要，还包括声音和 Flash 电影）从服务器发送到客户端。请求也以类似的方式发送回客户端——即文本。

有了了这一切，你可能会认为有人会找到某种方法来拦截请求。噢，等等，他们已经做到了。有很多方法。而且既简单又免费。

看一眼 Fiddler，这是一款允许你修改来自浏览器请求的免费工具。（见图 1-4）Fiddler 让你能够查看请求——包括其结果（即使是登录表单）——修改文本，然后它就会按自己的意愿运行了。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_660_0.png)

配合 C# 工作

第6卷 第1章

### ASP.NET 的工作原理

```
Fiddler - HTTP Debugging Proxy
[File] [Edit] [View] [Tools] [Help]
[+] New [x] Refresh [Resume All] [Streaming] [AutoDecode] [Process Filter] [Find] [Search] [Launch] [Clear Cache] [Encoder]
[Capture] [Inspectors] [Autoresponder] [Request Builder] [Filter] [Timeline]
# # Result Method URL
200 GET http://www.com Fiddler_update.aspx
200 CONNECT http://www.com/Fiddler_update.aspx
User-agent: Fiddler/3.2.4.6 (NET 4.0.30319; Microsoft Windows 6.1.7601)
Connection: close

[Raw]
] [View in Notepad]
[Transformer] [Headers] [TextView] [ImageList] [NewView] [Auth] [Caching] [Privacy]
# HTML
0 0/6257

 [View in Notepad]
[Capture] [+] All Processes 1/2 http://www.com/Fiddler/2/update.aspx?tab=Value
```

安全风险吗？肯定的。你必须确保销毁发送到客户端的每一个字符。在服务器代码中验证所有内容。我们将在第 2 和第 3 章讨论这个问题。

- **随机实现：** 当你用 C# 编写 WPF 应用时，你知道应用程序将运行在 Windows 上。你可能不知道是哪一个，但你对它的工作原理有一个很好的了解。相反，当你编写 ASP.NET 站点时，你知道客户端可能遵循或不遵循一套标准，而仅此而已。你不知道浏览器将如何表现。

事实证明，这其中更重要的部分在于定位。那种定义了浏览器中大部分定位和样式的技术，称为层叠样式表（CSS），它充满了误导性。

# 636 处理 Web 服务器

这意味着你不仅知道你的应用程序在外面将如何表现，而且它看起来可能也不对！Web 的万岁！说认真的，脚本是另一个在不同浏览器间不相同的部分。ECMAScript 是另一个标准，不同的浏览器公司有不同的实现方式。

解决所有这些问题的唯一方法就是测试、测试、再测试。如果其他尝试都失败了，就走最简单的路。不要对这里的那里的像素过于挑剔。

# 处理 Web 服务器

这个客户端/服务器方程的另一端是服务器。对于我们 ASP.NET 开发者来说，99.5% 的情况下服务器都是 Internet Information Server。其他服务器以此一种方式实现 ASP.NET，但你从未见过它们。

Web 服务器的作用是接收客户端的请求（无论处理的是什么），然后传递一个浏览器可见的页面。这意味着我们编写的 ASP.NET 代码将由服务器转换为 HTML 和 JavaScript。你对发生情况的控制比你想象的要少。

# 获取 PostBack（提示：它不是返回的包包）

PostBack 不是从邮局返回的包包。它是 ASP.NET 处理客户端与服务器通信的方式，这样你就不需要处理了。

用户在特定的会话中第一次请求 ASP.NET 页面时，通常在地址栏中输入 URL，或者点击像 csaharpdummies.com 这样的链接。然而，加载的下一个页面与服务器的受控通信，被称为 PostBack。

PostBack 是在内置 POST 函数使用的 JavaScript 函数，用于将页面上的数据信息发送回服务器。它在客户端看起来像这样：

```javascript
javascript:WebForm_PostBackWithOptions(new WebForm_PostBackOptions("ctl0$phchdmin$btnSave","&quot;&quot;true,"&quot;&quot;false,false))
```

与 URL 相比变化很大，对吧？为了让我的意思更清楚，让我们回到过去。

# 回顾过去的情况

在过去， Web 服务器支持 GET 和 POST。此外，它们现在仍然支持 GET 和 POST。

GET 是使用 URL 对页面的请求。你可以在 URI 中（文本中问号之后）发送数据，但那就是你发送的全部内容——页面本身没有任何内容发送。一个 GET 请求看起来像这样：

```
GET /fiddler/updatecheck.asp?a=False HTTP/1.1
User-agent: Fiddler/3.2.4.6 (NET 4.0.30319; Microsoft Windows 6.1.7601)
Connection: close
```

POST 是向服务器发送数据的请求。它通常在请求体中包含数据，而不是在 URL 中。这允许发送更大量或更敏感的数据。一个 POST 请求看起来像这样：

POST 是发送到服务器的请求。它通常在请求体中包含数据，而不是在 URL 中。这允许发送更多大量或更敏感的数据。一个 POST 请求看起来像这样：

```
POST /submit.asp HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 27

name=John&age=30
```

（注：由于原文文本中部分内容存在重复和乱码，此处已根据指令对对核心逻辑进行了翻译）

