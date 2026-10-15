

![](img/d99870e80390742f93963da7be0b2e61_533_0.png)

图 13-6

请记住，你的服务仅在控制台窗口保持打开且处于活动状态时可用；当你关闭控制台时，也就停止了新服务的侦听器。

## 查看 WSDL 文档

前面的控制台应用程序代码实例化了 ServiceMetadataBehavior 对象，并为其定义了一个 Uri 对象。你只需在浏览器中输入该地址，即可获取刚刚构建的服务的 WSDL 文件。因此，在浏览器中访问 http://localhost:8000/calculator 会显示如图 13-7 所示的 WSDL 文件。

![](img/d99870e80390742f93963da7be0b2e61_533_1.png)

图 13-7

有了这个 WSDL 文件，你现在可以通过 TCP 使用它所定义的服务。请注意文档底部的以下元素：

```
<wsdl:service name="Calculator">
    <wsdl:port name="NetTcpBinding_ICalculator"
        binding="tns:NetTcpBinding_ICalculator">
        <soap12:address location="net.tcp://localhost:8080/Calculator/" />
        <wsa10:EndpointReference>
            <wsa10:Address>net.tcp://localhost:8080/Calculator/</wsa10:Address>
        </wsa10:EndpointReference>
    </wsdl:port>
</wsdl:service>
```

XML 文档中的此元素表明，最终用户需要通过 TCP 使用 SOAP 1.2 才能使用该服务。这一点通过文档中的 `<soap12:address>` 元素来体现。`<wsa10:EndpointReference>` 是一个 WS-Addressing 终结点定义。

利用这个简单的 WSDL 文档，你现在可以构建一个使用该接口的客户端。同样重要的是，你不仅创建了一个符合 Web 服务标准的服务，还创建了一个通过标准协议进行通信的自定义宿主。

## 构建 WCF 客户端

现在，你已经使用 WCF 框架构建了一个 TCP 服务，下一步是构建一个使用简单 Calculator 服务的客户端应用程序。客户端通过 TCP 并使用 SOAP 发送请求。使用 TCP 意味着实际消费可以通过在线路上对 SOAP 消息进行二进制编码来完成，从而大幅减小所传输有效负载的大小。

本节介绍如何使用此服务。此时你有两种选择：打开另一个 Visual Studio 2010 实例并创建一个新的 Windows Forms 项目来引用服务，或者向当前解决方案中添加一个新的 Windows Forms 项目。为简单起见，本示例采用后一种方式。

就所需操作而言，唯一区别出现在添加服务引用的环节。如果你在新解决方案中创建应用程序，那么为了添加引用，你需要有一个正在运行的服务副本。为此，在新建一个名为 ProVB_WCFCalculatorClient 的解决方案后，就可以开始添加引用的过程。

### 添加服务引用

在解决方案资源管理器中右键单击项目名称，然后从弹出菜单中选择“添加服务引用”。

选择“添加服务引用”后，会看到如图 13-8 所示的对话框。你在此对话框中所做的选择，以及在一定程度上最终获得的结果，取决于你创建项目的方式。我们先从客户端位于独立解决方案中时需要执行的操作开始。

“添加服务引用”对话框会要求你提供两项内容：服务 URI（基本上是指向 WSDL 文件的指针）以及你希望为引用指定的名称。你为引用提供的名称将用于实例化对象，以便你与该服务交互。

参见图 13-8，可以看到“地址”文本框的值为 http://localhost:8000/calculator。请记住，这是你之前在构建服务时定义的位置。此 URI 是在服务代码中直接定义的：

```
Dim smb As New ServiceMetadataBehavior()
smb.HttpGetEnabled = True
smb.HttpGetUrl = New Uri("http://localhost:8000/calculator")
serviceHost.Description.Behaviors.Add(smb)
```

手动输入该 URL 是客户端位于独立解决方案中的做法，与我们接下来为同一解决方案中的客户端所采用的做法不同。由于本例中你要处理的是同一解决方案中的服务，因此你将使用“发现”按钮。“发现”按钮只有一个选项：“解决方案中的服务”。使用此按钮会触发 Visual Studio 查看当前解决方案，定位任何服务，并动态为该服务创建宿主。

