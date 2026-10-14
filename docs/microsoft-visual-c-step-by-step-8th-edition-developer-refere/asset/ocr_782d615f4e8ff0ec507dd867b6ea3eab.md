through the items in a collection, usually with Language-Integrated Query (LINQ). Behind the scenes, the entity model converts your queries into SQL SELECT commands that fetch the data. You can modify the data in the collection, and then you can arrange for the entity model to generate and perform the appropriate SQL INSERT, UPDATE, and DELETE commands to perform the equivalent operations in the database. In short, the Entity Framework is an excellent vehicle for connecting to a database and retrieving and managing data without requiring you to embed SQL commands in your code.

In the following exercise, you will create a very simple entity model for the Customer table in the AdventureWorks database. You will follow what is known as the database-first approach to entity modeling. In this approach, the Entity Framework generates classes based on the definitions of tables in the database. The Entity Framework also provides a code-first approach; that strategy can generate a set of tables in a database based on classes that you have implemented in your app.

# Note

If you want more information about the code-first approach to creating an entity model, see “Code First to an Existing Database” on the Microsoft website at http://msdn.microsoft.com/data/jj200620.

# Create the AdventureWorks entity model

+   1. In Visual Studio, open the Customers project, located in the \Microsoft Press\VCSBS\Chapter 27\Web Service folder in your Documents folder. This project contains a modified version of the Customers app from Chapter 26. The ViewModel implements additional commands, which let a user navigate to the first or last customer in the customers collection, and the command bar contains First and Last buttons that invoke these commands. Additionally, the Cortana search functionality has been removed to enable you to focus on the tasks at hand. (You are more than welcome to add this feature back if you want a voice-activated version of the app.)

+   2. In Solution Explorer, right-click the Customers solution (not the Customers project), point to Add, and then click New Project.

+   3. In the Add New Project dialog box, in the left pane, click the Web node. In the middle pane, click the ASP.NET Web Application template. Verify that the version specified in the drop-down list box above the middle pane is set to .NET Framework 4.6 (and change it if necessary). In the Name box, type AdventureWorksService, and then click OK.

+   4. In the New ASP.NET Project – AdventureWorksService dialog box, under