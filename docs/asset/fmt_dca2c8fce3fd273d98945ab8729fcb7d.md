
```javascript
function getLatestReviewsCallback(result) {

  var listItems = '';

  for (var i = 0; i < result.length; i++) {

    listItems += '<li>' + result[i].Title + '</li>';

  }

  document.getElementById('Reviews').innerHTML = listItems;

}
```

这段代码声明了一个用于存储评论标题的字符串。它遍历 `result` 变量中的评论。虽然 JavaScript 无法预见，但通过使用字符串进行循环，你可以轻松访问集合中的所有项。在 `for` 循环内部，使用 `result[i].Title` 获取评论标题，然后将其封装在 `<li>` 标签中并附加到字符串变量中。最后，该字符串作为名为 `Reviews` 的元素的 `innerHTML` 添加（该元素在 HTML 中可能像这样：`<ul id="Reviews"></ul>`），这样评论标题就会以项目列表的形式出现。

当你输入这些内容时，你会注意到 `result` 对象没有 IntelliSense（智能感知）。由于 VS 并不不知道 `result` 变量的实际类型，因此无法帮助你找到如 `Id` 和 `Title` 之类的属性。

注意，这段代码有点笨拙。使用 `document.getElementById` 和 `innerHTML` 并不是编写此类代码的最佳方式。因此，下一章在讨论 jQuery 时将向你介绍更好的替代方案。不过，目前这足够了，展示了处理从 WCF 服务返回的复杂对象的核心概念。

重要的是，你在 JavaScript 中处理的 `Reviews` 对象与你在服务中使用的并不完全相同。VB.NET 或 C# 代码针对的是服务器端的 .NET Framework，而你的 JavaScript 运行在客户端。为了将对象传递到客户端，WCF 将评论集合序列化为 JavaScript 对象表示法 (JSON) —— 对象的字符串表示形式，可以直接在你的 JavaScript 代码中使用。你将在稍后的练习中看到 JSON 的示例。

Planet Wrox 项目中的 Web 服务将仅用于让浏览器中的客户端页面与服务器通信并交换数据。因此，在这个站点中，服务器和客户端都在同一个 Web 项目中——一个运行在客户端（调用 Web 服务器的 JavaScript）。

# 创建 Web 服务

使用 VS 创建 WCF 服务非常简单。就像所有其他类型一样，VS 都带了服务的模板。只需将服务添加到站点中。然后修改服务代码以符合你的需求。

## 创建 Web 服务

在本练习中，你创建一个简单的 "Hello World" Web 服务。该服务接受你的名称作为输入参数并返回一个个性化的问候。由于该服务的简单性，你可以专注于关注底层概念。

- 1. 在站点根目录下创建一个名为 `services` 的文件夹，将所有服务分组在一个文件夹中。这不是必须的，但有助于组织你的站点。
- 2. 接下来，右单击此文件夹并选择“新建项”。点击“WCF 服务（启用 Ajax）”。由于模板列表可能很长，你可以在对话框右上角的搜索框中搜索 WCF 来快速找到正确的项。
- 3. 点击“添加”将服务添加到站点。
- 4. 打开 `App_Code` 文件夹中的 `NameService` 后代码文件，将 `Do` 方法重命名为 `HelloWorld`，并修改代码使其接受字符串并返回个性化问候。在 VB 中你需要将代码从 `Sub` 改为 `Function` 并使其返回 `String`，在 C# 中则从 `void` 改为字符串方法，因为服务方法返回字符串。

# 第10章 ASP.NET AJAX

确保你点击对应你编程语言的项，并如图 10-6 所示调用 `NameService`。

```vbnet
Public Class NameService

    <OperationContract()>

    Public Function HelloWorld(name As String) As String

        Return String.Format("Hello {0}", name)

    End Function

End Class
```

```csharp
public class NameService
{
    [OperationContract]
    public string HelloWorld(string name)
    {
        return "Hello " + name;
    }
}
```

```c
public string HelloWorld(string name)
{
    return string.Format("Hello {0}", name);
}
```

5. 就这样。你刚刚创建了一个可以从客户端代码中调用的 WCF 服务。如果你尝试直接在浏览器中请求 .svc 文件，你会看到一个类似于图 10-8 的屏幕。

![](img/9e033e3b9560597824f8b22941d6d8bb_396_0.png)

图 10-8

