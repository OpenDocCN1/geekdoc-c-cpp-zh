
到目前为止，本章介绍了许多强大的功能，例如样式化和客户端脚本的编辑，你可以在编写自己的自定义控件时利用这些功能。如果你正在利用这些功能，可能还需要考虑如何处理不同的浏览器（通常称为低级浏览器 down-level browsers），这些浏览器可能无法理解这些高级功能，或者不具备这些功能。在创建控件时，能够检测并响应低级浏览器是一个重要的考虑因素。ASP.NET 包含了一些强大的功能，你可以使用它们来检测请求页面的浏览器类型和版本，以及该浏览器支持的能力。

## .browser 文件

ASP.NET 使用了一种非常灵活的方法来配置、存储和发现浏览器能力。所有的浏览器识别和能力信息都存储在 `.browser` 文件中。ASP.NET 将这些文件存储在 `C:\Windows\Microsoft.NET\Framework\v4.0.xxxxx\Config` 目录下。打开此文件夹，你会发现 ASP.NET 为你提供了多种 `.browser` 文件，描述了今天大多数常见桌面浏览器的能力，以及 PDA 和手机等设备上浏览器的信息。打开其中一个文件，你会发现该文件包含了浏览器的所有识别和能力信息。列表 7-24 显示了 iPhone 能力文件的内容，你通常可以在机器的 `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config\Browsers\iphone.browser` 找到。

> 注意：提醒一下，如果你使用的是 64 位版本的 .NET Framework，也可以浏览到 `C:\Windows\Microsoft.NET\Framework64\v4.0.xxxxx\Config\`。

## 列表 7-24：示例浏览器能力文件

```xml
<browsers>
<!-- Mozilla/5.0 (iPhone; CPU like Mac OS X; en) AppleWebKit/420+ (HTML, like Gecko)
Version/3.0/Mobile/1A543 Safari/419.3 -->
<gateway id="iPhone" parentID="Safari">
  <identification>
    <userAgent match="iPhone" />
  </identification>
  <capabilities>
    <capability name="isMobileDevice" value="true" />
    <capability name="mobileDeviceManufacturer" value="Apple" />
    <capability name="mobileDeviceModel" value="iPhone" />
    <capability name="canInitiateVoiceCall" value="true" />
  </capabilities>
</gateway>
</browsers>
```

## 列表 7-24（续）

```xml
<!-- Mozilla/5.0 (iPod; CPU like Mac OS; en) AppleWebKit/420.1 (KHTML, like Gecko)
Version/3.0 Mobile/4A93 Safari/419.3 -->
<gateway id="iPod" parentID="Safari">
  <identification>
    <userAgent match="iPod" />
  </identification>
  <capabilities>
    <capability name="isMobileDevice" value="true" />
    <capability name="mobileDeviceManufacturer" value="Apple" />
    <capability name="mobileDeviceModel" value="iPod" />
  </capabilities>
</gateway>
```

```xml
<!-- Mozilla/5.0 (iPad; CPU OS4_3 like Mac OS; en; en-us) AppleWebKit/653.17.9
(KHTML, like Gecko) Version/5.0.2 Mobile/8F191 Safari/653.18.5 -->
<gateway id="iPad" parentID="Safari">
  <identification>
    <userAgent match="iPad" />
  </identification>
  <capabilities>
    <capability name="isMobileDevice" value="true" />
    <capability name="mobileDeviceManufacturer" value="Apple" />
    <capability name="mobileDeviceModel" value="iPad" />
  </capabilities>
