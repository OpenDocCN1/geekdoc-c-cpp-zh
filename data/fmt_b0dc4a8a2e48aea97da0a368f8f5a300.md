
```asp
<asp:ImageMap ID="ImageMap" runat="server" ImageUrl="~/Images/kids.jpg"
    HotSpotMode="Navigate" />
    <asp:CircleHotSpot AlternateText="Addison" NavigateUrl="Addison.aspx" 
        Radius="24" X="345" Y="372" />
    <asp:CircleHotSpot AlternateText="Brayden" NavigateUrl="Brayden.aspx" 
        Radius="20" X="181" Y="314" />
    <asp:CircleHotSpot AlternateText="Arianna" NavigateUrl="Arianna.aspx" 
        Radius="28" />
```

# 摘要

本章探索了许多服务器控件、它们的功能以及提供的特性。在 ASP.NET 4.5 中，你有 50 多个服务器控件可用。由于在创建 ASP.NET 应用程序时你有许多服务器控件，你必须仔细考虑哪种控件最适合任务。许多控件看起来相似，但它们提供的功能不同。这些控件确保你可以为所有浏览器构建出最好的应用程序。

服务器控件是你在 ASP.NET 库中可以找到的最有用工具之一。它们非常有用，可以为你节省大量时间。本章向你介绍了这些控件以及你将它们整合到项目的不同方法。所有这些控件都是 ASP.NET 页面的绝佳选择，更容易开发页面所需的功能。

# 验证服务器控件

本章内容：

- 理解提供的验证服务器控件
- 使用客户端和服务器端验证
- 启用无阻塞验证

## 本章代码下载

请注意，本章中的所有代码示例都可以在书籍网站 `www.wrox.com` 获取。

当你查看 Visual Studio 2012 中的工具箱窗口时——如果你已经读过第 4 章和第 5 章涵盖的各种服务器控件——你可能会被工具箱中出现的服务器控件数量感到震惊：`验证服务器控件`

验证服务器控件是一系列允许你处理用户输入你构建的应用程序表单元素信息的控件。这些控件用于确保表单中数据的有效性。

在学习如何使用这些控件之前，本章首先介绍验证过程。

# 理解验证

多年来，开发者一直在构建 Web 应用程序。通常的动机是提供或收集信息。在本章中，你将重点关注 Web 应用程序的信息收集和验证方面。如果你通过应用程序收集数据，`收集有效数据` 对你来说应该是重要的。如果信息无效，那么收集它就没有意义。

验证是你应用到收集的数据上的一套规则。这些控件可以多可以少，执行可以严格可以松散：这取决于你的业务规则和需求。不存在完美的验证，因为无论你建立什么规则，某些用户可能会在某种程度上作弊。诀窍是在最少的规则和适当的严格之间找到平衡，而不损害应用程序的可用性。

# 第 6 章 验证服务器控件

你为验证收集的数据来自你在应用程序提供的 Web 表单。Web 表单由不同类型的 HTML 元素组成，使用原始表单元素、ASP.NET 服务器控件或 ASP.NET 表单控件构建。最后，你的表单由许多不同的 HTML 元素组成，例如文本框、单选按钮、复选框、下拉列表等。

在学习过程中，你将看到应用于表单元素的不同类型的验证规则。记住，你无法验证你所收集信息的真实性；相反，你应用规则来回答此类问题：

- 文本框中是否有输入内容？
- 文本框中输入的数据是否为电子邮件格式？

从这些问题可以看出，你可以对 HTML 表单应用多个验证规则（这些示例将在本章稍后的部分出现）。事实上，你可以对单个元素应用你想要的任意规则。应用更多规则会增加应用于数据验证的严格性。

# 客户端验证与服务器端验证

如果你是 Web 开发的新手，你可能不知道客户端验证和服务器端验证之间的区别。假设最终用户在填写某些信息后点击表单上的“提交”按钮。在 ASP.NET 中发生的是，该表单被封装在一个请求中并发送到应用程序所在的服务器。在请求/响应周期的这个时间点，你可以对提交的信息运行验证检查。这种做法被称为服务器端验证，因为它发生在服务器上。

另一方面，也可以在发布到最终用户浏览器的表单中提供客户端（通常是 JavaScript），以便在表单回传到原始服务器之前对表单中输入的数据进行验证。在这种情况下，就发生了客户端验证。

客户端验证对最终用户来说是快速且响应迅速的。它是表单用户在工作时面对的一项内容。如果表单有问题，客户端验证确保最终用户能够尽快获知。这是因为客户端验证，如果调用得当，会在表单回传到服务器之前执行。

服务器端验证也将验证的处理能力推向客户端，这意味着你不需要在服务器上花费 CPU 周期来验证。

## 服务器端控件

