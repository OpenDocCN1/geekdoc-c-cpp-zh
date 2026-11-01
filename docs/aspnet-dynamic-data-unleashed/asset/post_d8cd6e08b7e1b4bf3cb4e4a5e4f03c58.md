
When specifying order numbers explicitly, give yourself a little room by starting with appropriate gaps between neighboring properties. In the example just shown, the FirstName and LastName properties that sit next to each other have a gap of 10 in their order numbers. If you need to insert another property, perhaps the MiddleInitial, between them in the future, you will be able to do it without having to renumber all properties. Start with a gap of 100 for larger entities that have 20 or more properties. This allows you to move entire groups of properties without renumbering. When the entity design stabilizes, you can either renumber the properties to have a uniform gap or create a custom entity template and remove order numbers from the metadata entirely.

All properties with an explicit display order are displayed first. Properties that do not have DisplayAttribute or don't have the Order property specified are displayed at the end of the list. This logic is currently implemented by giving properties a default order of 10,000. Keep this in mind when working with large entities—you don't want your explicit order numbers to exceed this number.

Even though gaps allow you to change the order of properties on dynamic pages without having to renumber all of them, it is still a good idea to have the property order in the actual source file match the order of their order numbers. This makes it easier to understand how the dynamic page will look and make maintaining order numbers simpler.

## Configuring Appearance of Labels

In custom forms, the text elements and labels that appear on pages are specified explicitly in their markup. In dynamically generated pages, Dynamic Data uses the internal name of entities and their properties by default. When the internal name does not match what you want to appear on screen, your first choice should be to adjust the internal name in the entity model. For instance, if your entity model has a Customer entity, such as the one from the Northwind Traders sample shown in Figure 11.1, you might have properties such as ContactName and CompanyName that use PascalCase or another naming convention to concatenate multiple words into a single identifier.

![](img/11b373b78859e17d318fd76939a0df9d_370_0.png)

FIGURE 11.1 Customer entity in Entity Designer.

Although business users can easily understand the term ContactName, it is not a proper English word; it would be unprofessional to show it in the application. You already know from the previous chapters in this book that you can easily extend metadata information to specify that Name is the proper display name for the ContactName property. However, before you add a DisplayAttribute to the model, take this opportunity to stop and think about why the internal property name does not match its display name. This can be a sign of a mismatch between the domain terminology of your business users and the internal technical terminology you use in the implementation of the app. In this example, you might speculate that you cannot use the term Name because you want to distinguish between the name of the person and the name of his or her company: Thus, technical terms ContactName and CompanyName were chosen to distinguish them. But why is there ambiguity here in the first place? Does your company, Northwind Traders, serve consumers or businesses? If you are a consumer-focused company, you can reinforce this fact in your entity model by renaming the ContactName property to simply Name and changing the CompanyName property to simply Company, making it one of the address properties.

It is very important to keep internal entity and property names accurate. When names displayed on screen do not match expectations of your business users, the first choice should be to change the entity model to match terminology of your business domain. Ideally, you want to propagate these name changes all the way down to the database level and have the names of tables and columns consistent with the names of entities and properties. Refactoring tools in Visual Studio make this task possible today, even with significant amounts of .NET and SQL code. Getting in the habit of applying domain terminology throughout the application helps to reduce the cost of ongoing maintenance and helps the entire development team, including the new members, to understand the application better.

When the internal name of a property is consistent with the business terminology but still not appropriate for display to users, you can use data annotations to specify proper names that should be used instead. Of course, you might also have to resort to this approach when renaming properties in your entity model and columns in your database becomes too difficult. You can start by setting the Name property of the DisplayAttribute—Dynamic Data uses this value whenever a display name is required for the entity property, including form labels, grid column headers, and validation error messages. If a single display name is not enough, you can also specify a separate value in the ShortName property of the DisplayAttribute, which is automatically used in grid column headers. The code snippet for the HomePhone property of the Employee entity in the Northwind sample:

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

> **NOTE**
> It is not necessary to specify both ShortName and Name properties of the DisplayAttribute if they have the same value. If the ShortName is not specified, Dynamic Data automatically uses the Name instead.

## Prompt Annotation

The DisplayAttribute includes several additional properties that can be used to further tune the appearance of the entity property in dynamically generated pages, although not all of them are supported by the Dynamic Data out of the box. In particular, the Prompt property of the DisplayAttribute could be used to provide a custom string for use in form labels, similar to how the ShortName property specifies display name for grid column headers. To implement this, you can simply change the dynamic entity template, Default.ascx, to use the prompt string if it was specified and otherwise fall back to using the display name string, as shown next:

```csharp
protected void Label_Init(object sender, EventArgs e)
{
    var label = (Label)sender;
    label.Text = this.currentColumn.Prompt
        ?? this.currentColumn.DisplayName;
}
```

> **NOTE**
> Here and in the rest of this chapter, assume dynamic entity templates Default.ascx, Default_Edit.ascx, and Default_Insert.ascx have been combined into a single, multimode template, Default.ascx, as discussed in Chapter 10, “Building Custom Forms.”

This code first appeared in Listing 10.6 and was discussed in detail in Chapter 10. The Label_Init method handles the Init event of the Label control the entity template generates for each entity property. The currentColumn field contains a reference to the MetaColumn object describing the current entity property for which a label and a data entry control are being generated. The original version of this code initialized the label Text using only the DisplayName property of the MetaColumn object. The new version just shown first tries to initialize the label text using the Prompt before falling back to the DisplayName.

> **NOTE**
> As discussed in Chapter 7, "Metadata API," the MetaColumn class encapsulates data annotation attributes applied to the entity property. Although it allows accessing data annotation attributes, using its Attributes property, it also provides strongly typed properties to access specific annotations directly. For example, the DisplayName and Prompt properties of the MetaColumn class return values specified in the Name and Prompt properties of the DisplayAttribute, respectively. Using these properties is not only easier, it is also faster due to metadata caching performed by Dynamic Data.

> **NOTE**
> The ?? operator is a C# null-coalescing operator. It's a powerful shortcut but can be confusing if you are not familiar with it. Here is how a single line of code from the snippet just shown can be replaced with a more verbose, but straightforward, if statement:

```csharp
if (this.currentColumn.Prompt != null)
    label.Text = this.currentColumn.Prompt;
else
    label.Text = this.currentColumn.DisplayName;
```

After implementing support for the Prompt annotation in the dynamic entity template, you can further refine the definition of the Employee entity and specify a custom string for use with the HomePhone property in form labels as shown next. Also the RequiredAttribute is added to the HomePhone property to help illustrate the fact that the Name annotation is still important because it is used to generate validation error messages.

```csharp
[MetadataType(typeof(Metadata))]
partial class Employee
{
    private abstract class Metadata
    {
        [Required]
        [Display(Name = "Home Phone", ShortName = "Home #",
        Prompt = "Home Phone Number:")]
        public object HomePhone { get; set; }
    }
}
```

Notice how the Name, ShortName, and Prompt annotations look in a dynamically generated UI in Figure 11.2. At the top of the picture, you can see a fragment of a dynamic form where the Prompt annotation appears as a label to the left of the phone number text box.
