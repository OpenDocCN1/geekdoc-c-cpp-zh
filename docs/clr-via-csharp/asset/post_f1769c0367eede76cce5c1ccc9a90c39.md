
```csharp
// Assume AddIn assemblies are in same directory as host's EXE file
String[] AddInAssemblies = Directory.GetFiles(AddInDir, "*.dll");

// Create a collection of usable add-in Types
List<Type> AddInTypes = new List<Type>();

// Load add-in assemblies; discover which types are usable by the host
foreach (String file in AddInAssemblies) {
    Assembly AddInAssembly = Assembly.LoadFrom(file);

    // Examine each publicly exported type
    foreach (Type t in AddInAssembly.GetExportedTypes()) {
        // If the type is a class that implements the IAddIn
        // interface, then the type is usable by the host
        if (t.IsClass && typeof(IAddIn).IsAssignableFrom(t)) {
            AddInTypes.Add(t);
        }
    }
}

// Initialization complete: the host has discovered the usable add-ins

// Here's how the host can construct add-in objects and use them
foreach (Type t in AddInTypes) {
    IAddIn ai = (IAddIn) Activator.CreateInstance(t);
    Console.WriteLine(ai.DoSomething(5));
}
```

The simple host/add-in scenario just shown doesn't use AppDomains. However, in a real-life scenario, you will likely create each add-in in its own AppDomain with its own security and configuration settings. And of course, each AppDomain could be unloaded if you wanted to remove an add-in from memory. To communicate across the AppDomain boundary, you'd either tell the add-in developers to derive their add-in types from **MarshalByRefObject** or, more likely, have the host application define its own internal type that is derived from **MarshalByRefObject**. As each AppDomain is created, the host would create an instance of its own **MarshalByRefObject**-derived type in the new AppDomain. The host's code (in the default AppDomain) would communicate with its own type (in the other AppDomains) to have it load add-in assemblies and create and use instances of the add-in types.

## Using Reflection to Discover a Type’s Members

So far, this chapter has focused on the parts of reflection—assembly loading, type discovery, and object construction—necessary to build a dynamically extensible application. In order to have good performance and compile-time type safety, you want to avoid using reflection as much as possible. In the dynamically extensible application scenario, once an object is constructed, the host code typically casts the object to an interface type or a base class that is known at compile time; this allows the object's members to be accessed in a high-performance and compile-time type-safe way.

In the remainder of this chapter, I’m going to focus on some other aspects of reflection that you can use to discover and then invoke a type’s members. The ability to discover and invoke a type’s members is typically used to create developer tools and utilities that analyze an assembly by looking for certain programming patterns or uses of certain members. Examples of tools/utilities that do this are ILDasm.exe, FxCopCmd.exe, and Visual Studio’s Windows Forms and Web Forms designers. In addition, some class libraries use the ability to discover and invoke a type’s members in order to offer rich functionality as a convenience to developers. Examples of class libraries that do so are serialization/deserialization and simple data binding.

### Discovering a Type’s Members

Fields, constructors, methods, properties, events, and nested types can all be defined as members within a type. The FCL contains a type called **System.Reflection.MemberInfo**. This class is an abstract base class that encapsulates a bunch of properties common to all type members. Derived from **MemberInfo** are a bunch of classes; each class encapsulates some more properties related to a specific type member. Figure 23-1 shows the hierarchy of these types.

![](img/3c46ff5b170881db4209d365b1f7a808_655_0.png)

**FIGURE 23-1** Hierarchy of the reflection types that encapsulate information about a type’s member

The following program demonstrates how to query a type’s members and display some information about them. This code processes all of the public types defined in all assemblies loaded in the calling AppDomain. For each type, the **GetMembers** method is called and

