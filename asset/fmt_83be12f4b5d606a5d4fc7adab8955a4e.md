
```asp
<%@ Language="C#" AutoEventWireup="true" CodeFile="Marks.aspx.cs" Inherits="Marks" %>
<%@ PageType VirtualPath="~/Default.aspx" %>
<html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Display Marks</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<h1><h1>Marks obtained in Different Subjects</h1>
<asp:Label id="Label1" runat="server" style="z-index: 102; left: 16px; position:absolute; top: 159px; width: 321px; Text="Label" Visible="True" Font-Names="Bookman Old Style" Font-Size="Large"/>
<asp:Label id="Label2" runat="server" style="z-index: 102; left: 17px; position:absolute; top: 221px; width: 405px; Text="Label" Visible="True" Font-Names="Bookman Old Style" Font-Size="Large"/>
<asp:Label id="Label3" runat="server" style="z-index: 102; left: 12px; position:absolute; top: 289px; width: 475px; Text="Label" Visible="True" Font-Names="Bookman Old Style"/>
</div>
</form>
</body>
</html>
```

在 `Marks` 页的源代码视图中，注意我们使用了 `PreviousPageType` 指令来指定上一个页面，在这种情况下为 `Default.aspx` 页面。

### 3. 添加列表 10.13 提供的代码，该代码显示了 Default 页面的后置代码（code-behind）：

列表 10.13：`Default.aspx.cs` 的完整代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;

