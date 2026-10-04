
# 256 | CHAPTER 7 NAVIGATION

2. Between the opening and closing tags of the control, add the following <LevelStyles> element:

<LevelStyles>
<asp:TreeNode CssClass="FirstLevelMenuItems" />
</LevelStyles>

The FirstLevelMenuItems class selector is defined by the file Grey.css that you added in the preceding chapter and is used to create some room above each item at the first level.

3. Switch to Design View, click the TreeView once, and click the small arrow to orient the Smart Tasks panel. From the Choose Data source dropdown, select MapDataSource, the data source you created for the Menu control (see Figure 7-9).

![](img/9e033e3b9560597824f8b22941d6d8bb_293_0.png)

FIGURE 7-9

As soon as you select the data source, the TreeView is updated in Design View; it now shows the correct menu items from the site map.

4. Open the Properties Grid for the TreeView and set the ShowExpandCollapse property to False.

5. Click somewhere in the document to put the focus on it, and then press F7 to open the Code Behind the Page_Load event that you used earlier to preselect the theme in the Theme list. Right below that code, and before the end of the method, add the following code that shows or hides the TreeView and Menu controls on the currently active theme:

VB.NET

```
item.Selected = True
End If
End If
End If
Select Case Page.Theme.ToLower()
    Case "darkgrey"
        Menu.Visible = False
        TreeView.Visible = True
    Case Else
        Menu.Visible = True
        TreeView.Visible = False
End Select
End Sub
```

# C#

```sharp
item.Selected = true;
}
switch (Page.Theme.ToLower())
{
    case "darkgrey":
        Menu1.Visible = false;
        TreeView1.Visible = true;
        break;
    default:
        Menu1.Visible = true;
        TreeView1.Visible = false;
        break;
}
```

6. Save all changes and open Default.aspx in the browser. Depending on your current theme, you should either see the Menu or the TreeView control. Select a different theme from the list and the page will reload, showing the other control as a navigation system of the website (see Figure 7-10).

![](img/9e033e3b9560597824f8b22941d6d8bb_294_0.png)

FIGURE 7-10

> COMMON MISTAKES If you get an error from the code in the BasePage class that checks the title, make sure you set a valid theme in the <pages> element in the Web.config file. If the theme is switched when you move from one page to another, make sure your pages inherit BasePage, which should be the case if you based the new pages on your custom template.

# How It Works

Just like the Menu control, the TreeView control can get its data from a SiteMapDataSource control, which in turn gets its information from the Web sitemap. By default, the TreeView shows plus and minus signs to indicate that items can be collapsed and expanded. For a site this may not make sense, so by setting ShowExpand to False, you effectively hide the images. The TreeView enables you to set a number of style properties, including the NodeStyle, RootNodeStyle, and LevelStyles that influence the appearance of individual items in the tree. In this exercise, you used LevelStyles to apply a class FirstMenuItems that adds some room above each item at the top level, such as Home and Reviews.

The code in the Backend of the manager page looks at the current node by investigating the Theme property of the Page. When DarkGrey is the current theme, the code hides the Menu and displays the TreeView. In the Case Else / default the reverse is true. This means that for Monochrome theme the TreeView is hidden and the Menu is used instead as the navigation system.

The TreeView suffers from the same problems as the Menu control in previous versions of ASP.NET that it generates a lot of bloated HTML. Unfortunately, this control has no RenderingMode property, so if you're using the TreeView you're stuck with the table-based HTML.

With two of the navigation controls discussed, the final control you need to look at is the SiteMapPath control.

# Using the SiteMapPath Control

The SiteMapPath control shows where you are in the site's structure. It presents itself as a series of links, often referred to as a breadcrumb. It's a pretty yet powerful control with more than 50 public properties you can set through the Properties Grid to influence the way it looks. Just like the Menu and TreeView, it has a number of style properties you use to change the look of elements like the current node, a normal node, and the path separator.

The following table lists a few of the most common properties of the SiteMapPath control.

| PROPERTY | DESCRIPTION |
| --- | --- |
| PathDirection | Supports two values: RootToCurrent and CurrentToRoot. The first setting shows the root element on the left, intermediate levels in the middle, and the current page at the right of the path. The CurrentToRoot setting is the exact opposite, where the current page is shown at the left of the breadcrumb path. |
| PathSeparator | Defines the symbol or text to show between the different elements of the path. The default is the "greater than" (>), but you can change it to something like the pipe character (|). |

# RenderCurrentNodeLink

Determines whether the last element of the path (current page) is rendered as a text link or as plaintext. The default is False, which is usually fine because you are already on the page that element is representing, so there's no need for a link.

# ShowToolTips

Determines whether the control displays tooltips (retrieved from the description attribute of the siteMapNode elements in the Web.itemap file) when the user hovers over the elements in the path. The default is True, which means the tooltips are shown by default.

Depending on your personal preferences, you don't need to define any of the styles of the SiteMap control. In the final page in the browser, the SiteMap consists of many anchor tags <a> and plaintext. If you have set up a selector for anchors in your CSS file, the SiteMap automatically shows in one line with the others of the page.

# TRY OUT Creating a Breadcrumb with the SiteMap Control

A good location for the SiteMapPath is the global map page of the site. That way it becomes visible in all your pages. 1. Open Default.aspx in the browser. Depending on your current theme, you should either see the Menu or the TreeView control. Select a different theme from the list and the page will reload, showing the other control as a navigation system of the website (see Figure 7-10).

![](img/9e033e3b9560597824f8b22941d6d8bb_294_0.png)

> COMMON MISTAKES If you get an error from the code in the BasePage class that checks the title, make sure you set a valid theme in the <pages> element in the Web.config file. If the theme is switched when you move from one page to another, make sure your pages inherit BasePage, which should be the case if you based the new pages on your custom template.

# How It Works

Just like the Menu control, the TreeView control can get its data from a SiteMapDataSource control, which in turn gets its information from the Web sitemap. By default, the TreeView shows plus and minus signs to indicate that items can be collapsed and expanded. For a site this may not make sense, so by setting ShowExpand to False, you effectively hide the images. The TreeView enables you to set a number of style properties, including the NodeStyle, RootNodeStyle, and LevelStyles that influence the appearance of individual items in the tree. In this exercise, you used LevelStyles to apply a class FirstMenuItems that adds some room above each item at the top level, such as Home and Reviews.

The code in the Backend of the manager page looks at the current node by investigating the Theme property of the Page. When DarkGrey is the current theme, the code hides the Menu and displays the TreeView. In the Case Else / default the reverse is true. This means that for Monochrome theme the TreeView is hidden and the Menu is used instead as the navigation system.

The TreeView suffers from the same problems as the Menu control in previous versions of ASP.NET that it generates a lot of bloated HTML. Unfortunately, this control has no RenderingMode property, so if you're using the TreeView you're stuck with the table-based HTML.

With two of the navigation controls discussed, the final control you need to look at is the SiteMapPath control.

# Using the SiteMapPath Control

The SiteMapPath control shows where you are in the site's structure. It presents itself as a series of links, often referred to as a breadcrumb. It's a pretty yet powerful control with more than 50 public properties you can set through the Properties Grid to influence the way it looks. Just like the Menu and TreeView, it has a number of style properties you use to change the look of elements like the current node, a normal node, and the path separator.

The following table lists a few of the most common properties of the SiteMapPath control.

| PROPERTY | DESCRIPTION |
| --- | --- |
| PathDirection | Supports two values: RootToCurrent and CurrentToRoot. The first setting shows the root element on the left, intermediate levels in the middle, and the current page at the right of the path. The CurrentToRoot setting is the exact opposite, where the current page is shown at the left of the breadcrumb path. |
| PathSeparator | Defines the symbol or text to show between the different elements of the path. The default is the "greater than" (>), but you can change it to something like the pipe character (|). |

# RenderCurrentNodeLink

Determines whether the last element of the path (current page) is rendered as a text link or as plaintext. The default is False, which is usually fine because you are already on the page that element is representing, so there's no need for a link.

# ShowToolTips

Determines whether the control displays tooltips (retrieved from the description attribute of the siteMapNode elements in the Web.itemap file) when the user hovers over the elements in the path. The default is True, which means the tooltips are shown by default.

Depending on your personal preferences, you don't need to define any of the styles of the SiteMap control. In the final page in the browser, the SiteMap consists of many anchor tags <a> and plaintext. If you have set up a selector for anchors in your CSS file, the SiteMap automatically shows in one line with the others of the page.

# TRY OUT Creating a Breadcrumb with the SiteMap Control

A good location for the SiteMapPath is the global map page of the site. That way it becomes visible in all your pages. 1. Open Default.aspx in the browser. Depending on your current theme, you should either see the Menu or the TreeView control. 

```html
<div id="ContentPlaceHolder1">
</div>
<br />
<asp:SiteMapPath ID="SiteMapPath1" runat="server">
</asp:SiteMapPath>
</br>
<br />
<asp:SiteMapPath ID="SiteMapPath1" runat="server">
</asp:SiteMapPath>
```
