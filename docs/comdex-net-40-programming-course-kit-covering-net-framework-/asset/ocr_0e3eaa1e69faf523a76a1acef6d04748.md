![](bbox=[0.19, 0.136, 0.416, 0.326])

![](bbox=[0.439, 0.136, 0.834, 0.338])

Fig.ASP-10.1　　　　　　　　　　　　　　　　Fig.ASP-10.2

You can see the default files of the Web service (**WebService.cs** and **WebService.asmx**) added in the Solution Explorer window, as shown in Fig.ASP-10.3:

![](bbox=[0.427, 0.395, 0.596, 0.559])

Fig.ASP-10.3

Next, you need to create the class and methods to implement the Web service.

+   6. Replace the source code with the code shown in Listing 10.1 in the code-behind file (**WebService.cs**) of the **WebService.asmx** file:

# Listing 10.1: Code for the WebService.cs File

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Services;
[WebService(Namespace = "http://tempuri.org/")]
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
public class WebService : System.Web.Services.WebService
{
    public WebService()
    {
        //Uncomment the following line if using designed components
        //InitializeComponent();
    }

    [WebMethod]
    public double calculateSimpleInterest(double principal, double rate, int duration)
    {
        double SI;
        SI = principal * rate * duration / 100;
```
```