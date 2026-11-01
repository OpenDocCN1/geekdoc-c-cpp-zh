
你还需要在该文件的代码隐藏中添加以下事件处理程序：

```csharp
protected void OnSelect(object sender, EventArgs e)
{
    favoriteColorLabel.Text = ((LinkButton)sender).Text;
    favoriteColorLabel.Style["color"] = ((LinkButton)sender).Style["color"];
}
```

*代码片段 PCSExtenderDemo/Default.aspx.cs*

在浏览器中，起初几乎看不到任何内容，扩展器似乎没有任何效果。这在图 41-16 中显示。

![](img/d7d2ffa0a76feaab821930e95daace93_1294_0.png)

图 41-16

然而，当你将鼠标悬停在写着“green”的文本上时，会动态出现一个下拉菜单。如果你点击此下拉菜单，则会出现一个列表，如图 41-17 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1294_1.png)

图 41-17

当你点击下拉列表中的其中一个链接时，文本会相应更改（在部分页面回发操作之后）。

关于这个简单示例，有两点需要注意：

- 将扩展器与目标控件关联起来非常容易。
- 下拉列表使用自定义代码进行样式设置——这意味着你可以在列表中放置任何你喜欢的内容。这个简单的扩展器是为你的 Web 应用程序添加功能的好方法，而且使用起来非常简单。

AJAX Control Toolkit 中包含的扩展器会不断添加和更新，因此请定期查看 http://www.asp.net/ajax/AjaxControlToolkit/Samples/。此网页包含所有当前扩展器的实时演示，以便你可以看到它们的效果。

除了 AJAX Control Toolkit 提供的扩展器控件之外，你还可以创建自己的扩展器。要创建有效的扩展器，必须使用 AJAX 库。

| 事件 | 描述 |
|---|---|
| PageRequestManager.pageLoaded | 此事件在部分页面回发后、在 UpdatePanel 控件处理完毕后引发。此处理可能包括已创建或更新的 <div> 元素，你可以通过使用 panelsCreated 和 panelsUpdated 属性，通过 Sys.WebForms.PageLoadedEventArgs 对象引用它们。 |
| PageRequestManager.endRequest | 此事件在部分页面回发处理完成后发生。传递给事件处理程序的 Sys.WebForms.EndRequestEventArgs 对象使你能够检测和处理服务器端错误（通过使用 error 和 errorHandled 属性），以及通过 response 访问响应对象。 |
| Application.unload | 此事件在应用程序中的对象被释放之前引发，这给了你一个机会在必要时执行最后的操作或清理。 |

你可以使用静态 add_xxx() 函数为 Application 对象的事件添加事件处理程序，例如：

```
Sys.Application.add_load(loadHandler);
function LoadHandler(sender, args)
{
  // Event handler code.
}
```

对于 PageRequestManager 过程类似，但你必须使用 get_instance() 函数获取当前对象的实例，例如：

```
Sys.WebForms.PageRequestManager.getInstance().add_beginRequest(
  BeginRequestHandler);
function BeginRequestHandler(sender, args)
{
  // Event handler code.
}
```

在 PCSLibraryDemo 应用程序中，已将事件处理程序添加到 PageRequestManager.endRequest 事件。此事件处理程序响应服务器端处理错误，并在 id 为 errorDisplay 的 <span> 元素中显示错误消息。要测试此方法，请点击 Test Client-Side Error Display 按钮，如图 41-19 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1299_0.png)

实现此功能的代码如下：

```
Sys.WebForms.PageRequestManager.getInstance().add_endRequest(
EndRequestHandler);

function EndRequestHandler(sender, args)
{
    if (args.get_error() != undefined)
    {
        var errorMessage = args.get_error().message;
        args.set_errorHandled(true);
        $get('errorDisplay').innerHTML = errorMessage;
    }
}
```

请注意，EndRequestEventArgs 对象的 errorHandled 属性被设置为 true。这会阻止默认行为，即使用 JavaScript alert() 函数在对话框中显示错误消息。

错误本身是通过在服务器上抛出异常生成的，如下所示：

