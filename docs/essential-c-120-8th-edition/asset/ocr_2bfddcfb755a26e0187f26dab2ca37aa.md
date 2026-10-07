```
// ...
}
```

Constant fields are static, since no new field instance is required for each object instance. Declaring a constant field as static explicitly will cause a compile error. Also, constant fields are usually declared only for types that have literal values (e.g., string, int, and double). Types such as Program or System.Guid cannot be used for constant fields.

It is important that the types of values used in public constant expressions are permanent in time (see the Public Constants Should Be Permanent Values Advanced Block). Values such as pi, Avogadro's number, and Earth's circumference are good examples. However, values that could potentially change over time are not. For example, population counts, the poorest country, and exchange rates would be poor choices for constants.

# Guidelines

+   - **DO** constant fields for values that will never change.
- **AVOID** constant fields for values that will change over time.

# ADVANCED TOPIC

# Public Constants Should Be Permanent Values

Publicly accessible constants should be permanent, because changing the value of a constant will not necessarily take effect in the assemblies that use. If an assembly references a constant from a different assembly, the value of the constant is compiled directly into the referencing assembly. Therefore, if the value in the referenced assembly is changed but the referencing assembly is not recompiled, the referencing assembly will still use the original value, not the new value. Values that could potentially change in the future should be specified as `readonly` instead.