
Delegate.CreateDelegate function. The performance penalty for using reflection is incurred only during the delegate-creation process. Once the delegate is created, there is little-to-no performance penalty for invoking it:

```csharp
// Get a MethodInfo for the Math.Max(int, int) method...
var maxMethod = typeof(Math).GetMethod("Max", new Type[] { typeof(int), typeof(int) });
// Now get a strongly-typed delegate for Math.Max(int, int)...
var stronglyTypedDelegate = (Func<int, int, int>)Delegate.CreateDelegate(typeof(Func<int, int, int>), null, maxMethod);
// Invoke the Math.Max(int, int) method using the strongly-typed delegate...
Console.WriteLine("Max of 3 and 5 is: {0}", stronglyTypedDelegate(3, 5));
```

This technique can be extended to properties as well. If we have a class named MyClass with an int property named MyIntProperty, the code to get a strongly-typed getter would be (the following example assumes 'target' is a valid instance of MyClass):

```csharp
// Get a MethodInfo for the MyClass.MyIntProperty getter...
var theProperty = typeof(MyClass).GetProperty("MyIntProperty");
var theGetter = theProperty.GetGetMethod();
// Now get a strongly-typed delegate for MyIntProperty that can be executed against any MyClass instance...
var stronglyTypedGetter = (Func<MyClass, int>)Delegate.CreateDelegate(typeof(Func<MyClass, int>), theGetter);
// Invoke the MyIntProperty getter against MyClass instance 'target'...
Console.WriteLine("target.MyIntProperty is: {0}", stronglyTypedGetter(target));
```

...and the same can be done for the setter:

```csharp
// Get a MethodInfo for the MyClass.MyIntProperty setter...
var theProperty = typeof(MyClass).GetProperty("MyIntProperty");
var theSetter = theProperty.GetSetMethod();
// Now get a strongly-typed delegate for MyIntProperty that can be executed against any MyClass instance...
var stronglyTypedSetter = (Action<MyClass, int>)Delegate.CreateDelegate(typeof(Action<MyClass, int>), theSetter);
// Set MyIntProperty to 5...
stronglyTypedSetter(target, 5);
```

## Section 63.5: Get a generic method and invoke it

Let's say you have class with generic methods. And you need to call its functions with reflection.

```csharp
public class Sample
{
    public void GenericMethod<T>()
    {
        // ...
    }

    public static void StaticMethod<T>()
    {
        //...
    }
}
```

Let's say we want to call the GenericMethod with type string.

```csharp
Sample sample = new Sample();//or you can get an instance via reflection
```

```csharp
MethodInfo method = typeof(Sample).GetMethod("GenericMethod");
MethodInfo generic = method.MakeGenericMethod(typeof(string));
generic.Invoke(sample, null);//Since there are no arguments, we are passing null
```

For the static method you do not need an instance. Therefore the first argument will also be null.

```csharp
MethodInfo method = typeof(Sample).GetMethod("StaticMethod");
MethodInfo generic = method.MakeGenericMethod(typeof(string));
generic.Invoke(null, null);
```

## Section 63.6: Get a System.Type

For an instance of a type:

```csharp
var theString = "hello";
var theType = theString.GetType();
```

From the type itself:

```csharp
var theType = typeof(string);
```

## Section 63.7: Getting and setting properties

Basic usage:

```csharp
PropertyInfo prop = myInstance.GetType().GetProperty("myProperty");
// get the value myInstance.myProperty
object value = prop.GetValue(myInstance);

int newValue = 1;
// set the value myInstance.myProperty to newValue
prop.SetValue(myInstance, newValue);
```

Setting read-only automatically-implemented properties can be done through its backing field (in .NET Framework name of backing field is "k__BackingField"):

```csharp
// get backing field info
FieldInfo fieldInfo = myInstance.GetType()
    .GetField("<myProperty>k__BackingField", BindingFlags.Instance | BindingFlags.NonPublic);

int newValue = 1;
// set the value of myInstance.myProperty backing field to newValue
fieldInfo.SetValue(myInstance, newValue);
```

## Section 63.8: Create an instance of a Generic Type and invoke its method

```csharp
var baseType = typeof(List<>);
var genericType = baseType.MakeGenericType(typeof(String));
var instance = Activator.CreateInstance(genericType);
var method = genericType.GetMethod("GetHashCode");
var result = method.Invoke(instance, new object[] { });
```

