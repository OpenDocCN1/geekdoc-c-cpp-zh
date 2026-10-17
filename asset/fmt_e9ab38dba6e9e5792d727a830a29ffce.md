
第一个方法`Purge`是一个私有方法，它检查`shoutList`变量中的喊话并删除任何过旧的喊话。它首先将一个名为`purgeTime`的变量设置为当前时间，然后减去三分钟。此变量用于确定喊话的显示时长。

接下来，`Purge`方法使用`while`语句确定喊话列表中是否有任何项超过三分钟。该语句的条件会导致循环对`shoutList`变量中的每个项执行。虽然你可能认为这里可以使用`foreach`语句，但你不能使用。因为在循环执行时喊话列表正在被更新。因此，你必须使用带有索引变量的`while`循环来手动跟踪喊话列表中的当前位置。

在`while`循环内部，当前喊话项的`Timestamp`属性与`purgeTime`变量进行比较。然后，如果时间戳小于或等于清除时间，则喊话项会从喊话列表中删除。在这种情况下，索引不会更新，因为被删除项之后的元素会向上移动。如果喊话项未从列表中删除，则索引变量会增加一，以便可以检查下一个项。

公共`Add`方法将传递给它的喊话项添加到喊话列表的开头。但首先，它调用`Purge`方法以删除任何旧的喊话项。此外，它执行当前线程的`Sleep`方法，将`Add`方法延迟两秒。我加入此方法是为了确保`UpdateProgress`控件被显示。当然，你不会想在生产应用程序中包含此类代码。

公共`Display`方法返回一个包含喊话框内容的文本字符串。与`Add`方法一样，它首先调用`Purge`方法。然后，它创建一个`StringBuilder`对象来存储喊话框文本。

如果喊话列表包含至少一个项，`Display`方法会继续将一个`<dl>`标签添加到`StringBuilder`对象。此标签定义一个定义列表，可包含格式化的文本项列表。然后，它使用`foreach`循环将每个喊话项的信息添加到此列表中。在这种情况下，用户名称

## `ShoutItem.cs` 文件

```
using System;

public class ShoutItem
{
    public string UserName { get; set; };
    public DateTime Timestamp { get; set; };
    public string Comment { get; set; };
}
```

## `ShoutItemList.cs` 文件

```
using System;
using System.Collections.Generic;
using System.Text;

public class ShoutItemList
{
    private List<ShoutItem> shoutList = new List<ShoutItem>();

    private void Purge() {
        DateTime purgeTime = DateTime.Now;
        purgeTime = purgeTime.AddMinutes(-3);
        int i = 0;
        while (i < shoutList.Count)
        {
            if (shoutList[i].Timestamp <= purgeTime)
                shoutList.RemoveAt(i);
            else
                i += 1;
        }
    }

    public void Add(ShoutItem shout) {
        Purge();
        System.Threading.Thread.Sleep(2000);
        shoutList.Insert(0, shout);
    }

    public string Display() {
        Purge();
        StringBuilder shoutBoxText = new StringBuilder();
        if (shoutList.Count > 0)
        {
            shoutBoxText.AppendLine("<dl>");
            foreach (ShoutItem shout in shoutList)
            {
                shoutBoxText.Append("<dt>" + shout.UserName + " (");
                shoutBoxText.Append(shout.Timestamp.ToShortTimeString() + ")");
                shoutBoxText.Append("</dt>");
                shoutBoxText.AppendLine("<dd>" + shout.Comment + "</dd>");
            }
            shoutBoxText.AppendLine("</dl>");
        }
        return shoutBoxText.ToString();
    }
}
```

## `Default.aspx` 文件

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">

    <title>Chapter 21: Product List with AJAX Shout Box</title>

    <link href="Main.css" rel="stylesheet" type="text/css" />

</head>

