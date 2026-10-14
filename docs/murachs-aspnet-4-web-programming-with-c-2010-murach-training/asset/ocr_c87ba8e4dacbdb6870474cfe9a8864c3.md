# A drop-down list bound to an ObjectDataSource control

![](bbox=[0.15, 0.1, 0.43, 0.18])

# The code for the drop-down list and the ObjectDataSource control

```
<asp:DropDownList ID="ddlCategories" runat="server" AutoPostBack="True"
    DataSourceID="ObjectDataSource1"
    DataTextField="ShortName"
    DataValueField="CategoryID">
</asp:DropDownList>
<asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
    TypeName="ProductDB"
    SelectMethod="GetAllCategories">
</asp:ObjectDataSource>
```

# The GetAllCategories method of the ProductDB class

```
[DataObjectMethod(DataObjectMethodType.Select)]
public static IEnumerable GetAllCategories()
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string sel = "SELECT CategoryID, LongName "
        + "FROM Categories ORDER BY LongName";
    SqlCommand cmd = new SqlCommand(sel, con);
    con.Open();
    SqlDataReader dr = cmd.ExecuteReader(CommandBehavior.CloseConnection);
    return dr;
}
```

# Basic attributes of the ObjectDataSource control

| Attribute | Description |
|---|---|
| ID | The ID of the control. |
| Runat | Must specify "server." |
| TypeName | The name of the data access class. |
| SelectMethod | The name of the method that retrieves the data. |
| UpdateMethod | The name of the method that updates the data. |
| DeleteMethod | The name of the method that deletes the data. |
| InsertMethod | The name of the method that inserts the data. |
| DataObjectTypeName | The name of a class that provides properties that are used to pass parameter values. |
| ConflictDetection | Specifies how concurrency conflicts will be detected. CompareAllValues uses optimistic concurrency checking. OverwriteValues, which is the default, does no concurrency checking. |

# Description

+   - The ObjectDataSource control specifies the name of the data access class and the methods used to select, update, delete, and insert data.