</gateway>
</browsers>
```

这种存储浏览器能力的方法优点是，当有新浏览器创建或新版本发布时，开发者只需创建或更新 `.browser` 文件来描述该浏览器的能力。

## 浏览器能力信息

现在你已经了解 ASP.NET 如何存储浏览器能力信息，你需要知道如何在运行时访问这些信息并根据浏览器控制其渲染。要通过请求浏览器访问能力信息，你可以使用 `Page.Request.Browser` 属性。该属性让你能够访问 `System.Web.HttpBrowserCapabilities` 类，该类提供了有关发起请求的浏览器能力的信息。浏览器可以支持并渲染所需的内容。列表使用这些信息为 TextBox 控件添加能力。列表 7-25 显示了如何检测浏览器能力以确保浏览器支持 JavaScript。

## 列表 7-25：在服务器端代码中检测浏览器能力

### VB

```vb
Protected Overrides Sub OnPreRender(ByVal e As EventArgs)
  If Page.Request.Browser.JavaScriptEnabled Then
    ' JavaScript is supported
  End If
End Sub
```

### C#

```csharp
protected override void OnPreRender(EventArgs e)
{
    if (Page.Request.Browser.JavaScriptEnabled)
    {
        // JavaScript is supported
    }
}
```

## C# 属性示例

```csharp
public string Text
{
    set(string value)
    {
        ViewState["Text"] = value;
    }
}
```

```csharp
public string Text
{
    get
    {
        string s = (string)ViewState["Text"];
        return (s == null) ? "[" + this.ID + "]" : s;
    }
    set
    {
        ViewState["Text"] = value;
    }
}
```

当你在 ASP.NET 服务器控件（`server control`）中创建新属性时，你应该记住使用这种相同的技术，以确保终端用户在你的控件中设置的值在跨页面回传（`postbacks`）时持久化。

> 注意：`ViewState` 的加载是在页面触发 `OnInit` 事件之后发生的。如果你的控件在事件触发之前对自身或另一个服务器控件进行了更改，则这些更改不会保存到 `ViewState` 中。

## 类型与 ViewState

如前节所述，`ViewState` 基本上是一个通用的对象集合，但并不是所有对象都可以添加到 `ViewState` 中。只有可以被持久化的类型才会被用于 `ViewState`，因此像数据库连接或文件句柄这样的对象不应被添加到 `ViewState`。

此外，某些数据类型针对 `ViewState` 的使用进行了优化。在向 `ViewState` 添加数据时，你将数据封装为这些类型：

- 原始类型（`Int32`、`Boolean` 等）。
- 原始类型的数组。
- `ArrayList`、`HashTable`。
- `Pair`（对）、`Triplet`（三元组）。
- `Color`（颜色）、`DateTime`（日期）。
- `String`（字符串）、`IndexedString`。
- 这些类型的 `HybridDictionary`。
- 具有 `TypeConverter`（类型转换器）的对象。但注意，如果你使用这些类型，性能将会降低。
- 可序列化对象（标记有 `Serializable` 特性）。

## 控件状态 (Control State)

有时，你的控件必须在跨回传存储少量的关键的（通常是私有的）信息。为了允许存储此类信息，如果开发者禁用了 `ViewState`，ASP.NET 会包含一种名为 `ControlState` 的独立 `ViewState` 类型。`ControlState` 本质上是为你控件提供的私有 `ViewState`。

## 第 7 章 用户控件与服务器控件

> 注意：为了确保你的数据在跨回传时可用，请使用 `ControlState` 而不是 `ViewState` 来存储信息。`ViewState` 可以在 Web 应用程序或站点内禁用，这可能会导致依赖 `ViewState` 的控件失效。

两个方法 `SaveControlState` 和 `LoadControlState` 提供了对 `ControlState` 的访问；然而，这些方法的实现由你决定。列表 7-27 显示了你如何使用 `LoadControlState` 和 `SaveControlState` 方法。

## 列表 7-27：在服务器控件中使用 ControlState

### VB

```vb
<DefaultProperty("Text")>
<ToolboxData("<{0}:Listing0727 runat=server></{0}:Listing0727>")>
Public Class Listing0727
    Inherits WebControl

    Dim state As String
    Protected Overrides Sub OnInit(ByVal e As System.EventArgs)
        Page.RegisterRequiresControlState(Me)
        MyBase.OnInit(e)
    End Sub

    Protected Overrides Sub LoadControlState(ByVal savedState As Object)
        state = CStr(savedState)
    End Sub

    Protected Overrides Function SaveControlState() As Object
        Return CType("ControlSpecificData", Object)
    End Function