那么正确的路径是什么？嗯，实际上是两者都有！最好的方法是总是进行客户端验证，然后在表单通过并回传到服务器时，使用服务器端验证进行验证。这种方法提供了最好的平衡。这是因为黑客无法简单地绕过验证。这种验证技术也是高效——兼顾了速度和安全性。

## 第 6 章 验证服务端控件

使用 ASP.NET 验证控件与使用任何其他 ASP.NET 服务端控件没有区别。这些控件中的每一个都允许你将其拖放到设计表面上，或直接在 ASP.NET 页面的代码中对其操作。你还可以配置这些控件，使其完全按照你想要的方式出现——确保应用程序可能所需的视觉独特性。在本章中，你将看到这些内容的许多方面。

> 注意：如果 ASP.NET 验证控件不能满足你的需求，你完全可以使用自定义验证控件来编写自己的控件。不过，也有第三方控件，例如来自 `www.peterblum.com/DES` 的 Peter Blum 提供的 Validation and More (WAM)，它包含了超过 50 多个 ASP.NET 验证控件。

### 表 6-1

| 验证服务端控件 | 描述 |
| --- | --- |
| `RequiredFieldValidator` | 确保用户不会跳过某个表单字段。 |
| `CompareValidator` | 允许使用比较运算符（等于、大于等）对用户输入与另一个项目进行比较。 |
| `RangeValidator` | 根据数字或字符的下限和上限范围检查用户的输入。 |
| `RegularExpressionValidator` | 检查用户的输入是否符合正则表达式定义的模式。该控件非常适合检查电子邮件地址和电话号码。 |
| `CustomValidator` | 使用自定义代码的验证逻辑检查用户的输入。 |
| `DynamicValidator` | 与实体数据模型和扩展方法抛出的异常配合。该控件是 ASP.NET 数据框架的一部分。有关此的更多信息，请务必在互联网上搜索 `DynamicValidator`。 |
| `ValidationSummary` | 在页面的特定位置显示所有验证器的错误消息。 |

## 验证的触发

验证并非凭空发生；它是响应某个事件而发生的。在大多数情况下，它是由于按钮点击。`Button`、`LinkButton` 和 `ImageButton` 控件都具有触发页面验证的能力。这是默认行为。将服务端控件拖放到你的表单上，会产生以下初始设置：

```xml
<asp:Button ID="Button" runat="server" Text="Button" />
```

如果你查看 `Button` 控件的属性，你会发现 `CausesValidation` 属性被设置为 `True`。如所述，这种行为是默认的——页面上的所有按钮，无论有多少个，都会触发表单验证。

如果你在 ASP.NET 页面上有多个按钮，并且你不希望每个按钮都触发验证，你可以对在验证过程中想要忽略的所有按钮将 `CausesValidation` 设置为 `False`（例如，表单的取消按钮或在作为搜索框的另一个表单元素中输入）：

```xml
<asp:Button ID="Button" runat="server" Text="Cancel" CausesValidation="false" />
```

## ASP.NET 4.5 中的无干扰验证

传统上，验证是在服务端通过使用内置控件或方法检查表单上的值来处理的。在客户端，浏览器中会省略 JavaScript。在这种情况下，用户可能会被验证消息所淹没。此外，如果 JavaScript 本身包含错误，页面可能无法正常加载。为了规避这个问题，jQuery 验证插件已更新以支持无干扰验证。

无干扰验证有助于减少用户与 Web 应用程序交互时的干扰。它不是内联渲染 JavaScript，而是向适当的表单元素添加 HTML5 `data-*` 属性。在 ASP.NET 4.5 中，使用了 jQuery 验证插件并默认启用了无干扰验证功能。

与之前的 Visual Studio 版本不同，Visual Studio 2012 包含一个空项目模板。如果你选择创建一个新网站，`web.config` 文件包含以下内容：

```xml
<?xml version="1.0"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5"/>
  </system.web>
</configuration>
```

ASP.NET 中可用的验证控件之一是 `RequiredFieldValidator`。代码列表 6-1 显示了 `RequiredFieldValidator` 控件的简单用法。

### 代码列表 6-1：RequiredFieldValidator 服务控件的简单用法

```vb
<% Page Language="VB" %>
<!DOCTYPE html>
<script runat="server">
  Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    If Page.IsValid Then
      Label1.Text = "Page is valid!"
    End If
  End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
  <head runat="server">
    <title></title>
  </head>
  <body>
    <form id="form1" runat="server">
      <asp:TextBox Id="TextBox1" runat="server"></asp:TextBox>
      <asp:RequiredFieldValidator Id="RequiredFieldValidator1" runat="server" Text="Required:" ControlToValidate="TextBox1" EnableClientScript="true"/>
      <br />
      <asp:Button Id="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />
      <br />
      <br />
      <asp:Label Id="Label1" runat="server"></asp:Label>
    </form>
  </body>
</html>
```

# 206 | 第 6 章 验证服务器控件

