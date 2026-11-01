
## XML Web 服务消费基础

在创建 Xcode 项目以消费 Web 服务之前，先检查一个真实的 Web 服务以了解可以消费它的不同方式是很有益的。我最喜欢的示例是使用用 .NET 创建的 ASMX XML Web 服务。为了讨论目的，让我们来看一个名为 IPToCountry 的 Web 服务，它允许你提供一个 IP 地址并返回该 IP 地址所属的国家。

IPToCountry Web 服务位于 http://www.ecubicle.net/iptocountry.asmx 。如果使用 Safari 加载此 URL，你会看到它公开了两个 Web 方法，如图 14-1 所示。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_401_0.png)

图 14-1

对于本示例，以 FindCountryAsXml 方法为例，它将结果（国家）作为 XML 字符串返回。点击 FindCountryAsXml 链接会显示如图 14-2 所示的页面。

页面上显示的 Test 部分之后的各部分是重要的内容。它们详细说明了消费 Web 服务的各种方式——SOAP、HTTP GET 和 HTTP POST。在 .NET 世界中，访问 Web 服务相当直接——Visual Studio 提供了内置工具，只需下载 WSDL 文档即可为 Web 服务创建 Web 代理服务对象。对于 iPad 开发，你需要亲自动手，因此必须了解消费 Web 服务的底层机制。

## 使用 SOAP 1.1

消费 Web 服务的第一种方法是使用 SOAP（简单对象访问协议）。使用 SOAP 时，你需要使用 POST 方法向 Web 服务发送以下请求：

```
POST /iptocountry.asmx HTTP/1.1
Host: www.ecubicle.net
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://www.ecubicle.net/webservices/FindCountryAsXml"
```

```
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:xsd="http://www.w3.org/2001/XMLSchema"
xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
<soap:Body>
  <FindCountryAsXml xmlns="http://www.ecubicle.net/webservices/">
    <V4IPAddress>string</V4IPAddress>
  </FindCountryAsXml>
</soap:Body>
</soap:Envelope>
```

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_402_0.png)

图 14-2

代码中的粗斜体字是需要替换为实际值的占位符。

在本示例中，有几件重要的事情需要注意：

- Web 服务的 URL 为 "http://www.ecubicle.net/iptocountry.asmx"。这就是图 14-1 中显示的 URL。
- SOAPAction 的 URL 为 "http://www.ecubicle.net/webservices/FindCountryAsXml"。
- 请求的 Content-Type 为 text/xml; charset=utf-8。

HTTP 方法为 POST。

SOAP 请求为：

```
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <FindCountryAsXml xmlns="http://www.ecubicle.net/webservices/">
      <V4IPAddress>string</V4IPAddress>
    </FindCountryAsXml>
  </soap:Body>
</soap:Envelope>
```

SOAP 请求的 Content-Length 是 SOAP 请求字符的总数。

Web 服务将返回以下响应：

```
HTTP/1.1 200 OK
Content-Type: text/xml; charset=utf-8
Content-Length: length

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <FindCountryAsXmlResponse xmlns="http://www.ecubicle.net/webservices/">
      <FindCountryAsXmlResult>xml</FindCountryAsXmlResult>
    </FindCountryAsXmlResponse>
  </soap:Body>
</soap:Envelope>
```

特别是，结果（国家）将被包含在 XML 结果块中。你需要从 XML 结果中提取它。

## 使用 SOAP 1.2

使用 SOAP 1.2 与使用 SOAP 1.1 非常相似。以下显示了 SOAP 1.2 的 SOAP 请求：

```
POST /iptocountry.asmx HTTP/1.1
Host: www.ecubicle.net
Content-Type: application/soap+xml; charset=utf-8
Content-Length: length

<?xml version="1.0" encoding="utf-8"?>
<soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
  <soap12:Body>
    <FindCountryAsXml xmlns="http://www.ecubicle.net/webservices/">
      <V4IPAddress>string</V4IPAddress>
    </FindCountryAsXml>
  </soap12:Body>
</soap12:Envelope>
```

