tag enables you to customize the control's appearance too, so you can produce other results, as shown in Figure 22-9.

![](bbox=[0.09, 0.14, 0.66, 0.33])

FIGURE 22-9

The code for this version of the SiteMapPath control is as follows:

```
<asp:SiteMapPath ID="SitePath1" runat="server" Font-Names="Verdana" Font-Size="0.8em" PathSeparator=" : ">
  <CurrentNodeStyle ForeColor="#333333" />
  <NodeStyle Font-Bold="True" ForeColor="#284E98" />
  <PathSeparatorStyle Font-Bold="True" ForeColor="#507CD1" />
  <RootNodeStyle Font-Bold="True" ForeColor="#507CD1" />
</asp:SiteMapPath>
```

Code snippet from magazines_us.aspx

This example illustrates that a lot of style elements and attributes can be used with the SiteMapPath control. Many options at your disposal enable you to create breadcrumb navigation that is unique.

# Menu Server Control

Another navigation control enables end users of your application to navigate throughout the pages based upon information stored within the web.sitemap file. The Menu server control produces a compact navigation system that pops up sub-options when the user hovers the mouse over an option. The result of the Menu server control when bound to the site map is shown in Figure 22-10.

![](bbox=[0.09, 0.69, 0.66, 0.88])

FIGURE 22-10

To see this, examine the Web Form named magazines_eur.aspx. It has both a Menu and a SiteMapDataSource control on the page: