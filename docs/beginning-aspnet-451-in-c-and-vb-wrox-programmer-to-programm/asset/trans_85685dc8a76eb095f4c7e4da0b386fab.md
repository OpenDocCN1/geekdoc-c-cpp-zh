

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

你只需要通过设置 `Path` 属性来引用该服务。与你目前为止在书中看到的其他服务器端 URL 一样，你可以使用波浪号（~）来引用应用程序根目录。

一旦注册了服务，它就会在你的客户端代码中变为可用。现在，IntelliSense（智能感知）足够智能可以发现你定义并注册的 WCF 服务。当你一输入 `NameService` 并紧跟一个客户端脚本块时，IntelliSense 再次启动并显示它找到的方法。这使得找到你在站点中定义的正确服务变得极其简单。这比 Visual Studio 的旧版本有了巨大的改进，旧版本的 IntelliSense 列表中只有少数几个与 JavaScript 相关的项。从 Visual Studio 2008 开始，IntelliSense 现在实际上能够锁定你的代码，并在包含代码中找到的变量名、方法、服务等的列表中找到 IntelliSense 列表。

# 364 | 第 10 章节 ASP.NET AJAX

从 VS 2010 开始，微软通过提高 IntelliSense 中显示项的性能和准确性，进一步改进了 IntelliSense。

要查看实际页面如何工作以及它如何访问 Web 服务，请查看 `script` 块中的代码。

你需要查看的第一段代码是 `helloWorld`：

```javascript
function helloWorld() {
    var yourName = document.getElementById('yourName').value;
    NameService.HelloWorld(yourName, helloCallback);
}
```

首先，这段代码提供了你之前创建的文本框的引用。然后你可以访问它的 `value` 属性来获取下方的名称。

此名称通过以下代码发送到 Web 服务方法 `HelloWorld`：

```javascript
NameService.HelloWorld(yourName, helloCallback);
```

调用 `HelloWorld` 的第一个参数是 Web 服务期望的参数：一个字符串值。第二个参数是回调函数 `helloCallback`。

（注：原文处处处处处，，，，，，，，，， 转发为真正的 `ScriptManager` 控件）。