```
protected void testErrorDisplay_Click(object sender, EventArgs e)
{
    throw new ApplicationException(
        "This is the message set in the exception on the server.");
}
```

在许多其他情况下，你会想要使用事件处理技术来响应 Application 和 PageRequestManager 事件。

## JavaScript 调试

过去，JavaScript 有难以调试的名声。然而，这在 Visual Studio 的最新版本中已得到解决。你现在可以像 C# 代码一样为 JavaScript 代码添加断点并逐步执行。你还可以在断点模式下检查对象状态、更改属性值等等。在最新版本的 Visual Studio 中编写 JavaScript 代码时可用的 IntelliSense 也得到了极大改进。

然而，仍然会有时候你想要添加调试和跟踪代码来报告代码执行时的信息。例如，你可能想要使用 JavaScript alert() 函数在对话框中显示信息。

你还可以使用一些第三方工具来添加客户端调试 UI。这些包括：

- **Fiddler** — 你可以从 www.fiddlertool.com 获取此工具，它可以记录你计算机与 Web 应用程序之间的所有 HTTP 流量——包括部分页面回发。还有一些额外的工具可供你更详细地查看网页处理过程中发生的情况。
- **Nikhil's Web Development Helper** — 此工具可在 http://projects.nikhilk.net/WebDevHelper 获取，也可记录 HTTP 流量。此外，该工具包含许多专门针对 ASP.NET 和 ASP.NET AJAX 开发的实用程序，例如检查视图状态和执行即时 JavaScript 代码的能力。后者功能对于测试你在客户端可能创建的对象特别有用。Web Development Helper 在 JavaScript 错误发生时还会显示扩展的错误信息，这使得追踪 JavaScript 代码中的错误变得更容易。

AJAX 库还提供了 Sys.Debug 类，你可以使用它为应用程序添加一些额外的调试功能。该类的最有用功能之一是 Sys.Debug.traceDump() 函数，它使你能够分析对象。使用此函数的一种方法是 在你的网页上放置一个 id 属性为 TraceConsole 的 textarea 控件。然后，所有来自 Debug 的输出都将发送到此控件。例如，你可以使用 traceDump() 方法将有关 Application 对象的信息输出到控制台：

```javascript
Sys.Application.add_load(LoadHandler);
function LoadHandler(sender, args)
{
    Sys.Debug.traceDump(sender);
}
```

这会产生类似于以下内容的输出：

```
traceDump (Sys._Application)
    updating: false
    _id: null
    _disposing: false
    _creatingComponents: false
    _disposableObjects (Array)
    _components (Object)
    _createdComponents (Array)
    _secondPassComponents (Array)
    _loadHandlerDelegate: null
    _events (Sys.UI.EventHandlerList)
        _list (Object)
            load (Array)
                [0] (Function)
    _initialized: true
    _initializing: true
```

你可以在此输出中看到该对象的所有属性。这种技术对于 ASP.NET AJAX 开发非常有用。

## 进行异步 Web 方法调用

ASP.NET AJAX 最强大的功能之一是从客户端脚本调用 Web 方法的能力。这使你能够访问数据、服务器端处理以及各种其他功能。

直到第 43 章“Windows Communication Foundation”，本书才不会讨论 Web 方法，因此我们将把细节留到那时，并在此介绍基础知识。简单来说，Web 方法是你可从 Web 服务公开的方法，使你能够通过 Internet 访问远程资源。在 ASP.NET AJAX 中，你还可以将 Web 方法公开为服务器端网页代码隐藏代码的静态方法。你可以在 Web 方法中使用参数和返回值，就像在其他方法类型中一样。

在 ASP.NET AJAX 中，Web 方法是异步调用的。你将参数传递给 Web 方法并定义一个回调函数，当 Web 方法调用完成后会调用该函数。你使用此回调函数来处理 Web 方法响应。你还可以提供一个备用的回调函数，以便在调用失败时调用。

在 PCSLibraryDemo 应用程序中，你可以通过点击 Call Web Method 按钮来查看 Web 方法调用，如图 41-20 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1301_0.png)
