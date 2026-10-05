
Visual Studio connects to the database, which appears in the SQL Server Object Explorer window on the left side of the Visual Studio IDE.

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1072_0.png)

- 6. In the SQL Server Object Explorer pane, expand the **Adventure Works** database, expand **Tables**, expand **SalesLT.Customer**, and then expand Columns.

The columns in the table are listed. The columns that aren’t used by the application and that disapp null values must be removed.

- 7. Select the **NameStyle** column, press the **Ctrl** key, and then select the **PasswordHash**, **PasswordSalt**, **rowguid**, and **ModifiedDate** columns.

- 8. Right-click any of the selected columns, and then select **Delete**.

# SQL Server Object Explorer

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1073_0.png)

Visual Studio analyzes these columns. In the Preview Database Updates dialog, it displays a list of warnings and other issues that could occur if the columns are removed.

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1074_0.png)

- 9. In the Preview Database Updates dialog, select Update Database.
10. When the columns have been removed, close the SQL Server Object Explorer pane, but leave Visual Studio 2022 open.

# Creating an entity model

Now that you've created the AdventureWorks database in the cloud, you can use the Entity Framework to create an entity model that an app can use to query and update information in this database. If you have worked with databases in the past, you might be familiar with technologies such as ADO.NET, which provides a library of classes that you can use to connect to a database and run SQL commands. ADO.NET is useful but requires a decent understanding of SQL, and if you're not careful, it can force you into structuring your code around the logic necessary to perform SQL commands instead of focusing on the business operations of your app. The Entity Framework provides a level of abstraction that reduces the dependencies that your apps have on SQL.

Essentially, the Entity Framework implements a mapping layer between a relational database and your app. It generates an entity model that consists of collections of objects that your app can use just as it would other collection. A collection typically corresponds to a table in the database, and each row in a table corresponds to an item in the collection. You perform queries by iterating through the items in a collection, usually with Language-Integrated Query (LINQ). Behind the scenes, the entity model converts your queries into SELECT commands that You can modify the data in the collection, and then you can arrange for the entity model to generate and perform the appropriate SQL INSERT, `UPDATE`, and `DELETE` commands to perform the equivalent operations in the database. In short, the Entity Framework is an excellent vehicle for connecting to a database and retrieving and managing data without requiring you to embed SQL commands in your code.

In this exercise, you'll create a Web API project that you'll use to provide access to an entity model for the Customer table in the AdventureWorks database.

# To create the AdventureWorks Web API project

- 1. In Visual Studio, open the Customers solution, located in the \Microsoft Press\VCSB\Chapter 27\Web Service folder in your Documents folder.

This project contains a modified version of the Customers app from Chapter 26. The ViewModel implements additional commands, which let a user navigate to the first or last customer in the customers collection, and the command bar contains First and Last buttons that invoke these commands. The sample data created by the constructor in the ViewModel has been removed.

- 2. In Solution Explorer, right-click the Customers solution (not the Customers project), point to `Add`, and select `New Project`.

- 3. In the New Project dialog, select C# in the language dropdown list box, select Windows in the platform dropdown list box, select Web in the project type dropdown list box, scroll down and select the ASP.NET Web API template, and then select Next.

# Note

Make sure you don’t accidentally select the ASP.NET Core Web App template.

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1076_0.png)

- 4. In the Configure your new project dialog, set the Project name to AdventureWorksService. Accept the default location, and then select Next.

- 5. In the additional information dialog, select the .NET 6.0 framework. Leave the remaining options at their default values, and then select Create. Visual Studio creates the new project and adds it to the Customers solution.

- 6. The default Web API project contains sample code that you don’t need for this application. In Solution Explorer, select the WeatherForecast.cs file and delete it. Expand the Controllers folder, select the WeatherForecastController.cs file and delete it too.

- 7. In the Build menu, select Rebuild Solution. This process will ensure that any cached references in the project to the items you have just deleted removed.

As mentioned, you cannot access a relational database directly from a UWP app. Instead, you have created a web api project (this is not a UWP app), which will provide access to the entity model. This web service allows you build quickly and easily.

# To create the entity model

- 1. In Solution Explorer, right-click the AdventureService project, point to Add, and select Models.

- 2. In Solution Explorer, right-click the Models folder, point to Add, and select Class.

- 3. In the Add New Item dialog, in the Name box, type CustomerModel.cs, and select Add.

- 4. In the Code Editor window displaying the CustomerModel.cs, delete the existing using directives from the top of the file and replace them with:

```csharp
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.Schema;
```

- 5. Annotate the CustomerModel class with the Table attribute:

```csharp
[Table("Customer", Schema = "SalesLT")]
public class CustomerModel
{
}
```

- 6. Add the following automatic properties in bold to the CustomerModel class. The Key specifies that the CustomerID column is the primary key for the database.

```csharp
[Table("Customer", Schema = "SalesLT")]
public class CustomerModel
{
    [Key]
    public int CustomerID { get; set; }
    public string Title { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string EmailAddress { get; set; }
    public string Phone { get; set; }
}
```

- 7. In Solution Explorer, right-click the AdventureWorksService project, and then select Manage NuGet Packages.

- 8. In the NuGet Package Manager window, on the Browse tab, in the Search box, type Microsoft.EntityFrameworkCore. Select the Microsoft.EntityFrameworkCore package, and then select Install to add the package to the project.

# Important

Make you install version 6.0.0 or later. At the time of writing, .NET 6 of Entity Framework was only available as a prereleased package. If necessary, select the Include prerelease checkbox, and install the latest prerelease build of the package.

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_1079_0.png)

- 9. In the Preview Changes dialog, select OK to confirm the package installation. In the License Acceptance dialog, select Accept.
10. Return to the Browse tab in the NuGet Package Manager, select the Microsoft.EntityFrameworkCore.SqlServer package, and then select Install to add to the project.
11. In the Preview Changes dialog, select OK to confirm the package installation. In the License Acceptance dialog, select Accept.