默认情况下，你会看到这个屏幕，这是因为出于安全考虑，WCF 服务不会公开其元数据。这意味着它们不会告诉世界它们是如何运行的以及如何调用它们。如果你想测试你的 WCF 服务，可以按照所示图 10-8 所示的服务页面上的说明来启用发布元数据。一旦启用了元数据，你就可以使用 WCF 测试客户端程序获取更多关于测试服务的信息。不过，我通常不会对简单的 WCF 服务这样做；因为从客户端页面调用该服务同样简单，正如你稍后看到的“尝试执行”（Try Out）。

## 工作原理

WCF 服务本质上是可以通过网络（如互联网或本地网络）调用的方法。对于启用 Ajax 的 WCF 服务，默认使用的消息格式是 JSON。这是一种非常简洁的数据交换方式。例如，你在之前的示例中看到的两个条评论是按照以下 JSON 代码从服务器传输到客户端的：

```json
{"d":[{"_type":"Review#","Id":1,"Title":"21st Century Breakdown\nby Green Day"},{"_type":"Review#","Id":2,"Title":"nSonic Youth: Daydream Nation live in Roundhouse, London"}]}
```

为了便于阅读，我将代码分成了多行。实际上，如果你查看你的服务代码文件的注释，你会发现你也可以返回 XML。然而，对于大多数用途，JSON 是一个极佳的选择。

# 360 | 第 10 章 ASP.NET AJAX

当你将服务添加到项目时，此文件中的并非所有方法都会自动变为 Web 可调用的。要将某个方法暴露为服务，你需要应用 `OperationMethod` 特性：

### VB.NET

```vb
<OperationMethod()>
Public Function HelloWorld(name As String) As String
```

### C#

```csharp
[OperationMethod]
public string HelloWorld(name)
```

通过此特性，该方法对外部世界可见，因此可以被外部系统访问。

服务创建完成后，下一步是将其注册到 `ScriptManager` 中并从客户端代码中调用它。这两个主题将在接下来的内容讨论。

# 配置 ScriptManager

在本章的早些章节中，你看到 `ScriptManager` 控件是所有 Ajax 相关操作的必选组件。它注册客户端 JavaScript 文件（供 Ajax 框架和你自己使用），通过 `UpdatePanel` 处理部分页面更新，并处理与你在网站中定义的 Web 服务之间的交互。你可以将 `ScriptManager` 添加到单个页面，也可以添加到主页中，使其在整个站点中都可用。

使用服务时，你还需要告诉 `ScriptManager` 你想将 Web 服务暴露给客户端代码。你有两种方法可以实现这一点：

- 在主页的 `ScriptManager` 中
- 在使用该 Web 服务的页面中，使用 `ScriptManagerProxy` 类

当你要在所有或大多数页面中使用 Web 服务时，最好在主页的 `ScriptManager` 控件中声明 `<Services>` 元素，该元素包含一个或多个指向你服务的 `ServiceReference` 元素。例如，为了让你创建的 `NameService.svc` 服务在所有页面中可用，请向主页添加以下高亮代码：

```asp
<asp:ScriptManager ID="ScriptManager" runat="server">
  <Services>
    <asp:ServiceReference Path="~/WebServices/NameService.svc" />
  </Services>
</asp:ScriptManager>
```

通过在主页中注册服务，它将对基于该主页的所有页面可用。这意味着每个页面都会下载运行此服务所需的 JavaScript 文件。如果你完全没有使用该 Web 服务，这将浪费带宽和资源。因此，对于在单个页面上使用的服务，最好在页面本身中注册服务。在不使用带有 `ScriptManager` 主页的普通页面上，你可以直接向 Web Form 添加一个 `ScriptManager`。然而，如果你正在使用已经有自己的 `ScriptManager` 的主页（如 Planet Wrox 网站所示），你需要使用

![](img/9e033e3b9560597824f8b22941d6d8bb_397_0.png)

`ScriptManagerProxy` 控件。因为一个页面只能有一个 `ScriptManager`，所以你不能在使用主页的内容页面中再次添加另一个。`ScriptManagerProxy`充当内容页面与主页中 `ScriptManager` 之间的桥梁，为你在注册服务的位置上提供了极大的灵活性。

当你放置好 `ScriptManagerProxy` 后，就像你之前对 `ScriptManager` 那样向它添加 `<Services>` 元素：

```asp
<asp:ScriptManagerProxy ID="ScriptManagerProxy1" runat="server">
  <Services>
    <asp:ServiceReference Path="~/WebServices/NameService.svc" />
  </Services>
</asp:ScriptManagerProxy>
```

接下来的示例演示了如何注册和访问服务。

# 从客户端调用 Web 服务

在这个练习中，我们将从客户端访问 Web 服务。

1. 在你添加的 `ScriptManager` 中添加 `<Services>` 元素。你将得到：

