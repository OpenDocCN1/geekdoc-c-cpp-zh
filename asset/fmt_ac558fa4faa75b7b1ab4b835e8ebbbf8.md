
```
SELECT [CategoryID], [ShortName], [LongName]
    FROM [Categories]

DELETE FROM [Categories]
    WHERE [CategoryID] = @original_CategoryID
      AND [ShortName] = @original_ShortName
      AND [LongName] = @original_LongName

UPDATE [Categories]
    SET [ShortName] = @ShortName,
        [LongName] = @LongName
    WHERE [CategoryID] = @original_CategoryID
      AND [ShortName] = @original_ShortName
      AND [LongName] = @original_LongName

INSERT INTO [Categories]
    ([CategoryID], [ShortName], [LongName])
    VALUES (@CategoryID, @ShortName, @LongName)
```

这里，`Where` 子句通过查找具有原始检索值的行来实现乐观并发。然后，aspx 代码中的 `DeleteParameters`、`UpdateParameters` 和 `InsertParameters` 元素定义了这些语句使用的参数。

最后，此图的 part 3 显示了用于输入新类别数据的输入控件。如你所见，每个文本框都由一个必填字段验证器验证，确保用户已为该字段输入数据。此验证在用户点击 Add New Category 按钮时执行。此外，每个文本框都编码了 `MaxLength` 属性，以便用户不能输入超过数据源中关联列允许的字符数。

## `Default.aspx` 文件

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Chapter 14: Category Maintenance</title>
    <link href="Main.css" rel="stylesheet" type="text/css" />
</head>
<body>
    <form id="form1" runat="server">
        <div id="page">
            <div id="header">
                <asp:Image ID="Image1" runat="server" ImageUrl="~/Images/banner.jpg" />
            </div>
            <div id="main">
                <h1>Category Maintenance</h1>
                <asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False" DataKeyNames="CategoryID" DataSourceID="SqlDataSource1" ForeColor="Black">
                    <Columns>
                        <asp:BoundField DataField="CategoryID" HeaderText="ID" ReadOnly="True" >
                            <HeaderStyle HorizontalAlign="Left" />
                            <ItemStyle Width="100px" />
                        </asp:BoundField>
                        <asp:BoundField DataField="ShortName" HeaderText="Short Name">
                            <HeaderStyle HorizontalAlign="Left" />
                            <ItemStyle Width="150px" />
                        </asp:BoundField>
                        <asp:BoundField DataField="LongName" HeaderText="Long Name">
                            <HeaderStyle HorizontalAlign="Left" />
                            <ItemStyle Width="200px" />
                        </asp:BoundField>
                        <asp:CommandField ButtonType="Button" CausesValidation="False" ShowEditButton="True" />
                        <asp:CommandField ButtonType="Button" CausesValidation="False" ShowDeleteButton="True" />
                    </Columns>
                    <HeaderStyle BackColor="Gray" Font-Bold="True" ForeColor="White" />
                    <RowStyle BackColor="White" ForeColor="Black" />
                    <AlternatingRowStyle BackColor="#F5F5F5" ForeColor="Black" />
                    <EditRowStyle BackColor="#F46D11" ForeColor="White" />
                </asp:GridView>
            </div>
        </div>
    </form>
