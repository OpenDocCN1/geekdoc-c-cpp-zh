```
<asp:SiteMapDataSource ID="SiteMapDataSource1" runat="server" />
<asp:Menu ID="Menu1" runat="server" DataSourceID="SiteMapDataSource1">
</asp:Menu>
```

Code snippet from magazines_eur.aspx

The SiteMapDataSource control automatically works with the application’s web.sitemap file and the Menu control to bind to the SiteMapDataSource (just like a GridView can bind to a SqlDataSource). Like many of the other visual controls in ASP.NET, you can easily modify the appearance of the Menu control by clicking the Auto Format link in the control’s smart tag. Choosing Classic produces the result shown in Figure 22-11.

![](bbox=[0.145, 0.26, 0.71, 0.455])

# FIGURE 22-11

As with the other controls, a lot of sub-elements contribute to the changed look of the control’s style:

```
<asp:Menu ID="Menu1" runat="server" DataSourceID="SiteMapDataSource1"
BackColor="#B5C7DE" DynamicHorizontalOffset="2" Font-Names="Verdana"
Font-Size="0.8em" ForeColor="#284E98" StaticSubMenuIndent="10px">
<DynamicHoverStyle BackColor="#284E98" ForeColor="White" />
<DynamicMenuItemStyle HorizontalPadding="5px" VerticalPadding="2px" />
<DynamicMenuStyle BackColor="#B5C7DE" />
<DynamicSelectedStyle BackColor="#507CD1" />
<StaticHoverStyle BackColor="#284E98" ForeColor="White" />
<StaticMenuItemStyle HorizontalPadding="5px" VerticalPadding="2px" />
<StaticSelectedStyle BackColor="#507CD1" />
</asp:Menu>
```

Code snippet from magazines_eur.aspx

# WORKING WITH THE ASP.NET PROVIDER MODEL

Ever since the beginning days of ASP.NET, users wanted to be able to store sessions by means other than the three traditional storage modes: InProc, StateServer, and SQLServer. One such request was for a new storage mode that could store sessions in an Oracle database. This might seem like a logical thing to add, but if the team added a storage mode for Oracle they would soon get requests to add additional modes for other databases and data storage methods. For this reason, instead of building storage modes for specific scenarios, the ASP.NET team made the system extensible by designing a plugable provider model that enables anyone to add new modes as needed.

In addition to session state, there are several other features included in ASP.NET that require state storage of some kind. In addition, instead of recording state in a fragile mode (the way sessions are stored by default), many of these features require their state to be stored in more concrete data stores such as databases or XML files. This also enables a longer-lived state for the users visiting an application — something else that is required by these new systems.