

```
set { _Priority = value; }
}
private System.Diagnostics.ProcessPriorityClass _Priority =
System.Diagnostics.ProcessPriorityClass.Normal;
}
```

In Listing 17.7, the Help and Out properties are decorated with attributes. The purpose of these attributes is to allow an alias of /? for /Help, and to indicate that /Out is a required parameter. The idea is that from within the CommandLineHandler.TryParse() method, you enable support for option aliases and, assuming the parsing was successful, you can check that all the required switches were specified.

There are two ways to combine attributes on the same construct. You can either separate the attributes with commas within the same square brackets, or place each attribute within its own square brackets, as shown in Listing 17.8.

### LISTING 17.8: Decorating a Property with Multiple Attributes

```
[CommandLineSwitchRequired]
[CommandLineSwitchAlias("FileName")]
public string Out
{
get { return _Out; }
set { _Out = value; }
}
```

```
[CommandLineSwitchRequired,
CommandLineSwitchAlias("FileName")]
public string Out
{
get { return _Out; }
set { _Out = value; }
}
```

In addition to decorating properties, developers can use attributes to decorate classes, interfaces, structs, enums, delegates, events, methods, constructors, fields, parameters, return values, assemblies, type parameters, and modules. For the majority of these, applying an attribute involves the same square bracket syntax shown in Listing 17.8. However, this syntax doesn’t work for return values, assemblies, and modules.

Assembly attributes are used to add additional metadata about the assembly. Visual Studio's Project Wizard, for example, generates an AssemblyInfo.cs file that includes numerous attributes about the assembly. Listing 17.9 is an example of such a file.

### Listing 17.9: Assembly Attributes within AssemblyInfo.cs

```
using System.Reflection;
using System.Runtime.CompilerServices;
using System.Runtime.InteropServices;

// General information about an assembly is controlled
// through the following set of attributes. Change these
// attribute values to modify the information
// associated with an assembly.
[assembly: AssemblyTitle("CompressionLibrary")]
[assembly: AssemblyDescription("")]
[assembly: AssemblyConfiguration("")]
[assembly: AssemblyCompany("Michaelis.net")]
[assembly: AssemblyProduct("CompressionLibrary")]
[assembly: AssemblyCopyright("Copyright © Michaelis.net 2006")]
[assembly: AssemblyTrademark("")]
[assembly: AssemblyCulture("")]

// Setting ComVisible to false makes the types in this
// assembly not visible to COM components. If you need to
// access a type in this assembly from COM, set the ComVisible
// attribute to true on that type.
[assembly: ComVisible(false)]

// The following GUID is for the ID of the typelib if this project is exposed to COM
[assembly: Guid("417a9609-24ae-4223-b1d6-cf0f878a42c3")]

// Version information for an assembly consists
// of the following four values:
//
//      Major Version
//      Minor Version
//      Build Number
//      Revision
//
// You can specify all the values or you can
// default the Revision and Build Numbers
// by using the '*' as shown below:
[assembly: AssemblyVersion("1.0.0.0")]
[assembly: AssemblyFileVersion("1.0.0.0")]
```

The assembly attributes define things such as company, product, and assembly version number. Similar to assembly, identifying an attribute usage as module requires prefixing it with module:. The restriction on assembly and module attributes is that they appear after the using directive but before any namespace or class declarations.

Return attributes, such as the one shown in Listing 17.10, appear before a method declaration but use the same type of syntax structure.

### LISTING 17.10: Specifying a Return Attribute

```
[return: Description("Returns true if the object is in a valid state.")]
public bool IsValid()
{
    // ...
    return true;
}
```

In addition to assembly: and return:, C# allows for explicit target identifications of module:, class:, and method:, corresponding to attributes that decorate the module, class, and method. class: and method:, however, are optional, as demonstrated earlier.

One of the conveniences of using attributes is that the language takes into consideration the attribute naming convention, which is to place Attribute at the end of the name. However, in all the attribute uses in the preceding listings, no such suffix appears, despite the fact that each attribute used follows the naming convention. This is because although the full name (DescriptionAttribute, AssemblyVersionAttribute, and so on) is allowed when applying an attribute, C# makes the suffix optional. Generally, no such suffix appears when applying an attribute; it appears only when defining one or using the attribute inline (such as typeof(DescriptionAttribute)).

## Custom Attributes

Defining a custom attribute is relatively trivial. Attributes are objects; therefore, to define an attribute, you need to define a class. The characteristic that turns a general class into an attribute is that it derives from System.Attribute. Therefore, you can create a CommandLineSwitchRequiredAttribute class, as shown in Listing 17.11.

### LISTING 17.11: Defining a Custom Attribute

```
public class CommandLineSwitchRequiredAttribute : Attribute
{
}
```

With that simple definition, you now can use the attribute as demonstrated in Listing 17.7. So far, no code responds to the attribute; therefore, the Out property that includes the attribute will have no effect on command-line parsing.

## Looking for Attributes

In addition to providing properties for reflecting on a type's members, Type includes methods to retrieve the Attributes decorating that type. Similarly, all the reflection types (PropertyInfo and MethodInfo, for example) include members for retrieving a list of attributes that decorate a type. Listing 17.12 defines a method to return a list of required switches that are missing from the command line.

### LISTING 17.12: Retrieving a Custom Attribute

```
using System;
using System.Collections.Specialized;
using System.Reflection;

public class CommandLineSwitchRequiredAttribute : Attribute
{
    public static string[] GetMissingRequiredOptions(
        object commandLine)
    {
        StringCollection missingOptions = new StringCollection();
        PropertyInfo[] properties =
            commandLine.GetType().GetProperties();

        foreach (PropertyInfo property in properties)
        {
            Attribute[] attributes =
                (Attribute[])property.GetCustomAttributes(
                    typeof(CommandLineSwitchRequiredAttribute),
                    false);
            if ((attributes.Length > 0) &&
                (property.GetValue(commandLine, null) == null))
            {
                if (property.GetValue(commandLine, null) == null)
                {
                    missingOptions.Add(property.Name);
                }
                return missingOptions.Add(property.Name);
            }
        }
    }
}
```

The code that checks for an attribute is relatively simple. Given a PropertyInfo object (obtained via reflection), you call GetCustomAttributes() and specify the attribute sought, followed by whether to check any overloaded methods. (Alternatively, you can call the GetCustomAttributes() method without the attribute type to return all of the attributes.)

Although it is possible to place code for finding the CommandLineSwitchRequiredAttribute attribute within the CommandLineHandler's code directly, it makes for better object encapsulation to place the code within the CommandLineSwitchRequiredAttribute class itself. This is frequently the pattern for custom attributes. What better location to place code for finding an attribute than in a static method on the attribute class?

## Initializing an Attribute through a Constructor

The call to GetCustomAttributes() returns an array of objects that will successfully cast to an Attribute array. However, since the attribute in this example didn't have any instance members, the only metadata information that it provided in the returned attribute was whether it appeared. Attributes can also encapsulate data, however. Listing 17.13 defines a CommandLineAliasAttribute attribute. This is another custom attribute, and it provides alias command-line options. For example, you can provide command-line support for /help or /? as an abbreviation. Similarly, /s could provide an alias to /Subfolders that indicates that the command should traverse all the subdirectories.

To support this, you need to provide a constructor on the attribute. Specifically, for the alias you need a constructor that takes a string argument. (Similarly, if you want to allow multiple aliases, you need to define an attribute that has a params string array for a parameter.)

