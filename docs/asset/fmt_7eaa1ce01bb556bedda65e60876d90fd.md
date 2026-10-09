
```csharp
<%@ Page Language="C#" %>
<%@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="cc" %>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>AccordionControl</title>
<style type="text/css">
.titlebar {
    background-color:Blue;
    font-size:large;
    font-family:Verdana;
    border:3px Black;
}
</style>
</head>
<body>
<form id="form1" runat="server">
    <div>
    <asp:ScriptManager ID="ScriptManager1" runat="server">
    </asp:ScriptManager>
    <cc:Accordion ID="Accordion" runat="server" HeaderCssClass="titlebar"
HeaderSelectedCss="titlebar"
FadeTransitions="true"
TransitionDuration="333"
FramesPerSecond="30">
<Panes>
<cc:AccordionPane runat="server">
<Header>
    This is the first pane
</Header>
```

```html
<Content>
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Donec accumsan lorem. Ut consectetuer metus. A Aenean tincidunt metus. Suspendisse molestie cursus. Curabitur lectus. Nulla dolor nec elit convallis vulputate. Nullam pharetra pulinar nunc orci. Phasellus a pretulum porta eu orci. Suspendisse massa. Maecenas erat, non ullamcorper non, mauris eleifend, ut gravida nisl neque a. Vivamus facilisis. Cras vivera. Curabitur augue et dolor posuere. Aenean at magna eros tempora pharetra. Aenean mauris.
</Content>
</cc:AccordionPane>
<cc:AccordionPane runat="server">
<Header>
This is the second pane
</Header>
<Content>
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Donec accumsan lorem. Ut consectetuer metus. A Aenean tincidunt metus. Suspendisse molestie cursus. Curabitur lectus. Nulla dolor nec elit convallis vulputate. Nullam pharetra pulinar nunc orci. Phasellus a pretulum porta eu orci. Suspendisse massa. Maecenas erat, non ullamcorper non, mauris eleifend, ut gravida nisl neque a. Vivamus facilisis. Cras vivera. Curabitur augue et dolor posuere. Aenean at magna eros tempora pharetra. Aenean mauris.
</Content>
</cc:AccordionPane>
</Panes>
</Accordion>
</div>
</form>
</body>
</html>
```

该页面包含一个用于表单的文本框、一个提交按钮，并按照惯常的方式构建了一个 `RegularExpressionValidator` 控件，只不过你可能使用了 `Display` 属性将其设置为 `None`。你不希望普通的 ASP.NET 验证控件显示其消息，因为这将会与 `ValidatorCalloutExtender` 显示的消息冲突。尽管 `Display` 属性被设置为 `None`，但你仍然使用 `ErrorMessage` 属性提供错误信息。运行此页面将产生图 20-41 所示的结果。

![](img/eb54f286ad47e89bbf83e32d279e6dd_1029.png)

## CascadingDropDown 控件（级联下拉控件）

一个 `DropDownList` 的可用选项可以是另一个 `DropList` 选择的函数。`CascadingDropDown` 控件使得在应用程序中启用此功能变得简单。你将 `TargetControlID` 设置为应通过回调服务器填充的 `DropDownList`。你分配一个类别对 `DropDownList` 进行分类。

# 第 20 章：ASP.NET AJAX Control Toolkit

在 `DropList` 填充之前，会显示 `PromptText` 属性的值。此外，当服务器正在处理请求时，会显示 `LoadingText` 属性的值。你可以设置 `ServicePath` 来调用单独 Web 服务器上的 `ServiceMethod`，也可以直接将 `ServiceMethod` 设置为位于页面中的静态 `ScriptMethod`，如示例 20-37 所示。

此示例中的第一个 `DropList` 允许用户选择一个州。在这个示例中，我包含了密苏里州（Missouri）和俄勒冈州（Oregon）。一旦选择了一个州，第二个 `DropList` 将根据用户在第一个 `DropList` 中选中的值进行填充。指定该关系的方法是设置 `CascadingDown` 控件的 `ParentControl`。

## 20-37：使用 CascadingDown 控件

