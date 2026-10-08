

```cs
[DataContract]
public class CompositeType
{
    bool boolValue = true;
    string stringValue = "Hello ";

    [DataMember]
    public bool BoolValue
    {
        get { return boolValue; }
        set { boolValue = value; }
    }

    [DataMember]
    public string StringValue
    {
        get { return stringValue; }
        set { stringValue = value; }
    }
}
```

## 创建服务接口

任何 WCF 服务类都至少实现一个服务合约。在示例中，Service 类将实现的服务合约是 `IEmployeeDataService`。

在解决方案资源管理器中右键点击项目，并创建一个新文件 `EmployeeDataService.cs`。将以下代码放在此处：

```cs
[ServiceContract]
public interface IEmployeeDataService
{
    [OperationContract]
    List<string> GetData();
    [OperationContract]
    List<string> GetEmployeeList();
}
```

这是你稍后创建的服务类将要扩展的服务。注意，此接口中有两个方法声明——`GetData()` 方法和 `GetEmployeeList()` 方法。前者没有标记 `OperationContract` 特性，而后者标记了。这意味着在这两个方法中，只有 `GetEmployeeList()` 方法将暴露给客户端可调用操作。因为这意味着任何未标记 `OperationContract` 特性的方法都不会被包含在服务合约中。

鉴于使用接口来定义服务，由于服务实现不需要 `GetData` 方法，因此通常的最佳实践是从接口定义中省略该方法，以防止任何服务实现者创建不需要的方法。

## 创建服务类

此示例中的服务类是 `EmployeeDataService`。它实现了 `IEmployeeDataService` 接口。打开 `EmployeeDataService.cs` 文件，并并在早之前创建的服务合约旁边放置以下代码：

```cs
public class EmployeeDataService : IEmployeeDataService {
    public List<String> GetData() {
        List<String> lstEmployee = new List<string>();
        lstEmployee.Add("Joydip");
        lstEmployee.Add("Peter");
        lstEmployee.Add("Michael");
        lstEmployee.Add("Sandry");
        lstEmployee.Add("Albert");
        lstEmployee.Add("Russell");
        return lstEmployee;
    }

    public List<String> GetEmployeeList() {
        List<String> lstEmployee = new List<string>();
        lstEmployee.Add("Joydip");
        lstEmployee.Add("Peter");
        lstEmployee.Add("Michael");
        lstEmployee.Add("Sandry");
        lstEmployee.Add("Albert");
        lstEmployee.Add("Russell");
        return lstEmployee;
    }
}
```

以下是 `EmployeeDataService.cs` 文件的完整源代码的样式：

```cs
using System.ServiceModel;
using System.Collections.Generic;
using System;

namespace MyDataService {
    [ServiceContract]
    public interface IEmployeeDataService {
        List<String> GetData();
        [OperationContract]
        List<String> GetEmployeeList();
    }

public class EmployeeDataService : IEmployeeDataService {
    public List<String> GetData()
    {
        List<String> l1Employee = new List<string>();
        l1Employee.Add("Joydip");
        l1Employee.Add("Peter");
        l1Employee.Add("Michael");
        l1Employee.Add("Sandry");
        l1Employee.Add("Albert");
        l1Employee.Add("Russell");
        return l1Employee;
    }

    public List<String> GetEmployeeList()
    {
        List<String> l1Employee = new List<string>();
        l1Employee.Add("Joydip");
        l1Employee.Add("Peter");
        l1Employee.Add("Michael");
        l1Employee.Add("Sandry");
        l1Employee.Add("Albert");
        l1Employee.Add("Russell");
        return l1Employee;
    }
}
```

重要的是，在此示例中，接口和具体实是在同一个程序集内完成的。在许多情况下，具体服务实现可能在另一个文件中。

## 定义数据合约

