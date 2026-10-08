

## TabContainer 控件

你可以使用 TabContainer 控件将页面组织成几个面板。TabContainer 是多个 TabPanel 控件的宿主机。ActControlSamples 项目包含一个 `TabContainerSample` 页面，它提供了一个类似的专家列表视图，就像你在 `FindAnExpertDemo` 项目中构建的那样。图 20-9 和图 20-10 显示了该页面使用的 TabContainer 的两个标签页。

![](img/b5597c749e848b27b0d305153ae16106_962_0.png)

![](img/b5597c749e848b27b0d305153ae16106_962_1.png)

图 20-9：TabContainerSample.aspx 的数据标签。

图 20-10：TabContainerSample.aspx 的照片标签。

打开 `TabContainerSample.aspx` 页面查看其详情。该页面使用 `UpdatePanel` 控件根据图 20-9 顶部下拉列表的变化来刷新 TabContainer 内容。列表 20-10 显示了 TabContainer 控件的结构。

列表 20-10：TabContainerSample.aspx（代码提取）

```asp
<asp:TabContainer ID="TabContainer1" runat="server"
AutoPostBack="true"
OnActiveTabChanged="TabContainer1_ActiveTabChanged">
<asp:TabPanel ID="DataPanel" HeaderText="Data" runat="server">
<ContentTemplate>
<table>
<tr valign="top">
<td>专业：</td>
<td><asp:Label ID="ExpertiseLabel" runat="server" Text=""

##列表 20-10（续）

```asp
<td>
  <asp:Label Id="DescriptionLabel" runat="server" Text="" />
</td>
</tr>
</table>
</ContentTemplate>
</asp:TabPanel>
<asp:TabPanel Id="PhotoPanel" HeaderText="Photo" runat="server">
  <ContentTemplate>
    <br />
    <asp:Image Id="Photo" runat="server" Height="128px" Width="128px" />
    <br />
  </ContentTemplate>
</asp:TabPanel>
</asp:TabContainer>
```

> 代码文件 [TabContainerSample.aspx] 可在 Wrox.com 下载。

你可以将一个或多个 TabPanel 实例嵌入 TabContainer 中。每个 TabPanel 可以在其 `<ContentTemplate>` 元素中定义多个控件。当活动标签页更改时，你捕获事件。列表 20-11 显示了属于 `TabContainerSample.cs` 的代码。

列表 20-11：TabContainerSample.cs

```cs
using System;
using System.Web.UI;
using System.Web.UI.Controls;

namespace ActControlSamples
{
    public partial class TabContainerSample : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs args)
        {
        }

        protected void ExpertList_SelectedIndexChanged(object sender, EventArgs args)
        {
            var fields = ExpertList.SelectedValue.Split('$');
            var expLabel =
                Page.FindControl("TabContainer1$DataPanel$ExpertiseLabel") as Label;
                expLabel.Text = fields[0];
            var descLabel =
                Page.FindControl("TabContainer1$DataPanel$DescriptionLabel") as Label;
                descLabel.Text = fields[1];
            var photo =
                Page.FindControl("TabContainer1$PhotoPanel$Photo") as Image;
                photo.ImageUrl = "/Photos/" + fields[2] + ".png";
```

![](img/b5597c749e848b27b0d305153ae16106_963_0.png)

```cs
}
  protected void TabContainer1_ActiveTabChanged(object sender, EventArgs args)
  {
    ActiveTabLabel.Text = TabContainer1.ActiveTab.ID;
  }
  protected void ExpertList_DataBound(object sender, EventArgs args)
  {
    ExpertList_SelectedIndexChanged(ExpertList, EventArgs.Empty);
    TabContainer1_ActiveTabChanged(ExpertList, EventArgs.Empty);
  }
