
## 17. Attributes

Much of the C# language enables the programmer to specify declarative information about the entities defined in the program. For example, the accessibility of a method in a class is specified by decorating it with the *method-modifiers* *public*, *protected*, *internal*, and *private*.

C# enables programmers to invent new kinds of declarative information, called *attributes*. Programmers can then attach attributes to various program entities, and retrieve attribute information in a runtime environment. For instance, a framework might define a HelpAttribute attribute that can be placed on certain program elements (such as classes and methods) to provide a mapping from those program elements to their documentation.

> > **JESSE LIBERTY** A common and powerful use of attributes can be seen throughout Silverlight and WPF, where attributes are used to indicate the available *view states* associated with a class.
> >
> > Similarly, Test Libraries use attributes to differentiate test methods from supporting methods. Web services use attributes to designate which methods are exposed to clients.

Attributes are defined through the declaration of *attribute classes* (§17.1), which may have positional and named parameters (§17.1.2). Attributes are attached to entities in a C# program using *attribute specifications* (§17.2), and can be retrieved at runtime as *attribute instances* (§17.3).

> > **ERIC LIPPERT** Try to use attributes only to talk about the *type itself* rather than representing details about the *semantics* of that type. For example, suppose you have a class *Book* with a property *Author*. That is part of the semantics of the class: The class represents books, and books have authors. If you put an *AuthorAttribute* on the class *Book*, that doesn't represent the author of the *book*, but rather the author of the *class*. A class *Television* might have a property *Obsolete* that indicates whether a particular model is out of production. If you put an *ObsoleteAttribute* on the class, it means that the *class itself* is obsolete, not that it represents an obsolete product.

### 17.1 Attribute Classes

A class that derives from the abstract class System.Attribute, whether directly or indirectly, is an attribute class. The declaration of an attribute class defines a new kind of attribute that can be placed on a declaration. By convention, attribute classes are named with a suffix of Attribute. Uses of an attribute may either include or omit this suffix.

### 17.1.1 Attribute Usage

The attribute AttributeUsage (§17.4.1) is used to describe how an attribute class can be used.

AttributeUsage has a positional parameter (§17.1.2) that enables an attribute class to specify the kinds of declarations on which it can be used. The example

```
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute
{
    ...
}
```

defines an attribute class named SimpleAttribute that can be placed on class-declarations and interface-declarations only. The example

```
[Simple] class Class1 {...}
[Simple] interface Interface1 {...}
```

shows several uses of the Simple attribute. Although this attribute is defined with the name SimpleAttribute, when this attribute is used, the Attribute suffix may be omitted, resulting in the short name Simple. Thus the example above is semantically equivalent to the following:

```
[SimpleAttribute] class Class1 {...}
[SimpleAttribute] interface Interface1 {...}
```

AttributeUsage has a named parameter (§17.1.2) called AllowMultiple, which indicates whether the attribute can be specified more than once for a given entity. If AllowMultiple for an attribute class is true, then that attribute class is a multi-use attribute class, and can be specified more than once on an entity. If AllowMultiple for an attribute class is false or it is unspecified, then that attribute class is a single-use attribute class, and can be specified at most once on an entity.

The example

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
class Class1
{
    ...
}
```

shows a class declaration with two uses of the Author attribute.

> CHRIS SELLS  For those of you who are reading this example and don’t know who Brian Kernighan or Dennis Ritchie is: For shame! They are true software legends.

> JON SKEET  While I agree with Chris, I certainly hope that neither of the esteemed gentlemen in question would ever write a class named Class1.

AttributeUsage has another named parameter called Inherited, which indicates whether the attribute, when specified on a base class, is also inherited by classes that derive from that base class. If Inherited for an attribute class is true, then that attribute is inherited. If Inherited for an attribute class is false, then that attribute is not inherited. If it is unspecified, its default value is true.

An attribute class X not having an AttributeUsage attribute attached to it, as in

```
using System;
class X: Attribute {...}
```

is equivalent to the following:

```
using System;
[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true
)]
class X: Attribute {...}
```

### 17.1.2 Positional and Named Parameters

> **BILL WAGNER** In most cases, using named parameters will result in a clearer, more easily understood program. Positional parameters should be used only for attributes with one property, where the property is made clear by the attribute name, such as AuthorAttribute.

Attribute classes can have *positional parameters* and *named parameters*. Each public instance constructor for an attribute class defines a valid sequence of positional parameters for that attribute class. Each nonstatic public read-write field and property for an attribute class defines a named parameter for the attribute class.

The example

```
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute: Attribute
{
    public HelpAttribute(string url) { // Positional parameter
        ...
    }

    public string Topic {
        get {...}
        set {...}
    }

    public string Url {
        get {...}
    }
}
```

defines an attribute class named HelpAttribute that has one positional parameter, url, and one named parameter, Topic. Although it is nonstatic and public, the property Url does not define a named parameter, since it is not read-write.

This attribute class might be used as follows:

```
[Help("http://www.mycompany.com/.../Class1.htm")]
class Class1
{
    ...
}
[Help("http://www.mycompany.com/.../Misc.htm", Topic = "Class2")]
class Class2
{
    ...
}
```

### 17.1.3 Attribute Parameter Types

The types of positional and named parameters for an attribute class are limited to the attribute parameter types:

- One of the following types: bool, byte, char, double, float, int, long, sbyte, short, string, uint, ulong, ushort.
- The type object.
- The type System.Type.
- An enum type, provided it has public accessibility and the types in which it is nested (if any) also have public accessibility (§17.2).
- Single-dimensional arrays of the above types.

> JON SKEET Note that decimal cannot be used as a parameter type, even though you can declare decimal constants. This is one example of CLI rules leaking into C#.

> MAREK SAFAR Although arrays are supported, array covariance is not allowed for attributes of reference types. Similarly, the C# 4.0 dynamic type cannot be used where type object is expected.

A constructor argument or public field that does not have one of these types cannot be used as a positional or named parameter in an attribute specification.
