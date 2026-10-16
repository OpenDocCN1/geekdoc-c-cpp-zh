you already know, all classes in .NET will derive from that class because Object is the base class of everything.

The code below shows you how to iterate through a method’s attributes. If you have defined custom attributes of the methods, the method called GetCustomAttributes can be used in the instance of the class called MethodInfo to get the method attributes:

```
foreach (MethodInfo temp in methodInfo)
{
    foreach (Attribute attribute in temp.GetCustomAttributes(true))
    {
        //You usual code will go here
    }
}
```

If you use attributes to decorate business objects in your application, C# reflection can be used to reflect on the type, get the attributes for the type methods, and then do whatever action needs to be performed.

# C# Type Class

The C# Type class is used to represent the type declarations for the interface types, class types, array type, enumeration types, value types, and so on. It is located in the System namespace and inherits the class called System.Reflection.MemberInfo.

Here is a list of the more important properties of the Type class:

| Property | Description |
|---|---|
| Assembly | Retrieves the assembly for the type |
| AssemblyQualifiedName | Retrieves the name of the type that is Assembly qualified |
| Attributes | Retrieve the attributes that are associated with the specified type |