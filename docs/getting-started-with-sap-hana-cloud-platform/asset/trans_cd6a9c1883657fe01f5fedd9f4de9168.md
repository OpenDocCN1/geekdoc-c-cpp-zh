

Web 资源。从 Java 开发角度来看，这可以通过两种方式之一实现：

- **声明式**

采用声明式方法时，Web 资源受随 SAP HCP SDK 提供的 Servlet 过滤器类保护：com.sap.cloud.security.oauth2.OAuthAuthorizationFilter。可在 web.xml 部署描述符中配置此过滤器类，以拦截传入的 HTTP 请求并确保提供 OAuth 访问令牌。这样一来，下游 Web 资源无需修改即可提供 OAuth 支持。

- **编程式**

声明式方法的替代方案是使用 com.sap.cloud.security.oauth2.OAuthAuthorized 类中定义的 isAuthorized() 方法的各种重载版本。在此，Web 应用程序资源本身会即时执行授权检查，并相应作出响应。有关此方法的更多信息，我们建议您查阅在线 SAP HCP API 文档 https://help.hana.ondemand.com/javadoc/index.html。

大多数情况下，采用声明式方法更合理，因为它提供了逻辑上的关注点分离，因此让我们来看看它是如何工作的。清单 8.13 包含为我们的示例航班搜索 API 创建的 web.xml 部署描述符摘录。（此内容包含在图书源代码包中的 EXAMPLE08_02 应用程序内，可从 www.sap-press.com/3638 下载。）在此，您可以看到我们定义了一个名为 TravelAgentAPIServlet 的自定义 Servlet 类，以及基于 OAuthAuthorizationFilter 类的相应 Servlet 过滤器定义。将过滤器与 Servlet 资源关联的粘合剂是 Servlet/过滤器定义中包含的 <url-pattern> 元素。由于 URL 模式匹配，SAP HCP Web 容器会自动将指向此 URL 的传入请求路由到 OAuthAuthorizationFilter 类，以便验证 OAuth 访问令牌的存在。如果未提供令牌，则请求会失败，客户端永远无法访问受保护的 Web 资源。

```
<web-app>
<servlet>
<servlet-name>TravelAgentAPIServlet</servlet-name>
<servlet-class>
com.sapress.hcpbook.chp08.TravelAgentAPIServlet
</servlet-class>
</servlet>
<servlet-mapping>
<servlet-name>TravelAgentAPIServlet</servlet-name>
<url-pattern>/api/v1/flights/</url-pattern>
</servlet-mapping>
<filter>
<display-name>OAuth Scope for Flight Lookups</display-name>
<filter-name>TravelAgentFlightsFilter</filter-name>
<filter-class>
com.sap.cloud.security.oauth2.OAuthAuthorizationFilter
</filter-class>
<init-param>
<param-name>scope</param-name>
<param-value>get-flights</param-value>
</init-param>
<init-param>
<param-name>http.method</param-name>
<param-value>get</param-value>
</init-param>
</filter>
<filter-mapping>
<filter-name>TravelAgentFlightsFilter</filter-name>
<url-pattern>/api/v1/flights/</url-pattern>
</filter-mapping>
</web-app>
```

### 清单 8.13 在 web.xml 文件中配置 OAuth 授权过滤器

仔细查看清单 8.13 中包含的过滤器定义，您会发现包含多个初始化参数：

- scope

此参数用于指定在授权处理期间检查的 OAuth 范围。您很快就会了解 OAuth 范围的相关内容。

- http.method

此可选参数允许您指定要为其提供授权的 HTTP 方法（例如，在此情况下为 GET）。如果省略此参数（经常会发生这种情况），则将不加区分地检查所有 HTTP 方法。

- user-principal

此参数决定 OAuth 过滤器在成功身份验证或授权后是否会映射资源所有者的用户 ID。如果设置为 true，则您可以像往常一样使用 Servlet API 获取用户 ID。

信不信由你，从开发角度来看，为基于 Java 的 Web 资源启用基于 OAuth 的授权就只需做这些。但是，在将资源交给客户端之前，服务器端还有一项最后需要配置的内容。

