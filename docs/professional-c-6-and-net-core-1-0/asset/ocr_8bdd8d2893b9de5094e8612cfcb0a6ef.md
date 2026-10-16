# Figure 43.8

Next, add the NuGet packages
Microsoft.AspNet.WebHooks.Receivers.Dropbox and Microsoft.AspNet.WebHooks.Receivers.GitHub. These are the NuGet packages that support receiving messages from Dropbox and GitHub. With the NuGet package manager you’ll find many more NuGet packages that support other SaaS services.

# Configuring WebHooks for Dropbox and GitHub

You can initialize WebHooks for Dropbox by invoking the extension method InitializeReceiveDropboxWebHooks and initialize WebHooks for GitHub by invoking the extension method InitializeReceiveGitHubWebHooks. You invoke these methods with HttpConfiguration in the startup code (code file SaaSWebHooksReceiverSample/App_Start/WebApiConfig.cs):

```
using System.Web.Http;

namespace SaaSWebHooksReceiverSample
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name:"DefaultApi",
                routeTemplate:"api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
```