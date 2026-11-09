
**Important** You should think of an attribute as a logical state container. That is, while an attribute type is a class, the class should be simple. The class should offer just one public constructor that accepts the attribute's mandatory (or positional) state information, and the class can offer public fields/properties that accept the attribute's optional (or named) state information. The class should not offer any public methods, events, or other members.

In general, I always discourage the use of public fields, and I still discourage them for attributes. It is much better to use properties because this allows more flexibility if you ever decide to change how the attribute class is implemented.

So far, instances of the FlagsAttribute class can be applied to any target, but this attribute should really be applied to enumerated types only. It doesn't make sense to apply the attribute to a property or a method. To tell the compiler where this attribute can legally be applied, you apply an instance of the System.AttributeUsageAttribute class to the attribute class. Here's the new code:

```csharp
namespace System {
    [AttributeUsage(AttributeTargets.Enum, Inherited = false)]
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
        }
    }
}
```

In this new version, I've applied an instance of AttributeUsageAttribute to the attribute. After all, the attribute type is just a class, and a class can have attributes applied to it. The AttributeUsageAttribute is a simple class that allows you to specify to a compiler where your custom attribute can legally be applied. All compilers have built-in support for this attribute and generate errors when a user-defined custom attribute is applied to an invalid target. In this example, the AttributeUsage attribute specifies that instances of the Flags attribute can be applied only to enumerated type targets.

Because all attributes are just types, you can easily understand the AttributeUsageAttribute class. Here's what the FCL source code for the class looks like:

```csharp
[Serializable]
[AttributeUsage(AttributeTargets.Class, Inherited=true)]
public sealed class AttributeUsageAttribute : Attribute {
    internal static AttributeUsageAttribute Default =
        new AttributeUsageAttribute(AttributeTargets.All);

    internal Boolean m_allowMultiple = false;
    internal AttributeTargets m_attributeTarget = AttributeTargets.All;
    internal Boolean m_inherited = true;

    // This is the one public constructor
    public AttributeUsageAttribute(AttributeTargets validOn) {
        m_attributeTarget = validOn;
    }

    internal AttributeUsageAttribute(AttributeTargets validOn,
        Boolean allowMultiple, Boolean inherited) {
        m_attributeTarget = validOn;
        m_allowMultiple = allowMultiple;
        m_inherited = inherited;
    }

    public Boolean AllowMultiple {
        get { return m_allowMultiple; }
        set { m_allowMultiple = value; }
    }

    public Boolean Inherited {
        get { return m_inherited; }
        set { m_inherited = value; }
    }

    public AttributeTargets ValidOn {
        get { return m_attributeTarget; }
    }
}
```

As you can see, the AttributeUsageAttribute class has a public constructor that allows you to pass bit flags that indicate where your attribute can legally be applied. The System.AttributeTargets enumerated type is defined in the FCL as follows:

```csharp
[Flags, Serializable]
public enum AttributeTargets {
    Assembly          = 0x0001,
    Module             = 0x0002,
    Class              = 0x0004,
    Struct             = 0x0008,
    Enum               = 0x0010,
    Constructor        = 0x0020,
    Method             = 0x0040,
    Property           = 0x0080,
    Field              = 0x0100,
    Event              = 0x0200,
    Interface          = 0x0400,
    Parameter          = 0x0800,
    Delegate           = 0x1000,
    ReturnValue        = 0x2000,
    GenericParameter   = 0x4000,
    All                = Assembly   | Module    | Class   | Struct | Enum   |
                         Constructor | Method    | Property | Field  | Event  |
                         Interface   | Parameter | Delegate | ReturnValue |
                         GenericParameter
}
```

The AttributeUsageAttribute class offers two additional public properties that can optionally be set when the attribute is applied to an attribute class: AllowMultiple and Inherited.

