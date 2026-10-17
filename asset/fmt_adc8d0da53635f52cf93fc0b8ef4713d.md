
```xml
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
      <binding name="WSHttpbinding" closeTimeout="00:01:00" openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00" bypassProxyOnLocal="false" transactionFlow="false" hostNameOnLocalMode="Wildcard" maxBufferPoolSize="524288" maxReceivedMessageSize="65536" messageEncoding="Text" textEncoding="utf-8" defaultWebProxy="true" allowCookies="false" readerQuotas maxDepth="12" stringContentLength="8192" maxArrayLength="16384" maxBytesPerRead="4096" maxNameCharCount="16384"/>
      <reliableSession ordered="true" inactivityTimeout="00:10:00" abled="false"/>
      <security mode="Message">
        <transport clientCredentialType="Windows" proxyCredentialType="None"/>
        <message clientCredentialType="Windows" negotiateServiceCredential="true" algorithmSuite="Default" establishSecurityContextContext="true"/>/>
      </security>
    </binding>
  </wsHttpBinding>
  </bindings>
  <client>
    <endpoint address="http://localhost:51715/WCFService/Calculator.svc" binding="WSHttpBinding" bindingConfiguration="WSHttpBinding_ICalculator" contract="ServiceReference,ICalculator" name="WSHttpBinding_ICalculator">
      <identity>
        <userPrincipalName value="Lipper-STL-LAP"/>
      </identity>
    </endpoint>
  </client>
</system.serviceModel>
<ServiceReference>
```

该配置文档的重要部分是 `<client>` 元素。它包含一个名为 `<endpoint>` 的子元素，定义了服务消费过程的位置和方式。

`<endpoint>` 元素提供了服务的地址——`http://localhost:51715/WCFService/Calculator.svc`，并指定了使用哪些 WCF 绑定。在这种情况下，`wsHttpBinding` 是所需的绑定。尽管你使用的是 WCF 框架中建立的绑定，但客户端也可以自定义其行为。定义绑定行为的设置是通过 `<endpoint>` 元素的 `bindingConfiguration` 属性指定的。在这种情况下，提供给 `bindingConfiguration` 属性的值是 `WSHttpBinding_ICalculator`，它是 `<wsHttpBinding>` 元素内部 `<binding>` 元素的引用。

如所示，Visual Studio 2008 对 WCF 的增强并没有让服务消费变得异常轻而易举。下一步是编写代码，将服务接口的消费到到步骤之一创建的 GUI 中。

## 编写消费代码

消费接口的代码非常简单。终端用户在提供的两个文本框之一中输入数字，并点击按钮调用服务对提供的数字执行指定的操作。列表 31-31 是按钮点击事件的代码。

### 列表 31-31：按钮点击的代码

```vb
Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
    Dim client As New CalculatorClient()
    Dim result As Integer = client.Add(Integer.Parse(txt1.Text), Integer.Parse(txt2.Text))
    lblResult.Text = result.ToString()
    client.Close()
End Sub
```

```csharp
private void Button1_Click(object sender, EventArgs e)
{
    var client = new CalculatorClient();
    int result = client.Add(int.Parse(txt1.Text), int.Parse(txt2.Text));
    lblResult.Text = result.ToString();
    client.Close();
}
```

# 第 31 章：构建与消费服务

```vb
<OperationContract()>
Function HelloFirstName(ByVal cust Customer) As String
```

```vb
<OperationContract()>
Function HelloFullName(ByVal cust Customer) As String
End Interface
```

C#

```csharp
using System.Runtime.Serialization;
using System.ServiceModel;
```

```csharp
[DataContract]
public class Customer
{
```

```csharp
[DataMember]
public string Firstname;
```

```csharp
[DataMember]
public string Lastname;
}
```

```csharp
[ServiceContract] IHelloCustomer
public interface IWithContract
{
```

```csharp
<OperationContract>
string HelloFirstName(Customer cust);
```

```csharp
[OperationContract]
string HelloFullName(Customer cust);
}
```

在这里，同时也导入了 `System.Runtime.Serialization` 命名空间，并且数据中的第一个类是服务的数据合约。该类（`Customer` 类）有两个成员：`FirstName` 和 `Lastname`。这两个属性的类型都是 `String`。你通过使用 `<DataContract()>` 特性将一个类指定为数据合约。

```vb
<OperationContract()>
Public Class Customer
```

> 为了清晰起见，已删除代码

End Class

现在，类中包含的任何属性通过使用 `<DataMember()>` 特性也是数据合约的一部分：

```vb
<DataContract()>
Public Class Customer
```

```vb
<DataMember()>
Public First Name As String
```

```vb
<DataMember()>
Public Last Name As String
End Class
```

# 第 31 章：构建与消费服务

最后，`Customer` 对象被用在接口以及实现 `IHelloCustomer` 接口的类中，如列表 31-35 所示。

### 列表 31-35：实现接口

```vb
Public Class HelloCustomer
    Implements IHelloCustomer

    Public Function HelloFirstName(ByVal cust as Customer) As String \
        Implements IHelloCustomer.HelloFirstName
        Return "Hello " & cust.FirstName

    Public Function HelloFullName(ByVal cust as Customer) As String \
        Implements IHelloCustomer.FullName
        Return "Hello " & cust.FirstName & " " & cust.LastName
```

