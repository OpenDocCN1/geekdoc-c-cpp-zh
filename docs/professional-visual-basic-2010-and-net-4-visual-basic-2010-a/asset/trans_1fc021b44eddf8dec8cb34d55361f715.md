

```
Public Class NorthwindService
    Public Function GetCountryNames() As String()
        Dim dc As New NorthwindDataContext
        Dim query = From cust In dc.Customers
                    Select cust.Country Distinct
                    Order By Country
        Return query.ToArray()
    End Function

    Public Function GetCustomersByCountry(ByVal country As String) As CustomerDto()
        Dim dc As New NorthwindDataContext
        Dim query = From cust In dc.Customers
                    Where cust.Country = country
                    Select New CustomerDto With {
                        .CustomerID = cust.CustomerID,
                        .CompanyName = cust.CompanyName,
                        .ContactName = cust.ContactName,
                        .ContactTitle = cust.ContactTitle,
                        .OrderCount = cust.Orders.Count
                    }
        Return query.ToArray()
    End Function
End Class
```

来自 Service\NorthwindService.vb 的代码片段

接下来展示的是 Web 服务的代码（Client.NorthwindService），请注意它只是将调用委托给服务实现类：

```
Imports System.Web.Services
Imports System.Web.Services.Protocols
Imports System.ComponentModel

<System.Web.Script.Services.ScriptService()>
<System.Web.Services.WebService(Namespace:="http://mycompany.com/Northwind")>
<System.Web.Services.WebServiceBinding(ConformsTo:=WsiProfiles.BasicProfile1_1)>
<ToolboxItem(False)>
Public Class NorthwindService
    Inherits System.Web.Services.WebService

    <WebMethod()>
    Public Function CountryNames() As String()
        Dim svc As New Service.NorthwindService()
        Return svc.GetCountryNames()
    End Function

    <WebMethod()>
    Public Function GetCustomersByCountry(ByVal country As String) As Service.CustomerDto()
        Dim svc As New Service.NorthwindService()
        Return svc.GetCustomersByCountry(country)
    End Function
End Class
```

来自 Client\NorthwindService.asmx.vb 的代码片段

最后，这里展示了页面的标记（Client.Demo01-NoAjax）。它使用 ObjectDataSource 控件与 Web 服务通信以获取数据，并使用标准数据绑定来填充 DropDownList 和 GridView 控件：

```
<%@ Page Language="vb" AutoEventWireup="false" CodeBehind="Demo01-NoAjax.aspx.vb" Inherits="Client.Demo01_NoAjax" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" >
<head id="Head1" runat="server">
<title>No Ajax</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:ObjectDataSource ID="ObjectDataSource1" runat="server" SelectMethod="CountryNames" TypeName="Client.NorthwindService">
</asp:ObjectDataSource>
<asp:DropDownList ID="DropDownList1" runat="server" DataSourceID="ObjectDataSource1" AutoPostBack="True">
</asp:DropDownList>
<br /><br />
<asp:ObjectDataSource ID="ObjectDataSource2" runat="server" SelectMethod="GetCustomersByCountry" TypeName="Client.NorthwindService">
<SelectParameters>
<asp:ControlParameter ControlID="DropDownList1" Name="country" PropertyName="SelectedValue" Type="String" />
</SelectParameters>
</asp:ObjectDataSource>
<asp:GridView ID="GridView1" runat="server" AutoGenerateColumns="False" DataSourceID="ObjectDataSource2">
<Columns>
<asp:BoundField DataField="CustomerID" HeaderText="Customer ID" SortExpression="CustomerID" />
<asp:BoundField DataField="CompanyName" HeaderText="Company Name" SortExpression="CompanyName" />
<asp:BoundField DataField="ContactName" HeaderText="Contact Name" SortExpression="ContactName" />
<asp:BoundField DataField="ContactTitle" HeaderText="Contact Title" SortExpression="ContactTitle" />
<asp:BoundField DataField="OrderCount" HeaderText="Order Count" SortExpression="OrderCount" />
</Columns>
</asp:GridView>
</div>
</form>
</body>
</html>
```

来自 Client\Demo01-NoAjax.aspx 的代码片段

