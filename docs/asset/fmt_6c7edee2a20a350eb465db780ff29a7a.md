
## 查看 WSDL 文档

图 13-19 显示的页面是关于服务的信息。在图像中，注意指向服务的 WSDL 文件的链接。通过 ASP.NET Web Services，WCF 服务也可以自动生成 WSDL 文件。WCF 4.5 的功能之一是单个 WSDL 文件选项。点击单个 WSDL 链接将在浏览器中显示 WSDL 文件，如图 13-20 所示。

通过此 WSDL 文件，你可以通过 HTTP 绑定使用它定义的服务。请注意文档底部的以下元素，如列表 13-25 所示（此代码列表取自在浏览器中生成的 WSDL 文件）。

### 列表 13-25：显示服务端点的 WSDL 文件部分

```xml
<wsdl:service name="Calculator">
  <wsdl:port name="BasicHttpBinding_Calculator" binding="tns:BasicHttpBinding_Calculator">
    <soap:address location="http://localhost:2109/Calculator.svc/"/>
  </wsdl:port>
</wsdl:service>
```

XML 文档中的此元素指示了如何使用该服务，用户必须在 HTTP 上使用 SOAP。这通过文档中使用 `<soap:address>` 元素体现。使用这个简单的 WSDL 文档，你现在可以构建一个使用此接口的客户端程序了。

## 构建 WCF 客户端

现在你已经使用 WCF 框架构建了一个 HTTP 服务，下一步是在 ASP.NET 中构建一个使用 Calculator 服务的客户端应用程序。客户端通过 HTTP SOAP 发送其请求。本节描述了如何使用该服务。打开 Visual Studio 2012 并创建一个新的 ASP.NET 应用程序。此示例展示了如何创建一个 ASP.NET 应用程序，你也可以通过 .NET 中的任何其他类型进行此客户端调用。

将新的 ASP.NET 应用程序命名为 `WCFConsumer`。此应用程序消耗 Calculator 服务，因此它的布局应包含两个文本框和一个用于调用的按钮。对于此示例，你将只使用服务的 `Add()` 方法。

### 添加服务引用

在布局好 ASP.NET 页面后，为新的 WCF 服务建立引用。这种方法比使用 WSDL Web 服务引用要快得多。在 Visual Studio 资源管理器中右键点击解决方案名称，并在弹出的对话框中选择“添加服务引用”。添加服务引用已包含在 Visual Studio 的过去三个版本中——在此之前，只有“添加引用”和“添加 Web”选项。

> 注意：为了保持本章的一致性，我分别将 C# 和 VB 的项目称为 `Chapter13-CustomerConsumer-CS` 和 `Chapter13-CustomerConsumer-VB`。

选择“添加服务引用”后，会出现图 13-21 所示的“添加服务引用”对话框。

“添加服务引用”对话框要求提供两个内容：服务 URI 或地址（基本上指向 WSDL 文件的指针）以及你想给引用的名称。你提供的名称将是用于实例化对象的名称，它使你能够与服务进行交互。

参考图 13-21，你可以看到提供给服务地址的名称就是之前文中运行服务时使用的名称。点击“添加服务引用”对话框中的确定。这将你的项目添加到“服务引用”文件夹，其中包含一些代理文件，如图 13-22 所示。

确实，添加了服务引用文件夹，并且该文件夹内包含了一系列文件。另一个重要的添加是 `System.ServiceModel` 引用，它在“引用”文件夹中为你生成。在你通过“添加服务引用”对话框创建服务之前，该引用是不存在的。

### 配置文件更改

查看 `web.config` 文件，你可以看到 Visual Studio 已将服务信息放在文档中，如列表 13-26 所示。

#### 列表 13-26：Visual Studio 对 web.config 文件的修改

```xml
<system.serviceModel>
  <bindings>
    <basicHttpBinding>
      <binding name="BasicHttpBinding_ICalculator" />
    </basicHttpBinding>
  </bindings>
  <client>
    <endpoint address="http://localhost:2109/Calculator.svc"
             binding="basicHttpBinding"
             configuration="Basic_ICalculator"
             contract="CalcServiceReference.ICalculator"
             name="BasicHttpBinding_ICalculator" />
  </client>
</system.serviceModel>
```

此配置文档的重要部分是 `<client>` 元素。该元素包含一个 `<endpoint>` 子元素，它定义了服务消费过程的位置和方式。`<endpoint>` 提供了地址——`http://localhost:2109/Calculator.svc`，并指定了应该使用 WCF 绑定中的哪种绑定。在这种情况下，使用了 `basicHttpBinding`。即使你使用来自 WCF 框架的建立绑定，从客户端侧也可以自定义这些绑定的工作方式。定义绑定行为的设置是使用 `<endpoint>` 元素的 `bindingConfiguration` 属性指定的。在这种情况下，`bindingConfiguration` 属性提供的值为 `BasicHttpBinding_ICCalculator`，它是对 `<basicHttpBinding>` 元素包含的 `<binding>` 元素的引用。

如所示，Visual Studio 2012 使这些服务的消费变得非常简单，如果你以前处理过 WCF，你会发现配置比之前的版本要简单得多。

下一步是将服务接口的消费代码写入你在本章早些步骤中创建的 GUI 中。

## 自定义数据协定示例

### VB

```vb
Public Class Customer
    <DataMember()>
    Public FirstName As String

    <DataMember()>
    Public LastName As String
End Class
```

```vb
<ServiceContract()>
Public Interface MyCustomDataContractService
    <OperationContract()>
    Function HelloFirstName(ByVal cust As Customer) As String

    <OperationContract()>
    Function HelloFullName(ByVal cust As Customer) As String
End Interface
```

### C#

```csharp
using System.Runtime.Serialization;
using System.ServiceModel;
```

```csharp
[DataContract]
public class Customer
{
    [DataMember]
    public string FirstName;

    [DataMember]
    public string Lastname;
}
```

```csharp
[ServiceContract]
public interface MyCustomDataContractService
{
    [OperationContract]
    string HelloFirstName(Customer cust);

    [OperationContract]
    string HelloFullName(Customer cust);
}
```
