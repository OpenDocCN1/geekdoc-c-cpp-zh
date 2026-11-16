

为简单起见，我们设计了示例应用程序，以便在运行时从使用 web.xml 部署描述符文件的 Servlet 上下文中获取 API 密钥。有关如何设置此功能的更多信息，请查看本章源代码包中的 readme 文件以及 web.xml 文件本身中的注释。

拿到 API 密钥后，您基本上就拥有了开始所需的一切。因为您将使用 Connectivity Service 来代理连接，所以必须创建一个 HTTP 目标来指向 API 端点。图 6.40 显示了我们创建的目标。如您所见，我们将目标命名为 GoogleGeocodeDest，并将其指向 Geocoding API URL https://maps.googleapis.com/maps/api/geocode/json。请注意，代理类型设置为 INTERNET，因为这是一次外部调用。如果您要调用托管在本地的 API，那么您将选择 OnPREMISE 选项。

![](img/cf7012644082c115a2181376d9b7486d_275_0.png)

图 6.40 为 Geocoding API 创建 HTTP 目标

在此特定场景中，所需的设置仅此而已。在更高级的场景中，您的工作只会稍微困难一些，因为您可能需要配置更高级的身份验证属性，以支持使用证书、OAuth/SAML 断言等进行相互身份验证。有关每种身份验证类型的具体详细信息，请参阅在线帮助文档。

## 在 Java 应用程序中调用 RESTful 服务

HTTP 目标就位后，在事件管理应用程序中设置对 Geocoding API 服务调用所需的步骤如下：

- 1. 在应用程序的 web.xml 文件中定义对 HTTP 目标的资源引用：

```
<web-app>
    ...
    <res-ref>
        <res-ref-name>GoogleGeocodeDest</res-ref-name>
        <res-type>com.sap.core.connectivity.api.http.HttpDestination
        </res-type>
        <res-auth>Application</res-auth>
    </res-ref>
</web-app>
```

- 2. 使用依赖注入在运行时分配 HttpDestination 对象：

```
public class IncidentBean
{
    @Resource(mappedName="GoogleGeocodeDest")
    private HttpDestination geocodeDestination;
    ...
}
```

- 3. 使用 HttpDestination 类的 createHttpClient() 实例方法获取对 org.apache.http.client.HttpClient 实例的引用。从这一点开始，您可以使用此 HTTP 客户端连接来调用服务，就像在 SAP HCP 之外一样。

为简洁起见，本节不会包含详细的 HTTP 请求处理逻辑。但是，如果您有兴趣了解其工作原理，请查看 com.sappress.hcbook.chp06.persistence.IncidentBean 类的 loadGeoCoordinates() 方法。在那里，您可以看到我们如何对位置地址进行编码以进行传输、解析 JSON 结果，并将坐标数据存储在 Address 实体对象中。您可以通过在“编辑事件”屏幕中单击“获取坐标”链接来测试此功能，如图 6.41 所示。

![](img/cf7012644082c115a2181376d9b7486d_277_0.png)

图 6.41 在事件编辑器中触发 Geocoding API 调用

## 6.3.5 案例研究：发送电子邮件消息

在我们的最后一个案例研究中，我们将演示如何使用 Connectivity Service 发送电子邮件消息。在此，您将增强事件管理应用程序，以包含一个链接，允许用户根据需要向相关方发送事件通知消息。

### 设计方法和初始设置

从很多方面来看，此场景的初始设置与我们在第 6.3.4 节中演示的 RESTful 服务调用设置步骤相似。您基本上需要收集要连接的邮件服务器的连接参数，然后创建一个 Mail 目标来封装这些参数。为了演示目的，我们将使用 SMTP 协议连接到 Google 的 Gmail 服务器。

![](img/cf7012644082c115a2181376d9b7486d_278_0.png)

图 6.42 在 SAP HCP Cockpit 中创建 Mail 目标

每当保存目标时，参数将用于创建 javax.mail.Session 对象，该对象存储在 Java EE 容器的 JNDI 上下文中，上下文路径为 mail/<目标名称>（例如，在我们的示例中为 mail/Session）。在下一节中，您将看到 Java 应用程序如何获取此对象并使用它来发送电子邮件消息。

