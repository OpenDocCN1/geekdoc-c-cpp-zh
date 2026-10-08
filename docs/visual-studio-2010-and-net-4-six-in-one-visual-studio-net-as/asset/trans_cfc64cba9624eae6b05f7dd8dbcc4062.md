

```
LoadingText="Loading..."
ServicePath=ExpertiseService.asmx ServiceMethod=GetDropDownContent /
<asp:CascadingDropDown Id="ccdExpert" runat="server" TargetControlID="ExpertList"
Category="Expert" ParentControlID="ExpertList"
PromptText="Please select an Expert"
LoadingText="Loading..." ServicePath=ExpertiseService.asmx
ServiceMethod=GetDropDownContent /
</form>
<body>
</body>
</html>
```

代码文件 [Default.aspx] 可在 Wix.com 下载。

UpdatePanel 内部的 Triggers 元素包含一个挂载到 ExpertList 控件的 `AsyncPostBackTrigger`。当用户从列表中选择一个专家时，会向服务器发送异步后回，该后回可以设置专家的描述和照片。一旦异步调用完成，更新面板内的控件将使用相应的描述文本和照片进行刷新。当然，你必须编写 `ExpertList_SelectedIndexChanged` 事件处理程序的代码，如列表 20-7 所示。

![](img/b5597c749e848b27b0d305153ae16106_948_0.png)

# 列表 20-7：处理 ExpertList 事件后的 Default.aspx

```csharp
using System;

namespace FindAnExpertDemo
{
    public partial class Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            if (!IsPostBack)
            {
                Photo.Visible = false;
            }
        }

        protected void ExpertList_SelectedIndexChanged(object sender, EventArgs e)
        {
            var fields = ExpertList.Value.Split('$');
            Description.Text = fields[2];
            Photo.ImageUrl = "/Photos/" + fields[1] + ".png";
            Photo.Visible = true;
        }
    }
}
```

代码文件 [Default.aspx.cs] 可在 Wix.com 下载。

`ExpertList_SelectedIndexChanged` 的主体非常短，它使用了一种简单的序列化技巧。在 `ExpertiseService.asmx` 文件中，专家信息作为其值的一部分被添加到 ExpertList 控件中：

```csharp
foreach (var item in da.GetExpertList(values["Expertise"]))\{
    result.Add(
        new CascadingDropDownNameValue(item.Name,
            String.Format("{0}${1}({2})",
                item.Id, item.Photo, item.Description)));
}
```

选中项目的值的内容如下，且 `Description` 和 `Photo` 控件被设置为下面的值。

现在，构建并运行 `FindExpertDemo`。如你所见，它提供了与原始实现相同的功能，当你更改下拉列表的选择时不会出现闪烁。

应用程序代码保留了原始架构（仍然有一个数据访问层），而 UI 代码变得更短，并将许多元素转为了声明式。

# 使用工具集中的控件

当你查看工具箱（Toolbox）时，你可以控制 Ajax Toolkit 中超过 40 个控件。早些，你检查了 `CascadingDropDown` 扩展程序，它可以挂载到 ASP.NET `DropDownList` 上；那里还有许多其他控件可以改进你网站的用户体验并提供简单的编程模型。本节提供了其中大多数控件的详细概述。

表 20-1 总结了 Ajax Toolkit Beta 0911 版本随附的控件。如你所见，Toolkit 中有可以单独使用的服务器端控件，以及扩展其挂载的其他控件功能的扩展程序（Extender controls）。扩展程序控件在表 20-1 中用斜体字体标记。

**表 20-1：Ajax Toolkit Beta 0911 随附控件**

| 控件 | 描述 |
|---|---|
| Accordion | 此控件定义了多个面板并一次显示一个。Accordion 控件包含一个或多个 `AccordionPane` 控件。每个 `AccordionPane` 控件都有其头部和内容的模板。选中的面板在后回传后会自动持久化。 |
| AlwaysVisibleControlExtender | 此扩展程序扩展任何 ASP.NET 控件，并允许将其固定在页面上，使其在滚动或调整大小时悬浮在背景内容之上。该扩展程序将控件扩展到距离水平和垂直侧边指定距离的位置。 |
| AnimationExtender | 此类允许你以简单、声明式的方式在现有页面上使用强大的框架。当目标控件触发如 `OnLoad`、`OnClick`、`OnMouseEnter` 或 `OnMouseOut` 等特定事件时，它会播放动画。 |
| AsyncFileUpload | 这是一个 ASP.NET Ajax 控件，允许你异步上传文件到服务器。文件上传结果可以在服务器端和客户端进行检查。 |
| AutoCompleteExtender | 此控件扩展了 ASP.NET `TextBox` 控件。它将该控件与弹出面板关联，以显示与文本框中输入的前缀开头的单词。当用户输入的字符超过指定的最小长度时，弹出窗口会显示相应的词汇。 |
| CalendarExtender | 此控件允许在焦点移动到输入元素时显示日期选择器。此扩展程序可以挂载到任何 ASP.NET `TextBox` 控件。它提供具有自定义格式的客户端日期选择功能。你可以通过点击日期或“今天”链接与日历进行交互。 |
| CascadingDropDown | 这种扩展程序可以挂载到任何 ASP.NET `DropDownList` 控件以管理 `DropDownList`set。每当 `DropDownList` 的选择更改时，`CascadingDropDown` 调用指定的 Web 服务来获取 `DropDownList` 的值列表。 |
| CollapsiblePanelExtender | 此扩展程序为网页添加可折叠区域。`CollapsiblePanelExtender` 针对任何 ASP.NET `Panel` 控件。你可以指定页面上的哪些控件作为面板的打开和关闭控制器。或者，面板可以在鼠标移入或移出时自动展开和折叠。 |

# 表 20-1（续）

| 控件 | 描述 |
| --- | --- |
| ColorPickerExtender | 此扩展程序允许在焦点移动到输入元素时显示弹出颜色选择器。你可以将 `ColorPickerExtender` 挂载到任何 ASP.NET `TextBox` 控件。它提供弹出式的颜色选择功能。可选，你可以指定一个按钮显示颜色选择器弹出窗口，以及预览调色板颜色的控件。 |
| ComboBox | 这种控件类似于 `AutoCompleteExtender`，将 `TextBox` 的灵活性与用户可选的选项列表相结合。它从 Windows Forms `ComboBox` 控件继承了许多属性、行为和命名规范，并与 `ListBox`、`BulletList` 和 `DropDownList` 自相同的基类。 |
| ConfirmExtender | 此扩展程序拦截按钮（或任何派自 `Button` 的类型）的点击并向用户显示消息。如果用户点击确定，按钮或链接将正常工作。如果用户未点击确定，则点击事件被拦截，按钮不会执行默认的提交行为。可选，你可以指定在点击对话框中的按钮时执行的客户端脚本。 |
| DragPanelExtender | 此扩展程序允许用户轻松地为控件添加“可拖动性”。`DragPanelExtender` 针对任何 ASP.NET `Panel` 并接收一个额外的参数，指定用作“拖柄”的控件。初始化后，用户可以使用拖柄在网页上自由移动面板。 |
| DropDownExtender | 此扩展程序可以挂载到任何 ASP.NET 控件上，以提供 SharePoint 风格的下拉菜单。显示的菜单仅仅另一个面板或控件。在之前的示例中，下拉菜单是一个包含 `LinkButton` 的面板。通过左键或右键点击挂载的控件激活下拉。如果行为挂载在 `Hyperlink` 或 `LinkButton` 上，点击链接本身将正常操作。 |

