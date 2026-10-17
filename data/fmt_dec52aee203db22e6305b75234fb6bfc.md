
# 列表 13-31：实现接口

## VB

```vb
Public Class MyCustomDataContractService
    Implements MyCustomDataContractService

    Public Function HelloFirstName(cust Customer) As String
        Implements MyCustomDataContractService.HelloFirstName
        Return "Hello " + cust.FirstName
    End Function

    Public Function HelloFullName(cust Customer) As String
        Implements MyCustomDataContractService.FullName
        Return "Hello " + cust.FirstName + " " + cust.LastName
    End Function
End Class
```

## C#

```csharp
public class MyCustomDataContractService : ICustomDataContractService
{
    public string HelloFirstName(Customer cust)
    {
        return "Hello " + cust.FirstName;
    }

    public string HelloFullName(Customer cust)
    {
        return "Hello " + cust.FirstName + " " + cust.LastName;
    }
}
```

# 构建构造端

现在服务已经运行并就绪，下一步是构建构造端。开始，你将更新你一直用于消费 Web 服务的 Web 应用程序。再次右键点击解决方案，从菜单提供的选项中选择“添加服务引用”。

在“添加引用”对话框中，添加服务的 WSDL 文件位置并点击确定。这会像以前一样将更改添加到引用和 `web.config` 文件中，使你能够消费该服务。列表 13-32 所示的代码显示了如果你使用 `Button` 控件来启动调用，消费该服务所需的内容。

# 列表 13-32：通过 WCF 服务消费自定义类型

## VB

```vb
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
    Dim ws As New MyCustomDataContractServiceReference.MyCustomDataContractServiceClient()
    Dim myCustomer As New MyCustomDataContractServiceReference.Customer()

    myCustomer.FirstName = "Jason"
    myCustomer.LastName = "Gaylord"

    Response.Write(ws.HelloFullName(myCustomer))
    ws.Close()
End Sub
```

## C#

```csharp
protected void ButtonClick(object sender, EventArgs e)
{
    MyCustomDataContractServiceReference.MyCustomDataContractServiceClient ws = new MyCustomDataContractServiceReference.MyCustomDataContractServiceClient();
    MyCustomDataContractServiceReference.Customer myCustomer = new MyCustomDataContractServiceReference.Customer();

    myCustomer.FirstName = "Jason";
    myCustomer.LastName = "Gaylord";

    Label.Text = ws.HelloFullName(myCustomer);
    ws.Close();
}
```

作为构造端，在你建立引用后，你会发现服务引用同时提供了 `MyCustomDataContractServiceClient` 对象和通过服务数据合约定义的 `Customer` 对象。

因此，前面的代码块只是实例化了这两个对象，并在将其传递到服务提供的 `HelloFullName()` 方法之前构建了 `Customer` 对象。

# 查看 MyCustomDataContractService 的 WSDL 和架构

当你对服务合约建立引用时，你会在 WSDL 中发现如下的 XSD 导入：

```xml
<wsdl:types>
  <xsd:schema namespace="http://tempuri.org/Imports">
    <xsd:import namespace="http://tempuri.org/" schemaLocation="http://localhost:2109/MyCustomDataContractService.svc?xsd=d0"/>
    <xsd:import namespace="http://tempuri.org/" schemaLocation="http://localhost:2109/MyCustomDataContractService.svc?xsd=d1"/>
    <xsd:import namespace="http://tempuri.org/" schemaLocation="http://localhost:2109/MyCustomDataContractService.svc?xsd=d2"/>
  </xsd:schema>
</wsdl:types>
```

`http://localhost:2109/MyCustomDataContractService.svc?xsd=d2` 提供了 `Customer` 对象。这里是代码：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:ns="http://tempuri.org/2009/" xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified">
  <xs:complexType name="Customer">
    <xs:sequence>
      <xs:element name="FirstName" type="xs:string" minOccurs="0"/>
      <xs:element name="LastName" type="xs:string" minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>
  <xs:element name="Customer" type="ns:Customer"/>
</xs:schema>
```

> **注意**
> 这段代码是 `Customer` 对象的 XSD 描述。对 WSDL 建立引用允许你创建本地实例。

# 定义命名空间

注意本章中构建的服务没有定义命名空间。如果你查看生成的 WSDL 文件，你会发现提供的命名空间是 `tempuri.org`。显然，你不想使用这个默认值。相反，你必须定义自己的命名空间。

为了实现这一点，接口的 `[ServiceContract]` 属性允许你设置命名空间，如下：

```csharp
[ServiceContract(Namespace="http://jsonglord.com/ns/")]
public interface ICustomDataContractService
{
    [OperationContract]
    string HelloFirstName(Customer cust);

