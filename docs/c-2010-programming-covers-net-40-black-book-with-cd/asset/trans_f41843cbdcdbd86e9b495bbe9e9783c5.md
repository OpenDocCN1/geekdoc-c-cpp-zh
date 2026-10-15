

MyFirstWebservice。如果 Web 服务项目的 \bin 文件夹中有不止一个程序集，则 ASP.NET 会检查每个程序集，直到找到适当的类。

将编译后的源代码存储在代码隐藏文件中的主要优点是，恶意用户无法访问代码，因为代码未存储在 Web 服务器中。声明代码隐藏属性的语法是：

```
<%@ WebService Language="c#" CodeBehind="~/App_Code/MyFirstWebService.cs" Class="MyFirstWebservice" %>
```

让我们讨论代码隐藏文件的各种属性。

## The WebService Attribute

WebService 属性是 System.Web.Services 命名空间的成员，并传达有关 Web 服务的信息，例如 Web 服务的名称、描述和命名空间。WebService 属性由以下三个属性组成：

- Name – 在 WSDL 文档中定义 Web 服务的类名。当代理使用 WSDL 文档并构建代理类时，生成的类的名称对应于 Web 服务的名称值。此属性允许覆盖默认值。
- Description – 提供有关 Web 服务的类，例如 MyFirstWebservice 所执行功能的简要描述。
- Namespace – 为 Web 服务设置 XML 命名空间，通常为 URL。使用 URL 设置 Web 服务的 XML 命名空间的原因是 URL 总是唯一的。

例如，

```
[WebService(Name="CalculateInterest",Description="This class contains methods for calculating Simple Interest as well as Compound Interest and population of DataSet with the calculated Amount.", Namespace="http://www.InterestRate.com/")]
```

在前面的示例中，Name 属性的值定义如下：

```
Name="CalculateInterest"
```

Description 属性的值定义如下：

```
Description="This class contains methods for calculating Simple Interest as well as Compound Interest and population of DataSet with the calculated Amount."
```

Namespace 属性的值定义如下：

```
Namespace="http://www.InterestRate.com/"
```

## The System.Web.Services.WebService Class

Web 服务继承自 System.Web.Services.WebService 类。WebService 类定义了一些常见的 ASP.NET 对象，例如 Application、User、Session 和 Context，以便您可以在 Web 服务中直接使用它们，而无需重新定义它们。

WebService 类的继承层次结构如下：

```
System.Object
System.ComponentModel.MarshalByValueComponent
System.Web.Services.WebService
```

## The WebMethod Attribute

Web 服务类可以包含一个或多个 WebMethod 属性，这些属性可通过 HTTP 协议访问。WebMethod 属性由以下六个属性组成：

- CacheDuration – 指定客户端发送的请求响应的时间（以秒为单位）。它应保存在系统的缓存中。默认情况下，缓存被禁用。通过将服务的响应放入缓存，可以提高 Web 服务的性能。例如，

```
[WebMethod(CacheDuration=30)]
```

在前面的示例中，[WebMethod] 属性的 CacheDuration 属性的值设置为 30。
- BufferResponse – 允许服务器存储 Web 服务生成的响应。整个响应存储后，响应将一次性传输给客户端。默认情况下，BufferResponse 属性设置为 True。如果将 BufferResponse 属性设置为 False，则响应会在服务器上构建时传输给客户端。
- Description – 提供 [WebMethod] 属性的简要描述，此描述成为 WSDL 文档的一部分。
- EnableSession – 为 Web 方法启用会话状态。默认情况下，此属性设置为 False。
- MessageName – 在处理重载的 Web 方法时，标识类中的多态方法。
- TransactionOption – 使 Web 方法充当事务中的根对象。这意味着 Web 方法可以调用其他启用事务的对象，但它不能被另一个对象作为事务的一部分调用。这种限制存在的原因是 HTTP 协议是无状态的。

到目前为止，您已经了解了 ASP.NET Web 服务的基础结构和 ASP.NET Web 服务的代码模型。现在，让我们讨论 Web 服务的属性。

## Web Service Properties

Web 服务由许多属性组成，这些属性在 WebService 类中定义。此类没有任何公共方法或事件，不是继承的。表 18.4 列出了 WebService 类的公共属性：

Table 18.4: Public Properties of the WebService Class

| Property | Description |
|---|---|
| Application | Obtains the application object for the current HTTP request. |
| Context | Obtains the HttpContext object for the current request, which encapsulates all HTTP-specific context used by the HTTP server to process Web requests. |
| Server | Obtains the HttpServerUtility object for the current request. |
| Session | Obtains the HttpSessionState object for the current request. |
| SoapVersion | Obtains the version of the SOAP protocol used to make the SOAP request to a Web service. |
| User | Obtains the server User object. This property can be used to authenticate whether a user is authorized to execute the request. |

在了解了 WebService 类的公共属性后，让我们详细讨论以下属性：

- Application
- Context
- Server
- Session

### Application Property

WebService 类的 Application 属性用于获取当前 HTTP 请求的应用程序对象。此属性的语法是：

```
[BrowsableAttribute(false)]
public HttpApplicationState Application
{
    get;
}
```

现在，让我们举一个例子来说明 Application 属性如何获取当前 HTTP 请求的应用程序对象。在此示例中，我们展示了 Application 属性中的 Visit_Counter 变量的值获取应用程序对象，并且每次浏览器调用 Web 服务时都会递增 1。列表 18.7 显示了 Application 属性的示例：

### Listing 18.7: Example of the Application Property

```
<%@ WebService Language="C#" Class="Util"%>
using System.Web.Services;
public class Util: WebService
{
  [WebMethod(Description="Number of visits",EnableSession=false)]
  public int Visit_Counter () {
    if (Application["visit_counter"] == null)
    {
      Application["visit_counter"] = 1;
    }
    else
    {
      Application["visit_counter"] = ((int) Application["visit_counter"]) + 1;
    }
    return ((int) Application["visit_counter"]);
  }
}
```

您可以在 Web 服务中使用应用程序状态和会话状态。应用程序状态在访问 Web 服务的会话期间始终启用，而在前面的列表中，会话状态已通过将 [WebMethod] 属性的 EnableSession 属性设置为 False 而被禁用。

### Context Property

WebService 类的 Context 属性用于获取当前请求的 HttpContext 类，该类封装了 HTTP 服务器用于处理 Web 请求的所有 HTTP 特定上下文。此属性的语法是：

```
[BrowsableAttribute(false)]
public HttpContext Context
{
  get;
}
```

列表 18.8 演示了如何使用 Context 属性获取服务器上的请求时间：

### Listing 18.8: Example of the Context Property

```
<%@ WebService Language="C#" Class="Util" %>
using System;
using System.Web.Services;
public class Util: WebService
{
  [WebMethod(Description="Get the Request Time on the Server",EnableSession=false)]
  public string GetTime()
  {
    return Context.Timestamp.TimeOfDay.ToString();
  }
}
```

前面的示例使用 Context 属性返回服务器上请求的时间。

### Server Property

WebService 类的 Server 属性用于获取当前请求的 HttpServerUtility 类。此属性的语法是：

```
[BrowsableAttribute(false)]
public HttpServerUtility Server
```