```asp
<asp:ScriptManager ID="ScriptManager" runat="server">
  <Services>
    <asp:ServiceReference Path="~/WebServices/NameService.svc" />
  </Services>
</asp:ScriptManager>
```

2. 在关闭标签下方添加一个输入框（Text）和一个输入框（Button）。你将得到：

```asp
<asp:ScriptManager ID="ScriptManager" runat="server">
  <Services>
    <asp:ServiceReference Path="~/WebServices/NameService.svc" />
  </Services>
</asp:ScriptManager>

<input id="YourName" type="text" />
<input id="SayHello" type="button" value="Hello" />
```

3. 在输入框下方，添加以下 JavaScript 块：

```javascript
<script>
function helloWorld() {
  var name = document.getElementById('YourName').value;
  NameService.HelloWorld(name, helloCallback);
}
function helloCallback(result) {
  alert(result);
}
</script>
```

4. 为按钮添加 `onclick` 属性，以便在你点击时调用 `helloworld` 方法。你的代码如下：

```html
<input id="SayHello" type="button" value="Hello" onclick="helloWorld(); />
```

5. 按 `Ctrl+Shift+S` 保存所有更改，然后在浏览器中请求 `WebServices.aspx` 页面。输入你的名字并点击 Say Hello。如果一切顺利，你将收到来自 Web 服务的消息。图 10-9 显示了 Apple Safari 中的弹出窗口。

常见错误如果你得到的不是这个对话框，或者在代码段左下角看到一个小三角形，请确保你是完全按照所示编写 JavaScript 的。JavaScript 是区分大小写的，请确保所有的大小写正确。此外，确保你添加的 JavaScript 块位于定义的输入框和按钮之后。最后，确保你的 Web 服务路径与 .svc 文件的实际路径匹配。

## 工作原理

为了将 Web 服务暴露给应用程序中的客户端脚本，你需要在 `Web.config` 文件中注册它。此外，你还需要对服务类应用正确的特性。当你向项目添加启用 Ajax 的 WCF 服务时，会自动这两个操作。如果你查看 `web.config` 文件，你会看到类似的内容：

```xml
<system.serviceModel>
<behaviors>
  <endpointBehaviors>
    <behavior name="NameServiceAspNetAjaxBehavior*>
      <enableWebScript />
    </behavior>
  </endpointBehaviors>
</behaviors>
</system.serviceModel>
```

```xml
</behavior>
</endpointBehaviors>
<behaviors>
<serviceHostingEnvironment aspnetCompatibilityEnabled="true"
multipleSiteBindingsEnabled="true" />
</serviceHostingEnvironment>
<services>
<service name="NameService">
<endpoint address=""
    behaviorConfiguration="NameServiceAspNetAjaxBehavior"
    binding="httpBinding" contract="NameService" />
</service>
</services>
</system.serviceModel>
```

该服务定义了一个单一用途，即其中的 `NameService`。如果你的站点有更多可用服务，你可以将它们添加到与 `NameService` 相同的 `<services>` 元素中。`binding`（绑定）和 `contract`（合约）属性告诉运行时，该服务可以通过 HTTP 调用，并由 `NameService` 类实现。`address`（地址）属性是空的，意味着运行时负责分配地址。对于更多场景，你可以在此处使用相对地址。`behaviorConfigurations` 指向 `behaviors` 节点下定义的行为 `NameServiceAspNetAjaxBehavior`。WCF 从实际的服务定义中获取行为，因此你可以在多个服务中重用同一个行为。在这种情况下，该行为被创建用于通过网页的 `enableWebScript` 元素启用。

一旦服务在 `web.config` 文件中注册，你就可以用 `ScriptManager` 注册它。你可以在主页的 `ScriptManager` 的 `<Services>` 元素中执行操作。在主页中注册 Web 服务的缺点是，它的 JavaScript 会在站点每个页面中被引用。对于只使用一两次的服务，更好的做法是在特定页面上添加 `ScriptManagerProxy` 并在那里注册服务。在页面内部，`ScriptManagerProxy` 的控制和作用类似于一个普通的 `ScriptManager` 控件。然而，它只是一个将其所有服务转发给真实 `ScriptManager` 的代理。在主页中，结合了两个控件的设置。你使用 `ScriptManagerProxy` 控件来设置了 `<services>`：

```asp
<asp:ScriptManagerProxy ID="ScriptManagerProxy" runat="server">
<Services>
<asp:ServiceReference Path="/Services/NameService.svc" />
</Services>
</asp:ScriptManagerProxy>
```
