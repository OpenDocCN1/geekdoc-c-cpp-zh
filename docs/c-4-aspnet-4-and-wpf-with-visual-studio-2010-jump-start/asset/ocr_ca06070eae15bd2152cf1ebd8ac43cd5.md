After selecting the Table check box, click the Finish button to have Visual Studio create the EDM for you. You will notice that Visual Studio will create a visual representation of the model for you in the O/R Designer.

If you look at the `Northwind.designer.vb` or the `Northwind.designer.cs` file in your solution, you will see all the generated code for your EDM in place. This class file is named `NORTHWIND.Entities`.

# Creating the Service

Now that the EDM is in place along with the database, the next step is to add your WCF Data Service. To accomplish this, right-click on your project within the Visual Studio Solution Explorer and select Add ➜ New Item from the provided menu. The Add New Item dialog appears again; select WCF Data Service from the middle section of the provided dialog (see the next figure).

![](bbox=[0.258, 0.337, 0.852, 0.664])

As shown in the figure, name your WCF Data Service `NorthwindDataService.svc`. When done, click the Add button and Visual Studio will then generate a WCF service for you on your behalf. The following listing shows the code of the default service file.

**Pro ASP.NET 9780470502204 Listing 31-33: The default .svc file for a WCF Data Service**

```
```vb
Imports System.Data.Services
Imports System.Linq
Imports System.ServiceModel.Web

Public Class NorthwindDataService
```
```