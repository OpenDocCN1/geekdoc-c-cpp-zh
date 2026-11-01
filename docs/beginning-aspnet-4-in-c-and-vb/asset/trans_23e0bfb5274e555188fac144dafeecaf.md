
![](img/d7d2ffa0a76feaab821930e95daace93_1771_0.png)

## SOAP

如前所述，与 Web 服务交换数据的一种方式是 SOAP。该技术首次发布时获得了大量关注，尤其是微软决定将其用于 .NET Framework。仔细想想，了解 SOAP 的具体工作原理有点像了解 HTTP 的工作原理——有趣，但并非必需。大多数情况下，你不必担心与 Web 服务交换的格式；它们只是发生，你得到想要的结果，每个人都满意。

因此，本节不会深入探讨太多，但你将看到一些简单的 SOAP 请求和响应，以便了解底层发生了什么。

假设你想调用一个 Web 服务中的方法，其签名如下：

```
int DoSomething(string stringParam, int intParam)
```

以下代码显示了此操作所需的 SOAP 头和正文，其中 Web 服务的地址（稍后详细介绍）在顶部：

```
POST /SomeLocation/myWebService.asmx HTTP/1.1
Host: hostname
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/DoSomething"
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <DoSomething xmlns="http://tempuri.org/">
      <stringParam>string</stringParam>
      <intParam>int</intParam>
    </DoSomething>
  </soap:Body>
</soap:Envelope>
```

这里的 length 参数指定内容的总字节大小，并根据在 string 和 int 参数中发送的值而变化。Host 也会根据 Web 服务的位置而变化。

这里引用的 SOAP 命名空间定义了用于构建消息的各种元素。当你通过 HTTP 发送它时，实际发送的数据略有不同（但相关）。例如，你可以使用简单的 GET 方法调用前述方法：

```
GET /SomeLocation/myWebService.asmx/DoSomething?stringParam=string&intParam=int HTTP/1.1
Host: hostname
```

该方法的 SOAP 响应如下：

```
HTTP/1.1 200 OK
Content-Type: text/xml; charset=utf-8
Content-Length: length
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <DoSomethingResponse xmlns="http://tempuri.org/">
```

```xml
</s:schema>
</wsdl:types>
...other definitions...
</definitions>
```

这些类型就是你在前面看到的 SOAP 和 HTTP 请求和响应所需的所有内容，并在文件后面的部分绑定到这些操作。所有类型均使用标准 XML 模式语法指定，例如：

```xml
<s:element name="DoSomethingResponse">
  <s:complexType>
    <s:sequence>
      <s:element minOccurs="1" maxOccurs="1" name="DoSomethingResult" type="s:int" />
    </s:sequence>
  </s:complexType>
</s:element>
```

这指定了一个名为 DoSomethingResponse 的元素有一个名为 DoSomethingResult 的子元素，其中包含一个整数。该整数必须出现 1 到 1 次，意味着它必须包含在内。

如果你有权访问 Web 服务的 WSDL，你可以使用它。正如你很快就会看到的那样，这并不难做到。

在简要了解 SOAP 和 WSDL 之后，是时候继续讨论如何创建和消费 Web 服务了。

## Web 服务

本章关于 Web 服务的信息分为两个小节：

- “公开 Web 服务”，涉及编写 Web 服务并将其放置在 Web 服务器上。
- “消费 Web 服务”，涵盖在客户端应用程序中使用 Web 服务。

## 公开 Web 服务

Web 服务通过将代码直接放置在 .asmx 文件中或通过从这些文件引用 Web 服务类来公开。与 ASP.NET 页面一样，在 Visual Studio .NET 中创建 Web 服务使用后一种方法，出于演示目的，你也将使用它。

在 C:\ProCSharp\Chapter55 目录中创建 Web 服务项目（通过 File ⇨ New ⇨ Web Site ...）并将其命名为 PCSWebService1（见图 55-1）。创建 Web 服务项目会生成与创建 Web 应用程序项目类似的一组文件，并且你有相同的项目创建位置选项。事实上，唯一的区别是，代替名为 Default.aspx 的文件，会创建一个名为 Service.asmx 的文件，其代码隐藏在 App_Code/Service.cs 中。