```
<MetadataSources>
    <MetadataSource Address="http://localhost:8732/Design_Time_Addresses/
        ProVB_WCFCalculatorLibrary/Service1/mex"
        Protocol="mex" SourceId="1" />
</MetadataSources>
<Metadata>
    <MetadataFile FileName="service.wsdl" MetadataType="Wsdl"
        ID="849df155-c852-4iae-99cf-730f184b9b72" SourceId="1"
        SourceUrl="http://localhost:8732/Design_Time_Addresses/
        ProVB_WCFCalculatorLibrary/Service1/mex" />
    <MetadataFile FileName="service.xsd" MetadataType="Schema"
        ID="10793301-16af-4981-ac16-b09e798357a6" SourceId="1"
        SourceUrl="http://localhost:8732/Design_Time_Addresses/
        ProVB_WCFCalculatorLibrary/Service1/mex" />
    <MetadataFile FileName="service1.xsd" MetadataType="Schema"
        ID="669fdea8-5375-4987-8922-bc2910d40492" SourceId="1"
        SourceUrl="http://localhost:8732/Design_Time_Addresses/
        ProVB_WCFCalculatorLibrary/Service1/mex" />
</Metadata>
<Extensions>
    <ExtensionFile FileName="configuration91.svcinfo" Name="configuration91.svcinfo" />
    <ExtensionFile FileName="configuration.svcinfo" Name="configuration.svcinfo" />
</Extensions>
</ReferenceGroup>
```

来自 Reference.svcmap 的代码片段

该文件提供了日后更新服务引用的能力（当服务接口发生变化时可按需更新）。你可以通过右键单击 CalculatorService 引用看到这一功能；在出现的菜单中会显示“更新服务引用”选项。

引用文件集合中的另一个文件 Reference.vb 是用于与服务交互的代理。该文件内容如下：

```
Option Strict On
Option Explicit On
Namespace CalculatorService

    <System.CodeDom.Compiler.GeneratedCodeAttribute("System.ServiceModel", "4.0.0.0"), _
    System.ServiceModel.ServiceContractAttribute(
        ConfigurationName:="CalculatorService.ICalculator")> _
    Public Interface ICalculator

        <System.ServiceModel.OperationContractAttribute(
        Action:="http://tempuri.org/ICalculator/Add",
        ReplyAction:="http://tempuri.org/ICalculator/AddResponse")> _
        Function Add(ByVal a As Integer, ByVal b As Integer) As Integer

        <System.ServiceModel.OperationContractAttribute(
        Action:="http://tempuri.org/ICalculator/Subtract",
        ReplyAction:="http://tempuri.org/ICalculator/SubtractResponse")> _
        Function Subtract(ByVal a As Integer, ByVal b As Integer) As Integer

        <System.ServiceModel.OperationContractAttribute(
        Action:="http://tempuri.org/ICalculator/Multiply",
        ReplyAction:="http://tempuri.org/ICalculator/MultiplyResponse")> _
        Function Multiply(ByVal a As Integer, ByVal b As Integer) As Integer

        <System.ServiceModel.OperationContractAttribute(
        Action:="http://tempuri.org/ICalculator/Divide",
        ReplyAction:="http://tempuri.org/ICalculator/DivideResponse")> _
        Function Divide(ByVal a As Integer, ByVal b As Integer) As Integer
```

```
End Interface

<System.CodeDom.Compiler.GeneratedCodeAttribute("System.ServiceModel", "4.0.0.0")> _
Public Interface ICalculatorChannel
    Inherits CalculatorService.ICalculator, System.ServiceModel.IClientChannel
End Interface

<System.Diagnostics.DebuggerStepThroughAttribute(), _
System.CodeDom.Compiler.GeneratedCodeAttribute("System.ServiceModel", "4.0.0.0")> _
Partial Public Class CalculatorClient
    Inherits System.ServiceModel.ClientBase(Of CalculatorService.ICalculator)
    Implements CalculatorService.ICalculator

    Public Sub New()
        MyBase.New
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String)
        MyBase.New(endpointConfigurationName)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String,
        ByVal remoteAddress As String)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal binding As System.ServiceModel.Channels.Binding,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(binding, remoteAddress)
    End Sub

    Public Function Add(ByVal a As Integer, ByVal b As Integer) As Integer
        Implements CalculatorService.ICalculator.Add
        Return MyBase.Channel.Add(a, b)
    End Function

    Public Function Subtract(ByVal a As Integer, ByVal b As Integer) As Integer
        Implements CalculatorService.ICalculator.Subtract
        Return MyBase.Channel.Subtract(a, b)
    End Function

    Public Function Multiply(ByVal a As Integer, ByVal b As Integer) As Integer
        Implements CalculatorService.ICalculator.Multiply
        Return MyBase.Channel.Multiply(a, b)
    End Function

    Public Function Divide(ByVal a As Integer, ByVal b As Integer) As Integer
        Implements CalculatorService.ICalculator.Divide
        Return MyBase.Channel.Divide(a, b)
    End Function
End Class
End Namespace
```

这里，一个接口定义了四个方法，以及实现类 CalculatorClient，其中包含的函数会反过来调用本章前面构建的服务。

