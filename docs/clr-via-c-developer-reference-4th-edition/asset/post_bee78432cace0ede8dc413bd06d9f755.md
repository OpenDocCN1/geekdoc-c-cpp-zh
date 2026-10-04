
zero-based array of any of these types. However, you should avoid using arrays because a custom attribute class constructor takes an array is not CLS-compliant.

When applying an attribute, you must pass a compile-time constant expression that matches the type defined by the attribute class. The attribute class defines a Type parameter, Type field, or Type property, you must use typeof operator, as shown in the following code. Wherever the attribute class defines an Object parameter, Object field or Object property, you can pass an Int32, String, or any other constant expression (including null). If the constant expression represents a value type, the value type will be boxed at run time when an instance of the attribute is constructed.

Here's an example of an attribute and its usage.

```csharp
using System;

[AttributeUsage(AttributeTargets.All)]
internal sealed class SomeAttribute : Attribute {
    public SomeAttribute(String name, Object o, Type[] types) {
        // 'name' refers to a String
        // 'o' refers to one of the legal types (boxing if necessary)
        // 'types' refers to a 1-dimension, 0-based array of Types
    }
}

Some("Jeff", Color.Red, new Type[]{ typeof(Console) });
internal sealed class SomeType {
}
```

Logically, when a compiler detects a custom attribute applied to a target, the compiler constructs an instance of the attribute class by calling its constructor, passing it any specified parameters. The compiler initializes any public fields and properties using the values specified by the enhanced constructor syntax. Now that the custom attribute is initialized, the compiler serializes the attribute object's state out to the target's metadata table entry.

> Important I found to be the best way for developers to think of custom attributes: instances of classes that have been serialized to a byte stream that resides in metadata. Later, at run time, an instance of the class can be constructed by deserializing the bytes contained in the metadata. In reality, what actually happens is that the compiler emits the information necessary to create an instance of the attribute class. Each constructor parameter is written out with a 1-byte type ID followed by the value. After 'serializing' the constructor's parameters, the compiler emits each of the specified field and property values by writing out the field/property name followed by a 1-byte ID and then the value. For arrays, the count of elements is saved first, followed by each individual element.

## Detecting the Use of a Custom Attribute

Defining an attribute class is useless by itself. Sure, you could define attribute classes all you want and apply instances of all you want, but this would just cause additional metadata to be written to the assembly—the behavior of your application code wouldn't change.

In Chapter 15, *Enumerated Types and Bit Flags*, you saw that applying the Flags attribute to an enumerated type altered the behavior of `System.Enum.ToString` and Format methods. The reason that these methods behave differently is that they check at run time if the enumerated type they're operating on has the Flags attribute metadata associated with it. Code could look for the presence of attributes by using a technology called *reflection*. I will give some brief demonstrations of reflection here, but I will discuss it fully in Chapter 23, "Assembly Loading and Reflection."

If you were the Microsoft employee responsible for implementing Enum's Format method, you would implement it like the following:

```csharp
public override string ToString() {
    // Does the enumerated type have an instance of
    // the FlagsAttribute type applied to it?
    if (this.GetType().IsDefined(typeof(FlagsAttribute), false)) {
        // Yes: execute code treating value as a bit flagged enumerated type.
    } else {
        // No: execute code treating value as a normal enumerated type.
    }
}
```

This code calls Type's `IsDefined` to see whether an instance of the FlagsAttribute class is associated with it. If `IsDefined` returns true, an instance of `FlagsAttribute` is associated with the enumerated type, and the Format method knows to treat the value as though it contained a set of bit flags. If `IsDefined` returns false, Format treats the value as a normal enumerated type.

So if you define your own classes, you must also implement some code checks for the existence of an instance of your attribute class (on some target) and execute some alternate code path. This is what makes custom attributes useful!

The FCL offers many ways to check for the existence of an attribute. If you're checking for the existence of an attribute via a `System.Type`, you can use the `IsDefined` method as shown earlier. However, sometimes you want to check for an attribute on a target other than the type, such as an assembly, or a module. For this discussion, let's concentrate on the extension methods defined by `System.Reflection.CustomAttributeExtensions` class. This class defines three static methods for retrieving the attributes associated with a target: `IsDefined`, `GetAttributes`, and `GetCustomAttribute`. Each of these functions has several overloaded versions. For example, each method has a version that works on type members (classes, structs, enums, interfaces, delegates, constructors, methods, properties, fields, events, and return types), parameters, and assemblies. There are also versions that allow you to tell the system to walk up the derivation hierarchy to include inherited attributes in the results. Table 18-1 briefly describes what each method does.

## TABLE 18-1 System.Reflection.CustomAttributeExtensions' Methods That Reflect over Metadata Looking for Instances of CLS-Compliant Custom Attributes

| Method | Description |
| --- | --- |
| IsDefined | Returns true if there is at least one instance of the specified Attribute-derived class as the target. This method is efficient because it doesn't construct (deserialize) any instances of the attribute class |
| GetAttributes | Returns a collection of the specified attribute objects that have been applied to the target. Each instance is constructed (deserialize) using the parameters, fields, and properties during compilation. If the target has no instances of the attribute class, an empty collection is returned. This method is typically used with attributes that AllowMultiple set to true |
| GetCustomAttribute | Returns an instance of the specified attribute class was applied to the target. The instance is constructed (deserialize) using the parameters, fields, and properties during compilation. If the target has no instances of the specified attribute applied, it returns null. This method is typically used with attributes that AllowMultiple set to false. |

If you want to see if an attribute has been applied to a target, you can call IsDefined because it's more efficient than the other two methods. However, you know that when an attribute is applied to a target, you can specify parameters to the attribute's constructor and optionally set fields and properties. Using IsDefined won't construct an attribute object, call its constructor, or set its fields and properties.

If you want to construct an attribute object, you may call GetCustomAttributes or GetCustomAttribute. Each time these is called, it constructs instances of the specified attribute type and each of the instance's fields and properties based on the values specified in the source code. These methods return references to fully constructed instances of the applied attribute classes.

When you call any of these methods, internally, they must scan the managed module's metadata, performing string comparisons to locate the specified custom attribute class. Obviously, these operations take time. If you're performance conscious, you should consider caching the result of calling them rather than calling repeatedly asking for the same information.

System.Reflection namespace defines classes that allow you to examine the contents of a module's metadata: Assembly, Module, ParameterInfo, MemberInfo, Type, MethodInfo, ConstructorInfo, FieldInfo, EventInfo, PropertyInfo, and their respective Builder classes. All of these classes also offer IsDefined and GetCustomAttributes.

The version of GetCustomAttributes defined by the reflection classes returns an array of Object instances (Object[]) instead of an Attribute instances (Attribute[]). This is because the reflection classes are able to return objects of non-CLS-compliant attribute classes.
