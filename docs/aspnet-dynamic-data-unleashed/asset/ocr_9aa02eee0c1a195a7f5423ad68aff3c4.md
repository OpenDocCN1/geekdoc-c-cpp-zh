```
```csharp
private abstract class Metadata
{
    [Required]
    public object ProductName { get; set; }
}
}
```
```

From a validation standpoint, placing any .NET attributes on fields or properties of the metadata class has the same effect as placing them on their counterparts in the real class. Only the name of the field or property matters from the matching perspective, so the metadata class could declare ProductName as a field of type object even though it is a property of type string in the real class. However, if the metadata class has a property or field that does not have a property with the same name in the real class, you get an InvalidOperationException whenever you try to access its attributes for the first time, such as when passing an object to the ValidateObject method of the Validator class.

> **NOTE**
> 
> The compiler does not issue an error when a partial class contains only one definition, which makes it easy to create partial classes that do not match their generated counterparts. You could mistype the name of the class itself or place it in a different namespace. If you notice that additional metadata attributes you applied in the metadata type seem to have no effect on the Dynamic Data pages, double-check that all partial class definitions match, or better yet, create an automated test to verify it, as you learn about later in this chapter.

> **NOTE**
> 
> Notice that the Metadata class was made abstract, private, and nested intentionally. The metadata classes are never instantiated by the application. In addition to violating object-oriented design principles, making metadata classes public unnecessarily pollutes the IntelliSense information in Visual Studio. This becomes more and more noticeable as the number of metadata classes in your application grows.

To eliminate the confusion of having a different type specified for a property as well as to avoid mistakes caused by incorrect property names in the metadata classes, you can use metadata interfaces instead. Here is the same partial Product class extended with a metadata interface instead of a metadata class:

```
```csharp
using System.ComponentModel.DataAnnotations;

internal interface IProduct
{
    [Required]
    string ProductName { get; set; }
}
```
```