public partial class Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
    }
    protected void Button1_Click(object sender, EventArgs e)
    {
        Label3.Visible = true;
        Label3.Text = "welcome " + TextBox2.Text;
        Session["Rno"] = TextBox2.Text;
    }
}
```

在列表 10.13 提供的代码中，我们声明了一个属性 `Rno`，它在整个应用程序中暴露了 `TextBox` 控件。

### 4. 现在如列表 10.14 所示添加 Marks Web 页面的后置代码：

```csharp
Listing 10.14: Marks.aspx.cs 的完整代码
using System;
using System.Collections;
using System.Configuration;
using System.Data;
using System.Linq;
using System.Web;
using System.Web.Security;
using System.Web.UI;
using System.Web.UI.HtmlControls;
using System.Web.UI.WebControls;
using System.Web.UI.WebParts;
using System.Xml.Linq;
public partial class Marks : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string Rno = Session["Rno"].ToString();
        Label1.Text = "Roll Number : " + Rno;
        ShowMarks(Rno);
    }
    private void ShowMarks(string rollno)
    {
        if (rollno == "000506")
        {
            Label2.Text = "Science : " + "88";
            Label3.Text = "Maths : " + "79";
        }
        else
        {
            Label2.Visible = false;
            Label3.Visible = false;
            Label1.Text = "Roll Number does not exist. Please enter valid roll number.";
        }
    }
}
```

在列表 13.14 中，我们使用了 `Session` 变量通过字符串 `Rno` 从 `TextBox` 中检索值。在这里，我们从上一个页面获取学号，并显示该特定页面学号的成绩。如果学号是有效的，则显示成绩；否则，显示错误信息。

### 5. 现在，按 `F5` 运行应用程序，并在文本框中提供有效的学号和姓名，然后点击 Show Marks 按钮，如图 10.43 所示。

![](img/17af790174c480761404624aeed9b30b_503_0.png)

- 6. 点击 Show Marks 按钮，Default Web 页将提交到 Marks Web 页，如如图 10.44 所示。

![](img/17af790174c480761404624aeed9b30b_503_1.png)

## 总结

本章介绍了 ASP.NET 的一些功能，例如 ASP.NET 站点、ASP.NET 的结构、ASP.NET 的生命周期及其服务器控件。在本章中，你学习了不同的服务器控件，如 `Button`、`TextBox`、`Label`、`HyperLink`、`RadioButton`、`Checkbox`、`PlaceHolder`、`Field`、`ListBox`、`DropDownList`、`BulletedList`、`Image`、`ImageButton`、`ImageMap` 和 `Wizard`。

## 属性

| 属性 | 描述 |

| :--- | :--- |

| AppRelativeDirectory | 获取或设置包含它的 Page 实例或 UserControl 的相对目录 |

| BindingContainer | 获取包含服务器数据绑定的控件 |

| ClientID | 由 ASP.NET 生成的 ID |

| ClientMode | 获取或设置生成 ClientID 属性值的算法 |

| Controls | 获取表示用户界面 (UI) 层级中指定控件子控件的集合对象 |

| DataItemContainer | 如果控件实现了 DataItemContainer 属性，则获取对容器的引用 |

| Enabling | 获取或设置指示是否应用于服务器控件的值 |

| EnableState | 获取或设置指示服务器控件是否持久化其状态及其包含的任何子控件的状态 |

| ID | 获取分配给控件的程序标识符 |

| NamingContainer | 获取服务器命名容器的引用，该容器创建唯一名称以区分具有相同 System.Web.UI.Control.ID 属性值的服务器控件 |

| Page | 获取包含服务器控件的 Page 实例引用 |

| Parent | 获取页面层级中服务器控件的父控件的引用 |

| RenderingCompatibility | 获取指定 ASP.NET 版本的值，该版本与超文本标记语言 (HTML) 代码兼容 |

## 深度解析

| 属性 | 描述 |

| --- | --- |

| Site | 当在设计表面上渲染时，获取持有当前控件的容器的信息 |

| SkinID | 获取或设置应用到服务器控件的样式 |

| TemplateControl | 获取或设置包含服务器控件的模板的引用 |

| TemplateSourceDirectory | 包含服务器控件的 Page 实例或 UserControl 的虚拟目录 |

| UniqueID | 获取服务器控件的唯一的、分层次限定的标识符 |

| ViewState | 获取或设置服务器控件的视图模式 |

| Visible | 获取或设置一个值，指示服务器控件是否在 WebPage 上渲染为 UI |

表 11.2 列出了 `Control` 类中值得关注的公共（Public）方法：

| 方法 | 描述 |

| --- | --- |

| ApplyStyle | 允许你将页面样式中定义的样式属性应用到服务器控件 |

| DataBind | 允许你将数据源绑定到调用的服务器控件及其所有子控件 |

| Dispose | 允许服务器控件在从内存中释放之前执行最终清理工作 |

| FindControl | 允许在当前命名容器中搜索指定的服务器控件 |

| Focus | 允许你将输入焦点设置为控件 |

| HasControls | 允许你查找服务器控件是否包含任何子控件 |

| RenderControl | 允许显示服务器控件的内容，并在启用追踪（tracing）时存储有关控件的追踪信息 |

| ResolveClientUrl | 允许你获取浏览器可以使用的统一资源定位符 (URL) |

| SetRenderMethodDelegate | 允许使用事件处理程序委托，以便将服务器控件及其内容渲染到其父控件中 |

`Control` 类值得关注的公共事件（Events）列在表 11.3 中：

| 事件 | 描述 |

| --- | --- |

| DataBinding | 当服务器控件附加到数据源时发生 |

| Disposed | 指服务器控件的最后一个生命周期，在服务器控件从内存中释放时发生 |

| Init | 指 ASP.NET Web 页面生命周期的第一步，在服务器控件初始化时发生 |

| Load | 当服务器控件加载到 Page 对象时触发 |

| PreRender | 当服务器控件即将渲染到其所在的 Page 时触发 |

| Unload | 当服务器控件从内存中卸载时触发 |

在讨论了 `Control` 类的主要属性、方法和事件之后，让我们讨论 `WebControl` 类，因为它是所有控件所依赖的类。

# 第 11 章：标准 Web 服务器控件

## WebControl 类

`WebControl` 类是一个基类，包含了所有 Web 控件通用的方法、属性和事件。

`WebControl` 类的层次结构如下：

```
System Object
System.web.ui.control
System.Web.ui.WebControls.WebControl
```

`WebControl` 类值得关注的公共属性列在表 11.4 中：

| 表 11.4: WebControl 类值得关注的公共属性 |

| 属性 | 描述 |

| --- | --- |

| AccessKey | 获取或设置访问键，允许你快速导航到 Web 服务器控件 |

| Attributes | 获取任意属性集合（仅用于渲染），这些属性不对应于服务器控件上的属性 |

| BackColor | 获取或设置 Web 服务器控件的背景颜色 |

| BorderRadius | 获取或设置 Web 服务器控件的边框颜色 |

| BorderStyle | 获取或设置 Web 服务器控件的边框样式 |

| BorderWidth | 获取或设置 Web 服务器控件的边框宽度 |

| ControlStyle | 获取或设置 Web 服务器控件的样式 |

| ControlStyleCreated | 获取一个值，指示是否为 `ControlStyle` 属性创建了样式对象。此属性主要供控件开发者使用 |

| CssClass | 设置 Web 服务器控件在客户端渲染的级联样式表 (CSS) 类 |

| Enabled | 获取或设置一个值，指示 Web 服务器控件是否已启用 |

| EnableTheming | 获取或设置一个值，指示是否将主题应用到 Web 服务器控件 |

| Font | 获取与 Web 服务器控件相关的字体属性 |

| ForeColor | 获取或设置 Web 服务器控件的前景色（通常是文本颜色） |

| HasAttributes | 指定一个值，指示是否为 Web 服务器控件设置了属性 |

| Height | 获取或设置 Web 服务器控件的高度 |

| SkinID | 获取或设置应用到 Web 服务器控件的样式 |

| Style | 获取文本属性集合，这些属性将作为样式属性渲染在 Web 服务器控件的外标签上 |

| TabIndex | 获取或设置 Web 服务器控件的制表索引 |

| ToolTip | 获取或设置当鼠标指针悬停在 Web 服务器控件上时显示的文本 |

| Width | 获取或设置 Web 服务器控件的宽度 |

表 11.5 列出了 `WebControl` 类值得关注的公共方法：

| 表 11.5: WebControl 类值得关注的公共方法 |

| 方法 | 描述 |

| --- | --- |

| ApplyStyle | 将指定样式的任何非空元素复制到 Web 控件。它还会覆盖控件的任何现有样式元素 |

| CopyBaseAttributes | 将指定的 Web 服务器控件中未被 `Style` 对象封装的属性复制到调用此方法的 Web 服务器控件中。此方法主要供控件开发者使用 |

| 表 11.5: WebControl 类值得关注的公共方法 |

| 方法 | 描述 |

| --- | --- |

| MergeStyle | 将指定样式的任何非空元素复制到 Web 控件中，但将不会覆盖控件的任何现有样式元素。此方法主要供控件开发者使用 |

| RenderBeginTag | 将指定标记元素的起始标签写入输出流 |

| RenderEndTag | 将标记元素的结束标签写入输出流 |

ASP.NET 中包含的一些基本标准控件如下：

- 按钮控件 (Button Control)
- 文本框控件 (TextBox Control)
- 标签控件 (Label Control)
- 超链接控件 (HyperLink Control)
- 链接按钮控件 (LinkButton Control)
- 字面量控件 (Literal Control)
- 占符控件 (Placeholder control)
- 隐藏字段控件 (HiddenField Control)
- 文件上传控件 (FileUpload Control)
- 复选框控件 (CheckBox Control)
- 单选按钮控件 (RadioButton Control)
- 列表框控件 (ListBox Control)
- 下拉列表控件 (DropDownList Control)
- 项目列表控件 (BulletList Control)
- 图像控件 (Image Control)
- 图像按钮控件 (ImageButton Control)
- 图像映射控件 (ImageMap Control)
- 表格控件 (Table Control)
- 链接控件 (Link Control)
- 向控件 (Wizard Control)

让我们详细讨论这些控件。

## 按钮控件 (Button Control)

按钮控件用于在 Web 页面上创建按钮。它存在于 `System.UI.WebControls` 命名空间中。点击时会将数据提交到服务器。`Button` 类的层次结构如下：

```
System object
System.web.ui.control
System.Web.ui.WebControls.WebControl
System.Web.ui.WebControls.Button
```

表 11.6 列出了 `Button` 类值得关注的属性：

| 表 11.6: Button 类属性 |

| 属性 | 描述 |

| --- | --- |

| CausesValidation | 获取或设置一个值，指示点击时是否执行验证 |

| CommandArgument | 获取或设置传递给 Command 事件的可选参数 |

| PostBack | 获取或设置按钮时的 URL |

| Text | 获取或设置显示在按钮上的文本 |

| UseSubmitBehavior | 获取或设置一个值，指示控件是否使用浏览器的提交 |

| ValidationGroup | 获取或设置按钮验证的控件组 |

表 11.7 列出了 `Button` 类值得关注的公共事件：

| 表 11.7: Button 类值得关注的公共事件 |

| 事件 | 描述 |

| --- | --- |

| Click | 点击按钮时触发 |
