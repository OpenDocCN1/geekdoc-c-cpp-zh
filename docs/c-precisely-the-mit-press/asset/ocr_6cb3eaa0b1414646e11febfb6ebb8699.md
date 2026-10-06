# 32 Attributes

Attributes are used to attach metadata to a target, where a target may be an assembly, class, constructor, delegate type, enum type, event, field, interface, method, module, parameter, property, return value, or struct type. An attribute is attached to its target by writing an attribute in square brackets [...] before the declaration.

The type of an argument can be any simple type (except decimal), Object, String, a simple enum type, System.Type, or a single-dimensional array of these types. Each argument expression must be compile-time constant, or a System.Type object (possibly involving typeof; see section 12.21), or a one-dimensional array of expressions that satisfy these requirements.

# 32.1 Some Predefined Attributes

The .Net Framework class has hundreds of predefined attributes; here are some examples:

| Attribute | Targets | Meaning |
| --- | --- | --- |
| Flags | Enum type | Print enum value combinations symbolically |
| Serializable | Class | Instances can be serialized and deserialized |
| NonSerialized | Field | Field is omitted when class is serialized |
| AttributeUsage | Class | Permissible attributes for this attribute class |
| Diagnostics.Conditional | Method | Determine when (diagnostic) method should be called |
| Obsolete | All | Inform users that target should not be used |
| MTAThread | Method | COM threading model is multithreaded apartment (MTA) |
| STATThread | Method | COM threading model is single-threaded apartment (STA) |

The Flags attribute is illustrated in example 76, the Serializable and NonSerialized attributes in example 254, and the AttributeUsage attribute in example 255.

# 32.2 Declaring and Using Custom Attributes

A custom attribute is declared as a non-generic subclass of System.Attribute. Its name should have the form XAttribute, where it suffices to use X when using it. The constructor of a custom attribute can take arguments as simple types, enum types, and strings. To specify what targets the custom attribute can be attached to, use AttributeUsage.

If an attribute has a read-write instance property P, then it has a named parameter P. That named parameter may be set in the attribute by assigning an of the form P = e, where e is an attribute parameter expression. For instance, AttributeUsage has a named parameter AllowMultiple.

The attributes of a target can be accessed using the reflection mechanisms of C#. An example is given in the full source code of example 255.

The custom attributes are usually created at run-time for every access. The body of the attribute constructor and the properties implementing named parameters are executed for each access.