End Class
```

### C#

```csharp
[DefaultProperty("Text")]
[ToolboxData("<{0}:Listing0727 runat=server></{0}:Listing0727>")]
public class Listing0727 : WebControl
{
    string state;
    protected override void OnInit(EventArgs e)
    {
        Page.RegisterRequiresControlState(this);
        base.OnInit(e);
    }

    protected override void LoadControlState(object savedState)
    {
        state = (string)savedState;
    }

    protected override object SaveControlState()
    {
        return (object)"ControlSpecificData";
    }

    protected override void RenderContents(HtmlTextWriter output)
    {
        output.Write("Control State: " + state);
    }
}
```

意图使用 `ControlState` 的控件在尝试保存控件状态之前必须调用 `Page.RegisterRequiresControlState` 方法。此外，每次页面加载都必须调用 `RegisterRequiresControlState` 方法，因为该值不会通过页面回传被保留。

## 触发回传事件 (Raising Postback Events)

正如你在本章中看到的，ASP.NET 提供了一套非常强大的工具，你可以使用它们来开发控件并将其发布到客户端浏览器。但这仍然是单向通信，因为服务器只向客户端推送数据。向服务器发送数据的过程通常被称为页面回传（`page postback`）。当你点击任何导致页面向 Web 服务器发送新请求的按钮或链接时，就会经历页面回传。

ASP.NET 为处理来自 ASP.NET Web 页面的回传提供了一个丰富的框架。它提供了一个模拟标准 Windows Forms 事件模型的开发模型，这使得你能够使用控件，尽管这些控件是在客户端浏览器中渲染的，它们也可以在服务器端代码中触发事件。它还提供了一种易用的机制，可以将服务器控件插入该框架中，使你能够创建触发页面回传的控件。图 7-15 显示了 ASP.NET 回传框架。

![](img/67a6707ff505c052edb96c0128fb3096_316_0.png)

图 7-15

要启动回传，默认情况下，ASP.NET 使用客户端脚本。如果你希望控件能够启动回传，你必须实现 `IPostBackEventHandler` 接口。

## 列表 7-28：在服务器控件中使用回传

### VB

```vb
Protected Overrides Sub RenderContents(ByVal output As HtmlTextWriter)
    Dim p As New PostBackOptions(Me)
    Page.RegisterRequiresControlState(Me)
    output.AddAttribute(HtmlTextWriterAttribute.OnClick,
        Page.ClientScript.GetPostBackEventReference(p))
    output.AddAttribute(HtmlTextWriterAttribute.Value,
        Me.ClientID & "_")
    output.AddAttribute(HtmlTextWriterAttribute.Name,
        Me.ClientID & "_")
    output.RenderBeginTag(HtmlTextWriterTag.Button)
    output.Write("My Button")
    output.RenderEndTag()
End Sub
```

### C#

```csharp
protected override void RenderContents(HtmlTextWriter output)
{
    PostBackOptions p = new PostBackOptions(this);
    Page.RegisterRequiresControlState(this);
    output.AddAttribute(HtmlTextWriterAttribute.OnClick,
        Page.ClientScript.GetPostBackEventReference(p));
    output.AddAttribute(HtmlTextWriterAttribute.Value,
        this.ClientID + "_");
    output.AddAttribute(HtmlTextWriterAttribute.Name,
        this.ClientID + "_");
    output.RenderBeginTag(HtmlTextWriterTag.Button);
    output.Write("My Button");
    output.RenderEndTag();
}
```

`GetPostBackEventReference` 方法被调用时需要一个 `PostBackOptions` 对象。它允许你指定任何影响 ASP.NET 如何回传的选项。你可以将回传 JavaScript 添加到任何客户端事件，甚至为你的控件添加服务器端逻辑。为了触发服务器事件，你需要实现 `IPostBackEventHandler` 接口。列表 7-29 显示了如何对按钮这样做。

## 列表 7-29：在服务器控件中处理回传事件

### VB
