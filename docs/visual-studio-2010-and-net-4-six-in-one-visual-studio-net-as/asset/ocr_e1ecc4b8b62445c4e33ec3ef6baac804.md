# WORKING WITH AN AJAX-ENABLED WCF SERVICE

You can create an Ajax-enabled WCF service using Visual Studio 2010 that will allow you to call a WCF service using client-side JavaScript. To create one, you right-click on the Solution Explorer, navigate to Add + New Project, and then select "AJAX enabled WCF Service" from the list of project templates displayed. Your Ajax-enabled WCF service would initially look like this:

```
using System.ServiceModel;
using System.ServiceModel.Activation;
namespace MyDataService
{
    [ServiceContract(Namespace = "")]
    [AspNetCompatibility(RequirementsMode.Allowed)]
    public class MyAjaxEnabledService
    {
        // To use HTTP, [Web] attribute. (Default ResponseFormat
        // is WebMessageFormat.Json)
        // To create an operation that returns XML,
        // [Web(GetResponse=WebMessageFormat.Xml)]
        // and include the following line in the operation body:
        // WebOperationContext.Current.Outgoing.ContentType = "text/xml";
        [OperationContract]
        public void DoWork()
        {
            // Add your operation implementation here
            return;
        }
        // Add more operations here and mark them with [OperationContract]
    }
```

You must replace the default operation called DoWork() with your custom method. In the case of this example, you will use a different implementation of the ServiceContract and OperationContract attributes where are applied directly to a class and its methods, to an interface that later has a concrete implementation. From this, you can start to see some of the flexibility provided by the WCF system.

When you create new Ajax-enabled WCF service, Visual Studio 2010 also automatically inserts the necessary configuration information in your application's web.config file. The default additions will similar to the following:

```
<system.serviceModel>
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />
    <services>
        <service name="MyDataService.MyAjaxEnabledService">
            <endpoint address="" behaviorConfiguration=
```