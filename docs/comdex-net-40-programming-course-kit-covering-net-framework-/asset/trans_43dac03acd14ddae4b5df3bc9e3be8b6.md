
```aspx
<PartChromeStyle BackColor="#F7F6F3" BorderColor="#E2DED6"
        Font-Names="Verdana" ForeColor="white" />
<MenuLabelHoverStyle ForeColor="#E2DED6" />
<EmptyZoneTextStyle Font-Size="0.8em" />
<MenuLabelStyle ForeColor="white" />
<MenuVerbHoverStyle BackColor="#F7F6F3" BorderColor="#CCCCCC" BorderStyle="Solid"
    BorderWidth="1px" ForeColor="#333333" />
<HeaderStyle Font-Size="0.7em" ForeColor="#CCCCCC" HorizontalAlign="Center" />
<MenuVerbStyle BackColor="#5D7B9D" BorderStyle="Solid"
    BorderWidth="1px" ForeColor="white" />
<PartStyle Font-Size="0.8em" ForeColor="#333333" />
<TitleBarVerbStyle Font-Size="0.6em" Font-Underline="False" ForeColor="white" />
<MenuPopupStyle BackColor="#5D7B9D" BorderColor="#CCCCCC" BorderWidth="1px"
    Font-Names="Verdana"
    Font-Size="0.6em" />
<PartTitleStyle BackColor="#5D7B9D" Font-Bold="True"
    Font-Size="0.8em" ForeColor="white" />
</td>
<td valign="top" align="center" style="width: 159px">
&nbsp;
<asp:WebPartZone ID="WebPartZone2" runat="server" Width="87px"
    Height="67px" BorderColor="#CCCCCC"
    Font-Names="Verdana" Padding="6">
<ZoneTemplate>
<asp:Label ID="Label1" runat="server" Text="City Name: Delhi"
    Width="50px" Title="My Label">
</asp:Label>
</ZoneTemplate>
<PartChromeStyle BackColor="#F7F6F3" BorderColor="#E2DED6"
    Font-Names="Verdana" ForeColor="white" />
<MenuLabelHoverStyle ForeColor="#E2DED6" />
<EmptyZoneTextStyle Font-Size="0.8em" />
<MenuLabelStyle ForeColor="white" />
<MenuVerbHoverStyle BackColor="#F7F6F3" BorderColor="#CCCCCC" BorderStyle="Solid"
    BorderWidth="1px" ForeColor="#333333" />
<HeaderStyle Font-Size="0.7em" ForeColor="#CCCCCC" HorizontalAlign="Center" />
<MenuVerbStyle BackColor="#5D7B9D" BorderStyle="Solid"
    BorderWidth="1px" ForeColor="white" />
<PartStyle Font-Size="0.8em" ForeColor="#333333" />
<TitleBarVerbStyle Font-Size="0.6em" Font-Underline="False" ForeColor="white" />
<MenuPopupStyle BackColor="#5D7B9D" BorderColor="#CCCCCC" BorderWidth="1px"
    Font-Names="Verdana"
    Font-Size="0.6em" />
<PartTitleStyle BackColor="#5D7B9D" Font-Bold="True"
    Font-Size="0.8em" ForeColor="white" />
</asp:WebPartZone>
</td>
<td valign="top" align="right">
<asp:EditorZone ID="Editorzone1" runat="server"
    BackColor="#F7F6F3" BorderColor="#CCCCCC"
    BorderWidth="1px" Font-Names="Verdana" Padding="6">
<ZoneTemplate>
<asp:AppearanceEditorPart ID="Appearanceeditorpart1" runat="server" />
<asp:LayoutEditorPart ID="Layouteditorpart1" runat="server" />
<asp:PropertyGridEditorPart ID="Propertygrideditorpart1" runat="server" />
</ZoneTemplate>
<LabelStyle Font-Size="0.8em" ForeColor="#333333" />
<HeaderStyle BackColor="#E2DED6" Font-Bold="True"
    Font-Size="0.8em" ForeColor="#333333" />
<HeaderVerbStyle Font-Bold="False" Font-Size="0.8em"
    Font-Underline="False" ForeColor="#333333" />
<PartChromeStyle BorderColor="#E2DED6" BorderStyle="Solid" BorderWidth="1px" />
<PartStyle BorderColor="#F7F6F3" BorderWidth="5px" />
<FooterStyle BackColor="#E2DED6" HorizontalAlign="Right" />
<EditUIStyle Font-Names="Verdana" Font-Size="0.8em" ForeColor="#333333" />
<InstructionTextStyle Font-Size="0.8em" ForeColor="#333333" />
<ErrorStyle Font-Size="0.8em" />
<VerbStyle Font-Names="Verdana" Font-Size="0.8em" ForeColor="#333333" />
<EmptyZoneTextStyle Font-Size="0.8em" ForeColor="#333333" />
<PartTitleStyle Font-Bold="True" Font-Size="0.8em" ForeColor="#333333" />
</asp:EditorZone>
</td>
<td valign="top" align="right" style="width: 312px">
<asp:CatalogZone ID="CatalogZone1" runat="server"
    Height="122px" BackColor="#F7F6F3"
    BorderColor="#CCCCCC" BorderWidth="1px" Font-Names="Verdana" Padding="6">
<ZoneTemplate>
<asp:PageCatalogPart ID="PageCatalogPart1" runat="server">
</asp:PageCatalogPart>
<asp:DeclarativeCatalogPart ID="DeclarativeCatalogPart1" runat="server">
</asp:DeclarativeCatalogPart>
</ZoneTemplate>
<HeaderVerbStyle Font-Bold="False" Font-Size="0.8em"
    Font-Underline="False" ForeColor="#333333" />
<PartTitleStyle BackColor="#5D7B9D" Font-Bold="True"
    Font-Size="0.8em" ForeColor="White" />
<FooterStyle BackColor="#E2DED6" HorizontalAlign="Right" />
<PartChromeStyle BorderColor="#E2DED6" BorderStyle="Solid" BorderWidth="1px" />
<InstructionTextStyle Font-Size="0.8em" ForeColor="#333333" />
<LabelStyle Font-Size="0.8em" ForeColor="#333333" />
<PartLinkStyle Font-Size="0.8em" />
<SelectedPartLinkStyle Font-Size="0.8em" />
<VerbStyle Font-Names="Verdana" Font-Size="0.8em" ForeColor="#333333" />
<HeaderStyle BackColor="#E2DED6" Font-Bold="True"
    Font-Size="0.8em" ForeColor="#333333" />
<EmptyZoneTextStyle Font-Size="0.8em" ForeColor="#333333" />
<EditUIStyle Font-Names="Verdana" Font-Size="0.8em" ForeColor="#333333" />
<PartStyle BorderColor="#F7F6F3" BorderWidth="5px" />
</asp:CatalogZone>
</td>
</tr>
</table>
```