    [OperationContract]
    string HelloFullName(Customer cust);
}
```

# 使用 EDM

实体数据模型（EDM）是你希望在代码中表示数据的抽象概念模型。近年来，EDM 及其优势被强调。

> **注意** 第 11 章提供了更多关于 EDM 以及如何在 Entity Framework 中使用它们的信息。

另一种可用的模型是 WCF Data Services 框架。该功能允许你轻松地为客户端应用程序创建一个接口，提供从简单的读取能力到完整的 CRUD 模型的所有功能。该功能以前被称为 ADO.NET Data Services。

# 第 13 章 运行服务

WCF Data Services 允许你快速将与应用程序底层数据源的交互暴露为基于 REST 的服务。当前版本的 WCF Data Services 允许你使用 JSON 或基于 Atom 的 XML 与数据存储进行工作。

# 创建你的第一个服务

在过去，如何构建一个服务层来与数据库进行所有的创建、读取、更新和删除（CRUD）操作需要花费大量的时间和思考。然而，正如我们在通过 .NET 完成这个第一个示例时将看到的，WCF Data Services 使这项任务变得可行得多。

要构建服务层，首先使用 Visual Basic 或 C# 创建一个标准的 ASP.NET Web 应用程序。这将创建一个标准的 Web 应用程序。由于 WCF Data Services 于底层数据库工作，你需要添加一个数据库。对于此示例，请像你之前使用的那样添加 AdventureWorks 数据库。将此数据库放在项目的 `App_Data` 文件夹中。

# 添加你的实体数据模型

在准备好数据库后，你将创建一个 WCF Data Services 将要使用的实体数据模型。要执行此操作，右键点击你的项目，并在提供的菜单列表中选择“新建项”。

出现“添加新建项”对话框。如图 13-24 所示，向你的项目添加 ADO.NET 实体数据模型。

![图 13-23](img/67a6707ff505c052edb96c0128fb3096_545_0.png)
![图 13-24](img/67a6707ff505c052edb96c0128fb3096_545_1.png)

如图所示，你的 ADO.NET 实体数据模型文件为 `AdventureWorks.edmx`。当你点击“添加”创建 `AdventureWorks.edmx` 文件时，会弹出实体数据模型向导，它为你提供创建 EDM 或从现有数据库创建的选项。对于此示例，选择从现有的（AdventureWorks）数据库创建一个的选项。然后点击向导中的“下一步”。

向导的下一个屏幕将找到你的 AdventureWorks 数据库并重新定义连接设置以及它们在应用程序中的存储方式。图 13-25 显示了向导的第二个屏幕。

![图 13-25](img/67a6707ff505c052edb96c0128fb3096_546_0.png)

在图 13-25 的截图中，注意连接字符串和映射详细信息的持久化将存储在模型部分的配置文件中。你也可以在此屏幕上看到你正在窗口边界的文本框为 `AdventureWorksEntities` 实例命名。这对于工作非常重要。

下一个屏幕允许你选择将作为模型部分的表、视图或存储过程。对于此示例，点击树形中“表”项的复选框以选择数据库中的所有表，如图 13-26 所示。

![图 13-26](img/67a6707ff505c052edb96c0128fb3096_546_1.png)

勾选“表”复选框后，点击“完成”按钮。你会注意到 Visual Studio 在设计器中为你创建了模型的视觉表示。

如果你查看解决方案中的 `AdventureWorks.designer.vb` 或 `AdventureWorks.designer.cs` 文件，你将看到所有为 EDM 生成的代码。该类文件名为 `AdventureWorksEntities`。

# 创建服务

现在 EDM 和数据库已就绪，下一步是添加你的 WCF Data 服务。要完成此操作，在 Visual Studio 资源管理器中右键点击你的项目，并在提供的菜单中选择“添加项”。出现“添加新建项”对话框；在提供的对话框的中间部分选择 WCF Data 服务（见图 13-27）。

![图 13-27](img/67a6707ff505c052edb96c0128fb3096_547_0.png)

如图所示，你的 WCF Data 服务为 `AdventureWorksDataService.svc`。当你完成后，点击“添加”按钮，Visual Studio 随后会为你生成一个 WCF 服务。列表 13-33 显示了默认服务文件的代码。

# 列表 13-33：WCF Data 服务的默认 .svc 文件

## VB

```vb
Imports System.Data.Services
Imports System.Data.Services.Common
Imports System.Linq
Imports System.ServiceModel.Web

Public Class AdventureWorksDataService
    ' TODO: 将 [[class name]] 替换为你的类名
    Inherits DataService(Of [[class name]])

    ' 此方法仅调用一次以初始化全局策略。
    Public Shared Sub InitializeService(ByVal config As DataServiceConfiguration)
        ' TODO: 设置规则以指示哪些实体和服务
        ' 操作是可见的、可更新的等
        ' 示例:
        config.SetEntitySetAccessRule("MyEntity", EntityRights.All)
        config.SetOperationAccessRule("*", EntityRights.All)
        config.DataServiceBehavior.MaxVersion = V3
    End Sub
End Class
```

## C#

```csharp
using System;
using System.Data.Services;
using System.Data.Services.Common;
using System.ServiceModel.Web;

public class AdventureWorksDataService : DataService<[[class name]]>
{
    // TODO: 将 [[class name]] 替换为你的类名
    // 此方法仅调用一次以初始化全局策略。
    public static void InitializeService(DataServiceConfiguration config)
    {
        // TODO: 设置规则以指示哪些实体和服务
        // 操作是可见的、可更新的等
        // 示例:
        config.SetEntitySetAccessRule("MyEntity", EntityRights.All);
        config.SetOperationAccessRule("*", EntityRights.All);
        config.DataServiceBehavior.MaxVersion = V3;
    }
}
```
