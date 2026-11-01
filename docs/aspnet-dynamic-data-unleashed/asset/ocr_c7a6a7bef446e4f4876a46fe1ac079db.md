Although business users can easily understand the term ContactName, it is not a proper English word; it would be unprofessional to show it in the application. You already know from the previous chapters in this book that you can easily extend metadata information to specify that Name is the proper display name for the ContactName property. However, before you add a DisplayAttribute to the model, take this opportunity to stop and think about why the internal property name does not match its display name. This can be a sign of a mismatch between the domain terminology of your business users and the internal technical terminology you use in the implementation of the app. In this example, you might speculate that you cannot use the term Name because you want to distinguish between the name of the person and the name of his or her company: Thus, technical terms ContactName and CompanyName were chosen to distinguish them. But why is there ambiguity here in the first place? Does your company, Northwind Traders, serve consumers or businesses? If you are a consumer-focused company, you can reinforce this fact in your entity model by renaming the ContactName property to simply Name and changing the CompanyName property to simply Company, making it one of the address properties.

It is very important to keep internal entity and property names accurate. When names displayed on screen do not match expectations of your business users, the first choice should be to change the entity model to match terminology of your business domain. Ideally, you want to propagate these name changes all the way down to the database level and have the names of tables and columns consistent with the names of entities and properties. Refactoring tools in Visual Studio make this task possible today, even with significant amounts of .NET and SQL code. Getting in the habit of applying domain terminology throughout the application helps to reduce the cost of ongoing maintenance and helps the entire development team, including the new members, to understand the application better.

When the internal name of a property is consistent with the business terminology but still not appropriate for display to users, you can use data annotations to specify proper names that should be used instead. Of course, you might also have to resort to this approach when renaming properties in your entity model and columns in your database becomes too difficult. You can start by setting the Name property of the DisplayAttribute—Dynamic Data uses this value whenever a display name is required for the entity property, including form labels, grid column headers, and validation error messages. If a single display name is not enough, you can also specify a separate value in the ShortName property of the DisplayAttribute, which is automatically used in grid column headers. The code snippet for the HomePhone property of the Employee entity in the Northwind sample:

```
```csharp
[MetadataType(typeof(Metadata))]
partial class Employee
{
    private abstract class Metadata
    {
        [Display(Name = "Home Phone", ShortName = "Home #")]
        public object HomePhone { get; set; }
    }
}
```
```