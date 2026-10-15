
supplied when a generic class is instantiated. You can determine whether a class or method contains generic parameters that have not yet been set by querying the Type.ContainsGenericParameters property, as demonstrated in Listing 17.5.

### LISTING 17.5: Reflection with Generics

```
using System;

public class Program
{
    static void Main()
    {
        Type type;
        type = typeof(System.Nullable<>);
        Console.WriteLine(type.ContainsGenericParameters);
        Console.WriteLine(type.IsGenericType);

        type = typeof(System.Nullable<DateTime>);
        Console.WriteLine(!type.ContainsGenericParameters);
        Console.WriteLine(type.IsGenericType);
    }
}
```

Output 17.3 shows the results of Listing 17.5.

### OUTPUT 17.3

```
True
True
True
True
```

Type.IsGenericType is a Boolean property that evaluates whether a type is generic.

## Obtaining Type Parameters for a Generic Class or Method

You can obtain a list of generic arguments, or type parameters, from a generic class by calling the GetGenericArguments() method. The result is an array of System.Type instances that corresponds to the order in which they are declared as type parameters of the generic class. Listing 17.6 reflects into a generic type and obtains each type parameter; Output 17.4 shows the results.

- The C# compiler ensures that the argument to the nameof operator is, in fact, a valid program element. This helps prevent errors when a program element name is changed, helps prevent misspellings, and so on.
- IDE tools work better with the nameof operator than with literal strings. For example, the “find all references” tool will find program elements mentioned in a nameof expression, but not in a literal string. The automatic renaming refactoring also works better, and so on.

In the snippet given earlier, nameof(textDigit) produces the name of a parameter. However, the nameof operator works with any program element. For example, Listing 17.7 uses nameof to pass the property name to INotifyPropertyChanged.PropertyChanged.

### LISTING 17.7: Dynamically Invoking a Member

```
using System.ComponentModel;

public class Person : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;
    public Person(string name)
    {
        Name = name;
    }
    private string _Name;
    public string Name
    {
        get { return _Name; }
        set
        {
            if (_Name != value)
            {
                _Name = value;
                // Using C# 6.0 conditional null reference.
                PropertyChanged?.Invoke(
                    this,
                    new PropertyChangedEventArgs(
                        nameof(Name)));
            }
        }
    }
    // ...
}
```

Notice that whether only the unqualified “Name” is provided (because it’s in scope) or the fully (or partially) qualified name like Person.Name is used, the result is only the final identifier (the last element in a dotted name).

You can still use C# 5.0’s CallerMemberName parameter attribute to obtain a property’s name; see http://itl.tc/CallerMemberName for an example.

## Attributes

Before delving into details on how to program attributes, we should consider a use case that demonstrates their utility. In the CommandLineHandler example in Listing 17.3, you dynamically set a class’s properties based on the command-line option matching the property name. This approach is insufficient, however, when the command-line option is an invalid property name. /?, for example, cannot be supported. Furthermore, this mechanism doesn’t provide any way of identifying which options are required versus which are optional.

Instead of relying on an exact match between the option name and the property name, attributes provide a way of identifying additional metadata about the decorated construct—in this case, the option that the attribute decorates. With attributes, you can decorate a property as Required and provide a /? option alias. In other words, attributes are a means of associating additional data with a property (and other constructs).

Attributes appear within square brackets preceding the construct they decorate. For example, you can modify the CommandLineInfo class to include attributes, as shown in Listing 17.8.

### LISTING 17.8: Decorating a Property with an Attribute

```
class CommandLineInfo
{
    [CommandLineSwitchAlias("?")]
    public bool Help { get; set; }

    [CommandLineSwitchRequired]
    public string Out { get; set; }

    public System.Diagnostics.ProcessPriorityClass Priority
    { get; set; } =
        System.Diagnostics.ProcessPriorityClass.Normal;
}
```

In Listing 17.8, the Help and Out properties are decorated with attributes. The purpose of these attributes is to allow an alias of /? for /Help, and to indicate that /Out is a required parameter. The idea is that from within the CommandLineHandler.TryParse() method, you enable support for option aliases and, assuming the parsing was successful, you check that all required switches were specified.

There are two ways to combine attributes on the same construct. First, you can separate the attributes with commas within the same square brackets. Alternatively, you can place each attribute within its own square brackets. Listing 17.9 provides examples.

### LISTING 17.9: Decorating a Property with Multiple Attributes

```
[CommandLineSwitchRequired]
[CommandLineSwitchAlias("FileName")]
public string Out { get; set; }
```

```
[CommandLineSwitchRequired,
CommandLineSwitchAlias("FileName")]
public string Out { get; set; }
```

In addition to decorating properties, developers can use attributes to decorate classes, interfaces, structs, enums, delegates, events, methods, constructors, fields, parameters, return values, assemblies, type parameters, and modules. For the majority of these cases, applying an attribute involves the same square bracket syntax shown in Listing 17.9. However, this syntax doesn’t work for return values, assemblies, and modules.

Assembly attributes are used to add metadata about the assembly. Visual Studio’s Project Wizard, for example, generates an AssemblyInfo.cs file that includes numerous attributes about the assembly. Listing 17.10 is an example of such a file.

### LISTING 17.10: Assembly Attributes within AssemblyInfo.cs

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
[assembly: AssemblyCompany("IntelliTect")]
[assembly: AssemblyProduct("Compression Library")]
[assembly: AssemblyCopyright("Copyright© IntelliTect 2006-2015")]
[assembly: AssemblyTrademark("")]
[assembly: AssemblyCulture("")]

// Setting ComVisible to false makes the types in this
// assembly not visible to COM components. If you need to
// access a type in this assembly from COM, set the ComVisible
// attribute to true on that type.
[assembly: ComVisible(false)]

// The following GUID is for the ID of the typelib
// if this project is exposed to COM.
[assembly: Guid("417a9609-24ae-4323-b1d6-cef0f87a42c3")]

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
// [assembly: AssemblyVersion("1.0.*")]
[assembly: AssemblyVersion("1.0.0.0")]
[assembly: AssemblyFileVersion("1.0.0.0")]
```

The assembly attributes define things such as the company, product, and assembly version number. Similar to assembly, identifying an attribute usage as module requires prefixing it with module:. The restriction on assembly and module attributes is that they must appear after the using directive but before any namespace or class declarations. The attributes in Listing 17.10 are generated by the Visual Studio Project Wizard and should be included in all projects to mark the resultant binaries with information about the contents of the executable or DLL.

Return attributes, such as the one shown in Listing 17.11, appear before a method declaration but use the same type of syntax structure.

### LISTING 17.11: Specifying a Return Attribute

```
[return: Description(
    "Returns true if the object is in a valid state.")]
public bool IsValid()
{
    // ...
    return true;
}
```
