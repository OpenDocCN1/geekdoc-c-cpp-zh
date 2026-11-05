
```
public class SimpleAttribute : Attribute
{
    ...
}
```

defines an attribute class named SimpleAttribute that can be placed on class_declarations and interface_declarations only. The example

```
[Simple] class Class1 {...}
[Simple] interface Interface1 {...}
```

shows several uses of the Simple attribute. Although this attribute is defined with the name SimpleAttribute, when this attribute is used, the Attribute suffix may be omitted, resulting in the short name Simple. Thus, the example above is semantically equivalent to the following

```
[SimpleAttribute] class Class1 {...}
[SimpleAttribute] interface Interface1 {...}
```

end example

AttributeUsage has a named parameter (§21.2.3), called AllowMultiple, which indicates whether the attribute can be specified more than once for a given entity. If AllowMultiple for an attribute class is true, then that attribute class is a multi-use attribute class, and can be specified more than once on an entity. If AllowMultiple for an attribute class is false or it is unspecified, then that attribute class is a single-use attribute class, and can be specified at most once on an entity.

Example: The example

```
using System;
[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]
public class AuthorAttribute : Attribute
{
    private string name;
    public AuthorAttribute(string name)
    {
        this.name = name;
    }
    public string Name
    {
        get { return name; }
    }
}
```

defines a multi-use attribute class named AuthorAttribute. The example

```
[Author("Brian Kernighan"), Author("Dennis Ritchie")]
class Class1
{
    ...
}
```

shows a class declaration with two uses of the Author attribute.

end example

AttributeUsage has another named parameter (§21.2.3), called Inherited, which indicates whether the attribute, when specified on a base class, is also inherited by classes that derive from that base class. If Inherited for an attribute class is true, then that attribute is inherited. If Inherited for an attribute class is false then that attribute is not inherited. If it is unspecified, its default value is true.

An attribute class X not having an AttributeUsage attribute attached to it, as in

```
using System;

class X : Attribute { ... }
```

is equivalent to the following:

```
using System;
[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X : Attribute { ... }
```

## 21.2.3 Positional and named parameters

Attribute classes can have positional parameters and named parameters. Each public instance constructor for an attribute class defines a valid sequence of positional parameters for that attribute class. Each non-static public read-write field and property for an attribute class defines a named parameter for the attribute class. For a property to define a named parameter, that property shall have both a public get accessor and a public set accessor.

Example: The example

```
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute : Attribute
{
    public HelpAttribute(string url) // url is a positional parameter
    {
        ...
    }

    // Topic is a named parameter
    public string Topic
    {
        get;
        set;
    }

    public string Url { get; }
}
```

defines an attribute class named HelpAttribute that has one positional parameter, url, and one named parameter, Topic. Although it is non-static and public, the property Url does not define a named parameter, since it is not read-write.

This attribute class might be used as follows:

```
[Help("http://www.mycompany.com/.../Class1.htm")]
class Class1
{
}
```

```
[Help("http://www.mycompany.com/.../Misc.htm", Topic ="Class2")]
class Class2
{
}
```

end example

## 21.2.4 Attribute parameter types

The types of positional and named parameters for an attribute class are limited to the attribute parameter types, which are:

- One of the following types: `bool`, `byte`, `char`, `double`, `float`, `int`, `long`, `sbyte`, `short`, `string`, `uint`, `ulong`, `ushort`.
- The type `object`.
- The type `System.Type`.
- Enum types.
- Single-dimensional arrays of the above types.
- A constructor argument or public field that does not have one of these types, shall not be used as a positional or named parameter in an attribute specification.

## 21.3 Attribute specification

Attribute specification is the application of a previously defined attribute to a program entity. An attribute is a piece of additional declarative information that is specified for a program entity. Attributes can be specified at global scope (to specify attributes on the containing assembly or module) and for type_declarations (§13.7), class_member_declarations (§14.3), interface_member_declarations (§17.4), struct_member_declarations (§15.3), enum_member_declarations (§18.2), accessor_declarations (§14.7.3), event_accessor_declarations (§14.8), elements of formal_parameter_lists (§14.6.2), and elements of type_parameter_lists (§14.2.3).