```

> 代码文件 [TabContainerSample.aspx] 可在 Wrox 下载。

`ExpertList_SelectedIndexChanged` 事件处理程序通过分隔符分割包含专家数据（如专业、描述和照片）的 `SelectedValue` 字符串，并用这些值设置相应的标签和图像控件。注意，无法直接访问标签内的控件，除非你在表示页面的类中有成员。你可以使用 `Page.FindControl` 方法指定它们。例如，可以通过 `TabContainer1$Photo` 访问 PhotoPanel 中标识符为 Photo 的控件。

`TabContainer1_ActiveTabChanged` 事件处理程序显示所选标签页的索引。`ExpertList` 控件是一个数据绑定控件。一旦控件被读取和设置，`ExpertList_DataBound` 方法就会调用，TabContainer 内部的信息就会刷新。

虽然列表 20-10 没有显示，但 TabContainer 和显示活动标签页的标签封装在 `UpdatePanel` 中，因此所有事件都是异步发生的。

TabContainer 包含了表 20-3 汇总的几个有趣属性。

## 表 20-3：TabContainer 属性

| 属性 | 描述 |
| --- | --- |
| ActiveTabChanged | 当回回后标签页更改时，在服务器端触发此事件。 |
| OnClientActiveTabChanged | 附加到客户端 tabChanged 事件的 JavaScript 函数名称。 |
| CssClass | 用于定义标签页自定义外观和效果的 CSS 类覆盖。 |
| ActiveTabIndex | 要显示的 TabPanel 索引。 |
| Height | 设置标签页的高度（不包括 TabPanel 表头）。 |

## 表 20-3（续）

| 属性 | 描述 |
|---|---|
| Width | 设置标签页主体的宽度。 |
| ScrollBars | 设置在 TabContainer 主体显示滚动条的模式。值取自 `ScrollBars` 枚举类型（None, Horizontal, Vertical, Both, Auto）。 |
| TabStripPlacement | 告诉是将标签渲染在容器的上方（Top）还是下方（Bottom）。 |

可以通过表 20-3 中描述的属性对 TabPanel 进行自定义。

## 折叠面板控件 (Accordion Control)

折叠面板控件允许你定义多个面板并一次只显示一个。它类似于多个 `CollapsibleExtender` 控件，其中一个可以展开。`ActControlSamples` 项目中的 `AccordionSample` 页面是折叠面板控件的良好演示。列表 20-12 显示了该控件的定义。

```asp
<asp:Accordion ID="Accordion1" runat="server"
Width="300px"
HeaderCssClass="header"
HeaderCssClass="selected"
ContentCssClass="content"
AutoSize="None">
<Panes>
<asp:AccordionPane ID="AccordionPanel" runat="server">
<Header>专家 1</Header>
<Content>
该专家曾是 Visual Basic 构建业务应用程序项目的首席程序员。
他特别擅长开发中间件。
</Content>
</asp:AccordionPane>
<asp:AccordionPane ID="Accordion2" runat="server">
<Header>专家 2</Header>
<Content>
他在 GigaSystems 公司担任解决方案架构师。过去五年里出版了多本关于 C# 架构模式的书。
</Content>
</asp:AccordionPane>
<asp:AccordionPane ID="Accordion3" runat="server">
<Header>专家 3</Header>
<Content>
她在 2003 年创立了名为 VeroThe Top 的公司，现在是欧洲 Visual Basic 开发者的著名导师。
</Content>
</asp:AccordionPane>
</Panes>
</asp:Accordion>
```

> 代码文件 [AccordionSample.aspx] 可在 Wrox 下载。

默认情况下，控件不会为元素分配任何特定样式。而且，如果没有样式，控件虽然可以工作，但当你在网页上看到它时，你不会认为它是交互式的。图 20 显示了默认样式外观。

当你点击其中一个控件时，控件会提供动画来显示被点击标题后的内容。`TransitionDuration` 属性允许设置面板之间过渡的时间，以毫秒为单位；默认值为 250。你可以使用 `FramesPerSecond` 属性定义过渡动画每秒的帧数；默认值为 30。通过 `FadeTransitions` 延迟，你可以影响在过渡时是否淡入折叠面板。