添加清单 7.1 中所示的代码后，Web 页面将如图 ASP-7.7 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_634_0.png)

图 ASP-7.7

- 14. *双击*“浏览”链接按钮，并将以下突出显示的代码片段*添加*到 Default.aspx 页面的 **代码隐藏** 文件中：

```csharp
protected void LinkButton1_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.BrowseDisplayMode;
}
```

在突出显示的代码片段中，我们通过使用 **WebPartManager** 类的 **BrowseDisplayMode** 属性，将 **WebPartManager1** 的显示模式更改为 **浏览**。

- 15. *双击*“编辑”链接按钮，并在代码隐藏文件中*添加*以下突出显示的代码片段：

```csharp
protected void LinkButton2_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.EditDisplayMode;
}
```

在突出显示的代码片段中，我们通过使用 **WebPartManager** 的 **EditDisplayMode** 属性，将 **WebPartManager1** 的显示模式更改为 **编辑**。

- 16. *双击*“目录”链接按钮，并将以下突出显示的代码片段*添加*到 **代码隐藏** 文件中：

```csharp
protected void LinkButton3_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.CatalogDisplayMode;
}
```

在突出显示的代码片段中，我们通过使用 **WebPartManager** 类的 **CatalogDisplayMode** 属性，将 **WebPartManager1** 的显示模式更改为 **目录**。

- 17. *双击*“设计”链接按钮，并将以下突出显示的代码片段*添加*到 **代码隐藏** 文件中：

```csharp
protected void LinkButton4_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.DesignDisplayMode;
}
```

在突出显示的代码片段中，我们通过使用 **WebPartManager** 类的 **DesignDisplayMode** 属性，将 **WebPartManager1** 的显示模式更改为 **设计**。

- 18. *添加*以下命名空间到 Default.aspx.cs 页面。

```csharp
using System.Web.UI.WebControls.WebParts;
```

- 19. *设置* Default.aspx 页面为 Web 站点中的起始页。

- 20. *按* F5 键获得输出，如图 ASP-7.8 所示。

- 21. *单击* **我的日历** 控件右上角的下指箭头（图 ASP-7.9）。

- 22. *选择* **关闭** 选项（图 ASP-7.9）。

![](img/9862a98a1a2d3bb14334137965a1ec60_635_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_635_1.png)

- 23. *单击* **目录**链接，如图 ASP-7.10 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_636_0.png)

图 ASP-7.10

**CatalogZone** 控件将出现（图 ASP-7.10）。

- 24. 从 **页面目录** 窗格中*选择* **MyCalendar** 复选框（图 ASP-7.11）。然后，从 **添加到** 下拉列表中*选择* **WebPartZone1**（图 ASP-7.11）。

- 25. *单击* **添加** 按钮，如图 ASP-7.11 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_636_1.png)

图 ASP-7.11

单击“添加”按钮后，**MyCalendar** 控件会立即添加到 **Default.aspx** 页面中，如图 ASP-7.12 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_636_2.png)

图 ASP-7.12