For most attributes, it makes no sense to apply them to a single target more than once. For example, nothing is gained by applying the Flags or Serializable attributes more than once to a single target. In fact, if you tried to compile the code below, the compiler would report the following message: 'error CS0579: Duplicate 'Flags' attribute.'

```csharp
[Flags][Flags]
internal enum Color {
    Red
}
```

For a few attributes, however, it does make sense to apply the attribute multiple times to a single target. In the FCL, the ConditionalAttribute attribute class allows multiple instances of itself to be applied to a single target. If you don't explicitly set AllowMultiple to true, your attribute can be applied no more than once to a selected target.

AttributeUsageAttribute's other property, Inherited, indicates if the attribute should be applied to derived classes and overriding methods when applied on the base class. The following code demonstrates what it means for an attribute to be inherited:

```csharp
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited=true)]
internal class TastyAttribute : Attribute {
}
```

```csharp
[Tasty][Serializable]
internal class BaseType {

    [Tasty] protected virtual void DoSomething() { }
}

internal class DerivedType : BaseType {
    protected override void DoSomething() { }
}
```

In this code, DerivedType and its DoSomething method are both considered Tasty because the TastyAttribute class is marked as inherited. However, DerivedType is not serializable because the FCL's SerializableAttribute class is marked as a noninherited attribute.

Be aware that the .NET Framework considers targets only of classes, methods, properties, events, fields, method return values, and parameters to be inheritable. So when you're defining an attribute type, you should set Inherited to true only if your targets include any of these targets. Note that inherited attributes do not cause additional metadata to be emitted for the derived types into the managed module. I'll say more about this a little later in the "Detecting the Use of a Custom Attribute" section.

**Note** If you define your own attribute class and forget to apply an AttributeUsage attribute to your class, the compiler and the CLR will assume that your attribute can be applied to all targets, can be applied only once to a single target, and is inherited. These assumptions mimic the default field values in the AttributeUsageAttribute class.

### Attribute Constructor and Field/Property Data Types

When defining your own custom attribute class, you can define its constructor to take parameters that must be specified by developers when they apply an instance of your attribute type. In addition, you can define nonstatic public fields and properties in your type that identify settings that a developer can optionally choose for an instance of your attribute class.

When defining an attribute class's instance constructor, fields, and properties, you must restrict yourself to a small subset of data types. Specifically, the legal set of data types is limited to the following: Boolean, Char, Byte, SByte, Int16, UInt16, Int32, UInt32, Int64, UInt64, Single, Double, String, Type, Object, or an enumerated type. In addition, you can use a single-dimensional, zero-based array of any of these types. However, you should avoid using arrays because a custom attribute class whose constructor takes an array is not CLS-compliant.

When applying an attribute, you must pass a compile-time constant expression that matches the type defined by the attribute class. Wherever the attribute class defines a Type parameter, Type field, or Type property, you must use C#'s typeof operator, as shown in the following code. Wherever the attribute class defines an Object parameter, Object field, or Object property, you can pass an Int32, String, or any other constant expression (including null). If the constant expression represents a value type, the value type will be boxed at runtime when an instance of the attribute is constructed.

Here's an example of an attribute and its usage:

```csharp
using System;

internal enum Color { Red }

[AttributeUsage(AttributeTargets.All)]
internal sealed class SomeAttribute : Attribute {
  public SomeAttribute(String name, Object o, Type[] types) {
    // 'name' refers to a String
    // 'o' refers to one of the legal types (boxing if necessary)
    // 'types' refers to a 1-dimension, 0-based array of Types
  }
}

[Some("Jeff", Color.Red, new Type[] { typeof(Math), typeof(Console) })]
internal sealed class SomeType {
}
```

Logically, when a compiler detects a custom attribute applied to a target, the compiler constructs an instance of the attribute class by calling its constructor, passing it any specified parameters. Then the compiler initializes any public fields and properties using the values specified via the enhanced constructor syntax. Now that the custom attribute object is initialized, the compiler serializes the attribute object's state out to the target's metadata table entry.
