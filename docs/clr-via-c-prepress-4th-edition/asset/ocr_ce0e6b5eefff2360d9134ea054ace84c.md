```
```csharp
Boolean allowMultiple, Boolean inherited) {
    m_attributeTarget = valid;
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
```
```

As you can see, the AttributeUsageAttribute class has a public constructor that allows you to pass bit flags that indicate where your attribute can legally be applied. The System.AttributeTargets enumerated type is defined in the FCL as follows:

```
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
```

The AttributeUsageAttribute class offers two additional public properties that can optionally be set when the attribute is applied to an attribute class: AllowMultiple and Inherited.

For most attributes, it makes no sense to apply them to a single target more than once. For example, nothing is gained by applying the Flags or Serializable attributes more than once to a