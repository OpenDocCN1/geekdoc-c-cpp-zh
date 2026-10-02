
## WebMethod 属性

在列表 13-5 中，`Customers` 类只有一个 `WebMethod`。`WebService` 类可以包含任意数量的 `WebMethod`，或者是标准方法与通过声明前的属性启用的 `WebMethod` 方法的混合。可以跨 HTTP 线路访问的方法仅是你应用了 `WebMethod` 属性的方法。

与 `WebService` 属性一样，`WebMethod` 可以包含一些属性，如下列表所示：

- **BufferResponse**: 当设置为 `True` 时，来自 XML Web 服务的响应将保存在内存中并作为完整包发送。如果设置为 `False`（默认设置），则响应在服务器上构建时发送给客户端。
- **CacheDuration**: 指定响应被缓存之前的秒数。默认设置为 `0`，意味着禁用缓存。将 XML Web 服务的响应放入缓存中可以提高 Web 服务的性能。
- **Description**: 为 WebMethod 应用文本描述，该描述将出现在 XML 服务的 .aspx 测试页面上。
- **EnableSession**: 将 `EnableSession` 设置为 `True` 可为特定的 WebMethod 启用会话状态。默认设置为 `False`。
- **Name**: 为 WebMethod 分配唯一的名称。如果你正在处理重载的 WebMethod（本章稍后会讨论），则此步骤是必须的。
- **TransactionOption**: 指定 WebMethod 的事务支持。默认设置为 `TransactionOption`。如果 WebMethod 是启动事务的根对象，则 Web 服务可以参与到另一个需要事务的 WebMethod 事务中。其他可能的值还包括 `NotSupported`、`Supported`、`Required` 和 `RequiredNew`。

## XML Web 服务接口

来自列表 13-5 的 Customers Web 服务只有一个 WebMethod，它返回一个包含来自 SQL Server AdventureWorks 数据库的完整 Customers 表格的 DataSet。

在浏览器中运行 `Customers.asmx` 会打开 ASP.NET Web 服务测试页面。这个你的 Web 服务的可视化界面实际上用于测试目的，或者作为对你所提供的 Web 服务感兴趣开发者的参考页面。图 13-3 显示为 Customers.asmx Web 服务 GetCustomers WebMethod 生成的页面。

![](img/67a6707ff505c052edb96c0128fb3096_511_0.png)

图 13-3

界面在页面顶部的蓝色条（在此黑白图像中为深色条）显示了 Web 服务的名称。默认情况下，除非你之前定义的通过 `WebService` 属性的 `Description` 属性更改了值，否则将使用类名称。页面会显示指向整个 Web 服务 WebMethod 的链接符号列表。此示例只有一个 WebMethod：GetCustomers。

还可以提供指向 Web 服务服务描述语言（WSDL）文档的链接（该链接在图中标题为“Service Description”）。WSDL 文件是与 Customers Web 服务交互的实际接口。XML 文档（如图 13-4 所示）并不是为了人类阅读的；它被设计用于与 Visual Studio 等工具配合工作，告知工具消费该 Web 服务需要什么。每个 Web 服务都需要一个具有特定类型参数的请求。当发出请求时，Web 服务响应将返回一组使用特定数据类型定义的特定数据。请求所需的所有内容以及你在响应中确切获得的返回内容列表（如果你是调用者）都在 WSDL 文档中进行了描述。

## 构建一个简单的 XML 服务

图 13-4

点击 GetCustomers 链接将为你提供一个新页面（如图 13-5 所示），该页面不仅详细描述了 WebMethod，还允许你直接在浏览器中测试该 WebMethod。

![](img/67a6707ff505c052edb96c0128fb3096_512_0.png)

图 13-5

页面顶部是 XML Web 服务的名称（Customers）；下方是此特定 WebMethod 的名称（GetCustomers）。页面显示了消费该 WebMethod 所需的 SOAP 消息结构，以及用于响应的 SOAP 消息结构。在 SOAP 示例下面使用 HTTP Post（带有键值对）消费 XML Web 服务的示例。这种不使用 SOAP 的方法调用方式是可能的。

你可以直接从该页面测试 WebMethod。在 Test 部分，你会发现一个表单。如果你调用的 WebMethod 需要输入参数来获取响应，你将看到文本框，这样你可以在点击 Invoke 按钮之前提供参数。如果你调用的 WebMethod 不需要任何参数，你只会看到 Invoke 按钮，而没有其他内容。