## Section 63.9: Custom Attributes

### Find properties with a custom attribute - MyAttribute

```csharp
var props = t.GetProperties(BindingFlags.NonPublic | BindingFlags.Public |
    BindingFlags.Instance).Where(
    prop => Attribute.IsDefined(prop, typeof(MyAttribute)));
```

### Find all custom attributes on a given property

```csharp
var attributes = typeof(t).GetProperty("Name").GetCustomAttributes(false);
```

### Enumerate all classes with custom attribute - MyAttribute

```csharp
static IEnumerable<Type> GetTypesWithAttribute(Assembly assembly) {
    foreach (Type type in assembly.GetTypes()) {
        if (type.GetCustomAttributes(typeof(MyAttribute), true).Length > 0) {
            yield return type;
        }
    }
}
```

### Read value of a custom attribute at runtime

```csharp
public static class AttributeExtensions
{
    /// <summary>
    /// Returns the value of a member attribute for any member in a class.
    /// (a member is a Field, Property, Method, etc...)
    /// <remarks>
    /// If there is more than one member of the same name in the class, it will return the first
    one (this applies to overloaded methods)
    /// </remarks>
    /// <example>
    /// Read System.ComponentModel Description Attribute from method 'MyMethodName' in class
    'MyClass':
    ///     var Attribute = typeof(MyClass).GetAttribute("MyMethodName", (DescriptionAttribute d)
    => d.Description);
    /// </example>
    /// <param name="type">The class that contains the member as a type</param>
    /// <param name="MemberName">Name of the member in the class</param>
    /// <param name="valueSelector">Attribute type and property to get (will return first
    instance if there are multiple attributes of the same type)</param>
    /// <param name="inherit">true to search this member's inheritance chain to find the
    attributes; otherwise, false. This parameter is ignored for properties and events</param>
    /// </summary>
    public static TValue GetAttribute<TAttribute, TValue>(this Type type, string MemberName,
    Func<TAttribute, TValue> valueSelector, bool inherit = false) where TAttribute : Attribute
    {
        var att =
        type.GetMember(MemberName).FirstOrDefault().GetCustomAttributes(typeof(TAttribute),
        inherit).FirstOrDefault() as TAttribute;
        if (att != null)
        {
            return valueSelector(att);
        }
        return default(TValue);
    }
}
```

### Usage

```
//Read System.ComponentModel Description Attribute from method 'MyMethodName' in class 'MyClass'
var Attribute = typeof(MyClass).GetAttribute("MyMethodName", (DescriptionAttribute d) =>
d.Description);
```

## Section 63.10: Instantiating classes that implement an interface (e.g. plugin activation)

If you want your application to support a plug-in system, for example to load plug-ins from assemblies located in plugins folder:

```csharp
interface IPlugin
{
    string PluginDescription { get; }
    void DoWork();
}
```

This class would be located in a separate dll

```csharp
class HelloPlugin : IPlugin
{
    public string PluginDescription => "A plugin that says Hello";
    public void DoWork()
    {
        Console.WriteLine("Hello");
    }
}
```

Your application's plugin loader would find the dll files, get all types in those assemblies that implement IPlugin, and create instances of those.

```csharp
public IEnumerable<IPlugin> InstantiatePlugins(string directory)
{
    var pluginAssemblyNames = Directory.GetFiles(directory, "*.addin.dll").Select(name => new FileInfo(name).FullName).ToArray();
    //load the assemblies into the current AppDomain, so we can instantiate the types later
    foreach (var fileName in pluginAssemblyNames)
        AppDomain.CurrentDomain.Load(File.ReadAllBytes(fileName));
    var assemblies = pluginAssemblyNames.Select(System.Reflection.Assembly.LoadFile);
    var typesInAssembly = assemblies.SelectMany(asm => asm.GetTypes());
    var pluginTypes = typesInAssembly.Where(type => typeof(IPlugin).IsAssignableFrom(type));
    return pluginTypes.Select(Activator.CreateInstance).Cast<IPlugin>();
}
```

## Section 63.11: Get a Type by name with namespace

To do this you need a reference to the assembly which contains the type. If you have another type available which you know is in the same assembly as the one you want you can do this:

```csharp
typeof(KnownType).Assembly.GetType(typeName);
```

- where typeName is the name of the type you are looking for (including the namespace), and KnownType is the type you know is in the same assembly.
