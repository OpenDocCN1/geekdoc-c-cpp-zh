
Implements `System.Web.UI.ICallEventHandler`

' 代码在此处...

End Class

这要求你实现一组方法——`RaiseCallbackEvent` 和 `GetCallbackResult` 方法，这两个方法都与客户端脚本请求协作。`RaiseCallbackEvent` 允许你执行从页面获取值的操作，但值只能是 `string` 类型：

```vb
Public Sub RaiseCallbackEvent(ByVal argument As String)
Implements System.Web.UI.ICallbackEventHandler.RaiseCallbackEvent
_callbackResult = R.ToString()
End Sub
```

...（后续略）...

由于 .NET Framework 2.0、3.5 和 4 浏览器都支持此功能：
```vb
If (Page.Request.SupportsXmlHttp) Then
    ' 执行逻辑
End If
```

使用带参数的回调函数：
```javascript
function GetTemp() {
  var zipcode = document.forms[0].TextBox1.value;
...
}
```

# 客户端回调

```vb
Dim ws As New Weather.TemperatureService
_callbackResult = ws.getTemp(eventArgument).ToString()
End Sub
Public Function GetCallbackResult() As String
Implements System.Web.UI.ICallEventHandler.GetCallbackResult
Return _callbackResult
End Function
End Class
```

# C# 代码

```csharp
using System;
using System.Data;
using System.Configuration;
using System.Collections;
using System.Web;
using System.Security;
using System.Web.UI;
using System.Web.UI.Controls;
using System.Web.UI.Controls.WebParts;
using System.Web.UI.HtmlControls;
public partial class WSCallback : System.Web.UI.Page,
System.Web.UI.ICallbackEventHandler
{
    private string _callbackResult = null;
    protected void Page_Load(object sender, EventArgs args)
    {
        string cbReference = Page.Client.GetCallbackReference(this,
            "arg","GetTempServer","context");
        string cbScript = "function UseCallback(arg, context) " +
            "('" + cbReference + "', arg, context + '\');";
        Page.Client.RegisterScriptBlock(this.GetType(),
            "UseCallback", cbScript, true);
    }
    public void RaiseCallbackEvent(string eventArg)
    {
        Weather.TemperatureService ws = new Weather.TemperatureService();
        _callbackResult = ws.getTemp(eventArg).ToString();
    }
    public string GetCallbackResult()
    {
        return _callbackResult;
    }
}
```

文件名 `WSCallback.aspx`、`WSCallback.aspx.vb` 和 `WSCallback.aspx.cs`

你在此页代码列表中没有看到的是，它引用了一个理论上的远程 Web 服务，该服务根据用户提供的邮政编码向应用程序返回最新的天气信息。

![](img/7040c21013b8e6c23c612d6da3599ff8_136_0.png)

- * 有更多关于在 ASP.NET 应用程序中使用 Web 服务的信息，请参阅第 31 章。

生成并运行此页面后，你将得到如图 2-14 所示的结果。

## 第 2 章 ASP.NET 控件和客户端脚本

![](img/7040c21013b8e6c23c612d6da3599ff8_137_0.png)

图 2-14

客户端回调功能的主要区别在于，此示例发送了一个必要的参数。这是在页面的 `.aspx` 部分的 `GetTemp()` JavaScript 函数中实现的：

```javascript
function GetTemp() {
    var zipcode = document.forms[0].TextBox.value;
    UseCallback(zipcode, __);
}
```

该 JavaScript 函数显示了用户输入到 `TextBox` 中的邮编，并将其值置于名为 `zipcode` 的变量，该变量作为参数通过 `UseCallback()` 方法发送。

此示例与上一个示例一样，在不进行完整页面刷新的情况下更新页面。

# 使用回调功能 —— 一个更复杂的示例

到为止，你已经看到了使用回调功能拉回单个项目，以及根据传递给引擎的单个参数拉回整个对象的示例。下一个示例更进一步，根据提供的参数拉回结果集。

此示例适用于 SQL Server 中的 Northwind 数据库实例。对于此示例，请创建一个包含 `TextBox` 服务器端控件和按钮的单页。在下方放置一个表格，该表格将根据文本框中提供的客户 ID 填充客户详情。相应的 `.aspx` 页面见列表 2-17。

## 列表 2-17：一个用于连接上一个示例 CustomerID 的 ASP.NET 页面

### .aspx 页面

