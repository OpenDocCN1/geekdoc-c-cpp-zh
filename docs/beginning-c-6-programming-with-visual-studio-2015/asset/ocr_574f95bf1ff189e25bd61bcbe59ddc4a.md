![](bbox=[0.1, 0.15, 0.52, 0.38])

# FIGURE 21-11

You'll see how with Code First, all you have to do is create the C# objects and collections, and the Entity Framework will create the database structure for you and let you easily navigate the relationships between your database objects and then query the related objects in the database.

# TRY IT OUT
Navigating Database Relationships: BegVCSharp_21_2_DatabaseRelations

Follow these steps to create the example in Visual Studio 2015:

+   1. Create a new console application project called BegVCSharp_21_2_DatabaseRelations in the directory C:\BegVCSharp\Chapter21.
+   2. Press OK to create the project.
+   3. Add the Entity Framework using NuGet as you did in the previous example. Go to Tools ⇨ NuGet Package Manager ⇨ Manage NuGet Packages for Solution.
+   4. In the NuGet Package Manager, choose the Entity Framework, uncheck the Include Prerelease checkbox and get the Entity Framework latest stable release. Click the Install button. It does not have to download because you already downloaded it in the previous step. Click OK on the Preview Changes and the I Accept button for the License Acceptance dialog.
+   5. Open the main source file Program.cs. As in the previous example, add the using statements for the System.Console, System.Data.Entity, and DataAnnotations namespaces, as well as the code to create the Book class:

```
```csharp
using System.Data.Entity;
using System.ComponentModel.DataAnnotations;
using static System.Console;

namespace BegVCSharp_21_2_DatabaseRelations
{
    public class Book
    {
        public string Title { get; set; }
        public string Author { get; set; }
    }
}
```
```