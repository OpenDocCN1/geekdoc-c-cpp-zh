```
```csharp
MemberInfo [] Members = t.GetMembers();

foreach (MemberInfo NextMember in Members)
{
    AddToOutput(NextMember.DeclaringType + " " +
    NextMember.MemberType + " " + NextMember.Name);
}
```
```

You implement the AnalyzeType() method by calling various properties of the Type object to get the information you need concerning the type names, then call the GetMembers() method to get an array of MemberInfo objects that you can use to display the details of each member. Note that you use a helper method, AddToOutput(), to build up the text to be displayed in the message box:

```
```csharp
static void AddToOutput(string Text)
{
    OutputText.Append("\n" + Text);
}
```
```

Compile the TypeView assembly using this command:

```
```
csc /reference:System.Windows.Forms.dll Program.cs
```
```

# The Assembly Class

The Assembly class is defined in the System.Reflection namespace and provides access to the metadata for a given assembly. It also contains methods to allow you to load and even execute an assembly — assuming that the assembly is an executable. As with the Type class, Assembly contains a large number of methods and properties — too many to cover here. Instead, this section is confined to covering those methods and properties that you need to get started and that you will use to complete the WhatsNewAttributes example.

Before you can do anything with an Assembly instance, you need to load the corresponding assembly into the running process. You can do this with either the static members Assembly.Load() or Assembly.LoadFrom(). The difference between these methods is that Load() takes the name of the assembly, and the runtime searches in a variety of locations in an attempt to locate the assembly. These locations include the local directory and the global assembly cache. LoadFrom() takes the full path name of an assembly and does not attempt to find the assembly in any other location:

```
```csharp
Assembly assembly1 = Assembly.Load("SomeAssembly");
Assembly assembly2 = Assembly.LoadFrom
    ("C:\My Projects\Software\SomeOtherAssembly");
```
```

A number of other overloads of both methods exist, which supply additional security information. After you have loaded an assembly, you can use various properties on it to find out, for example, its full name:

```
```csharp
string name = assembly1.FullName;
```
```

# Finding Out About Types Defined in an Assembly

One nice feature of the Assembly class is that it allows you to obtain details of all the types that are defined in the corresponding assembly. You simply call the Assembly.GetTypes() method, which returns an array of System.Type references containing details of all the types. You can then manipulate these Type references as explained in the previous section:

```
```csharp
Type[] types = theAssembly.GetTypes();

foreach(Type definedType in types)
{
    DoSomethingWith(definedType);
}
```
```