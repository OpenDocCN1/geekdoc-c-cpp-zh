AttributeUsageAttribute.s other property, Inherited, indicates if the attribute should be applied to derived classes and overriding methods when applied on the base class. The following code demonstrates what it means for attribute to be inherited.

```
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method
```

```
[Serializable]
internal class BaseType {
	[Tasty] protected virtual void DoSomething() { }
}
```

```
internal class DerivedType : BaseType {
	override void DoSomething() { }
}
```

In this code, DerivedType and its DoSomething method are both considered Tasty because the TastyAttribute is marked as inherited. However, DerivedType is not serializable because the FCL's SerializableAttribute is marked as a noninheritable attribute.

Be aware that the NET framework targets only of classes, methods, properties, events, fields, method return values, and parameters to be inherited. If you are defining an attribute, you should set Inherited to true only if your targets include any of these targets. Note that inherited attributes do not cause additional metadata to be emitted for the derived types into the managed module. I'll say more about this later in the "Detecting the Use of a Custom Attribute" section.

> Note If you define your own attribute class and apply an AttributeUsage attribute to your class, the compiler and the CLR will assume that your attribute can be applied to all targets, can be applied only once to a single target, and is inherited. These assumptions mimic the default field values in the AttributeUsageAttribute class.

# Attribute Constructor and Field/Property Data Types

When defining your own custom attribute class, you can define its constructor to take parameters that must be specified by developers when they apply an instance of your attribute. In addition, you can define nonstatic public fields and properties in your type that identifies a developer can optionally choose for an instance of your attribute class.

When defining an attribute's instance constructor, fields, and properties, you must restrict yourself to a small subset of data types. Specifically, the legal set of data types is limited to the following: Boolean, Char, Byte, SByte, Int16, UInt16, Int32, UInt32, Int64, UInt64, Single, Double, String, Type, Object, or an enumerated type. You can use a single-dimensional,

![](bbox=[0.055, 0.553, 0.095, 0.587])