与服务合约类似，你也可以定义数据合约。如果作为服务合约的操作返回简单类型（即原始类型），则不需要声明合约。但是，如果服务合约定义了复杂类型，则需要数据合约。例如，`GetEmployeeList()` 方法返回一个类实例，必须定义数据合约。数据合约用于使用 `[DataContract]` 特性定义内存类型如何转换为序列化格式。数据合约的各个成员使用 `DataMember` 特性定义。这是一个示例：

```cs
using System.Runtime.Serialization;
[DataContract]
class EmployeeData
{
    [DataMember] public int employeeID { get; set; }
    [DataMember] public String firstName { get; set; }
    [DataMember] public String lastName { get; set; }
}
```

在此示例中，`EmployeeData` 类被定义为数据合约，类中的每个成员作为 `DataMember` 提供。

现在你已经创建了数据合约和服务实现，必须为服务指定绑定信息以便服务或客户端访问。为了让客户端访问 WCF 服务，服务必须暴露至少一个端点。端点表示服务的地址、绑定和合约信息。要指定服务的绑定信息，打开 `App.Config` 文件并在 `<system.serviceModel>` 标签内插入以下代码：

```xml
<system.serviceModel>
  <bindings>
    <basicHttpBinding name="BasicHttpBinding_EmployeeService"
      closeTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00"
      allowCookies="false" bypassProxyOnLocalAddress="false"
      hostNameMode="Wildcard"
      maxBufferSize="65536" maxBufferPoolSize="52428"
      maxReceivedMessageSize="65536"
      messageEncoding="Text" encoding="utf-8" transferMode="Buffered"
      useHttps="true">
      <readerQuota maxDepth="32" maxContentLength="8192" maxArrayLength="16384" />
      maxBytesPerReader="4096" maxNameTableCount="16384" />
      <security mode="None">
        <transport clientCredentialType="None" />
        <message clientCredentialType="Username" algorithmSuite="Default" />
      </security>
    </basicHttpBinding>
  </bindings>
  <client>
    <endpoint address="http://myservice/DataService.svc" binding="basicHttpBinding"
      bindingConfiguration="BasicHttpBinding_EmployeeService" contract="IEmployeeDataService"
      name="BasicHttpBinding_EmployeeService" />
  </client>
</system.serviceModel>
```

这为示例服务创建了一个 `basicHttpBinding`，指定了绑定上的额外属性（如 `openTimeout`、`receiveTimeout`、`send timeout`、`bufferSize` 和最大消息大小）。绑定上的额外配置指定传输不使用安全性。端点的地址指定由 IIS 托管，端点应使用配置中定义的配置，且服务的合约为 `IEmployeeDataService`。

这种声明式的端点定义方法不是配置服务的唯一方法。还可以使用 .NET API 方法通过创建服务主机和端点，使用此方法的简单实现如下：

```cs
public static void main()
{
    ServiceHost serviceHost = new ServiceHost(
        typeof(MyDataService.EmployeeDataService));
    serviceHost.AddEndpoint(
        typeof(MyDataService.EmployeeDataService),
        new BasicHttpBinding(),
        "http://myserver/MyDataService/Service.svc");
    serviceHost.Open();
    Console.WriteLine("Press the ENTER key to stop the service");
    Console.ReadLine();
    serviceHost.Close();
}
```

## 托管 WCF 服务

WCF 服务可以使用 IIS 托管，也可以使用 Windows 激活服务 (WAS) 托管。要在 IIS 中托管你的 WCF 服务，必须创建一个虚拟目录并将其指向服务所在的目录。在 IIS 中托管的 WCF 服务可以通过 HTTP 使用 SOAP 访问。

以下是在托管应用程序中找到 `App.Config` 文件的位置，以访问 IIS 托管的 WCF 服务：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <serviceMetadata httpGetEnabled="true"/>
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <protocolMapping>
      <add bindings="wsHttpBinding" scheme="http"/>
    </protocolMapping>
  </system.serviceModel>
</configuration>
```

此配置信息说明服务可以使用 HTTP 协议的 Get 方法发布元数据信息。第二部分将 HTTP 协议映射到 wsHttpBinding。注意，你的端点配置必须完成，并已从示例中省略以保持简洁。

