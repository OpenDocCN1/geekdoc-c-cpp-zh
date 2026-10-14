# A menu with vertical orientation

![](bbox=[0.155, 0.095, 0.48, 0.185])

# A menu with horizontal orientation

![](bbox=[0.155, 0.22, 0.55, 0.295])

# Typical aspx code for a Menu control

```
<asp:Menu ID="Menu1" Orientation="Horizontal" runat="server"
    DataSourceID="SiteMapDataSource1">
</asp:Menu>
```

# Common attributes of the Menu control

| Attribute | Description |
|---|---|
| ID | The ID of the control. |
| runat | Must specify "server". |
| DataSourceID | The ID of the SiteMapDataSource control the menu should be bound to. |
| IncludeStyleBlock | If True, the CSS that formats the menu is included in a style element in the rendered HTML. If False, no style element is generated. The default is True. |
| ItemWrap | If True, words in the menu items will be word-wrapped if necessary. The default is False. |
| MaximumDynamicDisplay | The number of levels of dynamic submenus to display. |
| Orientation | Horizontal or Vertical. The default is Vertical. |
| StaticDisplayLevels | The number of levels that should always be displayed. The default is 1. |
| StaticEnableDefaultPopOutImage | If True, an arrow graphic is displayed next to any menu item that has a pop-out submenu. If false, the arrow graphic is not displayed. The default is True. |

# Description

+   - The Menu control displays site navigation information in a menu. Submenus automatically appear when the user hovers the mouse over a menu item that has a submenu.
+   - To display an application’s navigation structure, the Menu control must be bound to a SiteMapDataSource control.
+   - The Menu control has many formatting attributes that aren’t listed in this figure. You can quickly apply a coordinated set of formatting attributes by clicking the Smart Tag icon for the Menu control and choosing Auto Format from the menu that appears. Then, you can select one of several predefined schemes for the menu.