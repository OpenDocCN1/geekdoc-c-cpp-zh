
Converter={StaticResource boolToVisiblity}" />
</Grid>

When you start the application, you can see all available cultures in the tree view, and selecting a culture lists its characteristics, as shown in Figure 28.6.

![](img/3d365b72b289213a91ade7eb366b8f35_1041_0.png)

## Figure 28.6

## Sorting

The sample SortingDemo makes use of the following dependencies and namespaces:

### Dependencies

```
NETStandard.Library
```

```
System.Collections.NonGeneric
```

### Namespaces

```
System
```

```
System.Collections
```

```
System.Collections.Generic
```

```
System.Globalization
```

```
static System.Console
```

Sorting strings varies according to the culture. The algorithms that compare strings for sorting by default are culture-specific. For example, in Finnish the characters V and W are treated the same. To demonstrate this behavior with a Finnish sort, the following code creates a small sample console application in which some U.S. states are stored unsorted inside an array.

The method DisplayNames shown here is used to display all elements of an array or a collection on the console (code file SortingDemo/Program.cs):

```
public static void DisplayNames(string title,
IEnumerable<string> e)
{
    WriteLine(title);
    WriteLine(string.Join("-", e));
    WriteLine();
}
```

In the Main method, after creating the array with some of the U.S. states, the thread property CurrentCulture is set to the Finnish culture so that the following Array.Sort uses the Finnish sort order. Calling the method DisplayNames displays all the states on the console:

```
public static void Main()
{
    string[] names = {"Alabama","Texas","Washington","Virginia",
"Wisconsin","Wyoming","Kentucky","Missouri","Utah",
"Hawaii","Kansas","Louisiana","Alaska","Arizona"};

    CultureInfo.CurrentCulture = new CultureInfo("fi-FI");

    Array.Sort(names);
    DisplayNames("Sorted using the Finnish culture", names);
    // etc.
}
```

After the first display of some U.S. states in the Finnish sort order, the array is sorted once again. If you want a sort that is independent of the users’ culture, which would be useful when the sorted array is sent to a server or stored somewhere, you can use the invariant culture.

You can do this by passing a second argument to Array.Sort. The Sort method expects an object implementing IComparer with the second argument. The Comparer class from the System.Collections namespace implements IComparer. Comparer.DefaultInvariant returns a Comparer object that uses the invariant culture for comparing the array values for a culture-independent sort:

```
public static void Main()
{
    // etc.
    // sort using the invariant culture
    Array.Sort(names,
System.Collections.Comparer.DefaultInvariant);
    DisplayNames("Sorted using the invariant culture", names);
}
```

The program output shows different sort results with the Finnish and culture-independent cultures—Virginia is before Washington when using the invariant sort order, and vice versa when using Finnish:

```
Sorted using the Finnish culture
Alabama-Alaska-Arizona-Hawaii-Kansas-Kentucky-Louisiana-
Missouri-Texas-Utah-
Washington-Virginia-Wisconsin-Wyoming

Sorted using the invariant culture
Alabama-Alaska-Arizona-Hawaii-Kansas-Kentucky-Louisiana-
```

> **NOTE** *If sorting a collection should be independent of a culture, the collection must be sorted with the invariant culture. This can be particularly useful when sending the sort result to a server or storing it inside a file. To display a sorted collection to the user, it’s best to sort it with the user’s culture.*

In addition to a locale-dependent formatting and measurement system, text and pictures may differ depending on the culture. This is where resources come into play.

## Resources

You can put resources such as pictures or string tables into resource files or satellite assemblies. Such resources can be very helpful when localizing applications, and .NET has built-in support to search for localized resources. Before you see how to use resources to localize applications, the following sections explain how you can create and read resources without looking at language aspects.

## Resource Readers and Writers

With .NET Core, the resource readers and writers are limited compared to the full .NET version (at the time of this writing). However, for many scenarios—including multiplatform support—what is needed is available.

The `CreateResource` sample application creates a resource file dynamically, and reads resources from the file. This sample makes use of the following dependencies and namespaces:

### Dependencies

- `NETStandard.Library`
- `System.Resources.ReaderWriter`

### Namespaces

- `System.Collections`
- `System.IO`
- `System.Resources`
- `static System.Console`

`ResourceWriter` enables you to create binary resource files. The constructor of the writer requires a `Stream` that is created using the `File` class. You add resources by using the `AddResource` method. The simple resource writer for .NET Core requires strings with both the key and the value. The resource writer for the full .NET Framework defines

> **NOTE** *When saving text files with Unicode characters, you must save the file with the proper encoding. To select the UTF8 encoding, use the Save As dialog.*

You can use the Resource File Generator (`Resgen.exe`) utility to create a resource file out of `Wrox.ProCSharp.Localization.MyResources.txt`. Typing the line

```
resgen Wrox.ProCSharp.Localization.MyResources.txt
```

creates the file `Wrox.ProCSharp.Localization.MyResources.resources`. The resulting resource file can be either added to an assembly as an external file or embedded into the DLL or EXE. Resgen also supports the creation of XML-based `.resX` resource files. One easy way to build an XML file is by using Resgen itself:

```
resgen Wrox.ProCSharp.Localization.MyResources.txt
  Wrox.ProCSharp.Localization.MyResources.resX
```

This command creates the XML resource file `Wrox.ProCSharp.LocalizationMyResources.resX`. Resgen supports strongly typed resources. A strongly typed resource is represented by a class that accesses the resource. You can create the class with the `/str` option of the Resgen utility:

```
resgen
/str:C#,Wrox.ProCSharp.Localization,MyResources,MyResources.cs
Wrox.ProCSharp.Localization.MyResources.resX
```

With the `/str` option, the language, namespace, class name, and filename for the source code are defined, in that order.

## Using Resource Files with ResourceManager

With the old C# compiler `csc.exe`, you can add resource files to assemblies using the `/resource` option. With the new .NET Core compiler, you need to add a `resx` file to the folder, and it will be embedded within the assembly. By default, all `resx` files are embedded in the assembly. You can customize this by using the `resource`, `resourceFiles`, and `resourceExclude` nodes in the `project.json` file.

The default setting for `resource` is to embed all resource files:

```
"resource": ["embed/** /*.*"]
```

To define that the directories `foo` and `bar` should be excluded, you define the `resourceExclude`:

```
"resourceExclude": ["foo/** /*.resx","bar/** /*.*"],
```

To define specific resource files, you use the `resourceFiles` node:

```
"resourceFiles":
["embed/Resources/Sample.resx","embed/Views/View1.resources"],
```

To see how resource files can be loaded with the `ResourceManager` class, create a Console Application (Package) and name it `ResourcesDemo`. This sample makes use of the following dependencies and namespaces:

### Dependencies

NETStandard.Library

### Namespaces

- `System.Globalization`
- `System.Reflection`
- `System.Resources`
- `static System.Console`

Create a `Resources` folder, and add a `Messages.resx` file to this folder. The `Messages.resx` file is filled with a key and value for English-US content—for example, the key `GoodMorning` and the value `Good Morning!` This will be the default language. You can add other language resource files with the naming convention to add the culture to the resource file, for example, `Messages.de.resx` for German languages and `Messages.de-AT.resx` for Austrian differences.

To access the embedded resource, use the `ResourceManager` class from the `System.Resources` namespace and the `System.Resources.ResourceManager` NuGet package. When you’re instantiating the `ResourceManager`, one overload of the constructor needs the name of the resource and the assembly. The namespace of the application is `ResourcesDemo`; the resource file is in the folder `Resources`, which defines the sub-namespace Resources, and it has the name `Messages.resx`. This defines the name `ResourcesDemo.Resources.Messages`. You can retrieve the assembly of the resource using the `GetTypeInfo` method of the `Program` type, which defines an `Assembly` property. Using the resources instance, the `GetString` method returns the value of the key passed from the resource file. Passing a culture such as de-AT for the second argument looks for resources in the de-AT resource file. If it’s not found there, the neutral language for de is taken, the de resource file. If it’s not found there, the default resource file without culture naming succeeds to return the value (code file `ResourcesDemo/Program.cs`):

```
var resources = new
ResourceManager("ResourcesDemo.Resources.Messages",
    typeof(Program).GetTypeInfo().Assembly);
string goodMorning = resources.GetString("GoodMorning",
    new CultureInfo("de-AT"));
WriteLine(goodMorning);
```

Another overload of the `ResourceManager` constructor just requires the type of the class. This `ResourceManager` looks for a resource file named `Program.resx`:

```
var programResources = new ResourceManager(typeof(Program));
```