### 使用 javax.mail 库

因为 Connectivity Service 代为我们创建 javax.mail.Session 对象，所以发送（或接收）电子邮件消息的任务相当简单。清单 6.19 中包含的代码片段通过一个名为 sendMessage() 的简单方法演示了这一点，该方法可用于向特定收件人发送电子邮件消息。基本 API 调用序列如下：

- 1. 首先，该方法创建一个 MimeMessage 对象，用于封装您将要发送的电子邮件消息。此消息实例与 Session 对象相关联，该 Session 对象使用注入技术加载到上下文中，每当封装 EJB 实例化时。

- 2. 接下来，您绑定消息的发送方和接收方，并定义消息主题行。

- 3. 然后，因为您的示例场景发送基于 HTML 的消息，您创建一个 MIME 正文部分，并将 HTML 消息有效载荷附加到其中。

- 4. 最后，您可以使用 Session 实例打开连接并发送消息。在此，Mail 目标中指定的连接参数用于连接到用于传输消息的目标 SMTP 服务器。

```
@Stateless
@LocalBean
public class EmailAgentBean
{

@Resource(name="mail/Session")
private Session mailSession;

public void sendMessage(String sender,
                        String receiver,
                        String subject,
                        String body)
    throws MessagingException
{
    Transport transport = null;

    try
{
    MimeMessage message = new MimeMessage(mailSession);

InternetAddress[] recipients = {
    InternetAddress.parse(receiver),
    InternetAddress.parse(sender)};
message.setFrom(new InternetAddress(sender));
message.setRecipients(RecipientType.TO, recipients);
message.setSubject(subject, "UTF-8");

Multipart multipart = new MimeMultipart("alternative");
MimeBodyPart htmlPart = new MimeBodyPart();
htmlPart.setContent(body, "text/html");
multipart.addBodyPart(htmlPart);
message.setContent(multipart);

transport = mailSession.getTransport();
transport.connect();
transport.sendMessage(message, message.getAllRecipients());
}
catch (Exception ex)
{
    logger.error(ex.getMessage());
    throw new MessagingException(ex.getMessage(), ex);
}
finally
{
    if (transport != null)
    {
        try
        {
            transport.close();
        }
        catch (MessagingException me) { }
    }
} // -- public void sendMessage() -- //
...
```

清单 6.19 使用 javax.mail 库发送电子邮件消息

您可以在示例应用程序中测试此功能，方法是单击 INCIDENT WORKLIST 屏幕 Actions 列中可用的 EMAIL 图标（信封），如图 6.43 所示。如果遇到问题，可以通过将 mail.debug 属性设置为 true 来为 Mail 目标启用调试。调试输出将由 System.out 日志记录器提供。您可能需要调整日志记录器的日志级别，以便在运行时显示日志输出。

![](img/cf7012644082c115a2181376d9b7486d_281_0.png)

图 6.43 在示例应用程序中测试电子邮件通知功能

## 6.4 使用文档服务

在第 6.2 节中，您学习了如何使用 Persistence Service 将结构化数据存储在关系数据库中。结构化数据是指性质高度组织化且可预测的数据。此类数据非常适合存储在二维表中，并且可以使用 SQL 等查询语言轻松分析。

虽然许多企业应用程序几乎完全使用结构化数据，但有时应用程序也需要处理原始非结构化数据，例如文档附件、社交媒体信息流等。虽然您从技术上讲可以将此原始数据与其他所有数据一起存储在数据库中，但这样做就相当于在档案室里堆放箱子；没有人会再次看到这些数据。为了能够对这些非结构化数据进行有成效的操作，您需要的不仅仅是一个简单的数据存储。您需要的是一个内容存储库。

除了提供数据存储功能外，内容存储库还提供几项其他重要的增值功能，包括：

- 版本控制
- 使用访问控制列表 (ACL) 进行安全控制
- 索引
- 高级查询和搜索功能

总体而言，这些功能使您能够从非结构化数据中获得更多价值。