</body>
</html>
```

## 注释

- `GridView` 控件绑定到 `SqlDataSource1` 数据源。

- `Columns` 元素包含子元素定义了五个列。其中三个为绑定字段；另外两个为命令按钮。

## The `Default.aspx` file

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
    ConflictDetection="CompareAllValues"
    ConnectionString="<%= ConnectionStrings:HalloweenConnectionString %>"
    OldValuesParameterFormatString="original_{0}"
    SelectCommand="SELECT [CategoryID], [ShortName], [LongName] FROM [Categories]"
    DeleteCommand="DELETE FROM [Categories] WHERE [CategoryID] = @original_CategoryID AND [ShortName] = @original_ShortName AND [LongName] = @original_LongName"
    InsertCommand="INSERT INTO [Categories] ([CategoryID], [ShortName], [LongName]) VALUES (@CategoryID, @ShortName, @LongName)"
    UpdateCommand="UPDATE [Categories] SET [ShortName] = @ShortName, [LongName] = @LongName WHERE [CategoryID] = @original_CategoryID AND [ShortName] = @original_ShortName AND [LongName] = @original_LongName">
    <DeleteParameters>
        <asp:Parameter Name="original_CategoryID" Type="String" />
        <asp:Parameter Name="original_ShortName" Type="String" />
        <asp:Parameter Name="original_LongName" Type="String" />
    </DeleteParameters>
    <InsertParameters>
        <asp:Parameter Name="CategoryID" Type="String" />
        <asp:Parameter Name="ShortName" Type="String" />
        <asp:Parameter Name="LongName" Type="String" />
    </InsertParameters>
    <UpdateParameters>
        <asp:Parameter Name="ShortName" Type="String" />
        <asp:Parameter Name="LongName" Type="String" />
        <asp:Parameter Name="original_CategoryID" Type="String" />
        <asp:Parameter Name="original_ShortName" Type="String" />
        <asp:Parameter Name="original_LongName" Type="String" />
    </UpdateParameters>
</asp:SqlDataSource>
```

## Notes

- The `Select` statement retrieves all rows in the `Categories` table.

- The `Where` clauses in the `Delete` and `Update` statements provide for optimistic concurrency.

```
<p id="new">To create a new category, enter the category information and click Add New Category.</p>
<p>
<asp:Label ID="lblError" runat="server" EnableViewState="False" CssClass="error">
</asp:Label>
</p>
<p class="label">ID:</p>
<p class="entry">
<asp:TextBox ID="txtID" runat="server" Width="100" MaxLength="10">
</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" ControlToValidate="txtID" CssClass="error" ErrorMessage="ID is a required field.">
</asp:RequiredFieldValidator>
</p>
<p class="label">Short Name:</p>
<p class="entry">
<asp:TextBox ID="txtShortName" runat="server" Width="200" MaxLength="15">
</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server" ControlToValidate="txtShortName" CssClass="error" ErrorMessage="Short Name is a required field.">
</asp:RequiredFieldValidator>
</p>
<p class="label">Long Name:</p>
<p class="entry">
<asp:TextBox ID="txtLongName" runat="server" Width="200" MaxLength="50">
</asp:TextBox>&nbsp;
<asp:RequiredFieldValidator ID="RequiredFieldValidator3" runat="server" ControlToValidate="txtLongName" CssClass="error" ErrorMessage="Long Name is a required field.">
</asp:RequiredFieldValidator>
</p>
<p>
<asp:Button ID="btnAdd" runat="server" Text="Add New Category" OnClick="btnAdd_Click" />
</p>
</div>
</div>
</form>
</body>
</html>
```

## Notes

- The text boxes are used to enter data for a new row.

- The required field validators ensure that the user enters data for each column of a new row.

## The code-behind file

Although it would be nice if you could create a robust database application without writing any C# code, you must still write code to insert data into a `GridView` control and to catch and handle any database or concurrency errors that might occur. Figure 14-14 shows this code for the Category Maintenance application.

As you can see, this code-behind file consists of just three methods. The first, `btnAdd_Click`, sets the values of the three insert parameters to the values entered by the user. Then, it calls the `Insert` method of the data source control. If an exception is thrown, an appropriate error message is displayed.

The second method, `GridView1_RowUpdated`, is called after a row has been updated. This method checks the `Exception` property of the `e` argument to determine if an exception has been thrown. If so, an error message is displayed, the `ExceptionHandled` property is set to True to suppress the exception, and the `KeepInEditMode` property is set to True to leave the `GridView` control in edit mode. If an exception hasn’t occurred, the `e` argument’s `AffectedRows` property is checked. If it’s zero, it means that a concurrency error has occurred and an appropriate message is displayed.