![](img/d7d2ffa0a76feaab821930e95daace93_1773_0.png)

图 55-1

![](img/d7d2ffa0a76feaab821930e95daace93_1775_0.png)

## 图 55-2

> 请注意，默认情况下，此测试页面仅对本地计算机的调用者可用，即使你的 Web 服务托管在 Internet Information Services (IIS) 中也是如此。

浏览器中显示的大部分文本都涉及 Web 服务命名空间设置为 http://tempuri.org 这一事实。在开发期间这不是问题，尽管（正如网页上的文本所说）以后应更改它。这可以使用所示的 WebService 属性完成。不过现在，你可以保持现状。

单击方法名称会提供有关 SOAP 请求和响应的信息，以及使用 HTTP GET 和 HTTP POST 方法时请求和响应将如何显示的示例。你也可以通过单击 Invoke 按钮来测试方法。如果方法需要简单参数，你可以输入这些

此外，Web 服务以后可能会移动，也许在部署时。如果你你在客户端应用程序的 web.config 中查看，你会看到以下内容：

```xml
<appSettings>
  <add key="myWebService.Service" value="http://localhost:53678/PCSWebService1/Service.asmx" />
</appSettings>
```
*代码片段 PCSWebClient1\web.config*

此设置配置 Web 请求将被发送到的位置，因此你必须确保它与 Web 服务位置匹配，或者如果你愿意，使用其他方式记录此信息。

## 扩展事件预订示例

现在你已经了解了创建和消费 Web 服务的基础知识，你可以将你的知识应用于扩展第 40 章“Core ASP.NET”和第 41 章“ASP.NET Features”中的会议室预订应用程序。具体来说，你从应用程序中提取数据库访问方面并将其放入 Web 服务。此 Web 服务有两个方法：

- GetData()，返回包含 PCS Demo Site 数据库中全部三个表的 DataSet 对象。
- AddEvent()，添加一个事件并返回受影响的行数，以便客户端应用程序可以检查是否已进行更改。

此外，你将以减少负载为目标设计 Web 服务。具体来说，你将在 Web 服务应用程序的应用程序级别存储一个包含会议室预订数据的 DataSet。这意味着对数据的多次请求不需要额外的数据库请求。此应用程序级 DataSet 对象中的数据仅在向数据库添加新数据时刷新。这意味着通过其他方式（如手动编辑）对数据库所做的更改将不会反映在 DataSet 中。尽管如此，只要你知道你的 Web 服务是唯一可以直接访问数据的应用程序，就无需担心。

## 事件预订 Web 服务

在 C:\ProCSharp\Chapter55 目录中在 Visual Studio 中创建一个新的 Web 服务项目并将其命名为 PCSWebService2。首先要做的是将第 41 章代码中 PCS Demo Site 中的数据库文件（MeetingRoomBooker.mdf）复制到 Web 服务的 App_Data 目录。接下来，你需要在项目中添加一个 Global.asax 文件，然后修改其 Application_Start() 事件处理程序中的代码。你希望将 MeetingRoomBooker 数据库中的所有数据加载到数据集中并存储它。这主要涉及你已经见过的代码，因为将数据库放入 DataSet 是你已经做过的事情。你还将使用 web.config 中存储的连接字符串，如你在前几章中看到的那样。web.config 的代码如下（连接字符串应放在单行上）：

```xml
<?xml version="1.0" ?>
<configuration>
...
<connectionStrings>
<add name="MRCConnectionString"
connectionString="Data Source=.\SQLEXPRESS;Integrated Security=True;AttachDBFilename=|DataDirectory|MeetingRoomBooker.mdf;
User Instance=True"
providerName="System.Data.SqlClient"/>
</connectionStrings>
</configuration>
```
*代码片段 PCSWebService2\web.config*
