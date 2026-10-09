
![](img/ef6a8a417630b222bfb3f3b949facff0_473_0.png)

**FIGURE 10.2: The Project Menu**

![](img/ef6a8a417630b222bfb3f3b949facff0_473_1.png)

**FIGURE 10.3: The Browse Filter**

3. Click the **Install** button to install the package into the project.

Upon completion of these steps, it is possible to begin using the Microsoft.Extensions.CommandLineUtils library.

As with Dotnet CLI, you can use Visual Studio 2017 to build your own NuGet package using the **Build->Pack <Project Name>** menu item. Similarly, you can specify the package version number from the **Package** tab of the **Project Properties**.

## Invoking a NuGet Package

Once the package is referenced, you can begin using it as though all the source code was included in the project. Listing 10.12 shows, for example, how to use the Microsoft.Extensions.CommandLineUtils library, and Output 10.4 shows the sample output.

```csharp
Listing 10.12: Invoking a NuGet Package Reference
public class Program
{
    public static void Main(string[] args)
    {
        CommandLineApplication commandLineApplication =
            new CommandLineApplication(throwOnUnexpectedArg: false);
        CommandLineArgument name = commandLineApplication.Argument(
            "name", "Enter the full name of the person to be greeted.");
        CommandLineOption greeting = commandLineApplication.Option(
            "-g|g|--greeting <greeting>",
            "The greeting to display. The greeting supports"
            + " a format string where '{name}' will be "
            + "substituted with the name.",
            CommandLineOptionType.SingleValue);
        commandLineApplication.HelpOption("? | -h | --help");
        commandLineApplication.Execute(args);
        if (!greeting.HasValue())
        {
            Console.WriteLine($"Hello {name.Value}.");
        }
        else
        {
            Console.WriteLine(
                greeting.Value().Replace("{name}", name.Value));
        }
    }
}
```

```text
OUTPUT 10.4
>dotnet run "Inigo Montoya" -g "Hello {name}. Welcome!"
Hello Inigo Montoya. Welcome!"
```

This library is used to parse both arguments and options from the command line where options have switches to identify them, while arguments are void of such switches. See Table 10.1 for examples.

### TABLE 10.1: Microsoft.Extensions.CommandLineUtils Examples

| Argument Type | Example | Explanation |
| :-- | :-- | :-- |
| Options | `Program.exe -f=Inigo -L Montoya -hello` | Option -f with value "Inigo"<br>Option -L with value "Montoya"<br>Option -hello with value "on" |
| Command with argument | `Program.exe hello "Inigo" "Montoya"` | Command "hello"<br>Argument "Inigo"<br>Argument "Montoya" |
| Symbols | `Program.exe -?` | Display help |

## ADVANCED TOPIC

### Encapsulation of Types

Just as classes serve as an encapsulation boundary for behavior and data, so assemblies provide for similar boundaries among groups of types. Developers can break a system into assemblies and then share those assemblies with multiple applications or integrate them with assemblies provided by third parties.

### public or internal Access Modifiers on Type Declarations

By default, a class without any access modifier is defined as *internal*.<sup>1</sup> The result is that the class is inaccessible from outside the assembly. Even though another assembly references the assembly containing the class, all internal classes within the referenced assemblies will be inaccessible.

Just as *private* and *protected* provide levels of encapsulation to members within a class, so C# supports the use of access modifiers at the class level for control over the encapsulation of the classes within an assembly. The access modifiers available are *public* and *internal*. To expose a class outside the assembly, the assembly must be marked as *public*. Therefore, before compiling the Coordinates.dll assembly, it is necessary to modify the type declarations as public (see Listing 10.13).

```csharp
Listing 10.13: Making Types Available outside an Assembly

public struct Coordinate
{
// ...
}

public struct Latitude
{
// ...
}

public struct Longitude
{
// ...
}

public struct Arc
{
// ...
}
```

Similarly, declarations such as class and enum can be either public or internal.<sup>2</sup>

The internal access modifier is not limited to type declarations; that is, it is also available on type members. Consequently, you can designate a type as public but mark specific methods within the type as internal so that the members are available only from within the assembly. It is not possible for the members to have a greater accessibility than the type. If the class is declared as internal, public members on the type will be accessible only from within the assembly.

### The protected internal Type Modifier

Another type member access modifier is protected internal. Members with an accessibility modifier of protected internal will be accessible from all locations within the containing assembly and from classes that derive from the type, even if the derived class is not in the same assembly. The default state is private, so when you add an access modifier (other than public), the member becomes slightly more visible. Adding two modifiers compounds this effect.

> **NOTE**
> Members with an accessibility modifier of *protected internal* will be accessible from all locations within the containing assembly *and* from classes that derive from the type, even if the derived class is not in the same assembly.

### BEGINNER TOPIC

### Type Member Accessibility Modifiers

The full list of access modifiers appears in Table 10.2.

**TABLE 10.2: Accessibility Modifiers**

| Modifier | Description |
| :--- | :--- |
| public | Declares that the member is accessible anywhere the type is accessible. If the class is *internal*, the member will be internally visible. Public members will be accessible from outside the assembly if the containing type is public. |
| internal | The member is accessible from within the assembly only. |
| private | The member is accessible from within the containing type but inaccessible otherwise. |
| protected | The member is accessible within the containing type and any subtypes derived from it, regardless of assembly. |
| protected internal | The member is accessible from anywhere within the containing assembly *and* from any types derived from the containing type, even if the derived types are within a different assembly. |
| private protected | The member is accessible from any types derived from the containing type that are also in the same assembly. (This feature was added in C# 7.2.) |

## Defining Namespaces

As mentioned in Chapter 2, all data types are identified by the combination of their namespace and their name. However, in the CLR, there is no such thing as a “namespace.” The type's name actually is the fully qualified type name, including the namespace. For the classes you defined earlier, there was no explicit namespace declaration. Classes such as these are automatically declared as members of the default global namespace. It is likely that such classes will experience a name collision, which occurs when you attempt to define two classes with the same name. Once you begin referencing other assemblies from third parties, the likelihood of a name collision increases even further.

More important, there are thousands of types in the CLI framework and multiple orders of magnitude more outside the framework. Finding the right type for a particular problem, therefore, could potentially be a significant battle.

The resolution to both of these problems is to organize all the types, grouping them into logical related categories called namespaces. For example, classes outside the `System` namespace are generally placed into a namespace corresponding with the company, product name, or both. Classes from Addison-Wesley, for example, are placed into an `Awl` or `AddisonWesley` namespace, and classes from Microsoft (not `System` classes) are located in the `Microsoft` namespace. The second level of a namespace should be a stable product name that will not vary between versions. Stability, in fact, is key at all levels. Changing a namespace name is a version-incompatible change that should be avoided. For this reason, avoid using volatile names (organization hierarchy, fleeting brands, and so on) within a namespace name.

Namespaces should be PascalCase, but if your brand uses nontraditional casing, it is acceptable to use the brand casing. (Consistency is key, so if that will be problematic—with Pascal or brand-based casing—favor the use of whichever convention will produce the greater consistency.) You should use the namespace keyword to create a namespace and to assign a class to it, as shown in Listing 10.14.
