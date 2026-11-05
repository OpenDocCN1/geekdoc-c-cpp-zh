
```
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

Note: For convenience, a trailing comma is allowed in a global_attribute_section and an attribute_section, just as one is allowed in an array_initializer (§17.7). end note

The attribute_name identifies an attribute class.

- `return` — the target is the return value
- For an attribute specified on a set accessor for a property or indexer declaration the default target is the associated method. Otherwise when the *attribute_target* is equal to:
  - `method` — the target is the associated method
  - `param` — the target is the lone implicit parameter
- For an attribute on an automatically implemented property declaration the default target is the property. Otherwise when the *attribute_target* is equal to:
  - `field` — the target is the compiler-generated backing field for the property
- For an attribute specified on an event declaration that omits `event_accessor_declarations` the default target is the event declaration. Otherwise when the *attribute_target* is equal to:
  - `event` — the target is the event declaration
  - `field` — the target is the field
  - `method` — the targets are the methods
- In the case of an event declaration that does not omit `event_accessor_declarations` the default target is the method.
  - `method` — the target is the associated method
  - `param` — the target is the lone parameter

In all other contexts, inclusion of an *attribute_target_specifier* is permitted but unnecessary.

*Example: a class declaration may either include or omit the specifier type:*

```
~~~csharp
[type: Author("Brian Kernighan")]
class Class1 {}

[Author("Dennis Ritchie")]
class Class2 {}
~~~
```

*end example.*

An implementation can accept other *attribute_targets*, the purposes of which are implementation defined. An implementation that does not recognize such an *attribute_target* shall issue a warning and ignore the containing *attribute_section*.

By convention, attribute classes are named with a suffix of `Attribute`. An *attribute_name* can either include or omit this suffix. Specifically, an *attribute_name* is resolved as follows:

- If the right-most identifier of the *attribute_name* is a verbatim identifier (§6.4.3), then the *attribute_name* is resolved as a *type_name* (§7.8). If the result is not a type derived from `System.Attribute`, a compile-time error occurs.
- Otherwise,
  - The *attribute_name* is resolved as a *type_name* (§7.8) except any errors are suppressed. If this resolution is successful and results in a type derived from `System.Attribute` then the type is the result of this step.
  - The characters `Attribute` are appended to the right-most identifier in the *attribute_name* and the resulting string of tokens is resolved as a *type_name* (§7.8) except any errors are

```
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
[HelpString("Another description of Class1")]  // multiple uses not allowed
public class Class1 {}
```

results in a compile-time error because it attempts to use HelpString, which is a single-use attribute class, more than once on the declaration of Class1.

*end example*

An expression E is an attribute_argument_expression if all of the following statements are true:

- The type of E is an attribute parameter type (§22.2.4).
- At compile-time, the value of E can be resolved to one of the following:
  - A constant value.
  - A System.Type object obtained using a typeof_expression (§12.8.17) specifying a non-generic type, a closed constructed type (§8.4.3), or an unbound generic type (§8.4.4), but not an open generic type (§8.4.3).
  - A single-dimensional array of attribute_argument_expressions.

Example:

```
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Field)]
public class TestAttribute : Attribute
{
    public int P1 { get; set; }

    public Type P2 { get; set; }

    public object P3 { get; set; }
}

[Test(P1 = 1234, P3 = new int[]{1, 3, 5}, P2 = typeof(float))]
class MyClass {}

class C<T> {
    [Test(P2 = typeof(T))] // Error – T not a closed type.
    int x1;

    [Test(P2 = typeof(C<T>))] // Error – C<T>; not a closed type.
    int x2;

    [Test(P2 = typeof(C<int>))] // Ok
    int x3;
```

```
[Test(P2 = typeof(C<>))] // Ok
int x4;
}
end example
```

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
end example
```

Attributes on type parameters combine in the same way.

## 22.4 Attribute instances

### 22.4.1 General

An attribute instance is an instance that represents an attribute at run-time. An attribute is defined with an attribute class, positional arguments, and named arguments. An attribute instance is an instance of the attribute class that is initialized with the positional and named arguments.

Retrieval of an attribute instance involves both compile-time and run-time processing, as described in the following subclauses.

### 22.4.2 Compilation of an attribute

The compilation of an attribute with attribute class T, positional_argument_list P, named_argument_list N, and specified on a program entity E is compiled into an assembly A via the following steps:

- Follow the compile-time processing steps for compiling an object_creation_expression of the form new T(P). These steps either result in a compile-time error, or determine an instance constructor C on T that can be invoked at run-time.
- If C does not have public accessibility, then a compile-time error occurs.
- For each named_argument Arg in N:
  - Let Name be the identifier of the named_argument Arg.
  - Name shall identify a non-static read-write public field or property on T. If T has no such field or property, then a compile-time error occurs.
- If any of the values within positional_argument_list P or one of the values within named_argument_list N is of type System.String and the value is not well-formed as defined by the Unicode Standard, it is implementation-defined whether the value compiled is equal to the run-time
