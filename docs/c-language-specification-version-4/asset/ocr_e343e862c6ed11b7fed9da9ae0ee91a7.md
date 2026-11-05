# 4.4.1 Type arguments

Each argument in a type argument list is simply a type.

```
type-argument-list:
    < type-arguments >
type-arguments:
    type-argument
    type-arguments , type-argument
type-argument:
    type
```

In unsafe code (§18), a type-argument may not be a pointer type. Each type argument must satisfy any constraints on the corresponding type parameter (§10.1.5).

# 4.4.2 Open and closed types

All types can be classified as either open types or closed types. An open type is a type that involves type parameters. More specifically:

+   - A type parameter defines an open type.
+   - An array type is an open type if and only if its element type is an open type.
+   - A constructed type is an open type if and only if one or more of its type arguments is an open type. A constructed nested type is an open type if and only if one or more of its type arguments or the type arguments of its containing type(s) is an open type.

A closed type is a type that is not an open type.

At run-time, all of the code within a generic type declaration is executed in the context of a closed constructed type that was created by applying type arguments to the generic declaration. Each type parameter within the generic type is bound to a particular run-time type. The run-time processing of all statements and expressions always occurs with closed types, and open types occur only during compile-time processing.

Each closed constructed type has its own set of static variables, which are not shared with any other closed constructed types. Since an open type does not exist at run-time, there are no static variables associated with an open type. Two closed constructed types are the same type if they are constructed from the same unbound generic type, and their corresponding type arguments are the same type.

# 4.4.3 Bound and unbound types

The term unbound type refers to a non-generic type or an unbound generic type. The term bound type refers to a non-generic type or a constructed type.

An unbound type refers to the entity declared by a type declaration. An unbound generic type is not itself a type, and cannot be used as the type of a variable, argument or return value, or as a base type. The only construct in which an unbound generic type can be referenced is the typeof expression (§7.6.11).

# 4.4.4 Satisfying constraints

Whenever a constructed type or generic method is referenced, the supplied type arguments are checked against the type parameter constraints declared on the generic type or method (§10.1.5). For each where clause, the type argument A that corresponds to the named type parameter is checked against each constraint as follows:

+   - If the constraint is a class type, an interface type, or a type parameter, let C represent that constraint with the supplied type arguments substituted for any type parameters that appear in the constraint. To satisfy the constraint, it must be the case that type A is convertible to type C by one of the following: