
## 第 25 章 JQUERY

![](img/67a6707ff505c052edb96c0128fb3096_1027_0.png)

图 25-13

### JQUERY

到目前为止，你“只是”在使用 jQuery 的 JavaScript 特性，但你仍然需要实际代码编写行为和用户界面。然而，有一个名为 jQuery UI 的兄弟项目，其主页位于 `http://jquery.com/`。它将自己描述为“一组精选的用户界面交互、效果、部件和主题”。事实上，jQuery UI 的功能并不庞大，但质量非常高。可以将 jQuery UI 之于 jQuery 想象成 ASP.NET Web Controls 之于 ASP.NET。后者是框架，而前者在该框架的基础上构建了 UI 控件。本节将简要演示其中一个部件，以展示使用该库通用方法。

当你查看 jQuery UI 主页的右上角（参见图 25-14）时，你会发现下载完整的 jQuery UI 包（我们通常推荐“稳定”版本），或者点击“自定义下载”（Custom Download）并只选择你需要的组件（图 25-15）。为了简单起见，本示例使用了完整包。你也可以使用包管理器安装 jQuery UI。列表 25-20 安装了完整包。

### 列表 25-20：使用 NuGet 安装 jQuery UI

```
Install-Package jQuery.UI.Combined
```

> **警告** jQuery UI NuGet 包也会安装 jQuery。在新的 jQuery 发布后不久，jQuery UI 包可能会引用过时的 jQuery 版本，导致其安装可能失败。在这种情况下，我们建议进行手动安装。

### jQuery UI | 979

![](img/67a6707ff505c052edb96c0128fb3096_1028_0.png)

图 25-14

![](img/67a6707ff505c052edb96c0128fb3096_1028_1.png)

图 25-15

关于你如何安装 jQuery，本节稍后使用的某些路径可能会导致执行困难，因此请务必将代码适配到你的本地系统。我们假设 jQuery 和 jQuery UI 文件位于 `Scripts` 文件夹中，而 jQuery UI 分发的 css 文件夹置于网站的 `Content` 文件夹中。

使用 jQuery 非常简单，因为部件完全集成在 jQuery API 中。本质上，你首先加载 jQuery 库，然后是 jQuery UI 库，以及随包附的 jQuery CSS 文件。

列表 25-21 通过使用 jQuery UI 的 datepicker 控件演示了这一点。要做到这一点，你在页面上放置一个简单的文本框。然后，你使用 `$()` 选择此文本框。返回的 jQuery 对象支持 `datepicker()` 方法，你对其执行该方法。如图 25-16 所示，一旦你点击文本框，

### 列表 25-21：使用 jQuery UI datepicker

```xml
<@Page Language="C#" %>
```

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <link href="/Content/css/smoothness/jquery-ui-1.10.0.custom.css" rel="stylesheet" />
  <script type="text/javascript" src="Scripts/jquery.js"></script>
  <script type="text/javascript" src="Scripts/jquery-ui-1.10.0.custom.js"></script>
  <script type="text/javascript">
    $(function () {
      $(".dp").datepicker();
    });
  </script>
</head>
<body>
  <form id="" runat="server">
    <div>
      <input type="text" class="dp" />
    </div>
  </form>
</body>
</html>
```

如前所述，jQuery UI 试图模拟 ASP.NET Web Controls。有一种方法可以结合这两种技术。jQuery UI 项目已为每个 jQuery UI 元素创建了 Web 控件。该项目主页为 `http://jqueryui.com/`（图 25-17），通过 NuGet 完成安装（参见列表 25-22）。

![](img/67a6707ff505c052edb96c0128fb3096_1029_0.png)

图 25-16

![](img/67a6707ff505c052edb96c0128fb3096_1029_1.png)

图 25-17

### 列表 25-22：安装 Juice UI

```
Install-Package JuiceUI
```

之后，将列表 25-21 移植到 Juice UI 是非常容易：`<Juice:DatePicker>` 控件代表 datepicker 部件。与 Ajax Toolkit 的 API（参见第 24 章）类似，`TargetControlID` 属性用于定义接收 datepicker 的文本框。列表 25-23 显示了（简短）代码。

### 列表 25-23：结合 Juice UI 使用 jQuery UI datepicker

```xml
<Juice:DatePicker TargetControlID="txtDate" runat="server" />
<asp:TextBox ID="txtDate" runat="server" />
```

### 总结

本章结束。

## 第 26 章 实时通信

应用程序可以包含一个隐藏的 `iframe` 元素。每当服务器发送新消息时，消息会以分块的形式作为 `iframe` 元素发送。随着事件的发生，`iframe` 会被包含 JavaScript 的 `script` 标签所填充，这些标签需要在浏览器中执行。由于所有浏览器都按顺序处理页面，每个 `script` 标签在接收时就会被处理。

### 长轮询的 Ajax

长轮询（Long polling）是一种客户端通过轮询服务器来检查是否有服务器想要发送的新数据的技术。浏览器向服务器发送 Ajax 风格的请求，响应保持开启，直到服务器在响应中向客户端发送数据。客户端一收到响应，就会立即向服务器发送另一个请求，以便保持连接开启。这样，当服务器上发生事件时，服务器就可以立即发送新数据。

### 轮询

轮询（Polling）是客户端向服务器发送请求而服务器无论是否有数据都会立即响应的方法。客户端等待一段时间（几秒钟）然后向服务器发送另一个请求。如果服务器有新数据，则会发送；否则，它会向客户端返回一个空响应。图 26-2 显示了轮询的工作原理。

![](img/67a6707ff505c052edb96c0128fb3096_1034_0.png)

图 26-2

### 服务器发送事件

服务器发送事件（Server-sent events, SSE）是一种用于从服务器向客户端发送推送通知的技术。通知以 DOM 事件的形式发送，客户端可以通过名为 `EventSource` 的 JavaScript API 来处理这些事件。当你不需要双向数据传输（如聊天应用程序所需要的）时，SSE 是很有用的，因为服务器只需要发送数据。例如，如果你正在构建一个股票报价器应用程序，SSE 是一个很好的选择。图 26-3 显示了服务器发送事件的简单工作流。

![](img/67a6707ff505c052edb96c0128fb3096_1034_1.png)

图 26-3

目前存在许多这些方法的实现，开发者可以使用它们来构建实时 Web 应用程序。下一节将介绍这些方法的一些缺点，其中许多缺点正是开发 WebSockets 协议的初衷。

### 现有方法的缺点

上述所有推送技术都依赖于维持客户端和服务器之间的长连接，以便服务器可以将数据推送到客户端。

Comet 流传输（Comet streaming）的实现相当简单，但在不同浏览器之间很难运行。并不是所有浏览器都支持所有的流传输方法，因此开发者需要实现复杂的流传输以支持所有浏览器，并根据浏览器进行切换。由于数据是通过 HTML 标签传输的，无法实现可靠的错误处理或跟踪客户端与数据之间的连接状态。

带 Ajax 的长轮询在可靠的错误处理和连接管理方面比流传输好一点，但存在在服务器上一直保持连接直到有数据要发送的开销。这种方法的服务器端实现变得困难，因为请求会一直挂起直到有响应要发送。这时，服务器线程将一直被占用直到数据发送。

传统的轮询使得客户端和服务器的实现非常简单。然而，客户端每次向服务器发送请求时，都有创建 HTTP 请求和发送空响应的额外开销。如果你考虑聊天应用程序中交换的数据类型，消息大小相当小。但是，当你构建 HTTP 请求时，需要设置适当的请求头和关于请求的元数据。这导致了从服务器发送到客户端的每条消息都会产生巨大的开销，从而增加了延迟。

SSE 也不适合支持双向数据传输。在下一节中，你将看到在 HTTP 上执行双向数据传输的新标准。

### HTML5 WEBSOCKETS

上一节简要回顾了用于实现实时通信的一些传统模式以及使用它们的一些优缺点。

除了本章前面提到的问题外，所有现有的实时通信传统方法都依赖于通过 HTTP 传输数据，这意味着由于每个请求都需要 HTTP 请求头，数据传输存在开销。想象一下，如果你正在编写一个聊天应用程序并发送每条消息（通常很小，只有几个字节），因为你的消息是通过 HTTP 发送的，所以增加了发送 HTTP 请求头的额外开销。这增加了传输消息的负载。

此外还有开启底层 TCP 连接的额外开销。服务器将使用一个连接发送消息，并为来自不同客户端的每个入站消息使用一个连接。

#### 什么是 WebSockets？

WebSockets 是一种规范，允许客户端和服务器之间进行双向通信。通信通道通过单个 TCP 连接实现。WebSockets 在浏览器和 Web 服务器中实现。WebSockets 仅使用 HTTP 升级客户端和服务器之间的连接，以便遵循 WebSockets 协议交换数据。该协议通过为服务器向客户端发送数据提供标准化的方式，使得实时交互成为可能。

#### HTML5 WebSockets

WebSockets 的关键实现之一是所有通信都通过端口 80 或 443 完成的。这特别重要，因为有许多环境会拦截非 80 端口的非标准 HTTP 连接。由于 WebSocket 是这种方式实现的，该技术可以在现有环境中运行，而不会遇到某些 HTTP 连接可能会遇到的问题。

#### 引入 WebSockets 协议

WebSockets 协议的主要挑战之一是让它在现有环境中工作。这意味着协议必须与现有的代理、路由器和防火墙配合。在这些环境中，端口 80 或 443 为 HTTP/HTTPS 连接开放，并且可以交换任何数据。当客户端想要通过 WebSockets 连接发送数据时，它通过 HTTP 调用服务器进行连接。由于它仍然在使用 HTTP，中间代理或路由器不需要更新即可允许该连接。

该协议从客户端和服务器之间的握手开始，客户端表示它想通过 WebSockets 发送数据。这种握手发生在 HTTP 上，因此任何中间路由器都不会拒绝这种握手。列表 26-1 显示了客户端为了建立 WebSockets 连接需要向服务器发送的头。

##### 列表 26-1：WebSockets 握手

```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbBs2jZQ==
Origin: http://example.com
Sec-WebSocket-Protocol: superchat
Sec-WebSocket-Version: 13
```

这些头中的任何内容与普通的 HTTP 头都没有不同。这种握手是一个正常的 HTTP GET 请求。客户端在 `Host` 头中包含了主机名，以便客户端和服务器可以验证它们双方约定正在使用哪个主机。`Upgrade` 和 `Connection` 头部在 HTTP 中也有指定，并被客户端用于升级正在使用的协议。WebSocket 协议要求包含 `Upgrade` 头部。它表示客户端想要将连接升级到 WebSocket 协议。图 26-5 显示了 HTTP 请求是如何升级为 WebSocket 连接的。

![](img/67a6707ff505c052edb96c0128fb3096_1038_0.png)

图 26-5

`Origin` 头部字段用于防止浏览器中使用带有 WebSocket API 的脚本对 WebSockets 进行未经授权的跨源使用。如果服务器不想接受来自客户端的入站连接，它可以拒绝连接并返回错误代码。

`Sec-WebSocket-Version` 头部告诉服务器客户端支持哪个版本的 WebSocket 协议。如果你使用的是 Windows 8，则应将其设置为 13。如果服务器支持 WebSockets 但不支持此版本的协议，服务器可以请求此项。这非常重要，因为 WebSocket 规范允许不断演进，不同的客户端（如 IE、Chrome、Firefox 等）和服务器支持规范的不同版本。客户端和服务器按照各自的时间升级到规范的最新版本。在理想情况下，所有客户端和服务器都使用最新版本。然而，考虑到不同公司软件实现的差异，可能会出现服务器版本在客户端和服务器之间不一致的情况。此头部确保客户端和服务器可以验证各自支持哪种协议版本，并在不兼容时接受或拒绝 WebSocket 请求。

`Sec-WebSocket-Key` 头部防止来自非 WebSocket 客户端的连接。这可以防止攻击者通过使用 `XMLHttpRequest` 或表单提交发送数据包来欺骗 WebSocket 服务器。此头部告诉服务器已建立合法连接。该值必须是一个随机选择的（理想情况下是加密随机）16 字节数字，在安全领域称为 nonce（随机数），然后进行 base-64 编码作为此头部值。

额外的头部字段用于选择 WebSocket 协议中的子协议。此版本提供的典型选项包括子协议（`Sec-WebSocket-Protocol`），`Sec-WebSocket-Protocol` 请求头部字段可用于指示客户端支持哪些子协议（`Sec-WebSocket-Extensions`）。WebSocket 扩展（层在 WebSocket 协议之上的应用层协议）是可以接受的。服务器从所有接受的协议中选择一个或一个都不选，并在其握手中回显该值，以指示它已选择了该子协议。

一旦客户端发送握手且服务器理解了 WebSockets，服务器就会切换协议到 WebSockets。服务器向客户端发送 HTTP 101 响应，表示连接现在已升级到 WebSocket 协议。列表 26-2 显示了服务器发回客户端的响应头部。

##### 列表 26-2：WebSockets 握手响应

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pLMbITXaq9kYGzzZrRBk+xOo=
Sec-WebSocket-Protocol: chat
```

这些是有效的 HTTP 头部，使其成为正常的 HTTP 响应。客户端也需要验证来自服务器的响应内容。客户端通过使用 `Sec-WebSocket-Accept` 头部来实现这一点。当服务器获取 `Sec-WebSocket-Key` 值时，它不会对其进行解码。它将其与一个著名的 GUID（全局唯一标识符）拼接，并使用 SHA1 对组合进行哈希处理，生成一个经过 base64 编码的值，并通过此头部发回客户端。客户端可以执行相同的操作并验证结果。如果验证成功，客户端就可以接受握手响应并建立 WebSocket 连接。

客户端和服务器现在可以通过它们的 WebSocket 连接发送和接收数据。下一节将探究这种数据传输是如何发生的。

#### WebSockets 数据传输

WebSocket 协议的设计旨在为服务器和客户端之间的双向通信提供高扩展性和低开销。一旦连接升级，通信将在 TCP 上进行。该协议在 TCP 之上使用了数据帧机制，但没有数据包大小等限制。TCP 是基于流的，而 WebSocket 是基于消息的数据传输。这意味着当数据通过 WebSocket 传输时，它是以一系列帧（frames）的形式传输的。该协议只需要几个字节的额外开销，并且由于传输是在 TCP 上进行的，因此它具有 TCP 的可靠性和顺序交付的优点。帧有两种类型——控制帧和数据帧。控制帧用于通信 WebSocket 数据帧被用来传输数据的信息。
