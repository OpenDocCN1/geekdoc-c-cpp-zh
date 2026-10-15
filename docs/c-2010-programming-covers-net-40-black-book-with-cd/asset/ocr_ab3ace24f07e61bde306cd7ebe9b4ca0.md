1. Write the code, shown in Listing 18.16, in the code-behind file of the TypeSharingWebService1 Web service:

# Listing 18.16: Code for the Code-Behind File of the TypeSharingWebService1 Web Service

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Services;
/// <summary>
/// Summary description for TypesharingWebService1CS
/// </summary>
[WebService(Namespace = "http://tempuri.org/")]
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
// To allow this web service to be called from script, using ASP.NET AJAX, uncomment the following line.
// [System.Web.Script.Services.ScriptService]
public class TypesharingWebService1CS : System.Web.Services.WebService {
    public TypesharingWebService1CS () {
        //Uncomment the following line if using designed components
        //InitializeComponent();
    }
    public class EmpDetails
    {
        public string EmpFirstName;
        public string EmpMiddleName;
        public string EmpLastName;
        public string EmpID;
        public string EmpDesignation;
    }
    [WebMethod]
    public EmpDetails obtainEmpDetail(string FName, string MName, string LName)
    {
        EmpDetails name = new EmpDetails();
        name.EmpFirstName = FName;
        name.EmpMiddleName = MName;
        name.EmpLastName = LName;
        return name;
    }
}
```

2. After adding the preceding listing to obtain the name of the employee, add the code, shown in Listing 18.17, to obtain the employee's ID and designation in the code-behind file of the TypeSharingWebService2 Web service:

# Listing 18.17: Code for the Code-Behind File of the TypeSharingWebService2 Web Service

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Services;
/// <summary>
/// Summary description for TypesharingWebService2CS
/// </summary>
[WebService(Namespace = "http://tempuri.org/")]
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
// To allow this Web Service to be called from script, using ASP.NET AJAX, uncomment the following line.
// [System.Web.Script.Services.ScriptService]
```