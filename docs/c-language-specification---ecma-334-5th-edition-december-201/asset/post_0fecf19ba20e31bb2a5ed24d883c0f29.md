
shows several uses of the Simple attribute. Although this attribute is defined with the name SimpleAttribute, when this attribute is used, the Attribute suffix may be omitted, resulting in the short name Simple. Thus, the example above is semantically equivalent to the following

```
[SimpleAttribute] class Class1 {...}
[SimpleAttribute] interface Interface1 {...}
```

end example

AttributeUsage has a named parameter (§22.2.3), called AllowMultiple, which indicates whether the attribute can be specified more than once for a given entity. If AllowMultiple for an attribute class is true, then that attribute class is a multi-use attribute class, and can be specified more than once on an entity. If AllowMultiple for an attribute class is false or it is unspecified, then that attribute class is a single-use attribute class, and can be specified at most once on an entity.

[Example: The example

```
using System;
[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]
public class AuthorAttribute: Attribute
{
    private string name;
    public AuthorAttribute(string name) {
        this.name = name;
    }
    public string Name {
        get { return name; }
    }
}
```

defines a multi-use attribute class named AuthorAttribute. The example

```
[Author("Brian Kernighan"), Author("Dennis Ritchie")]
class Class1 {...}
```

shows a class declaration with two uses of the Author attribute. end example

AttributeUsage has another named parameter (§22.2.3), called Inherited, which indicates whether the attribute, when specified on a base class, is also inherited by classes that derive from that base class. If Inherited for an attribute class is true, then that attribute is inherited. If Inherited for an attribute class is false then that attribute is not inherited. If it is unspecified, its default value is true.

An attribute class X not having an AttributeUsage attribute attached to it, as in

```
using System;
class X: Attribute { ... }
```

is equivalent to the following:

```
using System;
[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X: Attribute { ... }
```

## 22.2.3 Positional and named parameters

Attribute classes can have positional parameters and named parameters. Each public instance constructor for an attribute class defines a valid sequence of positional parameters for that attribute class. Each non-static public read-write field and property for an attribute class defines a named parameter for the attribute class. Both accessors of a property need to be public for the property to define a named parameter.

[Example: The example

```
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute: Attribute
{
    public HelpAttribute(string url) { // url is a positional parameter
    }
    public string Topic {  // Topic is a named parameter
        get {...}
        set {...}
    }
    public string Url { get {...} }
}
```

defines an attribute class named HelpAttribute that has one positional parameter, url, and one named parameter, Topic. Although it is non-static and public, the property Url does not define a named parameter, since it is not read-write.

This attribute class might be used as follows:

```
[Help("http://www.mycompany.com/.../Class1.htm")]
class Class1
{
}

[Help("http://www.mycompany.com/.../Misc.htm", Topic ="Class2")]
class Class2
{
}
```

end example]

## 22.2.4 Attribute parameter types

The types of positional and named parameters for an attribute class are limited to the attribute parameter types, which are:

- One of the following types: bool, byte, char, double, float, int, long, sbyte, short, string, uint, ulong, ushort.
- The type object.
- The type System.Type.
- Enum types.
- Single-dimensional arrays of the above types.

A constructor argument or public field that does not have one of these types, shall not be used as a positional or named parameter in an attribute specification.

## 22.3 Attribute specification

**Attribute specification** is the application of a previously defined attribute to a program entity. An attribute is a piece of additional declarative information that is specified for a program entity. Attributes can be specified at global scope (to specify attributes on the containing assembly or module) and for *type-declarations* (§14.7), *class-member-declarations* (§15.3), *interface-member-declarations* (§18.4), *struct-member-declarations* (§16.3), *enum-member-declarations* (§19.2), *accessor-declarations* (§15.7.3), *event-accessor-declarations* (§15.8), elements of *formal-parameter-lists* (§15.6.2), and elements of *type-parameter-lists* (§15.2.3).

Attributes are specified in *attribute sections*. An attribute section consists of a pair of square brackets, which surround a comma-separated list of one or more attributes. The order in which attributes are specified in such a list, and the order in which sections attached to the same program entity are arranged, is not significant. For instance, the attribute specifications [A] [B], [B] [A], [A, B], and [B, A] are equivalent.

```
global-attributes:
    global-attribute-sections

global-attribute-sections:
    global-attribute-section
    global-attribute-sections global-attribute-section

global-attribute-section:
    [ global-attribute-target-specifier attribute-list ]
    [ global-attribute-target-specifier attribute-list , ]

global-attribute-target-specifier:
    global-attribute-target :

global-attribute-target:
    identifier equal to assembly or module

attributes:
    attribute-sections

attribute-sections:
    attribute-section
    attribute-sections attribute-section

attribute-section:
    [ attribute-target-specifier_opt attribute-list ]
    [ attribute-target-specifier_opt attribute-list , ]

attribute-target-specifier:
    attribute-target :

attribute-target:
    identifier not equal to assembly or module
    keyword

attribute-list:
    attribute
    attribute-list , attribute

attribute:
    attribute-name attribute-arguments_opt

attribute-name:
    type-name
```

```
attribute-arguments:
  ( positional-argument-list_opt )
  ( positional-argument-list , named-argument-list )
  ( named-argument-list )
positional-argument-list:
  positional-argument
  positional-argument-list , positional-argument
positional-argument:
  argument-name_opt attribute-argument-expression
named-argument-list:
  named-argument
  named-argument-list , named-argument
named-argument:
  identifier = attribute-argument-expression
attribute-argument-expression:
  expression
```

For the above productions global-attribute-target and attribute-target, and in the text below, the referenced equality is that defined in §7.4.3.

An attribute consists of an attribute-name and an optional list of positional and named arguments. The positional arguments (if any) precede the named arguments. A positional argument consists of an attribute-argument-expression; a named argument consists of a name, followed by an equal sign, followed by an attribute-argument-expression, which, together, are constrained by the same rules as simple assignment. The order of named arguments is not significant.

> [Note: For convenience, a trailing comma is allowed in a global-attribute-section and an attribute-section, just as one is allowed in an array-initializer (§17.7). end note]

The attribute-name identifies an attribute class.

When an attribute is placed at the global level, a global-attribute-target-specifier is required. When the global-attribute-target is equal to:

- assembly – the target is the containing assembly
- module – the target is the containing module

No other values for global-attribute-target are allowed.

The standardized attribute-target names are event, field, method, param, property, return, type, and typevar. These target names shall only be used in the following contexts:

- event — an event.
- field — a field. A field-like event (i.e., one without accessors) can also have an attribute with this target.
- method — a constructor, finalizer, method, operator, property get and set accessors, indexer get and set accessors, and event add and remove accessors. A field-like event (i.e., one without accessors) can also have an attribute with this target.
- param — a property set accessor, an indexer set accessor, event add and remove accessors, and a parameter in a constructor, method, and operator.
- property — a property and an indexer.
- return — a delegate, method, operator, property get accessor, and indexer get accessor.
