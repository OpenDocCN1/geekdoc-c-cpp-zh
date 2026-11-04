![](bbox=[0.37, 0.14, 0.6, 0.28])

Fig.C#13.3

10 Add a Web method, Add() to the code-behind file, MyWebService.aspx.cs of the MyWebService Web Service, as given in Listing 13.1:

# Listing 13.1: Showing the Code to be Added to the AddNumbers Web Service

```
```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Services;

namespace AddNumbers
{
    /// <summary>
    /// Summary description for MyWebService
    /// </summary>
    [WebService(Namespace = "http://tempuri.org/")]
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
    [System.ComponentModel.ToolboxItem(false)]
    // To allow this Web Service to be called from script, using ASP.NET AJAX,
    // uncomment the
    //following line
    // [System.Web.Script.Services.ScriptService]
    public class MyWebService : System.Web.Services.WebService
    {
        [WebMethod]
        public Decimal Add (Decimal a, Decimal b)
        {
            Decimal dc;
            dc = a + b;
            return dc;
        }
    }
}
```
```

In the Listing 13.1, the Add() method adds two Decimal numbers and then returns a Decimal number as output to the calling method.

11 Press the F5 key to execute the MyWebService Web Service. A Web page appears (Fig.C#13.4).

12 Click the Add hyperlink on the Web page, as shown in Fig.C#13.4: