```
```csharp
IList<CustomAttributeData> attributes =
    CustomAttributeData.GetCustomAttributes(attributeTarget);

Console.WriteLine("Attributes applied to {0}: {1}",
    attributeTarget.Name, (attributes.Count == 0 ? "None" : String.Empty));

foreach (CustomAttributeData attribute in attributes) {
    // Display the type of each applied attribute
    Type t = attribute.Constructor.DeclaringType;
    Console.WriteLine("{0}", t.ToString());
    Console.WriteLine("  Constructor called={0}", attribute.Constructor);

    IList<CustomAttributeTypedArgument> posArgs = attribute.ConstructorArguments;
    Console.WriteLine("  Positional arguments passed to constructor: " +
        ((posArgs.Count == 0) ? " None" : String.Empty));
    foreach (CustomAttributeTypedArgument pa in posArgs) {
        Console.WriteLine("    Type={0}, Value={1}", pa.ArgumentType, pa.Value);
    }

    IList<CustomAttributeNamedArgument> namedArgs = attribute.NamedArguments;
    Console.WriteLine("  Named arguments set after construction: " +
        ((namedArgs.Count == 0) ? " None" : String.Empty));
    foreach(CustomAttributeNamedArgument na in namedArgs) {
        Console.WriteLine("    Name={0}, Type={1}, Value={2}",
            na.MemberInfo.Name, na.TypedValue.ArgumentType, na.TypedValue.Value);
    }

    Console.WriteLine();
}
Console.WriteLine();
```
```

Building and running this application yields the following output:

```
```text
Attributes applied to Program:
System.SerializableAttribute
  Constructor called=Void .ctor()
  Positional arguments passed to constructor: None
  Named arguments set after construction: None

System.Diagnostics.DebuggerDisplayAttribute
  Constructor called=Void .ctor(System.String)
  Positional arguments passed to constructor:
    Type=System.String, Value=Richter
  Named arguments set after construction:
    Name=Name, Type=System.String, Value=Jeff
    Name=Target, Type=System.Type, Value=Program

System.Reflection.DefaultMemberAttribute
  Constructor called=Void .ctor(System.String)
  Positional arguments passed to constructor:
    Type=System.String, Value=Main
  Named arguments set after construction: None
```
```