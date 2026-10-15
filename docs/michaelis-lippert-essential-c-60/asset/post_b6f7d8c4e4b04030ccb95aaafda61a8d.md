
Like classes, namespaces support nesting. This provides for a hierarchical organization of classes. All the System classes relating to network APIs are in the namespace `System.Net`, for example, and those relating to the Web are in `System.Web`.

There are two ways to nest namespaces. The first approach is to nest them within one another (similar to classes), as demonstrated in Listing 9.14.

### LISTING 9.14: Nesting Namespaces within One Another

```csharp
// Define the namespace AddisonWesley
namespace AddisonWesley
{
    // Define the namespace AddisonWesley.Michaelis
    namespace Michaelis
    {
        // Define the namespace
        // AddisonWesley.Michaelis.EssentialCSharp
        namespace EssentialCSharp
        {
            // Declare the class
            // AddisonWesley.Michaelis.EssentialCSharp.Program
            class Program
            {
                // ...
            }
        }
    }
}
// End of AddisonWesley namespace declaration
```

Such a nesting will assign the `Program` class to the `AddisonWesley.Michaelis.EssentialCSharp` namespace.

The second approach is to use the full namespace in a single namespace declaration in which a period separates each identifier, as shown in Listing 9.15.

### LISTING 9.15: Nesting Namespaces Using a Period to Separate Each Identifier

```csharp
// Define the namespace AddisonWesley.Michaelis.EssentialCSharp
namespace AddisonWesley.Michaelis.EssentialCSharp
{
    class Program
    {
        // ...
    }
}
// End of AddisonWesley namespace declaration
```

Regardless of whether a namespace declaration follows the pattern shown in Listing 9.14, that in Listing 9.15, or a combination of the two, the resultant CIL code will be identical. The same namespace may occur multiple times, in multiple files, and even across assemblies. For example, with the convention of one-to-one correlation between files and classes, you can define each class in its own file and surround it with the same namespace declaration.

Given that namespaces are key for organizing types, it is frequently helpful to use the namespace for organizing all the class files. For this reason, it is helpful to create a folder for each namespace, placing a class such as AddisonWesley.Fezzik.Services.Registration into a folder hierarchy corresponding to the name.

When using Visual Studio projects, if the project name is AddisonWesley.Fezzik, you should create one subfolder called Services into which RegistrationService.cs is placed. You would then create another subfolder—Data, for example—into which you place classes relating to entities within the program—RealestateProperty, Buyer, and Seller, for example.

## Guidelines

- DO prefix namespace names with a company name to prevent namespaces from different companies having the same name.
- DO use a stable, version-independent product name at the second level of a namespace name.
- DO NOT define types without placing them into a namespace.
- CONSIDER creating a folder structure that matches the namespace hierarchy.

## Namespace Alias Qualifier

Namespaces on their own deal with the vast majority of naming conflicts that might arise. Nevertheless, sometimes (albeit rarely) conflict can arise because of an overlap in the namespace and class names. To account for this possibility, the C# 2.0 compiler includes an option for providing an alias with the /reference option. For example, if the assemblies CoordinatesPlus.dll and Coordinates.dll have an overlapping type of Arc, you can reference both assemblies on the command line by assigning

to one or both references a **namespace alias qualifier** that further distinguishes one class from the other (see Output 9.7).

## OUTPUT 9.7

```
csc.exe /R:CoordPlus=CoordinatesPlus.dll /R:Coordinates.dll Program.cs
```

However, adding the alias during compilation is not sufficient on its own. To refer to classes in the aliased assembly, it is necessary to provide an extern directive that declares that the namespace alias qualifier is provided externally to the source code (see Listing 9.16).

## LISTING 9.16: Using the extern Alias Directive

```csharp
// extern must precede all other namespace elements
extern alias CoordPlus;

using System;
using CoordPlus::AddisonWesley.Michaelis.EssentialCSharp
// Equivalent also allowed
// using CoordPlus.AddisonWesley.Michaelis.EssentialCSharp

using global::AddisonWesley.Michaelis.EssentialCSharp
// Equivalent NOT allowed
// using global.AddisonWesley.Michaelis.EssentialCSharp

public class Program
{
    // ...
}
```

Once the extern alias for CoordPlus appears, you can reference the namespace using CoordPlus, followed by either two colons or a period. To ensure that the lookup for the type occurs in the global namespace, C# 2.0 allows items to have the global:: qualifier (but not global., because it could imaginably conflict with a real namespace of global).

## XML Comments

Chapter 1 introduced comments. However, you can use XML comments for more than just notes to other developers reviewing the source code. XML-based comments follow a practice popularized with Java. Although the C# compiler ignores all comments as far as the resultant executable goes, the

developer can use command-line options to instruct the compiler⁴ to extract the XML comments into a separate XML file. By taking advantage of the XML file generation, the developer can generate documentation of the API from the XML comments. In addition, C# editors can parse the XML comments in the code and display them to developers as distinct regions (for example, as a different color from the rest of the code), or parse the XML comment data elements and display them to the developer.

Figure 9.2 demonstrates how an IDE can take advantage of XML comments to assist the developer with a tip about the code he is trying to write. Such coding tips offer significant assistance in large programs, especially when multiple developers share code. For this to work, however, the developer obviously must take the time to enter the XML comments within the code and then direct the compiler to create the XML file. The next section explains how to accomplish this.

![](img/25683ccec0773ba5b8794b11f2b12877_452_0.png)

FIGURE 9.2: XML Comments As Tips in Visual Studio IDE

## Associating XML Comments with Programming Constructs

Consider the listing of the DataStorage class, as shown in Listing 9.17.

4. The C# standard does not specify whether the C# compiler or a separate utility should take care of extracting the XML data. However, all mainstream C# compilers include the necessary functionality via a compile switch instead of within an additional utility.

## LISTING 9.17: Commenting Code with XML Comments

```csharp
/// <summary>
/// DataStorage is used to persist and retrieve
/// employee data from the files.
/// </summary>
class DataStorage
{
    /// <summary>
    /// Save an employee object to a file
    /// named with the Employee name.
    /// </summary>
    /// <remarks>
    /// This method uses
    /// <seealso cref="System.IO.FileStream"/>
    /// in addition to
    /// <seealso cref="System.IO.StreamWriter"/>
    /// </remarks>
    /// <param name="employee">
    /// The employee to persist to a file</param>
    /// <date>January 1, 2000</date>
    public static void Store(Employee employee)
    {
        // ...
    }

    /** <summary>
     * Loads up an employee object
     * </summary>
     * <remarks>
     * This method uses
     * <seealso cref="System.IO.FileStream"/>
     * in addition to
     * <seealso cref="System.IO.StreamReader"/>
     * </remarks>
     * <param name="firstName">
     * The first name of the employee</param>
     * <param name="lastName">
     * The last name of the employee</param>
     * <returns>
     * The employee object corresponding to the names
     * </returns>
     * <date>January 1, 2000</date>**/
    public static Employee Load(
        string firstName, string lastName)
    {
        // ...
    }
}
```

Single-Line XML Comment

XML Delimited Comment
(C# 2.0)
