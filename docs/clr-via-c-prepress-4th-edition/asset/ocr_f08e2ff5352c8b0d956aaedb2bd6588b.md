single target. In fact, if you tried to compile the code below, the compiler would report the following message: 'error CS0579: Duplicate 'Flags' attribute.'

```
```
[Flags][Flags]
internal enum Color {
    Red
}
```
```

For a few attributes, however, it does make sense to apply the attribute multiple times to a single target. In the FCL, the ConditionalAttribute attribute class allows multiple instances of itself to be applied to a single target. If you don't explicitly set AllowMultiple to true, your attribute can be applied no more than once to a selected target.

AttributeUsageAttribute's other property, Inherited, indicates if the attribute should be applied to derived classes and overriding methods when applied on the base class. The following code demonstrates what it means for an attribute to be inherited:

```
```
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited=true)]
internal class TastyAttribute : Attribute {
}
```
```

```
```
[Tasty][Serializable]
internal class BaseType {

    [Tasty] protected virtual void DoSomething() { }
}

internal class DerivedType : BaseType {
    protected override void DoSomething() { }
}
```
```

In this code, DerivedType and its DoSomething method are both considered Tasty because the TastyAttribute class is marked as inherited. However, DerivedType is not serializable because the FCL's SerializableAttribute class is marked as a noninherited attribute.

Be aware that the .NET Framework considers targets only of classes, methods, properties, events, fields, method return values, and parameters to be inheritable. So when you're defining an attribute type, you should set Inherited to true only if your targets include any of these targets. Note that inherited attributes do not cause additional metadata to be emitted for the derived types into the managed module. I'll say more about this a little later in the "Detecting the Use of a Custom Attribute" section.

**Note** If you define your own attribute class and forget to apply an AttributeUsage attribute to your class, the compiler and the CLR will assume that your attribute can be applied to all targets, can be applied only once to a single target, and is inherited. These assumptions mimic the default field values in the AttributeUsageAttribute class.