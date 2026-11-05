
- `return` — the target is the return value
- For an attribute on a method declaration the default target is the method. Otherwise when the *attribute_target* is equal to:
  - `method` — the target is the method
  - `return` — the target is the return value
- For an attribute on an operator declaration the default target is the operator. Otherwise when the *attribute_target* is equal to:
  - `method` — the target is the operator
  - `return` — the target is the return value
- For an attribute on a get accessor declaration for a property or indexer declaration the default target is the associated method. Otherwise when the *attribute_target* is equal to:
  - `method` — the target is the associated method
  - `return` — the target is the return value
- For an attribute specified on a set accessor for a property or indexer declaration the default target is the associated method. Otherwise when the *attribute_target* is equal to:
  - `method` — the target is the associated method
  - `param` — the target is the lone implicit parameter
- For an attribute specified on an event declaration that omits *event_accessor_declarations* the default target is the *event* declaration. Otherwise when the *attribute_target* is equal to:
  - `event` — the target is the event declaration
  - `field` — the target is the field
  - `method` — the targets are the methods
- In the case of an event declaration that does not omit *event_accessor_declarations* the default target is the *method*.
  - `method` — the target is the associated method
  - `param` — the target is the lone parameter

In all other contexts, inclusion of an *attribute_target_specifier* is permitted but unnecessary.

Example: A class declaration may either include or omit the specifier *type*:

```
[type: Author("Brian Kernighan")]
class Class1 {}

[Author("Dennis Ritchie")]
class Class2 {}
```

*end example.*

An implementation can accept other *attribute_targets*, the purposes of which are implementation defined. An implementation that does not recognize such an *attribute_target* shall issue a warning and ignore the containing *attribute_section*.

By convention, attribute classes are named with a suffix of Attribute. An attribute_name can either include or omit this suffix. Specifically, an attribute_name is resolved as follows:

- If the right-most identifier of the attribute_name is a verbatim identifier (§6.4.3), then the attribute_name is resolved as a type_name (§7.8). If the result is not a type derived from System.Attribute, a compile-time error occurs.
- Otherwise,
  - The attribute_name is resolved as a type_name (§7.8) except any errors are suppressed. If this resolution is successful and results in a type derived from System.Attribute then the type is the result of this step.
  - The characters Attribute are appended to the right-most identifier in the attribute_name and the resulting string of tokens is resolved as a type_name (§7.8) except any errors are suppressed. If this resolution is successful and results in a type derived from System.Attribute then the type is the result of this step.

If exactly one of the two steps above results in a type derived from System.Attribute, then that type is the result of the attribute_name. Otherwise a compile-time error occurs.

Example: If an attribute class is found both with and without this suffix, an ambiguity is present, and a compile-time error results. If the attribute_name is spelled such that its right-most identifier is a verbatim identifier (§6.4.3), then only an attribute without a suffix is matched, thus enabling such an ambiguity to be resolved. The example

```
using System;
[AttributeUsage(AttributeTargets.All)]
public class Example : Attribute
{
}

[AttributeUsage(AttributeTargets.All)]
public class ExampleAttribute : Attribute
{
}

[Example]      // Error: ambiguity
class Class1 {}

[ExampleAttribute]  // Refers to ExampleAttribute
class Class2 {}

[@Example]      // Refers to Example
class Class3 {}

[@ExampleAttribute]  // Refers to ExampleAttribute
class Class4 {}
```

shows two attribute classes named Example and ExampleAttribute. The attribute [Example] is ambiguous, since it could refer to either Example or ExampleAttribute. Using a verbatim identifier allows the exact intent to be specified in such rare cases. The attribute [ExampleAttribute] is not ambiguous (although it would be if there was an attribute class named ExampleAttributeAttribute!). If the declaration for class Example is removed, then both attributes refer to the attribute class named ExampleAttribute, as follows:

```
using System;

[AttributeUsage(AttributeTargets.All)]
public class ExampleAttribute : Attribute
{}

[Example]    // Refers to ExampleAttribute
class Class1 {}

[ExampleAttribute]  // Refers to ExampleAttribute
class Class2 {}

[@Example]    // Error: no attribute named "Example"
class Class3 {}
```
*end example*

It is a compile-time error to use a single-use attribute class more than once on the same entity.

