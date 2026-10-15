# My.User

The My.User namespace enables you to work with the IPrincipal interface. You can use the My.User namespace to determine whether the user is authenticated or not, the user's name, and more. For instance, if you have a login form in your application, you could allow access to a particular form with code similar to the following:

```
If (Not My.User.IsInRole("Administrators")) Then
' Code here
End If
You can also just as easily get the user's name with the following:

My.User.Name
In addition, you can check whether the user is authenticated:

If My.User.IsAuthenticated Then
' Code here
End If
```

# My.WebServices

When not using the My.WebServices namespace, you access your Web services references in a lengthier manner. The first step in either case is to make a Web reference to some remote XML Web Service in your solution. These references will then appear in the Web References folder in the Solution Explorer in Visual Studio 2010. Before the introduction of the My namespace, you would have accessed the values that the Web reference exposed in the following manner:

```
Dim ws As New ReutersStocks.GetStockDetails
Label1.Text = ws.GetLatestPrice.ToString()
```

This works, but now with the My namespace, you can use the following construct:

```
Label1.Text = My.WebServices.GetStockDetails.GetLatestPrice.ToString()
```

# EXTENDING THE MY NAMESPACE

You are not limited to only what the My namespace provides. Just as you can with other namespaces, you can extend this namespace until your heart is content. To show an example of extending the My namespace so that it includes your own functions and properties, in your Windows Forms application, create a new module called CompanyExtensions.vb.

The code for the entire module and the associated class is presented here:

```
Namespace My
    <HideModuleName()> _
    Module CompanyOperations
        Private _CompanyExtensions As New CompanyExtensions
        Friend Property CompanyExtensions() As CompanyExtensions
            Get
                Return _CompanyExtensions
            End Get
            Set(ByVal value As CompanyExtensions)
                _CompanyExtensions = value
            End Set
        End Property
    End Module
End Namespace
Public Class CompanyExtensions
    Public ReadOnly Property CompanyDateTime() As DateTime
        Get
            Return DateTime.Now()
```