
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

After adding the code shown in Listing 7.1, your Web page appears, as shown in Fig.ASP-7.7:

![](img/9862a98a1a2d3bb14334137965a1ec60_634_0.png)

Fig.ASP-7.7

- 14. *Double-click* the Browse link button and *add* the following highlighted code snippet to the **code-behind** file of the Default.aspx page:

```csharp
protected void LinkButton1_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.BrowseDisplayMode;
}
```

In the highlighted code snippet, we are changing the display mode of **WebPartManager1** to **Browse** by using the **BrowseDisplayMode** property of the **WebPartManager** class.

- 15. *Double-click* the Edit link button and *add* the following highlighted code snippet in the code-behind file:

```csharp
protected void LinkButton2_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.EditDisplayMode;
}
```

In the highlighted code snippet, we are changing the display mode of **WebPartManager1** to Edit by using the **EditDisplayMode** property of **WebPartManager**.

- 16. *Double-click* the Catalog link button and *add* the following highlighted code snippet to the **code-behind** file:

```csharp
protected void LinkButton3_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.CatalogDisplayMode;
}
```

In the highlighted code snippet, we are changing the display mode of **WebPartManager1** to Catalog by using the **CatalogDisplayMode** property of **WebPartManager** class.

- 17. *Double-click* the Design link button and *add* the following highlighted code snippet to the **code-behind** file:

```csharp
protected void LinkButton4_Click(object sender, EventArgs e)
{
    WebPartManager1.DisplayMode = WebPartManager.DesignDisplayMode;
}
```

In the highlighted code snippet, we are changing the display mode of **WebPartManager1** to Design by using the **DesignDisplayMode** property of the **WebPartManager** class.

- 18. *Add* the following namespace in the Default.aspx.cs page.

```csharp
using System.Web.UI.WebControls.WebParts;
```

- 19. *Set* the Default.aspx page as the start page in the Web site.

- 20. *Press* the F5 key to get the output, as shown in Fig.ASP-7.8.

- 21. *Click* the down-pointed arrow placed at the top-right corner of the **My Calendar** control (Fig.ASP-7.9).

- 22. *Select* the **Close** option (Fig.ASP-7.9).

![](img/9862a98a1a2d3bb14334137965a1ec60_635_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_635_1.png)

- 23. *Click* the **Catalog** link, as shown in Fig.ASP-7.10:

![](img/9862a98a1a2d3bb14334137965a1ec60_636_0.png)

Fig.ASP-7.10

The **CatalogZone** control appears (Fig.ASP-7.10).

- 24. *Select* the **MyCalendar** check box from the **Page Catalog** pane (Fig.ASP-7.11). Then, *select* **WebPartZone1** from the **Add to** drop-down list (Fig.ASP-7.11).

- 25. *Click* the **Add** button, as shown in Fig.ASP-7.11:

![](img/9862a98a1a2d3bb14334137965a1ec60_636_1.png)

Fig.ASP-7.11

As soon as you click the Add button, the **MyCalendar** control is added to the **Default.aspx** page, as shown in Fig.ASP-7.12:

![](img/9862a98a1a2d3bb14334137965a1ec60_636_2.png)

Fig.ASP-7.12