*Example:* The example

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class HelpStringAttribute : Attribute
{
    public HelpStringAttribute(string value)
    {
        Value = value;
    }

    public string Value { get; }
}
[HelpString("Description of Class1")]
[HelpString("Another description of Class1")]
public class Class1 {}
```

results in a compile-time error because it attempts to use HelpString, which is a single-use attribute class, more than once on the declaration of Class1.

An expression E is an attribute_argument_expression if all of the following statements are true:

- The type of E is an attribute parameter type (§21.2.4).
- At compile-time, the value of E can be resolved to one of the following:
  - A constant value.
  - A System.Type object obtained using a typeof_expression (§11.7.16) specifying a non-generic type, a closed constructed type (§8.4.3), or an unbound generic type (§8.4.4), but not an open generic type (§8.4.3).
  - A single-dimensional array of attribute_argument_expressions.

*Example:*

```csharp
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Field)]
public class TestAttribute : Attribute
{
    public int P1 { get; set; }
    public Type P2 { get; set; }
    public object P3 { get; set; }
}
[Test(P1 = 1234, P3 = new int[]{1, 3, 5}, P2 = typeof(float))]
class MyClass {}
class <T> {
[Test(P2 = typeof(T))] // Error – T not a closed type.
int x1;
[Test(P2 = typeof(<T>))] // Error – C<T> not a closed type.
int x2;
[Test(P2 = typeof(<int>))] // Ok
int x3;
[Test(P2 = typeof(<>))] // Ok
int x4;
}
```
*end example*

The attributes of a type declared in multiple parts are determined by combining, in an unspecified order, the attributes of each of its parts. If the same attribute is placed on multiple parts, it is equivalent to specifying that attribute multiple times on the type.

Example: The two parts:

```
[Attr1, Attr2("hello")]
partial class A {}
[Attr3, Attr2("goodbye")]
partial class A {}
```

are equivalent to the following single declaration:

```
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

Attributes on type parameters combine in the same way.

## 21.4 Attribute instances

### 21.4.1 General

An attribute instance is an instance that represents an attribute at run-time. An attribute is defined with an attribute class, positional arguments, and named arguments. An attribute instance is an instance of the attribute class that is initialized with the positional and named arguments.

Retrieval of an attribute instance involves both compile-time and run-time processing, as described in the following subclauses.

### 21.4.2 Compilation of an attribute

The compilation of an *attribute* with attribute class T, *positional_argument_list* P, *named_argument_list* N, and specified on a program entity E is compiled into an assembly A via the following steps:

- Follow the compile-time processing steps for compiling an *object_creation_expression* of the form `new T(P)`. These steps either result in a compile-time error, or determine an instance constructor C on T that can be invoked at run-time.
- If C does not have public accessibility, then a compile-time error occurs.
- For each *named_argument* Arg in N:
  - Let Name be the *identifier* of the *named_argument* Arg.
  - Name shall identify a non-static read-write public field or property on T. If T has no such field or property, then a compile-time error occurs.
- If any of the values within *positional_argument_list* P or one of the values within *named_argument_list* N is of type `System.String` and the value is not well-formed as defined by the Unicode Standard, it is implementation-defined whether the value compiled is equal to the run-time value retrieved (§21.4.3).
  *Note: As an example, a string which contains a high surrogate UTF-16 code unit which isn't immediately followed by a low surrogate code unit is not well-formed. end note*
- Store the following information (for run-time instantiation of the attribute) in the assembly output by the compiler as a result of compiling the program containing the attribute: the attribute class T, the instance constructor C on T, the *positional_argument_list* P, the *named_argument_list* N, and the associated program entity E, with the values resolved completely at compile-time.

### 21.4.3 Run-time retrieval of an attribute instance

The attribute instance represented by T, C, P, and N, and associated with E can be retrieved at run-time from the assembly A using the following steps:

- Follow the run-time processing steps for executing an *object_creation_expression* of the form `new T(P)`, using the instance constructor C and values as determined at compile-time. These steps either result in an exception, or produce an instance O of T.
- For each *named_argument* Arg in N, in order:
  - Let Name be the *identifier* of the *named_argument* Arg. If Name does not identify a non-static public read-write field or property on O, then an exception is thrown.
  - Let Value be the result of evaluating the *attribute_argument_expression* of Arg.
  - If Name identifies a field on O, then set this field to Value.
  - Otherwise, Name identifies a property on O. Set this property to Value.
  - The result is O, an instance of the attribute class T that has been initialized with the *positional_argument_list* P and the *named_argument_list* N.

*Note: The format for storing T, C, P, N (and associating it with E) in A and the mechanism to specify E and retrieve T, C, P, N from A (and hence how an attribute instance is obtained at runtime) is beyond the scope of this standard. end note*

*Example:* In an implementation of the CLI, the `Help` attribute instances in the assembly created by compiling the example program in §21.2.3 can be retrieved with the following program:
