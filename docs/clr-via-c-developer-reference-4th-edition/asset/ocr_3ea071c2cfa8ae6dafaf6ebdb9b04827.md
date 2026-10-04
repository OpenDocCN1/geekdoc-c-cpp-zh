C# offers keywords that you can apply to types and/or type members that impact component versioning. These keywords map directly to features supported in the CLR to support component versioning. Table 6-2 contains the C# keywords related to component versioning and indicates how each keyword affects a type or member definition.

# TABLE 6-2 C# Keywords and How They Affect Component Versioning

| C# Keyword | Type | Method/Property/Event | Constant/Field |
| --- | --- | --- | --- |
| abstract | Indicates that no instances of the type can be constructed | Indicates that derived type must override and implement this member before instances of the derived type can be constructed | (not allowed) |
| virtual | (not allowed) | Indicates that this member can be overridden by a derived type | (not allowed) |
| override | (not allowed) | Indicates that derived type is overriding the base type's member | (not allowed) |
| sealed | Indicates that the type cannot be used as a base type | Indicates that the cannot be overridden by a derived type. This keyword can be applied only to a method that is a virtual method | (not allowed) |
| new | When applied to a nested type, method, property, event, constant, or field, indicates that the member has no relationship to a similar member that may exist in the base class | |

I will demonstrate the value and use of all these keywords in the upcoming section titled "Dealing with Virtual Methods When Versioning Types." But before we get to a versioning scenario, let's focus on how the CLR actually calls virtual methods.

# How the CLR Calls Virtual Methods, Properties, and Events

In this section, I will be focusing on methods, but this discussion is relevant to virtual properties and virtual events as well. Properties and events are actually implemented as methods; this will be shown in their corresponding chapters.

Methods represent code that performs some operation on the type (static methods) or an instance of the type (nonstatic). All methods have a name, a signature, and a return type (that may be void). The CLR allows you to define multiple methods with the same name as long as each method has a different set of parameters or a different return type. So it's possible to define methods with the same name and parameters as long as the methods have a different return type. However, for IL assembly language, I'm not aware of any language that takes advantage of this "feature"; most languages (including C#) require that methods differ by parameters and ignore a method's return type when determining uniqueness. (C# actually relaxes this restriction when defining conversion operator methods; see Chapter 8 for details.)