```
MethodInfo: Int32 GetHashCode()
MethodInfo: System.Type GetType()
MethodInfo: Void Finalize()
MethodInfo: System.Object MemberwiseClone()
MethodInfo: Void FieldSetter(System.String, System.String, System.Object)
MethodInfo: Void FieldGetter(System.String, System.String, System.Object ByRef)
MethodInfo: System.Reflection.FieldInfo GetFieldInfo(System.String)
    ConstructorInfo: Void .ctor()
Type: System.Collections.Generic.IComparer`1[T]
    MethodInfo: Int32 Compare(T, T)
Type: System.Collections.IEnumerator
    MethodInfo: Boolean MoveNext()
    MethodInfo: System.Object get_Current()
    MethodInfo: Void Reset()
    PropertyInfo: System.Object Current
Type: System.IDisposable
    MethodInfo: Void Dispose()
Type: System.Collections.Generic.IEnumerator`1[T]
    MethodInfo: T get_Current()
    PropertyInfo: T Current
Type: System.ArraySegment`1[T]
    MethodInfo: T[] get_Array()
    MethodInfo: Int32 get_Offset()
    MethodInfo: Int32 get_Count()
    MethodInfo: Int32 GetHashCode()
    MethodInfo: Boolean Equals(System.Object)
    MethodInfo: Boolean Equals(System.ArraySegment`1[T])
    MethodInfo: Boolean op_Equality(System.ArraySegment`1[T], System.ArraySegment`1[T])
    MethodInfo: Boolean op_Inequality(System.ArraySegment`1[T], System.ArraySegment`1[T])
    ConstructorInfo: Void .ctor(T[])
    ConstructorInfo: Void .ctor(T[], Int32, Int32)
    PropertyInfo: T[] Array
    PropertyInfo: Int32 Offset
    PropertyInfo: Int32 Count
    FieldInfo: T[] _array
    FieldInfo: Int32 _offset
```

Since **MemberInfo** is the root of the member hierarchy, it makes sense for us to discuss it a bit more. Table 23-1 shows several read-only properties and methods afforded by the **MemberInfo** class. These properties and methods are common to all members of a type. Don’t forget that **System.Type** is derived from **MemberInfo**, and therefore, **Type** also offers all of the properties shown in Table 23-1.

**TABLE 23-1 Properties and Methods Common to All MemberInfo-Derived Types**

| Member Name | Member Type | Description |
|---|---|---|
| Name | **String** property | Returns the name of the member. In the case of a nested type, **Name** returns the concatenation of the name of the containing type, followed by '+', followed by the name of the nested type. |
| **MemberType** | **MemberTypes** (enum) property | Returns the kind of member (field, constructor, method, property, event, type (non-nested type or nested type)). |
| **DeclaringType** | **Type** property | Returns the **Type** that declares the member. |
| **ReflectedType** | **Type** property | Returns the **Type** used to obtain this member. |
| **Module** | **Module** property | Returns the **Module** that declares the member. |
| **MetadataToken** | **Int32** property | Returns the metadata token (within the module) that identifies the member. |
| **GetCustomAttributes** | Method returning **Object[]** | Returns an array in which each element identifies an instance of a custom attribute applied to this member. Custom attributes can be applied to any member. Use this method with assemblies that have not been loaded in the “reflection only” context. |
| **GetCustomAttributesData** | Method returning **IList<CustomAttributeData>** | Returns a collection in which each element identifies an instance of a custom attribute applied to this member. Custom attributes can be applied to any member. Even though **Assembly** does not derive from **MemberInfo**, it provides the same method that can be used with assemblies. |
| **IsDefined** | Method returning **Boolean** | Returns **true** if at least one instance of the specified custom attribute is applied to the member. |

Most of the properties mentioned in Table 23-1 are self-explanatory. However, developers frequently confuse the `DeclaringType` and `ReflectedType` properties. To fully understand these properties, let’s define the following type:

```csharp
public sealed class MyType {
    public override String ToString() { return null; }
}
```

What would happen if the following line of code executed?

```csharp
MemberInfo[] members = typeof(MyType).GetMembers();
```
