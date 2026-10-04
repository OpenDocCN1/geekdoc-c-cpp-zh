```
public AttributeTargetsValidOn {
    get { return m_attributeTarget; }
}
```

As you can see, the AttributeUsageAttribute class has a public constructor that allows you to pass flags that indicate where your attribute can legally be applied. The System.Attribute-Targets enumerated type is defined in the FCL

```
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
```

The AttributeUsageAttribute class offers two additional properties that can optionally be set when the attribute is applied to a class. AllowMultiple and Inherited.

For most attributes, it makes no sense to apply them to a single target more than once. For example, nothing is gained by applying the Flags or Serializable attributes more than once to a single target. In fact, if you tried to compile the following code, the compiler would report the following message: error CS0579: Duplicate 'Flags' attribute.

```
[Flags][Flags]
internal enum Color {
    Red
}
```

For a few attributes, however, it makes sense to apply the attribute multiple times to a single target. In the FCL, the ConditionalAttribute class allows multiple instances of itself to be applied to a single target. If you don't explicitly set AllowMultiple to true, your attribute can be applied no more than once to a selected target.