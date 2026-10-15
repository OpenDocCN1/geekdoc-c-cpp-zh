

## 配置文件更改

项目中的另一个新增项是 `app.config` 文件。在创建服务引用后，`app.config` 文件包含多个新的配置设置。这些配置设置是由 Visual Studio WCF 扩展自动添加的。新的 `app.config` 文件在以下代码块中呈现：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0,Profile=Client" />
  </startup>
  <system.serviceModel>
    <bindings>
      <wsHttpBinding>
        <binding name="WSHttpBinding_ICalculator" closeTimeout="00:01:00" openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00" bypassProxyOnLocal="false" transactionFlow="false" hostNameComparisonMode="StrongWildcard" maxBufferPoolSize="524288" maxReceivedMessageSize="65536" messageEncoding="Text" textEncoding="utf-8" useDefaultWebProxy="true" allowCookies="false">
          <readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384" maxBytesPerRead="4096" maxNameTableCharCount="16384" />
          <reliableSession ordered="true" inactivityTimeout="00:10:00" enabled="false" />
          <security mode="Message">
            <transport clientCredentialType="Windows" proxyCredentialType="None" realm="" />
            <message clientCredentialType="Windows" negotiateServiceCredential="true" algorithmSuite="Default" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    <client>
      <endpoint address="http://localhost:8732/Design_Time_Addresses/ProVB_WCFCalculatorLibrary/Service1/" binding="wsHttpBinding" bindingConfiguration="WSHttpBinding_ICalculator" contract="CalculatorService.ICalculator" name="WSHttpBinding_ICalculator">
        <identity>
          <dns value="localhost" />
        </identity>
      </endpoint>
    </client>
  </system.serviceModel>
</configuration>
```

来自 app.config 的代码片段

此文件有两个重要部分。首先，`wsHttpBinding` 部分中的信息很重要，因为它定义了诸如超时和可放置在消息中的最大数据量等行为。这些默认值通常会阻止人们成功发送消息并造成极大困惑而并不罕见。请注意，如果你右键单击服务引用，上下文菜单中还有另一个选项“配置服务引用”。此关键对话框使你能够编辑这些值以反映服务特定需求。

此配置文档的第二个重要部分是 `<client>` 元素。此元素包含一个名为 `<endpoint>` 的子元素，该元素定义了服务消费过程的何处和如何。

`<endpoint>` 元素提供了服务的地址——并且它指定应使用 WCF 可用绑定中的哪个绑定。在本例中，`wsHttpBinding` 是必需的绑定。虽然你正在使用 WCF 框架中的已建立绑定，但从客户端侧你可以自定义此绑定的行为。如前所述，定义绑定行为的设置是使用 `<endpoint>` 元素的 `bindingConfiguration` 属性指定的。在本例中，提供给 `bindingConfiguration` 属性的值是 `WSHttpBinding_ICalculator`，它是对包含在 `<wsHttpBinding>` 元素中的 `<binding>` 元素的引用：

```xml
<binding name="WSHttpBinding_ICalculator" closeTimeout="00:01:00"
openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00"
bypassProxyOnLocal="false" transactionFlow="false"
hostNameComparisonMode="StrongWildcard"
maxBufferPoolSize="524288" maxReceivedMessageSize="65536"
messageEncoding="Text" textEncoding="utf-8" useDefaultWebProxy="true"
allowCookies="false">
<readerQuotas maxDepth="32" maxStringContentLength="8192" maxArrayLength="16384"
maxBytesPerRead="4096" maxNameTableCharCount="16384" />
<reliableSession ordered="true" inactivityTimeout="00:10:00" enabled="false" />
<security mode="Message">
<transport clientCredentialType="Windows" proxyCredentialType="None"
realm="" />
<message clientCredentialType="Windows" negotiateServiceCredential="true"
algorithmSuite="Default" />
</security>
</binding>
```

这里有一个重要的区别需要注意。如果不是使用内置的 Visual Studio 测试引擎来测试你的服务声明，而是绑定到自定义客户端，你会发现此配置文件会略有不同。不是拥有 `wsHttpBinding`，你将拥有一个 `netTCP` 绑定。此绑定将具有不同的设置默认值，更重要的是，指示你的请求的不同传输协议。如果你使用这两种不同的绑定，你会发现 `netTCP` 使用的二进制格式响应速度比 Visual Studio 为你生成的 `wsHttpBinding` 快得多。

如上所示，Visual Studio 2010 对 WCF 的功能使这些服务的消费变得相当简单。下一步是编写 Windows 窗体项目以测试服务接口的消费。

## 编写消费代码

消费接口的代码非常简约。终端用户只需选择他们想要执行的运算的单选按钮。默认选中的单选按钮是 Add。用户在提供的两个文本框中各输入一个数字，然后单击 Calculate 按钮以调用服务对提供的数字执行指定的运算。

为此，在你的窗体中添加两个文本框、四个单选按钮、一个按钮和一个标签。显示（用于标记控件）应类似于图 13-11 所示。接下来，你需要创建两个事件处理程序；第一个是在窗体加载时预填充文本框的默认数字（以加快测试），第二个是为你标记为 Calculate 的按钮创建的事件处理程序。

单击 Calculate 按钮将创建服务的实例，然后打开连接并进行适当的调用。在生产环境中，你可能会在应用程序中保留服务的静态实例，以便可以一次创建而不是每次事件都创建。同样，你需要遵循前面提到的最佳实践，根据应用程序设置在运行时分配 URI。

![](img/d99870e80390742f93963da7be0b2e61_541_0.png)

**图 13-11**

窗体的代码如下：

```vb
Public Class Form1
    Private Sub Form1_Load(ByVal sender As System.Object,
        ByVal e As System.EventArgs) Handles MyBase.Load
        TextBox1.Text = "21"
        TextBox2.Text = "21"
    End Sub

    Private Sub Button1_Click(ByVal sender As System.Object,
        ByVal e As System.EventArgs) Handles Button1.Click
        Dim result As Integer
        Dim ws As New CalculatorService.CalculatorClient()
        ws.Open()
        If RadioButton1.Checked = True Then
            result = ws.Add(Integer.Parse(TextBox1.Text), Integer.Parse(TextBox2.Text))
        ElseIf RadioButton2.Checked = True Then
            result = ws.Subtract(Integer.Parse(TextBox1.Text),
                Integer.Parse(TextBox2.Text))
        ElseIf RadioButton3.Checked = True Then
            result = ws.Multiply(Integer.Parse(TextBox1.Text),
                Integer.Parse(TextBox2.Text))
        ElseIf RadioButton4.Checked = True Then
            result = ws.Divide(Integer.Parse(TextBox1.Text),
                Integer.Parse(TextBox2.Text))
        End If
        ws.Close()
        Label1.Text = result.ToString()
    End Sub

