![](bbox=[0.306, 0.066, 0.615, 0.255])

# Figure 17.58: Changing the Property

As seen in Figure 17.58, the Serialization Mode property is changed to Unidirectional to ensure that the data is serializable.

+   16. In the code-behind file of the IMyService interface, write the code given in Listing 17.20:

# Listing 17.20: Showing the Code for the IMyService Interface

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.Text;
namespace DataBindingInSilverlightCS.Web {
// NOTE: You can use the "Rename" command on the "Refactor" menu to change the interface name "IMyService" in both code and config file together.
[ServiceContract]
public interface IMyService {
[OperationContract]
void DoWork();
List<Employee> GetByLastName(string lastname);
}
}
```

+   17. Switch to the code-behind file of MyService.svc, after entering the code for the IMyService interface.

+   18. Right-click the IMyService interface and select Implement Interface→Implement Interface Explicitly in the code-behind file of the WCF service class, MyService.svc, as shown in Figure 17.59:

![](bbox=[0.215, 0.617, 0.723, 0.915])

# Figure 17.59: Implementing Interface