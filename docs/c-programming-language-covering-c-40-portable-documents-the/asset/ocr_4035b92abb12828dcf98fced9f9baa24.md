Each type parameter in a class declaration defines a name in the declaration space (§3.3) of that class. Thus it cannot have the same name as another type parameter or a member declared in that class. A type parameter also cannot have the same name as the type itself.

# 10.1.4 Class Base Specification

A class declaration may include a class-base specification, which defines the direct base class of the class and the interfaces (§13) directly implemented by the class.

```
class-base:
    :    class-type
    :    interface-type-list
    :    class-type    ,    interface-type-list

interface-type-list:
    interface-type
    interface-type-list    ,    interface-type
```

The base class specified in a class declaration can be a constructed class type (§4.4). A base class cannot be a type parameter on its own, although it can involve the type parameters that are in scope.

```
class Extend<V> : V { }        // Error: type parameter used as base class
```

> > **BILL WAGNER** | I wish this restriction could be removed. It would be a great way to create mixins. I realize it’s a very difficult problem because My may contain any arbitrary methods and properties. Depending on any concrete type used for V in a closed generic type, Extend<V> may not compile.

# 10.1.4.1 Base Classes

When a class-type is included in the class-base, it specifies the direct base class of the class being declared. If a class declaration has no class-base, or if the class-base lists only interface types, the direct base class is assumed to be object. A class inherits members from its direct base class, as described in §10.3.3.

In the example

```
class A { }

class B : A { }
```

class A is said to be the direct base class of B, and B is said to be derived from A. Since A does not explicitly specify a direct base class, its direct base class is implicitly object.

For a constructed class type, if a base class is specified in the generic class declaration, the base class of the constructed type is obtained by substituting, for each type-parameter in