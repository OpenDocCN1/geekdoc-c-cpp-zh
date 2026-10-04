# Using Web Services in Ajax Websites | 353

# VB.NET

```
<ServiceContract(Namespace="")
<AspNetCompatibilityRequirements(
RequirementsMode:=AspNetCompatibilityRequirementsMode.Allowed)>
Public Class NameService
<OperationContract()>
Public Function HelloWorld(name String) As String
    Return String.Format("{0}", name)
End Function
End Class
```

# C#

```
[ServiceContract(Namespace = "")]
[AspNetCompatibilityRequirements(
RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]
public class NameService
{
    [OperationContract]
    public string HelloWorld(string name)
    {
        return String.Format("{0}", name);
    }
}
```

You define the Service Contract by applying a ServiceContract attribute to your class. An attribute is like a tag or label that you can stick on code elements, like classes, methods, properties, and so on, making that piece of code as something special. Other code interacting with the attributed code can see what code contains and makes decisions based on that information. Don't worry about too much because you don't have to read those attributes when working with web services. All you need to do is stick the attribute on a class or method to enable it for WCF.

In C# use square brackets to wrap the attribute, whereas VB.NET uses angle brackets. You may also come across examples where the VB.NET is followed by a space and an underscore, because previous versions of VB.NET required it. You don't need the underscore, although it's perfectly valid to use it anyway.

The AspNetCompatibilityRequirements attribute that is applied to the service determines how the WCF service behaves. The Allowed value enables your service to run in what's called the ASP.NET Compatibility Mode, which runs the WCF service in a similar way as ASMX services run. When you set the to NotAllowed, your services won't be correct in your ASP.NET websites.

Besides the attribute on the class, each method you want to expose to the service is marked with the OperationContract attribute. This opt-in model enables you to create other methods (for example, helper methods that you call from your service methods) without exposing them from your service.