图 22-30 显示了 Demo01-NoAjax.aspx 页面运行时的情况。无法通过图像捕捉到的是，每当用户选择一个新国家时都会发生一次全页回发。然而，你可以使用 Fiddler（www.fiddlertool.com）之类的跟踪工具看到服务器的通信情况。图 22-31 显示了上窗格中的请求（1,590 字节）和下窗格中的响应（4,374 字节）。

![](img/d99870e80390742f93963da7be0b2e61_784_0.png)

**图 22-30**

![](img/d99870e80390742f93963da7be0b2e61_784_1.png)

**图 22-31**

## 添加 UpdatePanel 控件

当前实现的一个缺点是，包含国家的下拉列表的标记会在每次响应中发送，即使国家列表很少变化。当从列表中选择一个国家时，你真正需要更新的只是包含客户数据的网格。

前面提到的 UpdatePanel 控件使你能够非常轻松地做到这一点。UpdatePanel 以及其余的 Microsoft Ajax 框架允许进行*局部页面呈现*。换句话说，你可以指定页面上希望在用户交互发生时更新的部分，而页面的其余部分保持不变。额外的好处是，此过程将异步进行，因此在更新进行时页面保持响应。要实现此目标，你需要使用 UpdatePanel 的属性来指示哪些控件的哪些事件将触发异步回发而不是常规的全页回发。

在我们的示例中，我们希望将 GridView 控件包装在 UpdatePanel 中，并指示 DropDownList 控件上的 SelectedIndexChanged 事件应导致异步回发。为此，将 ScriptManager 控件添加到页面的顶部，然后更新包含 GridView 标记的部分页面（或创建修改后的副本），使其看起来像来自 Demo02-UpdatePanel.aspx 页面的这样：

```
```aspx
<asp:ScriptManager ID="ScriptManager1" runat="server">
</asp:ScriptManager>

<asp:ObjectDataSource ID="ObjectDataSource1" runat="server"
    SelectMethod="CountryNames" TypeName="Client.NorthwindService">
</asp:ObjectDataSource>
<asp:DropDownList ID="DropDownList1" runat="server"
    DataSourceID="ObjectDataSource1" AutoPostBack="True">
</asp:DropDownList>
<br /><br />

<asp:ObjectDataSource ID="ObjectDataSource2" runat="server"
    SelectMethod="GetCustomersByCountry"
    TypeName="Client.NorthwindService">
    <SelectParameters>
        <asp:ControlParameter ControlID="DropDownList1"
            Name="country"
            PropertyName="SelectedValue" Type="String" />
    </SelectParameters>
</asp:ObjectDataSource>
<asp:UpdatePanel ID="UpdatePanel1" runat="server">
<ContentTemplate>
    <asp:GridView ID="GridView1" runat="server"
        AutoGenerateColumns="False"
        DataSourceID="ObjectDataSource2">
        <Columns>
            <asp:BoundField DataField="CustomerID" HeaderText="Customer ID"
                SortExpression="CustomerID" />
            <asp:BoundField DataField="CompanyName" HeaderText="Company Name"
                SortExpression="CompanyName" />
            <asp:BoundField DataField="ContactName" HeaderText="Contact Name"
                SortExpression="ContactName" />
            <asp:BoundField DataField="ContactTitle" HeaderText="Contact Title"
                SortExpression="ContactTitle" />
            <asp:BoundField DataField="OrderCount" HeaderText="Order Count"
                SortExpression="OrderCount" />
        </Columns>
    </asp:GridView>
</ContentTemplate>
<Triggers>
    <asp:AsyncPostBackTrigger ControlID="DropDownList1"
        EventName="SelectedIndexChanged" />
</Triggers>
</asp:UpdatePanel>
```
```

> 来自 Client\Demo02-UpdatePanel.aspx 的代码片段

图 22-32 显示了页面运行时的情况。在这种情况下，当选择一个新国家时，页面会异步回发到服务器，并且页面生命周期会运行，但只有网格的标记会被发送到客户端。查看图 22-33 中的跟踪，你可以看到请求与之前几乎相同（1,668 字节），但响应明显更小（2,625 字节）。

