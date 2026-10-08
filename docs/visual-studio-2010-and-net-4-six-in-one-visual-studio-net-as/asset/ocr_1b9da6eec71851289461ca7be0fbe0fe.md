drop it into the page. Then, select the GridView and the SqlDataSource control, and move it into the grey content placeholder of the UpdatePanel. If you prefer to do it in markup, here is the code that designer generates:

![](bbox=[0.095, 0.183, 0.148, 0.223])

```
<asp:ScriptManager runat="server" />
<asp:UpdatePanel runat="server" id="up">
  <ContentTemplate>
    <asp:GridView runat="server"
      DataSourceID="NorthwindDS"
      AllowPaging="True" PageSize="30"
      AllowSorting="True" />
    <asp:SqlDataSource ID="NorthwindDS" runat="server"
      ConnectionString="<%# ConnectionStrings.Northwind %>"
      SelectCommand="SELECT SELECT [CompanyName], [ContactName] FROM [Customers]" />
  </ContentTemplate>
</asp:UpdatePanel>
```

Code file [2-ServerControls\Default.aspx] available for download at Wrox.com

As you can see, there is nothing special in it. The UpdatePanel is a server-side control with a ContentTemplate element that can contain any additional controls, and controls are automatically Ajax-enabled by the UpdatePanel. You can build and try it in a browser, and you will see the more user-friendly behavior of the page.

To enhance your experience, you can drag an UpdateProgress control onto the page and enter any text as its content. Then, do not forget to go to the Properties window and select the AssociatedUpdatePanel property to point to the previously used UpdatePanel, or do it in markup like this:

![](bbox=[0.095, 0.636, 0.148, 0.676])

```
<asp:UpdateProgress runat="server" AssociatedUpdatePanelID="up">
  <ProgressTemplate>
    Refreshing...
  </ProgressTemplate>
</asp:UpdateProgress>
```

Code file [2-ServerControls\Default.aspx] available for download at Wrox.com

If you try it now, the UpdateProgress is not displayed, the response from the server returns quickly. You can simulate network latency or slow response rendering by adding the following to the Page_Load event handler on the server:

![](bbox=[0.095, 0.82, 0.148, 0.86])

```
protected void Page_Load(object sender, EventArgs e)
{
    System.Threading.Thread.Sleep(3000);
}
```

Code file [2-ServerControls\Default.aspx] available for download at Wrox.com