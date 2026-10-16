
public members:
- System.Double Method IsInfinity
- System.Double Method IsPositiveInfinity
- System.Double Method IsNegativeInfinity
- System.Double Method IsNaN
- System.Double Method CompareTo
- System.Double Method CompareTo
- System.Double Method Equals
- System.Double Method op_Equality
- System.Double Method op_Inequality
- System.Double Method op_LessThan
- System.Double Method op_GreaterThan
- System.Double Method op_LessThanOrEqual
- System.Double Method op_GreaterThanOrEqual
- System.Double Method Equals
- System.Double Method GetHashCode
- System.Double Method ToString
- System.Double Method ToString
- System.Double Method ToString
- System.Double Method ToString
- System.Double Method Parse
- System.Double Method Parse
- System.Double Method Parse
- System.Double Method Parse
- System.Double Method TryParse
- System.Double Method TryParse
- System.Double Method GetTypeCode
- System.Object Method GetType
- System.Double Field MinValue
- System.Double Field MaxValue
- System.Double Field Epsilon
- System.Double Field NegativeInfinity
- System.Double Field PositiveInfinity
- System.Double Field NaN

The console displays the name, full name, and namespace of the data type as well as the name of the base type. Next, it simply iterates through all the public instance members of the data type, displaying for each member the declaring type, the type of member (method, field, and so on), and the name of the member. The declaring type is the name of the class that actually declares the type member (for example, System.Double if it is defined or overridden in System.Double, or the name of the relevant base type if the member is simply inherited from a base class).

TypeView does not display signatures of methods because you are retrieving details about all public instance members through MemberInfo objects, and information about parameters is not available through a MemberInfo object. To retrieve that information, you would need references to MethodInfo and other more specific objects, which means that you would need to obtain details about each type of member separately.

The sample code for TypeView makes use of the following dependencies and namespaces:

## Dependencies

```
NETStandard.Library
```

## Namespaces

- System
- System.Reflection
- System.Text
- static System.Console

TypeView does display details about all public instance members; but for doubles, the only details defined are fields and methods. The code for TypeView is as follows. To begin, you need to add a few using statements:

```
using System;
using System.Reflection;
using System.Text;
using static System.Console;
```

You need System.Text because you use a StringBuilder object to build up the text. The entire code is in one class, Program, which has a couple of static methods and one static field, a StringBuilder instance called OutputText, which is used to build the text to be displayed in the message box. The main method and class declaration look like this:

```csharp
class Program
{
    private static StringBuilder OutputText = new StringBuilder();

    static void Main()
    {
        // modify this line to retrieve details of any other data type
        Type t = typeof(double);

        AnalyzeType(t);
        WriteLine($"Analysis of type {t.Name}");
        WriteLine(OutputText.ToString());
        ReadLine();
    }
}
```

The Main method implementation starts by declaring a Type object to represent your chosen data type. You then call a method, AnalyzeType, which extracts the information from the Type object and uses it to build the output text. Finally, you write the output to the console. AnalyzeType is where the bulk of the work is done:

```csharp
static void AnalyzeType(Type t)
{
    TypeInfo typeInfo = t.GetTypeInfo();
    AddToOutput($"Type Name: {t.Name}");
    AddToOutput($"Full Name: {t.FullName}");
    AddToOutput($"Namespace: {t.Namespace}");

    Type tBase = t.BaseType;

    if (tBase != null)
    {
        AddToOutput($"Base Type: {tBase.Name}");
    }
}
```

```csharp
}
AddToOutput("\npublic members:");
foreach (MemberInfo NextMember in t.GetMembers())
{
#if DNXCORE
AddToOutput($"{member.DeclaringType} {member.Name} ");
#else
AddToOutput($"{member.DeclaringType} {member.MemberType} {member.Name} ");
#endif
}
```

You implement the AnalyzeType method by calling various properties of the Type object to get the information you need concerning the type names and then calling the GetMembers method to get an array of MemberInfo objects that you can use to display the details for each member. Note that you use a helper method, AddToOutput, to build the text to be displayed:

```csharp
static void AddToOutput(string Text)
{
    OutputText.Append("\n" + Text);
}
```

## The Assembly Class

The Assembly class is defined in the System.Reflection namespace and provides access to the metadata for a given assembly. It also contains methods that enable you to load and even execute an assembly— assuming that the assembly is an executable. As with the Type class, Assembly contains too many methods and properties to cover here, so this section is confined to covering those methods and properties that you need to get started and that you use to complete the WhatsNewAttributes example.

Before you can do anything with an Assembly instance, you need to load the corresponding assembly into the running process. You can do this with either the static members Assembly.Load or Assembly.LoadFrom. The difference between these methods is that Load takes the name of the assembly, and the runtime searches in a variety of locations in an attempt to locate the assembly. These locations include the local directory and the global assembly cache. LoadFrom takes the full path name of an assembly and does not attempt to find the assembly in any other location:

```csharp
Assembly assembly1 = Assembly.Load("SomeAssembly");
Assembly assembly2 = Assembly.LoadFrom
(@"C:\My Projects\Software\SomeOtherAssembly");
```

A number of other overloads of both methods exist, which supply additional security information. After you have loaded an assembly, you can use various properties on it to find out, for example, its full name:

```csharp
string name = assembly1.FullName;
```

## Getting Details About Types Defined in an Assembly

One nice feature of the Assembly class is that it enables you to obtain details about all the types that are defined in the corresponding assembly. You simply call the Assembly.GetTypes method, which returns an array of System.Type references containing details about all the types. You can then manipulate these Type references as explained in the previous section:

```csharp
Type[] types = theAssembly.GetTypes();

foreach(Type definedType in types)
{
    DoSomethingWith(definedType);
}
```

## Getting Details About Custom Attributes

The methods you use to find out which custom attributes are defined on an assembly or type depend on the type of object to which the attribute is attached. If you want to find out what custom attributes are attached to an assembly as a whole, you need to call a static method of the Attribute class, GetCustomAttributes, passing in a reference to the assembly:

> NOTE This is actually quite significant. You might have wondered why, when you defined custom attributes, you had to go to all the trouble of actually writing classes for them, and why Microsoft didn’t come up with some simpler syntax. Well, the answer is here. The custom attributes genuinely exist as objects, and when an assembly is loaded you can read in these attribute objects, examine their properties, and call their methods.

```csharp
Attribute[] definedAttributes = Attribute.GetCustomAttributes(assembly1);
// assembly1 is an Assembly object
```

GetCustomAttributes, which is used to get assembly attributes, has a few overloads. If you call it without specifying any parameters other than an assembly reference, it simply returns all the custom attributes defined for that assembly. You can also call GetCustomAttributes by specifying a second parameter, which is a Type object that indicates the attribute class in which you are interested. In this case, GetCustomAttributes returns an array consisting of all the attributes present that are of the specified type.

Note that all attributes are retrieved as plain Attribute references. If you want to call any of the methods or properties you defined for your custom attributes, you need to cast these references explicitly to the relevant custom attribute classes. You can obtain details about custom attributes that are attached to a given data type by calling another overload of Assembly.GetCustomAttributes, this time passing a Type.