```vb
<@ Import Namespaces="System.Web.Services" %>
< Register Assembly="AjaxControlToolkit" TagPrefix="c" %>

<html xmlns="http://www.w3.org/1999/xhtml">
  <head id="Head1">
  <script runat="server" language="vb">

  <WebMethod, System.Web.Services.ScriptMethod>
  Public Shared Function GetStates(ByVal
  knownCategories As String,
  ByVal category As String) As CascadingDownNameValue()

  Return New Object() { New
  CascadingDownNameValue("Missouri", "Missouri",
  CascadingDownNameValue("Oregon", "Oregon") }
  End Function

  <WebMethod, System.Web.Services.ScriptMethod>
  Public Shared Function GetCounties(ByVal
  knownCategories As String,
  ByVal category As String) As CascadingDownNameValue()

  If knownCategoryValues.Contains("Missouri") Then
  Return New Object() { New
  CascadingDownNameValue("St. Charles",
  "St. Charles"),
  CascadingDownNameValue("St. Louis",
  "St. Louis"),
  CascadingDownNameValue("Jefferson",
  "Jefferson"),
  CascadingDownNameValue("Warren", "Warren",
  CascadingDownNameValue("Franklin", "Franklin") }
  End If

  If knownCategoryValues.Contains("Oregon") Then
  Return New Object() { New
CascadingDropDownValue("Baker", "Baker"), -
New CascadingDropDownValue("Benton", "Benton"), -
New CascadingDropDownValue("Clackamas", "Clackamas"), -
New CascadingDropDownValue("Clatsop", "Clatsop"), -
New CascadingDropDownValue("Columbia", "Columbia") 
  End If
```

```vb
Return Nothing
End Function
```

```vb
</script>
```

```html
<title>CascadingDropDown</title>
<head>
<body>
<form id="form" runat="server" ID="scriptManager" />
<div>
<asp:DropDownList runat="server" ID="ddl" Width="200" />
<br />
<asp:DropDownList runat="server" ID="ddl2" Width="200" />
<br />
<asp:CascadingDropDown runat="server" ID="ddc1"
PromptText="Select a State"
Category="state" LoadingText="[Loading States]"
ServiceMethod="GetStates" />
<asp:CascadingDropDown runat="server" ID="ddc2"
TargetControlID="ddl1"
ParentControlID="ddl2"
PromptText="Select County" category="category"
LoadingText="[Loading Counties]"
ServiceMethod="GetCounties" />
</div>
</form>
</body>
</html>
```

## C#

```csharp
%@ Import Namespace=System.Web.Services %>
<%@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="c1" %>
```

```csharp
<html xmlns="http://www.w3.org/1999/xhtml"
<head id="Head1" runat="server">
```

```csharp
<script runat="server" language="C#">

[WebMethod]
[System.Web.Services.ScriptMethod]
public static CascadingDropDownValue[]
GetStates(string kind, string category)
{
  return new[] {
    new CascadingDropDownValue("Missouri", "Missouri"),
    new CascadingDropDownValue("Oregon", "Oregon");
  }
}

[WebMethod]
[System.Web.Services.ScriptMethod]
public static CascadingDropDownValue[]
GetCounts(string knownCategoryValues, string category) {
  if (knownCategoryValues.Contains("Missouri")) {
    return new[] {
      new CascadingDropDownValue("St. Charles", "St. Charles"),
      new CascadingDropDownValue("St. Louis", "St. Louis"),
      new CascadingDropDownValue("Jefferson", "Jefferson"),
      new CascadingDropDownValue("Warren", "Warren"),
      new CascadingDropDownValue("Franklin", "Franklin")
    };
  }
  if (knownCategoryValues.Contains("Oregon")) {
    return new[] {
      new CascadingDropDownValue("Baker", "Baker"),
      new CascadingDropDownValue("Benton", "Benton"),
      new CascadingDropDownValue("Clackamas", "Clackamas"),
      new CascadingDropDownValue("Clatsop", "Clatsop"),
      new CascadingDropDownValue("Columbia", "Columbia")
    };
  }
  return null;
}
```

## NoBot 控件

`NoBot` 控件决定了带有表单的实体如何操作。`NoBot` 控件决定了如何处理表单提交的实体。你可以设置 `ServicePath` 来调用单独 Web 服务器上的 `ServiceMethod`，也可以直接将 `ServiceMethod` 设置为位于页面中的静态 `ScriptMethod`，如示例 20-37 所示。

此示例中的第一个 `DropList` 允许用户选择一个州。在这个示例中，我包含了密苏里州（Missouri）和俄勒冈州（Oregon）。一旦选择了一个州，第二个 `DropList` 将根据用户在第一个 `DropList` 中选中的值进行填充。指定该关系的方法是设置 `CascadingDown` 控件的 `ParentControl`。

`NoBot` 控件决定了带有表单的实体如何操作。`NoBot` 控件决定了如何处理表单提交的实体。你可以设置 `ServicePath` 来调用单独 Web 服务器上的 `ServiceMethod`，也可以直接将 `ServiceMethod` 设置为位于页面中的静态 `ScriptMethod`，如示例 20-37 所示。

此示例中的第一个 `DropList` 允许用户选择一个州。在这个示例中，我包含了密苏里州（Missouri）和俄勒冈州（Oregon）。一旦选择了一个州，第二个 `DropList` 将根据用户在第一个 `DropList` 中选中的值进行填充。指定该关系的方法是设置 `CascadingDown` 控件的 `ParentControl`。

## 20-37：使用 CascadingDown 控件