SOAP 1.2 的 SOAP 响应将为：

```
HTTP/1.1 200 OK
Content-Type: application/soap+xml; charset=utf-8
Content-Length: length

<?xml version="1.0" encoding="utf-8"?>
<soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
  <soap12:Body>
    <FindCountryAsXmlResponse xmlns="http://www.ecubicle.net/webservices/">
      <FindCountryAsXmlResult>xml result</FindCountryAsXmlResult>
    </FindCountryAsXmlResponse>
  </soap12:Body>
</soap12:Envelope>
```

## 使用 HTTP GET

如果你不想使用 SOAP，可以使用更简单的 HTTP GET 方法。以下是发送请求的格式：

```
GET /iptocountry.asmx/FindCountryAsXml?V4IPAddress=string HTTP/1.1
Host: www.ecubicle.net
```

```
HTTP/1.1 200 OK
Content-Type: text/xml; charset=utf-8
Content-Length: length
```

请注意以下事项：

- Web 服务的 URL 为 http://www.ecubicle.net/iptocountry.asmx/FindCountryAsXml?V4IPAddress=string 。此 URL 是通过将第二行的主机名与第一行的 URL 连接形成。发送的数据格式为键/值对——key1=value1&key2=value2&key3=value3。
- 请求的 Content-Type 为 text/xml; charset=utf-8。
- 请求的 Content-Length 为 0，因为没有需要单独发送的内容（所有内容都通过查询字符串发送）。
- HTTP 方法为 GET。
- 结果将以以下格式返回：
  ```
  <?xml version="1.0"?>
  xml result
  ```

## 使用 HTTP POST

除了使用 HTTP GET，你还可以使用 HTTP POST。以下是发送请求的格式：

```
POST /iptocountry.asmx/FindCountryAsXml HTTP/1.1
Host: www.ecubicle.net
Content-Type: application/x-www-form-urlencoded
Content-Length: length

V4IPAddress=string
```

请注意以下事项：

- Web 服务的 URL 为 http://www.ecubicle.net/iptocountry.asmx/FindCountryAsXml 。此 URL 是通过将第二行的主机名与第一行的 URL 连接形成。
- 请求的 Content-Type 为 application/x-www-form-urlencoded。
- 请求的 Content-Length 为 V4IPAddress=string 的长度。发送的数据格式为键/值对——key1=value1&key2=value2&key3=value3。与 HTTP GET 不同，数据不会通过查询字符串发送；它在 HTTP 头之后发送。
- HTTP 方法为 POST。
- 结果将以以下格式返回：
  ```
  HTTP/1.1 200 OK
  Content-Type: text/xml; charset=utf-8
  Content-Length: length
  
  <?xml version="1.0"?>
  xml result
  ```

## 使用 SOAP、HTTP GET 和 HTTP POST 消费 Web 服务

现在你已经看到了消费 Web 服务的三种方式，应该使用哪种方法？使用 HTTP GET（最简单的方法），你会看到需要传递给 Web 服务的所有信息都可以通过查询字符串发送。然而，查询字符串的长度有限，因此不适合需要传递大量数据到 Web 服务的情况。另一种选择是使用 HTTP POST 方法，它允许发送更多数据。然而，HTTP POST 也有其局限性。与 HTTP GET 一样，发送的数据必须格式化为键/值对。但每个键/值对的大小限制为 1024 个字符。最通用的方法是使用 SOAP 方法，它允许通过 SOAP 请求向 Web 服务发送复杂数据类型。

## 在你的 iPad 应用中消费 Web 服务

现在你准备好迎接在你的 iPad 应用中消费 Web 服务的激动人心的任务了！首先，你将学习如何使用 SOAP 方法与 Web 服务通信。

