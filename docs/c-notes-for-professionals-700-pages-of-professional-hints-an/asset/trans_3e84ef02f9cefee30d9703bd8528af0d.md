

```
RequestSettings settings = new RequestSettings("App Name", oAuthparameters);
ContactsRequest cr = new ContactsRequest(settings);
ContactsQuery query = new ContactsQuery(ContactsQuery.CreateContactsUri("default"));
query.NumberToRetrieve = 5000;
Feed<Contact> ContactList = cr.GetContacts();

List<GmailContacts> olist = new List<GmailContacts>();
foreach (Contact contact in ContactList.Entries)
{
    foreach (Email email in contact.Emails)
    {
        GmailContacts gc = new GmailContacts();
        gc.EmailID = email.Address;
        var a = contact.Name.FullName;
        olist.Add(gc);
    }
    return olist;
}

public class GmailContacts
{
    public string EmailID
    {
        get { return _EmailID; }
        set { _EmailID = value; }
    }
    private string _EmailID;
}

public class GooglePlusAccessToken
{
    public GooglePlusAccessToken()
    { }

    public string access_token
    {
        get { return _access_token; }
        set { _access_token = value; }
    }
    private string _access_token;

    public string token_type
    {
        get { return _token_type; }
        set { _token_type = value; }
    }
    private string _token_type;

    public string expires_in
    {
        get { return _expires_in; }
        set { _expires_in = value; }
    }
    private string _expires_in;
}
}
```

### 第161.3节：视图中的源代码

唯一需要添加的操作方法，是添加下面显示的操作链接

```
<a href='@Url.Action("Import", "Home")'>Import Google Contacts</a>
```

## 第162章：.NET 中的垃圾回收器

### 第162.1节：弱引用

在 .NET 中，当对象不再有任何引用时，GC 会回收这些对象。因此，只要对象仍可从代码访问（即存在对其的强引用），GC 就不会回收该对象。如果存在大量大型对象，这可能成为问题。

弱引用是一种引用，它允许 GC 回收对象，同时仍允许访问该对象。弱引用仅在不确定的时间内有效，直到在没有强引用存在时对象被回收。使用弱引用时，应用程序仍可获取对该对象的强引用，从而阻止其被回收。因此，弱引用可用于持有初始化开销很大的大型对象，但如果这些对象未被积极使用，则应可供垃圾回收。

简单用法：

```
WeakReference reference = new WeakReference(new object(), false);

GC.Collect();

object target = reference.Target;
if (target != null)
    DoSomething(target);
```

因此，弱引用可用于维护例如对象缓存。但是，必须记住，始终存在这样的风险：垃圾回收器会在重新建立强引用之前回收该对象。

弱引用还便于避免内存泄漏。一个典型用例是事件。

假设我们有一个用于源上某个事件的处理程序：

```
Source.Event += new EventHandler(Handler)
```

此代码注册事件处理程序，并创建从事件源到侦听对象的强引用。如果源对象的生存期比侦听器长，并且当侦听器没有其他引用时不再需要该事件，那么使用普通的 .NET 事件会导致内存泄漏：源对象会在内存中保留本应被垃圾回收的侦听器对象。

在这种情况下，使用弱事件模式可能是个好主意。

类似如下：

```
public static class WeakEventManager
{
    public static void SetHandler<S, TArgs>(
        Action<EventHandler<TArgs>> add,
        Action<EventHandler<TArgs>> remove,
        S subscriber,
        Action<S, TArgs> action)
        where TArgs : EventArgs
        where S : class
    {
        var subscrWeakRef = new WeakReference(subscriber);
        EventHandler<TArgs> handler = null;
```

```csharp
class ExchangeManager
{
    private ExchangeService Service;

    public ExchangeManager()
    {
        var password = WebConfigurationManager.ConnectionStrings["Password"].ConnectionString;
        Connect("exchangeadmin", password);
    }
    private void Connect(string username, string password)
    {
        var service = new ExchangeService(ExchangeVersion.Exchange2010_SP2);
        service.Credentials = new WebCredentials(username, password);
        service.AutodiscoverUrl("autodiscoveremail@domain.com", RedirectionUrlValidationCallback);

        Service = service;
    }
    private static bool RedirectionUrlValidationCallback(string redirectionUrl)
    {
        return redirectionUrl.Equals("https://mail.domain.com/autodiscover/autodiscover.xml");
    }
    /// <summary>
    /// Updates the given user's Oof settings with the given details
    /// </summary>
    public void UpdateUserOof(int oofstate, DateTime starttime, DateTime endtime, int externalaudience, string internalmsg, string externalmsg, string emailaddress)
    {
        var newSettings = new OofSettings
        {
            State = (OofState)oofstate,
            Duration = new TimeWindow(starttime, endtime),
            ExternalAudience = (OofExternalAudience)externalaudience,
            InternalReply = internalmsg,
            ExternalReply = externalmsg
        };

        Service.SetUserOofSettings(emailaddress, newSettings);
    }
}
```

使用以下代码更新用户设置：

```csharp
var oofState = 1;
var startDate = new DateTime(01,08,2016);
var endDate = new DateTime(15,08,2016);
var externalAudience = 1;
var internalMessage = "I am not in the office";
var externalMessage = "I am not in the office <strong>and neither are you!</strong>"
var theUser = "theuser@domain.com";

var em = new ExchangeManager();
em.UpdateUserOof(oofstate, startDate, endDate, externalAudience, internalMessage, externalMessage, theUser);
```

请注意，你可以使用标准 HTML 标签来格式化消息。

## 第164章：Windows Communication Foundation

Windows Communication Foundation（WCF）是用于构建面向服务应用程序的框架。使用 WCF，你可以将数据作为异步消息从一个服务终结点发送到另一个服务终结点。服务终结点可以是由 IIS 承载的持续可用服务的一部分，也可以是在应用程序中承载的服务。这些消息既可以简单到以 XML 发送的单个字符或单词，也可以复杂到二进制数据流。

### 第164.1节：入门示例

服务在服务协定中描述其执行的操作，并作为元数据公开该协定。

```csharp
// Define a service contract.
[ServiceContract(Namespace="http://StackOverflow.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
}
```

服务实现会计算并返回相应结果，如下面的示例代码所示。

```csharp
// Service class that implements the service contract.
public class CalculatorService : ICalculator
{
    public double Add(double n1, double n2)
    {
        return n1 + n2;
    }
}
```

该服务公开一个用于与服务通信的终结点，该终结点使用配置文件（Web.config）定义，如下面的示例配置所示。

```xml
<services>
    <service
        name="StackOverflow.ServiceModel.Samples.CalculatorService"
        behaviorConfiguration="CalculatorServiceBehavior">
        <!-- ICalculator is exposed at the base address provided by host: http://localhost/servicemodelsamples/service.svc. -->
        <endpoint address=""
            binding="wsHttpBinding"
            contract="StackOverflow.ServiceModel.Samples.ICalculator" />
        ...
    </service>
</services>
```

默认情况下，框架不公开元数据。因此，该服务启用 ServiceMetadataBehavior，并在 http://localhost/servicemodelsamples/service.svc/mex 公开一个元数据交换（MEX）终结点。以下配置演示了这一点。

```xml
<system.serviceModel>
    <services>
        <service
            name="StackOverflow.ServiceModel.Samples.CalculatorService"
```

