# The starting dialog box of the Data Source Configuration Wizard

![](bbox=[0.124, 0.095, 0.628, 0.39])

# Aspx code generated for a basic SqlDataSource control

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
    ConnectionString="<%$ ConnectionStrings:HalloweenConnectionString %>"
    SelectCommand="SELECT [CategoryID], [LongName] FROM [Categories]
        ORDER BY [LongName]">
</asp:SqlDataSource>
```

# Basic SqlDataSource control attributes

| Attribute | Description |
|---|---|
| ID | The ID for the SqlDataSource control. |
| Runat | Must specify "server." |
| ConnectionString | The connection string. In most cases, you should use a <%$ expression to specify the name of a connection string saved in the web.config file (see figure 13-4). |
| ProviderName | The name of the provider used to access the database. Values can be System.Data.Odbc, System.Data.OleDb, System.Data.OracleClient, or System.Data.SqlClient. The default is System.Data.SqlClient. |
| SelectCommand | The SQL Select statement executed by the data source to retrieve data. |

# Description

+   - To create a SqlDataSource control, drag the control from the Data group of the Toolbox onto the form. Then, choose Configure Data Source from the control’s smart tag menu and proceed from there.
+   - You can also create a SQL data source using the Choose Data Source command in the smart tag menu of a bindable control. When you use this command, the dialog box shown above is displayed. Then, you can select the Database icon and proceed from there.