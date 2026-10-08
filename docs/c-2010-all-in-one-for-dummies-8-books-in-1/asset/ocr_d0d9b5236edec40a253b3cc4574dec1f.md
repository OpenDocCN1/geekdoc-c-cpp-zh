# Breaking down the sample code

The Service1 file does all the work in our new service, starting with the code in the template. Let's run through that code a line at a time:

```
using System;
using System.Collections.Generic;
using System.Ling;
using System.Web;
using System.Web.Services;

namespace AService
{
    /// <summary>
    /// Summary description for Servicel
    /// </summary>
    [WebService(Namespace = 'http://tempuri.org/')]
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile_1)]
    [System.ComponentModel.Toolbox(false)]
    // To allow this Web Service to be called from script, using ASP.NET AJAX,
    // uncomment the following line below:
    [System.Web.Services.ScriptService]
    public class ScriptService : System.Web.WebService
    {
        [WebMethod]
        public string HelloWorld()
        {
            return "Hello World";
        }
}
```

There are eight things to point out:

+   * Line 5 brings in the System.Web.Services namespace; it's essential to have the rest of the template.

+   * Line 12 sets the namespace for the service. The namespace, just like that of your .NET classes, can be anything you want. It doesn't refer to a real place on the Web.

+   * Line 13 sets the Web Service Binding, WS-I is the Web Services Interoperability organization who (you guessed) it sets even more standards for Web Services. Basic Profile 1.1 is more or less the industry standard. You can find out more at http://www.ws-i.org.

+   * Line 14 declares the item should be a Toolbox item in design environments. This declares whether it should show up in design Toolboxes.

+   * Line 16 (when uncommented) activates runtime support for AJAX.

+   * Line 17 is a normal, everyday class definition, but notice that it inherits System.Web.Service.WebService.

![](bbox=[0.875, 0.517, 0.962, 0.643])