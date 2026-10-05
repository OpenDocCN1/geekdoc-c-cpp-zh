delete it. Expand the Controllers folder, select the WeatherForecastController.cs file and delete it too.

+   7. In the Build menu, select Rebuild Solution. This process will ensure that any cached references in the project to the items you have just deleted removed.

As mentioned, you cannot access a relational database directly from a UWP app. Instead, you have created a web API project (this is not a UWP app), which will host the entity model you create in the app. The Web API template enables you to build a web service that you can host on Azure to allow applications to connect quickly and easily. This web service will provide remote access to the entity model for the Customers UWP app. Visual Studio provides additional wizards and tools with which you can quickly create the code for the web service.

# To create the Customers entity model

+   1. In Solution Explorer, right-click the AdventureWorksService project, point to Add, and then select New folder Models.

+   2. In Solution Explorer, right-click the Models folder, point to Add, and then select Class.

+   3. In the Add New Item – AdventureWorksService dialog, in the Name box, type CustomerModel.cs, and select Add.

+   4. In the Code and Text Editor window displaying the CustomerModel.cs file, delete the existing using directives from the top of the file and replace them with shown here:

Click to view code image

```
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;
```

+   5. Annotate the CustomerModel class with the Table attribute shown here:

Click to view code image

```
[Table("Customer", Schema = "SalesLT")
public class CustomerModel
{
}
```