```csharp
public class HelloCustomer: IHelloCustomer
{
    public string FirstName(Customer cust)
    {
        return "Hello " + cust.FirstName;
    }

    public string FullName(Customer cust)
    {
        return "Hello " + cust.FirstName + " " + cust.LastName;
    }
}
```

## 构建消费者

现在服务已经运行并就绪，下一步是使用 Visual Studio 2008 构建一个新的 .NET 应用程序并调用项目 `HelloWorldConsumer`。再次右键点击解决方案，并从菜单提供的选项中选择“添加服务引用”。

在“添加引用”对话框中，添加服务的 WSDL 文件位置并按确定。这像以前一样将更改添加到引用和 `web.config` 文件中，让你能够消费该服务。列表 31-36 中的的代码展示了如果你使用按钮控件来启动调用，消费该服务需要的内容。

### 列表 31-36：通过 WCF 服务消费自定义类型

```vb
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    Handles Button1.Click

    Dim ws As New ServiceReference.HelloCustomer()
    Dim myCustomer As New ServiceReference.Customer()
```

```vb
Response.Write(ws.HelloName(myCustomer))
```

```vb
ws.Close();
End Sub
```

```csharp
protected void Button_Click(object sender, EventArgs e)
```

```csharp
ServiceReference.HelloCustomerClient ws = new
ServiceReference.HelloCustomerClient();
ServiceReference.Customer Customer = new ServiceReference.Customer();
```

```csharp
myCustomer.FirstName = "Bill";
myCustomer.LastName = "Evjen";
```

```csharp
Response.Write(ws.HelloName(myCustomer))
```

```csharp
ws.Close();
}
```

作为消费者，一旦你建立了引用，你会发现服务引用同时提供了 `HelloCustomer` 对象和 `Customer` 对象，其中 `Customer` 对象是通过服务的数据合约定义的。

因此，前面的代码块实例化了这两个对象，并在将其传递到服务提供的 `HelloFullName()` 方法之前构建了 `Customer` 对象。

## 查看 HelloCustomerService 的 WSDL 和架构 (Schema)

当你对 `HelloCustomer` 服务建立引用时，你会在 WSDL 中发现以下 WSDL 导入：

```xml
<wsdl:types>
 <xs:schema targetNamespace="http://tempuri.org/Imports">
  <xs:import
    schemaLocation="http://localhost:51715/WCFService1/HelloCustomer.svc?xsd=0"
    namespace="http://tempuri.org/" />
  <xs:import
    schemaLocation="http://localhost:51715/WCFService1/HelloCustomer.svc?xsd=1"
    namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
  <xs:import
    schemaLocation="http://localhost:51715/WCFService1/HelloCustomer.svc?xsd=2"
    namespace="http://schemas.datacontract.org/2004/07/" />
 </xs:schema>
</wsdl:types>
```

`http://localhost:51715/WCFService1/HelloCustomer.svc?xsd=2` 提供了关于 `Customer` 对象的细节。该文件的代码显示在此：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema elementFormDefault="qualified">
```

```xml
targetNamespace="http://schemas.datacontract.org/2004/07/*"
xmlns:xs="http://www.w3.org/2001/XMLSchema"
xmlns:tns="http://schemas.datacontract.org/2004/07/"
<xs:complexType name="Customer">
  <xs:sequence>
    <xs:element minOccurs="0" name="FirstName" nillable="true">
    <xs:type type="string" />
    <xs:element minOccurs="0" name="LastName" nillable="true">
    <xs:type type="string" />
  </xs:sequence>
</xs:complexType>
<xs:element name="Customer" nillable="true" type="tns:Customer" />
</xs:schema>
```

这是 `Customer` 对象的 XSD 描述。对 WSDL 引用包含了 `Customer` 对象的 XSD 描述，并让你能够创建该对象的本地实例的能力。

使用此模型，你可以轻松地使用定义类型构建你的服务。

## 命名空间

注意，本章构建的服务没有定义命名空间。如果你查看生成的 WSDL 文件，你会发现所提供的命名空间是 `tempuri.org`。显然，你并不希望使用这个默认命名空间。相反，你需要定义你自己的命名空间。

要实现这一点，接口的 `ServiceContract()` 特性允许你设置命名空间，如下所示：

```vb
<ServiceContract(Namespace="http://www.lipper.com/ns/")
  Public Interface IHelloCustomer
  [OperationContract()]
  Function HelloFirstName(ByVal cust as Customer) As String
  [OperationContract()]
  Function HelloFullName(ByVal cust as Customer) As String
End Interface
```

在这里，`ServiceContract()` 特性使用 `Namespace` 属性来提供命名空间。

# 第 31 章：构建与消费服务

## 总结

本章是对 .NET 平台中 XML 服务的快速浏览。这绝对是一个值得专门写一本书的主题。本章向你展示了将数据和逻辑暴露为 SOAP 的力量，以及如何在 ASP.NET 中直接消费这些 SOAP 消息。

除了指出你在构建和消费基础 Web 服务方面的能力外，本章还花了一些时间帮助你理解缓存、性能以及 SOAP 头部的使用。

本章还查看了为 .NET Framework 世界提供的最新功能之一。.NET Framework 3.5 和 WCF 是构建高级服务的完美组合，可以将 ASP.NET Web 服务、.NET Remoting、企业和服务 MSMQ 提升到新的水平。

虽然并不详尽，但本章概括概述了框架的基本知识。当你开始深入研究这项技术时，你会发现它的功能强大且可扩展。

## 32

## ADO.NET Data Services
