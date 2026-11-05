```
public Type P2 { get; set; }
public object P3 { get; set; }
}
[Test(P1 = 1234, P3 = new int[]{1, 3, 5}, P2 = typeof(float))]
class MyClass {}
class <T> {
[Test(P2 = typeof(T))] // Error – T not a closed type.
int x1;
[Test(P2 = typeof(<T>))] // Error – C<;T>; not a closed type.
int x2;
[Test(P2 = typeof(<int>))] // Ok
int x3;
[Test(P2 = typeof(<>))] // Ok
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
```

Attributes on type parameters combine in the same way.

# 21.4 Attribute instances

# 21.4.1 General

An attribute instance is an instance that represents an attribute at run-time. An attribute is defined with an attribute class, positional arguments, and named arguments. An attribute instance is an instance of the attribute class that is initialized with the positional and named arguments.

Retrieval of an attribute instance involves both compile-time and run-time processing, as described in the following subclauses.