![](img/67a6707ff505c052edb96c0128fb3096_255_0.png)

图 6-2

现在看列表 6-1 中该示例的代码。首先，`TextBox`、`Button` 或 `Label` 控件没有任何变化。它们的构造方式与你没有使用任何类型验证时的构造完全相同。然而，此页面确实包含了一个简单的 `RequiredFieldValidator` 控件。该控件的几个属性特别值得注意，因为你将在创建的许多验证服务器控件中用到它们。

第一个要查看的属性是 `Text` 属性。该属性是在验证失败时通过网页显示给最终用户看到的值。在这种情况下，它是一个简单的 "Required" 字符串。第二个要查看的属性是 `ControlToValidate`。该属性用于建立此验证服务器控件与需要验证的 ASP.NET 表单元素之间的关联。在这种情况下，该值指定了表单中的唯一元素——文本框。

> 注意 使用 `ControlToValidate` 属性可以进行验证的 WebControls 有：
> - `DropDownList`
> - `FileUpload`
> - `ListBox`
> - `RadioButtonList`
> - `TextBox`
>
> 可以使用 `ControlToValidate` 属性进行验证的 HtmlControls 有：
> - `HtmlInputField`
> - `HtmlInputPassword`
> - `HtmlInputText`
> - `HtmlSelect`
> - `HtmlTextArea`

现在你可以从这个示例中看到，错误信息是由 `<asp:RequiredFieldValidator>` 控件内部的属性构造的。

你也可以将此错误信息写在 `<asp:RequiredFieldValidator>` 起始和结束节点之间，如列表 6-2 所示。

### 列表 6-2：在节点之间放置值

```xml
<asp:RequiredFieldValidator ID="RequiredFieldValidator1"
runat="server" ControlToValidate="TextBox1"
EnableClientScript="true"
Required=""
</asp:RequiredFieldValidator>
```

> 注意 `RequiredFieldValidator` 是唯一一个验证值是否已提交的验证控件。其他验证控件不需要提交值。

## 查看生成的结果

如果浏览器允许，`RequiredFieldValidator` 控件将使用客户端验证。你可以通过右键点击页面并从菜单中选择“查看源代码”来查看客户端验证是如何工作的。在页面代码中，你将看到列表 6-3 中的标记。

### 列表 6-3：部分生成的标记

```html
<!-- 为了清晰起见已省略 -->
<input name="TextBox" type="text" id="TextBox1" />
<span data-validation-controlvalidate="RequiredFieldValidator1" data-val="true"
data-evaluation-function="RequiredFieldValidator1evaluateIsValid"
data-initial-value="" style="visibility:hidden;">
Required=""
</span>
<br />
<input type="submit" name="Button1" value="Submit" onclick="javascript:WebForm
DoPostBackWithOptions(new WebForm PostBackOptions(&quot;,Button1&quot;, &quot;&quot;, true,
&quot;&quot; &quot;&quot; &quot;&quot;, false, false));" id="Button" />
```

`WebForm_DoPostBackWithOptions` JavaScript 函数启动了客户端验证。注意 `span` 元素包含了四个以 `data-val` 开头的属性。这些属性帮助 JavaScript 函数确定哪些元素应该用于验证以及应该如何处理验证。

> 注意 `data-*` 属性只有在开启了非侵入式验证（unobtrusive validation）时才会渲染。当未开启非侵入式验证时，JavaScript 将发送到浏览器中处理验证：

```javascript
<script type="text/javascript">
<![CDATA[
var RequiredFieldValidator1 = document.all ? document.all
["RequiredFieldValidator1"] : document.getElementById("RequiredFieldValidator1");
RequiredFieldValidator1.controltovalidate = "TextBox1";
RequiredFieldValidator1.evaluationfunction = "RequiredFieldValidator1evaluateIsValid";
RequiredFieldValidator1.initialvalue = "";
]]>
</script>
```

## 使用 InitialValue 属性

`RequiredFieldValidator` 控件的一个属性是 `InitialValue` 属性。在列表 6-3 中，你可以看到初始值被重构为 `span` 元素上的属性名 `data-initialvalue`。某些表单元素是通过某些默认属性填充的（例如，来自数据存储），这些表单元素向最终用户展示了在表单提交到服务器之前需要更改的值。

当使用 `InitialValue` 属性时，你向 `RequiredFieldValidator` 控件指定元素的初始文本。最终用户被要求在提交表单之前更改该文本。列表 6-4 显示了使用此属性的示例。

### 列表 6-4：使用 InitialValue 属性

```xml
<asp:TextBox Id="TextBox1" runat="server" Text="Wrox"></asp:TextBox>
<asp:RequiredFieldValidator Id="RequiredFieldValidator1"
runat="server" ControlToValidate="TextBox1" InitialValue="Wrox"
EnableClientScript="true" Text="Please change the value of the textbox!" />
```
