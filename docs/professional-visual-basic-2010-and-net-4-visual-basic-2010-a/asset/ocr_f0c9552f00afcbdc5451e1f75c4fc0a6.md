# Exposing Data Using WCF Data Services

WCF Data Services is a specialized WCF library that converts the HTTP requests to some provider. Currently, DS supports the Entity Framework as well as custom objects.

Adding DS support to a project containing an Entity Framework model is as simple as adding a new WCF Data Service class to the project (see Figure 12-37). This adds a new class to the project that represents the actual service:

```
Imports System.Data.Services
Imports System.Linq
Imports System.ServiceModel.Web

Public Class PubsService
  ' TODO: replace [[class name]] with your data class name
  Inherits DataService(Of [[class name]])

  ' This method is called only once to initialize service-wide policies.
  Public Shared Sub InitializeService(ByVal config As IDataServiceConfiguration)
    ' TODO: set rules to indicate which entity sets
    ' and service operations are visible, updatable, etc.
    ' Examples:
    ' config.SetEntitySetAccessRule("MyEntityset", EntitySetRights.AllRead)
    ' config.SetServiceOperationAccessRule("MyServiceOperation",
    ServiceOperationRights.All)
  End Sub

End Class
```

Code snippet from SimpleDataService

![](bbox=[0.145, 0.51, 0.802, 0.87])

FIGURE 12-37