Attributes are specified in attribute sections. An attribute section consists of a pair of square brackets, which surround a comma-separated list of one or more attributes. The order in which attributes are specified in such a list, and the order in which sections attached to the same program entity are arranged, is not significant. For instance, the attribute specifications [A][B], [B][A], [A, B], and [B, A] are equivalent.

```
global_attributes
    : global_attribute_section+
    ;

global_attribute_section
    : '[' global_attribute_target_specifier attribute_list ']'
    | '[' global_attribute_target_specifier attribute_list ',' ']'
    ;

global_attribute_target_specifier
    : global_attribute_target ':'
    ;

global_attribute_target
    : identifier
    ;
```

```
attributes
    : attribute_section+
    ;

attribute_section
    : '[' attribute_target_specifier? attribute_list ']'
    | '[' attribute_target_specifier? attribute_list ',' ']'
    ;

attribute_target_specifier
    : attribute_target ':'
    ;

attribute_target
    : identifier
    | keyword
    ;

attribute_list
    : attribute (',' attribute)*
    ;

attribute
    : attribute_name attribute_arguments?
    ;

attribute_name
    : type_name
    ;

attribute_arguments
    : '(' positional_argument_list? ')'
    | '(' positional_argument_list ',' named_argument_list ')'
    | '(' named_argument_list ')'
    ;

positional_argument_list
    : positional_argument (',' positional_argument)*
    ;

positional_argument
    : argument_name? attribute_argument_expression
    ;

named_argument_list
    : named_argument (',' named_argument)*
    ;

named_argument
    : identifier '=' attribute_argument_expression
    ;

attribute_argument_expression
: expression
;
```

For the production global_attribute_target, and in the text below, identifier shall have a spelling equal to assembly or module, where equality is that defined in §6.4.3. For the production attribute_target, and in the text below, identifier shall have a spelling that is not equal to assembly or module, using the same definition of equality as above.

An attribute consists of an attribute_name and an optional list of positional and named arguments. The positional arguments (if any) precede the named arguments. A positional argument consists of an attribute_argument_expression; a named argument consists of a name, followed by an equal sign, followed by an attribute_argument_expression, which, together, are constrained by the same rules as simple assignment. The order of named arguments is not significant.

> Note: For convenience, a trailing comma is allowed in a global_attribute_section and an attribute_section, just as one is allowed in an array_initializer (§16.7).

The attribute_name identifies an attribute class.

When an attribute is placed at the global level, a global_attribute_target_specifier is required. When the global_attribute_target is equal to:

- assembly — the target is the containing assembly
- module — the target is the containing module

No other values for global_attribute_target are allowed.

The standardized attribute_target names are event, field, method, param, property, return, type, and typevar. These target names shall only be used in the following contexts:

- event — an event.
- field — a field. A field-like event (i.e., one without accessors) can also have an attribute with this target.
- method — a constructor, finalizer, method, operator, property get and set accessors, indexer get and set accessors, and event add and remove accessors. A field-like event (i.e., one without accessors) can also have an attribute with this target.
- param — a property set accessor, an indexer set accessor, event add and remove accessors, and a parameter in a constructor, method, and operator.
- property — a property and an indexer.
- return — a delegate, method, operator, property get accessor, and indexer get accessor.
- type — a delegate, class, struct, enum, and interface.
- typevar — a type parameter.

Certain contexts permit the specification of an attribute on more than one target. A program can explicitly specify the target by including an attribute_target_specifier. Without an attribute_target_specifier a default is applied, but an attribute_target_specifier can be used to affirm or override the default. The contexts are resolved as follows:

- For an attribute on a delegate declaration the default target is the delegate. Otherwise when the attribute_target is equal to:
  - type — the target is the delegate
