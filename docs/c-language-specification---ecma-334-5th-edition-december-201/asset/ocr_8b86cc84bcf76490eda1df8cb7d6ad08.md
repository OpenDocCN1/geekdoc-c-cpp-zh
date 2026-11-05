# 16. Structs

# 16.1 General

Structs are similar to classes in that they represent data structures that can contain data members and function members. However, unlike classes, structs are value types and do not require heap allocation. A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to the data, the latter known as an object.

> [Note: Structs are particularly useful for small data structures that have value semantics. Complex numbers, points in a coordinate system, or key-value pairs in a dictionary are all good examples of structs. Key to these data structures is that they have few data members, that they do not require use of inheritance or referential identity, and that they can be conveniently implemented using value semantics where assignment copies the value instead of the reference. end note]

As described in §9.3.5, the simple types provided by C#, such as int, double, and bool, are, in fact, all struct types.

# 16.2 Struct declarations

# 16.2.1 General

A struct-declaration is a type-declaration (§14.7) that declares a new struct:

```
struct-declaration:
    attributesopt struct-modifiersopt partialopt struct identifier type-parameter-list opt
    struct-interfacesopt type-parameter-constraints-clausesopt struct-body ;opt
```

A struct-declaration consists of an optional set of attributes (§22), followed by an optional set of struct-modifiers (§16.2.2), followed by an optional partial modifier (§15.2.7), followed by the keyword struct and an identifier that names the struct, followed by an optional type-parameter-list specification (§15.2.3), followed by an optional struct-interfaces specification (§16.2.4), followed by an optional type-parameter-constraints-clauses specification (§15.2.5), followed by a struct-body (§16.2.5), optionally followed by a semicolon.

A struct declaration shall not supply a type-parameter-constraints-clauses unless it also supplies a type-parameter-list.

A struct declaration that supplies a type-parameter-list is a generic struct declaration.

# 16.2.2 Struct modifiers

A struct-declaration may optionally include a sequence of struct modifiers:

```
struct-modifiers:
    struct-modifier
    struct-modifiers struct-modifier

struct-modifier:
    new
    public
    protected
    internal
    private
```

It is a compile-time error for the same modifier to appear multiple times in a struct declaration.