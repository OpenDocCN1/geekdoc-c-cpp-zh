
of attributes no significance. Also, in C#, each attribute can be enclosed in square brackets, or multiple attributes can be comma-separated within a single set of square brackets. If the attribute class's constructor takes no parameters, the parentheses are optional. As mentioned earlier, the Attribute suffix is also optional. The following lines behave identically and demonstrate all of the possibilities of applying multiple attributes.

```cs
[Serializable][Flags]
[Serializable, Flags]
[FlagsAttribute, SerializableAttribute]
[FlagsAttribute()][Serializable]
```

## Defining Your Own Attribute Class

Now that you know an attribute is an instance of a class derived from System.Attribute, and you also now know how to apply an attribute. Let's look now at how to define your own attribute classes. Say you're the Microsoft employee responsible for adding the bit flag to enumerated types. To accomplish, the first thing you need to do is define a FlagsAttribute class.

```cs
namespace System {
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
    }
}
```

Notice that the FlagsAttribute class inherits from Attribute; this is what makes the FlagsAttribute class a CLS-compliant custom attribute. In addition, the class's name has a suffix of Attribute; this follows the standard convention but is not mandatory. Finally, all non-abstract attributes must contain at least one public constructor. The simple FlagsAttribute constructor takes no parameters and does absolutely nothing.

> Important: You should think of an attribute as a logical state container. That is, while an attribute type is a class, the class should be simple. The class should offer just one public constructor that accepts the attribute's mandatory (or positional) state information, and the class should offer public fields/properties that accept the attribute's optional (or named) state information. I always discourage the use of public fields, and I still discourage them for attributes. It is much better to use properties because this allows more flexibility if you ever decide to change how the attribute class is implemented.

In general, instances of the FlagsAttribute class can be applied to any target, but this attribute should really be applied to enumerated types only. It doesn't make sense to apply the attribute to a property or a method. To tell the compiler where this attribute can legally be applied, apply an instance of the System.AttributeUsageAttribute class to the attribute class. Here's the new code.

```cs
namespace System {
    [AttributeUsage(AttributeTargets.Enum, Inherited = false)]
    public class FlagsAttribute : System.Attribute {
        public FlagsAttribute() {
    }
}
```

In this version, I've applied an instance of AttributeUsageAttribute to the attribute. After, the type is just a class, and a class can have attributes applied to it. The AttributeUsage attribute is a simple class that allows you to specify to a compiler where your custom attribute can legally be applied. All compilers have built-in support for this attribute and generate errors when a user-defined custom attribute is applied to an invalid target. In this example, the AttributeUsage attribute specifies instances of the Flags attribute can be only enumerated to type targets.

Because all attributes are just types, you can easily understand the AttributeUsageAttribute class. Here's what the FCL source code for the class looks like.

```cs
[Serializable]
[AttributeUsage(AttributeTargets.Class, Inherited=true)]
public sealed class AttributeUsageAttribute : Attribute {
    internal static AttributeUsageAttribute Default =
        new AttributeUsageAttribute(AttributeTargets.All);

    internal Boolean m_allowMultiple = false;
    internal AttributeTargets m_allowMultipleTarget = AttributeTargets.All;
    internal Boolean m_inherited = true;
```

```cs
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
```

```cs
public Boolean AllowMultiple {
    get { return m_allowMultiple; }
    set { m_allowMultiple = value; }
}

public Boolean Inherited {
    get { return m_inherited; }
    set { m_inherited = value; }
}
```

```cs
public AttributeTargets ValidOn {
    get { return m_attributeTarget; }
}
```

As you can see, the AttributeUsageAttribute class has a public constructor that allows you to pass flags that indicate where your attribute can legally be applied. The System.AttributeTargets enumerated type is defined in the FCL.

```cs
[Serializable]
public enum AttributeTargets {
    Assembly = 00001,
    Module = 00002,
    Class = 00004,
    Struct = 00008,
    Enum = 00010,
    Method = 00020,
    Property = 00040,
    Field = 00080,
    Event = 00200,
    Interface = 00400,
    Parameter = 00800,
    Delegate = 01000,
    ReturnValue = 02000,
    GenericParameter = Assembly | Module | Class | Struct | Enum | Constructor | Method | Property | Field | Event | Interface | Parameter | Delegate | ReturnValue | GenericParameter
}
```

The AttributeUsageAttribute class offers two additional properties that can optionally be set when the attribute is applied to a class. AllowMultiple and Inherited.

For most attributes, it makes no sense to apply them to a single target more than once. For example, nothing is gained by applying the Flags or Serializable attributes more than once to a single target. In fact, if you tried to compile the following code, the compiler would report the following message: error CS0579: Duplicate 'Flags' attribute.

```cs
[Flags][Flags]
internal enum Color {
    Red
}
```

For a few attributes, however, it makes sense to apply the attribute multiple times to a single target. In the FCL, the ConditionalAttribute class allows multiple instances of itself to be applied to a single target. If you don't explicitly set AllowMultiple to true, your attribute can be applied no more than once to a selected target.

AttributeUsageAttribute's other property, Inherited, indicates if the attribute should be applied to derived classes and overriding methods when applied on the base class. The following code demonstrates what it means for attribute to be inherited.

```cs
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method)]
[Serializable]
internal class BaseType {
	[Tasty] protected virtual void DoSomething() { }
}
```

```cs
internal class DerivedType : BaseType {
	override void DoSomething() { }
}
```

In this code, DerivedType and its DoSomething method are both considered Tasty because the TastyAttribute is marked as inherited. However, DerivedType is not serializable because the SerializableAttribute is marked as a noninheritable attribute.

Be aware that the NET framework targets only classes, methods, properties, events, fields, method return values, and parameters to be inherited. If you are defining an attribute, you should set Inherited to true if your targets include any of these targets. Note that inherited attributes do not cause additional metadata to be emitted for the derived types into the managed module. I'll say more about this later in the "Detecting the Use of a Custom Attribute" section.

> Note If you define your own attribute class and apply an AttributeUsage attribute to your class, the compiler and the CLR will assume that your attribute can be applied to all targets, can be applied only once to a single target, and is inherited. These assumptions mimic the default field values in the AttributeUsage class.

## Attribute Constructor and Field/Property Data Types

When defining your own custom attribute class, you can define its constructor to take parameters that must be specified by developers when they apply an instance of your attribute. In addition, you can define nonstatic public fields and properties in your type that a developer can optionally choose for an instance of your attribute class.

When defining an attribute's instance constructor, fields, and properties, you must restrict yourself to a small subset of data types. Specifically, the legal set of data types is limited to the following: Boolean, Char, Byte, SByte, Int16, UInt16, Int32, UInt32, Int64, UInt64, Single, Double, String, Type, Object, or an enumerated type. You can use a single-dimensional,
