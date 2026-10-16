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

# Using Resource Files with ResourceManager

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