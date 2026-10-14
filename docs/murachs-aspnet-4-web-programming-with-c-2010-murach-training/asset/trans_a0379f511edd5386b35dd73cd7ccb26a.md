

## SqlDataSource 类用于插入行的方法和属性

| 方法 | 描述 |
|---|---|
| Insert() | 执行为数据源定义好的 Insert 命令。 |
| 属性 | 描述 |
| InsertCommand | 要执行的 Insert 命令。 |
| InsertParameters["name"] | 具有指定名称的参数。 |

## Parameter 类用于插入行的属性

| 属性 | 描述 |
|---|---|
| DefaultValue | 参数的默认值。如果未为参数分配其他值，则使用此值。 |

## 使用 SqlDataSource 控件插入行的代码

```
protected void btnAdd_Click(object sender, EventArgs e)
{
    SqlDataSource1.InsertParameters["CategoryID"].DefaultValue
        = txtID.Text;
    SqlDataSource1.InsertParameters["ShortName"].DefaultValue
        = txtShortName.Text;
    SqlDataSource1.InsertParameters["LongName"].DefaultValue
        = txtLongName.Text;
    try
    {
        SqlDataSource1.Insert();
        txtID.Text = "";
        txtShortName.Text = "";
        txtLongName.Text = "";
    }
    catch (Exception ex)
    {
        lblError.Text = "A database error has occurred. " +
            "Message: " + ex.Message;
    }
}
```

## 描述

- GridView 控件不支持插入操作，但你可以使用 GridView 的数据源向数据库中插入行。执行后，新行将自动显示在 GridView 控件中。
- 为了提供插入功能，页面应包含文本框等控件供用户输入数据，以及用户可以点击以插入数据的按钮。
- 要使用 SqlDataSource 控件插入数据库行，首先将每个插入参数的 DefaultValue 属性设置为你想要插入的值。然后，调用 Insert 方法。
- 如果发生 SQL 错误，Insert 方法可能会抛出 SqlException。异常最可能的原因是主键约束冲突。

Figure 14-11   如何在 GridView 控件中插入一行

## 使用 GridView 控件的维护应用程序

为了让你更好地了解如何使用 GridView 控件更新、删除和插入数据，以下主题介绍了一个维护 Halloween 数据库中 Categories 表的应用程序。

## Category Maintenance 应用程序

Figure 14-12 向你介绍了 Category Maintenance 应用程序。它允许用户在 Halloween 数据库的 Categories 表中更新、删除和插入行。这里，使用 GridView 控件显示 Categories 表中的行以及 Edit 和 Delete 按钮。在此图中，用户已点击第三个数据行的 Edit 按钮，将该行置于编辑模式。

在 GridView 控件下方，三个文本框允许用户输入新类别的数据。然后，如果用户点击 Add New Category 按钮，这些文本框中输入的数据将被用于向数据库添加一个类别行。虽然从此图看不出来，但每个文本框都使用了必填字段验证器。此外，GridView 控件下方还有一个标签控件，用于在更新、删除或插入操作失败时显示错误消息。

## Category Maintenance 应用程序

![](img/c024ccf88e28c30c07dd410d4342288f_486_0.png)

## 描述

- Category Maintenance 应用程序使用 GridView 控件让用户更新或删除 Categories 表中的行。
- 要编辑类别，用户点击 Edit 按钮。这会将 GridView 控件置于编辑模式。用户可以更改 Short Name 或 Long Name 然后点击 Update。或者，用户可以点击 Cancel 退出编辑模式。
- 要删除类别，用户点击 Delete 按钮。
- 用户可以通过在 GridView 控件下方的文本框中输入数据并点击 Add New Category 按钮来向表中添加类别。
- 如果用户尝试更新或添加某一列为空的行，将显示错误消息。

Figure 14-12  Category Maintenance 应用程序

## aspx 文件

Figure 14-13 显示了此应用程序的完整 aspx 列表。由于大部分代码已经介绍过，我只指出几个重点。

此图的 Part 1 显示了 GridView 控件的 aspx 代码。它指定数据源为 SqlDataSource1，数据的<|message|> 为 CategoryID。Columns 元素中定义的五个列显示了来自数据源的三个列、一个 Edit 按钮和一个 Delete 按钮。

此图的 Part 2 显示了 SqlDataSource 控件。请注意，此数据源包含 ConflictDetection 和 OldValuesParameterFormatString 属性。ConflictDetection 属性指示如何处理更新和删除操作。默认情况下，此属性设置为 CompareAllValues，这意味着将执行乐观并发检查。OldValuesParameterFormatString 属性指示用于保存原始列值的参数名称的格式。默认情况下，此属性设置为 original_{0}，这意味着每个原始参数的名称将包含列名前缀为“original_”。

由于这两个属性值，以下语句用于检索、删除、更新和插入类别行：

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

这里，Where 子句通过查找具有原始检索值的行来实现乐观并发。然后，aspx 代码中的 DeleteParameters、UpdateParameters 和 InsertParameters 元素定义了这些语句使用的参数。

最后，此图的 part 3 显示了用于输入新类别数据的输入控件。如你所见，每个文本框都由一个必填字段验证器验证，确保用户已为该字段输入数据。此验证在用户点击 Add New Category 按钮时执行。此外，每个文本框都编码了 MaxLength 属性，以便用户不能输入超过数据源中关联列允许的字符数。

## Default.aspx 文件

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

- GridView 控件绑定到 SqlDataSource1 数据源。
- Columns 元素包含子元素定义了五个列。其中三个为绑定字段；另外两个为命令按钮。