```asp
<%@ Language="VB" AutoEventWire="false"
CodeFile="Default.aspx.vb" Inherits="_Default" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Customer Details</title>
<script type="text/javascript">
function GetCustomer(customerCode) {
    var customerCode = document.forms[0].TextBox.value;
    UseCallback(customerCode, __);
}
```
```javascript
function GetCustomerDetailsFromServer(result, context) {
    var i = result.split("*");
    customerID.innerHTML = i[0];
    companyName.innerHTML = i[1];
    contactName.innerHTML = i[2];
    contactTitle.innerHTML = i[3];
    address.innerHTML = i[4];
    city.innerHTML = i[5];
    region.innerHTML = i[6];
    postalcode.innerHTML = i[7];
    country.innerHTML = i[8];
    phone.innerHTML = i[9];
    fax.innerHTML = i[10];
}
</script>
<body>
<form id="form" runat="server">
<<div>
<asp:TextBox id="TextBox1"&nbsp;>
<input id="Button" type="button" value="Get Customer Details" onclick="GetCustomer()" /><br />
<table cellspacing="0" cellpadding="4" rules="all" border="1">
<tr>
<td id="customerID"></</td>
</tr>
<tr>
<td id="companyName"></</td>
</tr>
<tr>
<td id="contactName"></</td>
</tr>
<tr>
<td id="contactTitle"></</td>
</tr>
<tr>
<td id="address"></</td>
</tr>
<tr>
<td id="city"></</td>
</tr>
<tr>
<td id="region"></</td>
</tr>
<tr>
<td id="postalcode"></</td>
</tr>
<tr>
<td id="country"></</td>
</tr>
<tr>
<td id="phone"></</td>
</tr>
<tr>
<td id="fax"></</td>
</tr>
</table>
</div>
</form>
</body>
</html>
```

```vb
Dim MyValues(10) As String
```
```vb
While MyReader.Read()
MyValues(0) = MyReader("CustomerID").ToString()
MyValues(1) = MyReader("CompanyName").ToString()
MyValues(2) = MyReader("ContactName").ToString()
MyValues(3) = MyReader("ContactTitle").ToString()
MyValues(4) = MyReader("Address").ToString()
MyValues(5) = MyReader("City").ToString()
MyValues(6) = MyReader("Region").ToString()
MyValues(7) = MyReader("PostalCode").ToString()
MyValues(8) = MyReader("Country").ToString()
MyValues(9) = MyReader("Phone").ToString()
MyValues(10) = MyReader("Fax").ToString()
End
```
```vb
_callbackResult = String.Join("*", MyValues)
```
```vb
Protected Sub Page_Load(ByVal sender As Object
```
```csharp
using System;
using System.Data;
using System.Configuration;
using System.Collections;
using System.Web;
using System.Web.Security;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Web.UI.WebControls.Parts;
using System.Web.UI.HtmlControls;
using System.Data.SqlClient;
```
```csharp
public class ClassCallbackNorth : System.Web.UI.Page
```

## 第 2 章 ASP.NET 服务器控件与客户端脚本

## 示例 2-18（续）

```csharp
#region ICallbackEventHandler
public string GetCallbackResult()
{
    return _callbackResult;
}
public void RaiseCallbackEvent(string eventArgument)
{
    SqlConnection conn = new
    SqlConnection("Data Source=.;.;Initial Catalog=Northwind;User ID=sa");
    SqlCommand cmd = new
    SqlCommand("Select * From Customers Where CustomerID=' + +
    eventArgument + "*", conn);
conn.Open();
SqlDataReader Reader = cmd.ExecuteReader();
MyReader = MyExecuteReader(CommandBehavior.CloseConnection);
string[] Values = new string[11];
while (Reader.Read())
{
    Values[0] = Reader("CustomerID").ToString();
    Values[1] = Reader("CustomerName").ToString();
    Values[2] = Reader("ContactName").ToString();
    Values[3] = Reader("ContactTitle").ToString();
    Values[4] = Reader("AddressLine1").ToString();
    Values[5] = Reader("City").ToString();
    Values[6] = Reader("Region").ToString();
    Values[7] = Reader("PostalCode").ToString();
    Values[8] = Reader("Country").ToString();
    Values[9] = Reader("Phone").ToString();
    Values[10] = Reader("Fax").ToString();
}
string _callbackresult = String.Join(",", Values);
#endregion
```