End Class
```

来自 Form1.vb 的代码片段

这与使用 XML Web Services 世界中的 Web 引用时采取的步骤非常相似。首先是代理类的实例化，如 `ws` 对象的创建所示：

```vb
Dim ws As New CalculatorService.CalculatorClient()
```

现在使用 `ws` 对象，IntelliSense 选项为你提供了适当的 Add、Subtract、Multiply 和 Divide 方法。运行此应用程序提供的结果类似于图 13-12 中呈现的结果。

在本例中，当窗体的 Calculate 按钮被按下时，Add 方法是从服务调用的。

另一个最佳实践是获取 Fiddler2 等工具来跟踪与服务的通信。 (www.fiddler2.com/fiddler2/) 此免费工具使你能够查看通过 HTTP/HTTPS 发送的消息。

请注意，虽然如果你已使用 Visual Studio 配置测试通过 HTTP 传输，如果你依赖自定义客户端，你会发现请求改为作为二进制数据通过 TCP 发送，并且不可用于 Fiddler2。

使用绑定到自定义客户端意味着请求和响应通过 TCP 以二进制形式发送，大大减少了大消息的有效载荷大小。这是在 WCF 框架发布之前使用 .NET Remoting 的用途。

这结束了简短的教程，演示了如何构建一个可以支持两个不同端点的单个服务。Visual Studio 2010 可以生成其中一个端点，它基于与传统 Web 服务相同的 XML 和开放标准。另一个你手动构建到命令行应用程序中以支持 TCP 协议和二进制数据传输。根据你将该服务映射到客户端的方式，你可以将其作为基于 XML 的数据传输或可以映射到 .NET Windows 窗体应用程序的二进制数据传输来消费。

![](img/d99870e80390742f93963da7be0b2e61_542_0.png)

**图 13-12**

## 使用数据契约

在前面的示例 WCF 服务中，数据契约依赖于简单类型或原始数据类型。公开了一个 .NET 类型 Integer，它反过来映射到 XSD 类型 int。你可能没有注意到 WSDL 文档中实际定义了输入和输出类型，但它们在那里。这些类型通过导入的 .xsd 文档（动态文档）公开。WSDL 文档的这一部分在此呈现：

```xml
<wsdl:types>
  <xsd:schema targetNamespace="http://tempuri.org/Imports">
    <xsd:import schemaLocation="http://localhost:8000/calculator?xsd=xsd0" namespace="http://tempuri.org/" />
    <xsd:import schemaLocation="http://localhost:8000/calculator?xsd=xsd1" namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
  </xsd:schema>
</wsdl:types>
```

输入 `http://localhost:8000/calculator?xsd=xsd0` 的 XSD 位置会给出服务的输入和输出参数。例如，查看 Add 方法的定义，你会看到以下 XML 片段：

```xml
<xs:element name="Add">
  <xs:complexType>
    <xs:sequence>
      <xs:element minOccurs="0" name="a" type="xs:int" />
      <xs:element minOccurs="0" name="b" type="xs:int" />
    </xs:sequence>
  </xs:complexType>
</xs:element>
<xs:element name="AddResponse">
  <xs:complexType>
```