点击 Invoke 实际上是向 Web 服务发送一个 SOAP 请求，导致出现一个带有结果的新浏览器实例，如图 13-6 所示。

## 第 13 章 使用服务

![](img/67a6707ff505c052edb96c0128fb3096_513_0.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Dataset xmlns="http://schemas.microsoft.com/xmlworks/dataset" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" id="NewDataSet">
  <element name="Customers">
    <complex name="CustomerID" minOccurs="0" type="string"/>
    <complex name="ContactName" minOccurs="0" type="string"/>
    <complex name="ContactTitle" minOccurs="0" type="string"/>
    <complex name="Company" minOccurs="0" type="string"/>
    <complex name="City" minOccurs="0" type="string"/>
    <complex name="Phone" minOccurs="0" type="string"/>
    <complex name="AddressLine1" minOccurs="0" type="string"/>
    <complex name="AddressLine2" minOccurs="0" type="string"/>
    <complex name="State" minOccurs="0" type="string"/>
    <complex name="PostalCode" minOccurs="0" type="string"/>
    <complex name="Country" minOccurs="0" type="string"/>
    <complex name="Fax" minOccurs="0" type="string"/>
    <complex name="HomePhone" minOccurs="0" type="string"/>
    <complex name="LastModified" minOccurs="0" type="System.DateTime;assembly=System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>
  </element>
  <diff xmlns="http://schemas.microsoft.com/xmlworks/dataset">
    <table name="Customers">
      <row>
        <cell name="CustomerID" value="A Bike"/>
      </row>
    </table>
  </diff>
</Dataset>
```

图 13-6

现在一切都就绪了，可以暴露 XML 服务，你可以在 ASP.NET 中消费它。

## 消费 XML 服务

到为止，你只看到了 Web 服务故事的一半。将数据和逻辑通过 SOAP 跨企业或全球暴露是一项简单的任务，特别是在 ASP.NET 中。另一半是 XML 服务的实际消费。ASP.NET 应用。

## 添加 Web 引用

要消费我们在在本节之前创建的 Customers 服务，创建一个新的 ASP.NET 网站。通过右键点击解决方案中的项目根目录，选择 Service Reference。在 Service Reference 对话框中，你可以输入服务的 URL。然而，要使用传统的 Web 服务，请选择 Advanced 按钮。在 Advanced 设置的底部，选择 Add Reference。出现 Add Reference 对话框，如图 13-7 所示。

## 简单的服务

![](img/67a6707ff505c052edb96c0128fb3096_514_0.png)

图 13-7

> **NOTE** 在 Visual Studio 2010 及之前的版本中，Add Reference 对话框有自己的菜单选项 Add Reference。然而，随着 WCF 和 WebAPI 的出现，该菜单项已被移除。

Add Reference 对话框允许你指向特定的 .asmx 文件以对其进行引用。要的是，Add Reference 对话框实际上是在寻找 WSDL 文件。Microsoft 的 XML Web 服务根据 .asmx 文件自动生成 WSDL 文件。在浏览器中，只需输入你的 Web 服务 .asmx 文件的 URL 并在字符串末尾添加 `?WSDL`。例如，你可能使用了以下结构（这只是一个示例）：

```
http://www.contoso.com/WebServices/Customers.asmx?WSDL
```

因为 Add Reference 对话框会自动找到任何基于 Microsoft 的 XML 服务的 WSDL 所在位置，对于任何非 Microsoft 的 Web 服务，你只需直接输入实际 WSDL 文件的 URL。

> **NOTE** 如果你使用 Microsoft 的 Visual Studio 及其内置 Web 服务器而不是 IIS，你将被要求将服务器正在使用的端口号也交叉 URL 中。在这种情况下，你的 URL 结构类似于 `http://localhost:4937/Customers.asmx?WSDL`。

在 Add Reference 对话框中，将引用从默认名称更改更有意义的名字。如果你在单机上工作，Web 引用的名称可能是 localhost，

## 第 13 章 处理服务

如果你实际上在与远程服务工作，该名称是 URL 的反转，例如 `com.conto.www`。无论何种情况，将其重命名为在应用程序中更有意义且易于使用的名称都是最好的。例如，将其重命名为 `AdventureWorksCustomers`。

点击“添加引用”按钮会导致 Visual Studio 从你应用程序的 `web.config` 文件（如图 13-8 所示）对 Web 服务创建实际引用。你可能会在 `App.WebReferences` 文件夹下找到其他文件——例如 `web service.WSDL` 文件的副本。

客户端应用程序的 `web.config` 文件在 `<appSettings>` 部分包含对 Web 服务的引用。列表 13-6 显示了该选项。

![](img/67a6707ff505c052edb96c0128fb3096_515_0.png)

图 13-8

### 列表 13-6：引用 Web 服务后 web.config 文件的更改

```xml
<?xml version="1.0"?>
<configuration>
  <system>
    <compilation debug="false" targetFramework="4.5"/>
    <httpRuntime targetFramework="4.5"/>
  </system>
  <appSettings>
    <add key="AdventureWorksCustomers.Customers" value="http://localhost:4473/Customers.asmx"/>
  </appSettings>
</configuration>
```

你可以看到已经创建了 `AdventureWorksCustomers` 引用，以及 Web 服务的名称。`value` 属性取的是 Customers Web 服务的位置值，该位置位于 `Customers.asmx` 页面中。

## 从客户端应用程序调用 Web 服务

现在已经对 XML Web 服务建立了引用，你就可以可以在 ASP.NET 应用程序中使用它。在项目中创建一个新的 Web 表单（Web Form）。通过此页面，你可以直接从远程 AdventureWorks 数据库将 `Customers` 表消费到你的应用程序中。

在页面的设计部分，放置一个按钮（Button）和一个 GridView 控件，使你的页面看起来如图 13-9 所示。

![](img/67a6707ff505c052edb96c0128fb3096_515_1.png)

图 13-9

其原理是，当最终用户点击表单上的按钮时，应用程序会向 Customers Web 服务发送 SOAP 请求，并返回一个包含 `Customers` 表的 SOAP 响应，该表将绑定到页面上的 GridView 控件。列表 13-7 显示了这个简单应用程序的代码。

### 列表 13-7：在 ASP.NET 页面中消费 Web 服务

```vb
<%@ Page Language="VB" %>
<!DOCTYPE html>
<script runat="server">
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        Dim ws As New AdventureWorksCustomers.Customers()
        GridView1.DataSource = ws.GetCustomers()
        GridView1.DataBind()
    End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Web Service Consumer Example</title>
</head>
<body>
<form id="form" runat="server">
    <div>
        <asp:Button ID="Button1" runat="server" Text="Get Customers"
            OnClick="Button1_Click" />
        <br />
        <br />
        <asp:GridView ID="GridView1" runat="server" Padding="3" CellSpacing="2" BorderStyle="None"
            BorderColor="#DBEB84">
            <FooterStyle ForeColor="#8C6504" BackColor="#FDF8B5"></FooterStyle>
            <PagerStyle ForeColor="#8C6504" HorizontalAlign="Center"></PagerStyle>
            <HeaderStyle ForeColor="White" Font-Bold="True"
                BackColor="#A55129"></HeaderStyle>
            <SelectedRow ForeColor="White" Font-Bold="True"
                BackColor="#738A9C"></SelectedRow>
            <RowStyle ForeColor="#8C6504" BackColor="#FFF7B7"></RowStyle>
        </asp:GridView>
    </div>
</form>
</body>
</html>
```

最终用户将看到一个简单的按钮。点击它会导致 ASP.NET 应用程序向远程 XML Web 服务发送 SOAP 请求。返回的 DataSet 将绑定到 GridView 控件，页面将重绘，如图 13-10 所示。

![](img/67a6707ff505c052edb96c0128fb3096_517_0.png)

图 13-10

通过实例化 `AdventureWorksCustomers.Customers` 代理对象来调用 Customers Web 服务：

```csharp
AdventureWorksCustomers.Customers ws = new AdventureWorksCustomers.Customers();
```

然后，你可以像使用项目中其他对象一样使用 `ws`。在列表 13-7 的代码示例中，`ws.GetCustomers()` 方法调用的结果赋值给 GridView 的 `DataSource` 属性：

```csharp
GridView.DataSource = ws.GetCustomers();
```
