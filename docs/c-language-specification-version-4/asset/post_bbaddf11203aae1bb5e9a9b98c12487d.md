
## C# LANGUAGE SPECIFICATION

- If S has a class-type constraint A and T has a class-type constraint B then there must be an identity conversion or implicit reference conversion from A to B or an implicit reference conversion from B to A.
- If S also depends on type parameter U and U has a class-type constraint A and T has a class-type constraint B then there must be an identity conversion or implicit reference conversion from A to B or an implicit reference conversion from B to A.

It is valid for S to have the value type constraint and T to have the reference type constraint. Effectively this limits T to the types System.Object, System.ValueType, System.Enum, and any interface type.

If the where clause for a type parameter includes a constructor constraint (which has the form new()), it is possible to use the new operator to create instances of the type (§7.6.10.1). Any type argument used for a type parameter with a constructor constraint must have a public parameterless constructor (this constructor implicitly exists for any value type) or be a type parameter having the value type constraint or constructor constraint (see §10.1.5 for details).

The following are examples of constraints:

```
interface IPrintable
{
    void Print();
}
interface IComparable<T>
{
    int CompareTo(T value);
}
interface IKeyProvider<T>
{
    T GetKey();
}
class Printer<T> where T : IPrintable { ... }
class SortedList<T> where T : IComparable<T> { ... }
class Dictionary<K,V>
    where K : IComparable<K>
    where V : IPrintable, IKeyProvider<K>, new()
{
    ...
}
```

The following example is in error because it causes a circularity in the dependency graph of the type parameters:

```
class Circular<S,T>
    where S : T
    where T : S    // Error, circularity in dependency graph
{
    ...
}
```

The following examples illustrate additional invalid situations:

```
class Sealed<S,T>
    where S : T
    where T : struct    // Error, T is sealed
{
    ...
}
class A { ... }
class B { ... }
class Incompat<S,T>
    where S: A, T
    where T: B    // Error, incompatible class-type constraints
{
    ...
}
class StructWithClass<S,T,U>
    where S: struct, T
    where T: U
    where U: A    // Error, A incompatible with struct
{
    ...
}
```

The effective base class of a type parameter T is defined as follows:

- If T has no primary constraints or type parameter constraints, its effective base class is object.
- If T has the value type constraint, its effective base class is System.ValueType.
- If T has a class-type constraint C but no type-parameter constraints, its effective base class is C.
- If T has no class-type constraint but has one or more type-parameter constraints, its effective base class is the most encompassed type (§6.4.2) in the set of effective base classes of its type-parameter constraints. The consistency rules ensure that such a most encompassed type exists.
- If T has both a class-type constraint and one or more type-parameter constraints, its effective base class is the most encompassed type (§6.4.2) in the set consisting of the class-type constraint of T and the effective base classes of its type-parameter constraints. The consistency rules ensure that such a most encompassed type exists.
- If T has the reference type constraint but no class-type constraints, its effective base class is object.

For the purpose of these rules, if T has a constraint V that is a value-type, use instead the most specific base type of V that is a class-type. This can never happen in an explicitly given constraint, but may occur when the constraints of a generic method are implicitly inherited by an overriding method declaration or an explicit implementation of an interface method.

These rules ensure that the effective base class is always a class-type.

The effective interface set of a type parameter T is defined as follows:

- If T has no secondary-constraints, its effective interface set is empty.
- If T has interface-type constraints but no type-parameter constraints, its effective interface set is its set of interface-type constraints.
- If T has no interface-type constraints but has type-parameter constraints, its effective interface set is the union of the effective interface sets of its type-parameter constraints.
- If T has both interface-type constraints and type-parameter constraints, its effective interface set is the union of its set of interface-type constraints and the effective interface sets of its type-parameter constraints.

A type parameter is known to be a reference type if it has the reference type constraint or its effective base class is not object or System.ValueType.

Values of a constrained type parameter type can be used to access the instance members implied by the constraints. In the example

```
interface IPrintable
{
    void Print();
}
class Printer<T> where T: IPrintable
{
    void PrintOne(T x) {
        x.Print();
    }
}
```

the methods of IPrintable can be invoked directly on x because T is constrained to always implement IPrintable.

## 10.1.6 Class body

The class-body of a class defines the members of that class.

```
class-body:
    { class-member-declarations_opt }
```

## 10.2 Partial types

A type declaration can be split across multiple partial type declarations. The type declaration is constructed from its parts by following the rules in this section, whereupon it is treated as a single declaration during the remainder of the compile-time and run-time processing of the program.

A class-declaration, struct-declaration or interface-declaration represents a partial type declaration if it includes a partial modifier. partial is not a keyword, and only acts as a modifier if it appears immediately before one of the keywords class, struct or interface in a type declaration, or before the type void in a method declaration. In other contexts it can be used as a normal identifier.

Each part of a partial type declaration must include a partial modifier. It must have the same name and be declared in the same namespace or type declaration as the other parts. The partial modifier indicates that additional parts of the type declaration may exist elsewhere, but the existence of such additional parts is not a requirement; it is valid for a type with a single declaration to include the partial modifier.

All parts of a partial type must be compiled together such that the parts can be merged at compile-time into a single type declaration. Partial types specifically do not allow already compiled types to be extended.

Nested types may be declared in multiple parts by using the partial modifier. Typically, the containing type is declared using partial as well, and each part of the nested type is declared in a different part of the containing type.

The partial modifier is not permitted on delegate or enum declarations.

### 10.2.1 Attributes

The attributes of a partial type are determined by combining, in an unspecified order, the attributes of each of the parts. If an attribute is placed on multiple parts, it is equivalent to specifying the attribute multiple times on the type. For example, the two parts:

```
[Attr1, Attr2("hello")]
partial class A {}
[Attr3, Attr2("goodbye")]
partial class A {}
```

are equivalent to a declaration such as:

```
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

### 10.2.4 Base class

When a partial class declaration includes a base class specification it must agree with all other parts that include a base class specification. If no part of a partial class includes a base class specification, the base class becomes System.Object (§10.1.4.1).

### 10.2.5 Base interfaces

The set of base interfaces for a type declared in multiple parts is the union of the base interfaces specified on each part. A particular base interface may only be named once on each part, but it is permitted for multiple parts to name the same base interface(s). There must only be one implementation of the members of any given base interface.

In the example

```
partial class C: IA, IB {...}
partial class C: IC {...}
partial class C: IA, IB {...}
```

the set of base interfaces for class C is IA, IB, and IC.

Typically, each part provides an implementation of the interface(s) declared on that part; however, this is not a requirement. A part may provide the implementation for an interface declared on a different part:

```
partial class X
{
    int IComparable.CompareTo(object o) {...}
}
partial class X: IComparable
{
    ...
}
```

### 10.2.6 Members

With the exception of partial methods (§10.2.7), the set of members of a type declared in multiple parts is simply the union of the set of members declared in each part. The bodies of all parts of the type declaration share the same declaration space (§3.3), and the scope of each member (§3.7) extends to the bodies of all the parts. The accessibility domain of any member always includes all the parts of the enclosing type; a private member declared in one part is freely accessible from another part. It is a compile-time error to declare the same member in more than one part of the type, unless that member is a type with the partial modifier.

```
partial class A
{
    int x;            // Error, cannot declare x more than once
    partial class Inner  // Ok, Inner is a partial type
    {
        int y;
    }
}
partial class A
{
    int x;            // Error, cannot declare x more than once
    partial class Inner  // Ok, Inner is a partial type
    {
        int z;
    }
}
```
