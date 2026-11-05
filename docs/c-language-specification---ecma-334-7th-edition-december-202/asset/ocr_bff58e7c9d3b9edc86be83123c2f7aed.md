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

# 22.4 Attribute instances

# 22.4.1 General

An attribute instance is an instance that represents an attribute at run-time. An attribute is defined with an attribute class, positional arguments, and named arguments. An attribute instance is an instance of the attribute class that is initialized with the positional and named arguments.

Retrieval of an attribute instance involves both compile-time and run-time processing, as described in the following subclauses.

# 22.4.2 Compilation of an attribute

The compilation of an attribute with attribute class T, positional_argument_list P, named_argument_list N, and specified on a program entity E is compiled into an assembly A via the following steps:

+   - Follow the compile-time processing steps for compiling an object_creation_expression of the form new T(P). These steps either result in a compile-time error, or determine an instance constructor C on T that can be invoked at run-time.
+   - If C does not have public accessibility, then a compile-time error occurs.
+   - For each named_argument Arg in N:
+     - Let Name be the identifier of the named_argument Arg.
+     - Name shall identify a non-static read-write public field or property on T. If T has no such field or property, then a compile-time error occurs.
+   - If any of the values within positional_argument_list P or one of the values within named_argument_list N is of type System.String and the value is not well-formed as defined by the Unicode Standard, it is implementation-defined whether the value compiled is equal to the run-time