应用程序部署后，您需要进入 SAP HCP 驾驶舱并配置一个或多个 OAuth 范围。从概念上讲，您可以将范围视为客户端从 OAuth 授权服务器请求访问权限的命名授权。例如，在我们的航班 API 示例中，我们定义了一个名为 get-flights 的单个范围，该范围在清单 8.13 所示的 web.xml 文件中被引用。此范围为客户端提供查找航班信息的访问权限。如果我们的 API 支持其他航班操作，那么我们可能还会定义 create-flight、update-flight 等范围。

要为 Java 应用程序定义 OAuth 范围，只需打开应用程序仪表板并导航到 OAUTH SCOPES 选项卡页面。从此处，您可以通过单击范围表中的 New Scope 按钮来定义任意数量的范围。这将打开图 8.29 底部所示的表单编辑器。在此表单中，您需要指定范围 ID 和范围的长文本描述。在第 8.6.4 节中，您将看到此描述将显示在类似于图 8.27 中所示的 Google+ 授权屏幕的基于 SAP HCP 的授权屏幕上。

最终，为应用程序定义的范围相当随意，取决于 API 提供者的偏好。基于范围的授权可以是粗粒度或细粒度；OAuth 并不在意。OAuth 唯一关心的是确保范围 ID 根据规范进行配置。

![](img/cf7012644082c115a2181376d9b7486d_371_0.png)

图 8.29 为已部署的 Java 应用程序定义 OAuth 范围

## 8.6.4 开发和配置 OAuth 客户端

在我们的 OAuth 演示服务器部分就绪后，现在让我们将注意力转向将使用航班查询服务的客户端应用程序。在此，虽然您可能不打算从事客户端应用程序开发，但至少了解客户端如何使用 OAuth 与受保护的资源进行交互是有帮助的。此外，这也让我们有机会了解如何在 SAP HCP 驾驶舱中配置和维护客户端。

为了保持简单，我们决定将客户端应用程序实现为托管在 SAP HCP 本地运行时实例上的服务器端 Java Web 应用程序。当然，我们也可以同样轻松地使用 .NET 技术、PHP 等开发此应用程序。的确，OAuth 的一大优点是它是一个开放标准，几乎可以由任何可想象的客户端设备支持。

![](img/cf7012644082c115a2181376d9b7486d_372_0.png)

图 8.30 航班客户端应用程序的流程

图 8.30 是一个流程图，描绘了客户端应用程序的高级流程。在此，流程分解如下：

- 1. 无论何时用户在其 Web 浏览器或用户代理中启动客户端应用程序，客户端首先要做的是确定自己是否已有 OAuth 访问令牌。

- 2. 如果没有，则用户的浏览器将被重定向到 SAP HCP 授权服务器的授权端点，以请求访问代码。

- 3. 授权端点首先会对用户进行身份验证（使用 SAML），然后显示提示，允许用户决定是否希望授予客户端应用程序访问航班查询服务的权限。

- 4. 假设用户批准请求，控制权将转移到 SAP HCP 授权服务器，该服务器生成授权代码并调用原始授权请求中提供的 OAuth 回调 URL。

- 5. 客户端应用程序上的 OAuth 回调服务将接收授权代码，并调用 SAP HCP 授权服务器的令牌端点，以用授权代码换取访问令牌。

- 6. 接收访问令牌后，客户端应用程序将用户的浏览器重定向到应用程序起始页面，用户可在该页面开始搜索航班。

- 7. 最后，无论何时用户提交航班查询，客户端都会格式化 REST 调用并将访问令牌嵌入 HTTP 请求标头。如果一切顺利，航班 API 将返回所需航班，结果将由客户端应用程序解析并在结果列表中显示。

仔细查看图 8.31，您可以看到客户端应用程序与 SAP HCP 授权服务器上的几个端点进行交互，以获取 OAuth 访问令牌。这就引出了一个问题：开发客户端应用程序时，如何知道要访问哪些 URL？与大多数与 SAP HCP 相关的配置项目一样，您必须前往 SAP HCP 驾驶舱才能找到此信息。从主登陆页面，您可以通过打开 OAuth 选项卡来找到 OAuth URL，如图 8.31 所示。

![](img/cf7012644082c115a2181376d9b7486d_373_0.png)

图 8.31 访问 OAuth 授权服务器端点

