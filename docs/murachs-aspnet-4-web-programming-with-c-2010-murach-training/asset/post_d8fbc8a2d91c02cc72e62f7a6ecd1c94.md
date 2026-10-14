
## How to use the Menu control

Figure 10-6 shows how to use the Menu control, which lets you create menus that are arranged either vertically or horizontally. *Vertical menus* are usually used in a sidebar alongside the content placeholder in a master page. In contrast, *horizontal menus* typically appear beneath a banner image and above the content placeholder.

Each item in a menu can contain a submenu that appears when you hover the mouse over the item for a moment. For example, the Service and Support submenu shown in the examples in this figure doesn’t appear until you hover the mouse over the Service and Support item. The part of the menu that is always displayed is called the *static menu*. Submenus that appear when you hover the mouse over a menu item are called *dynamic menus*.

Like the TreeView control, the Menu control must be bound to a site map data source. Then, the other attributes in this figure let you customize the appearance of the menu and specify which items will appear in the menu. For example, the Orientation attribute determines whether the menu is arranged vertically or horizontally. And the MaximumDynamicDisplayLevels attribute determines how many layers of dynamic submenus should be displayed.

The IncludeStyleBlock attribute is new with ASP.NET 4. The value of this attribute determines whether a style element with the CSS that’s used to format the menu is generated. If you set the value of this attribute to False, you can then customize the appearance of the menu by coding your own CSS. The easiest way to do that is to display the page in a browser with the value of this attribute set to True. Then, you can display the HTML for the page, copy the generated CSS, paste it into an external style sheet, and modify it any way you like.

As you set the properties for a Menu control, you’ll see that it includes many style properties that aren’t listed in this figure. You can set these properties to control the formatting that’s used to display the menu. The best way to do that is to define a skin for the control as shown in the next chapter.

Alternatively, you can automatically apply a predefined scheme to the menu by selecting Auto Format from the Menu control’s smart tag menu. When you select a scheme, Visual Studio generates attributes and style elements that apply the formatting that you selected. Then, you can customize these attributes and elements any way you like. You’ll see an example of this when I show you the aspx code for the master page of the Navigation application later in this chapter.

### A menu with vertical orientation

![](img/c024ccf88e28c30c07dd410d4342288f_368_0.png)

### A menu with horizontal orientation

![](img/c024ccf88e28c30c07dd410d4342288f_368_1.png)

### Typical ASPX code for a Menu control

```aspx
<asp:Menu ID="Menu1" Orientation="Horizontal" runat="server"
    DataSourceID="SiteMapDataSource1">
</asp:Menu>
```

### Common attributes of the Menu control

| Attribute | Description |
|---|---|
| ID | The ID of the control. |
| runat | Must specify "server". |
| DataSourceID | The ID of the SiteMapDataSource control the menu should be bound to. |
| IncludeStyleBlock | If True, the CSS that formats the menu is included in a style element in the rendered HTML. If False, no style element is generated. The default is True. |
| ItemWrap | If True, words in the menu items will be word-wrapped if necessary. The default is False. |
| MaximumDynamicDisplayLevels | The number of levels of dynamic submenus to display. |
| Orientation | Horizontal or Vertical. The default is Vertical. |
| StaticDisplayLevels | The number of levels that should always be displayed. The default is 1. |
| StaticEnableDefaultPopOutImage | If True, an arrow graphic is displayed next to any menu item that has a pop-out submenu. If False, the arrow graphic is not displayed. The default is True. |

### Description

- The Menu control displays site navigation information in a menu. Submenus automatically appear when the user hovers the mouse over a menu item that has a submenu.
- To display an application’s navigation structure, the Menu control must be bound to a SiteMapDataSource control.
- The Menu control has many formatting attributes that aren’t listed in this figure. You can quickly apply a coordinated set of formatting attributes by clicking the Smart Tag icon for the Menu control and choosing Auto Format from the menu that appears. Then, you can select one of several predefined schemes for the menu.

## How to use the SiteMapPath control

Figure 10-7 shows how to use the SiteMapPath control, which creates a series of links that lead from the application’s home page to the current page. These links are sometimes called *bread crumbs* because they let the user find his or her way back to the home page.

Unlike the TreeView and Menu controls, the SiteMapPath control doesn’t need to be bound to a data source. Instead, it obtains the site navigation information directly from the web.sitemap file.

The attributes listed in this figure let you customize the appearance of the SiteMapPath control. In particular, you can indicate how many parent nodes to list, which direction the nodes are listed in, what text to use to separate the nodes, and whether the current page should be formatted as a link or just plain text.

Although this figure doesn’t show it, the SiteMapPath control includes other attributes that let you completely customize the appearance of the site map path. Like the Menu control, you’re more likely to use a skin to apply this formatting. Or, you can use the Auto Format command to apply a predefined scheme.

### A SiteMapPath control

```
Home > Service and Support > Site Map
```

### ASPX code for a SiteMapPath control

```aspx
<asp:SiteMapPath ID="SiteMapPath1" runat="server">
</asp:SiteMapPath>
```

### Common attributes of the SiteMapPath control

| Attribute | Description |
|---|---|
| ID | The ID of the control. |
| runat | Must specify "server". |
| ParentLevelsDisplayed | The maximum number of parent nodes to display. The default is -1, which displays all parent nodes. |
| PathDirection | Indicates the order in which nodes should be listed. Allowable values are RootToCurrent and CurrentToRoot. The default is RootToCurrent. |
| PathSeparator | The string displayed between each node of the path. The default is a greater-than sign. |
| RenderCurrentNodeAsLink | Set to True if you want the node that represents the current page to be rendered as a link. The default is False. |

### Description

- The SiteMapPath control displays a list of the links for each node in the site map from the root node to the current page.
- Unlike the TreeView and Menu controls, you don’t need to bind the SiteMapPath control to a data source. Instead, it automatically uses the web.sitemap file to determine the current page’s position within the web site’s navigation structure.

## A master page for the Navigation application

To show you how the navigation controls work together, figure 10-8 presents the body of a master page that includes both a navigation menu and a site map path. This is the master page that was shown in figure 10-1.

Like the master page you saw in the last chapter, the content for this master page is divided into three divisions. The first division contains an Image control that displays a banner at the top of the page. Then, the second division contains a Menu control and a SiteMapDataSource control. Because of the way the CSS for this division is defined, it’s displayed down the left side of the page below the banner. Finally, the third division contains a SiteMapPath control that’s displayed below the banner, followed by a content placeholder. In figure 10-1, a Site Map page is displayed within the content placeholder.

Notice also that the asp:Menu element includes several style elements that specify the appearance of the menu. These elements were generated by Visual Studio when I selected a scheme for the menu. In the next chapter, you’ll see how you can apply formatting like this using skins. In addition to these style elements, several attributes were added to the Menu control. However, I replaced these attributes with a CSS style rule that provides for the same formatting.

In addition, this master page uses a code-behind file named Site.master.cs that displays a message in the label at the bottom of the page. Since this code-behind file is the same as the one presented in chapter 9, it’s not repeated here.