<body>

    <form id="form1" runat="server">

    <div id="page">

    <div id="header">

        <asp:Image ID="Image1" runat="server" ImageUrl="~/Images/banner.jpg" />

    </div>

    <div id="main">

        <p>Choose a category:&nbsp;

            <asp:DropDownList ID="Category" runat="server" AutoPostBack="True" Width="130px" DataSourceID="SqlDataSource1" DataTextField="LongName" DataValueField="CategoryID">

            </asp:DropDownList>

            <asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="<%$ ConnectionStrings:HalloweenConnectionString %>" SelectCommand="SELECT [CategoryID], [LongName] FROM [Categories] ORDER BY [LongName]">

            </asp:SqlDataSource>

        </p>

        <div id="datalist">

            <asp:DataList ID="ddlProducts" runat="server" DataKeyField="ProductID" DataSourceID="SqlDataSource2" CellPadding="3" GridLines="Vertical">

            <HeaderTemplate>

                <table>

                    <tr>

                        <td class="col1">ID</td>

                        <td class="col2">Product</td>

                        <td class="col3">Unit Price</td>

                        <td class="col4">On Hand</td>

                    </tr>

                </table>

            </HeaderTemplate>

<ItemTemplate>

<table>

<tr>

<td class="col1">

<asp:Label ID="lblID" runat="server"

Text='<%# Eval("ProductID") %>' />

</td>

<td class="col2">

<asp:Label ID="lblName" runat="server"

Text='<%# Eval("Name") %>' />

</td>

<td class="col3">

<asp:Label ID="lblUnitPrice" runat="server"

Text='<%# Eval("UnitPrice", "{0:C}") %>' />

</td>

<td class="col4">

<asp:Label ID="lblOnHand" runat="server"

Text='<%# Eval("OnHand") %>' />

</td>

</tr>

</table>

</ItemTemplate>

<AlternatingItemStyle BackColor="#CCCCCC" />

<HeaderStyle BackColor="Black" Font-Bold="True" ForeColor="White" />

</asp:DataList>

<asp:SqlDataSource ID="SqlDataSource2" runat="server"

ConnectionString="<%$ ConnectionStrings:HalloweenConnectionString %>"

SelectCommand="SELECT [ProductID], [Name], [UnitPrice], [OnHand]

FROM [Products]

WHERE ([CategoryID] = @CategoryID)

ORDER BY [ProductID]">

<SelectParameters>

<asp:ControlParameter Name="CategoryID" Type="String"

ControlID="Category" PropertyName="SelectedValue" />

</SelectParameters>

</asp:SqlDataSource>

</div>

<div id="shoutbox">

<asp:ScriptManager ID="ScriptManager1" runat="server">

</asp:ScriptManager>

<p>Here's what everyone is saying:</p>

<p>

<asp:UpdatePanel ID="ShoutBoxPanel1" runat="server">

<ContentTemplate>

<asp:Label ID="lblShoutBox" runat="server"></asp:Label>

<asp:Timer ID="Timer1" runat="server" Interval="5000">

</asp:Timer>

</ContentTemplate>

<Triggers>

<asp:AsyncPostBackTrigger ControlID="btnAddShout"

EventName="Click" />

</Triggers>

</asp:UpdatePanel>

</p>

<p>

    <asp:UpdatePanel ID="ShoutBoxPanel2" runat="server" UpdateMode="Conditional">

        <ContentTemplate>

            <p class="label">Name:</p>

            <p class="entry">

                <asp:TextBox ID="txtUserName" runat="server" MaxLength="15" Width="100px"></asp:TextBox>

                <asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" ErrorMessage="Name is required." ControlToValidate="txtUserName" Display="Dynamic" CssClass="error">

                </asp:RequiredFieldValidator>

            </p>

            <p class="label">Shout:</p>

            <p class="entry">

                <asp:TextBox ID="txtShout" runat="server" MaxLength="255" Width="220px"></asp:TextBox>

                <asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server" ErrorMessage="Shout is required." ControlToValidate="txtShout" Display="Dynamic" CssClass="error">

                </asp:RequiredFieldValidator>

            </p>

            <asp:Button ID="btnAddShout" runat="server" Text="Add Shout" />

            <asp:UpdateProgress ID="UpdateProgress1" runat="server" DynamicLayout="False">

                <ProgressTemplate>

                    <img src="Images/spinner.gif" alt="Please Wait" />

                    Uploading Comment...

                </ProgressTemplate>

            </asp:UpdateProgress>

        </ContentTemplate>

    </asp:UpdatePanel>

</p>

    </div>

    </div>

</div>

</form>

</body>

</html>
```
