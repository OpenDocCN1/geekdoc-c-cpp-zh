168 Generic Types and Methods

# 26.4 Constraints on Type Parameters

A declaration of a generic class C<T1,...,Tn> may have type parameter constraints

```
class-modifiers class C<T1,...,Tn> subtype-clause parameter-constraints
class-body
```

The parameter-constraints is a list of constraint-clauses, each of this form:

```
where T : C1, C2, ..., Cm
```

In the constraint clause, T is one of the type parameters T1,...,Tn and each ci is a constraint. A given type parameter Ti can have at most one constraint clause; that may constrain one or more constraints C1, C2, ..., Cm. The order of the constraint clauses for T1,...,Tn does not matter.
A constraint c must have one of these four forms:

+   - c is a type expression: a non-sealed class or an interface or a type parameter. The expression may be constructed by a type and involve the type parameters T1,...,Tn and type parameters of enclosing generic classes and structs. An array or a type parameter that has a struct constraint cannot be used as a constraint. Nor can the Object, System.ValueType, System.Delegate, System.Array, System.Enum. At most one of the constraints on a type can be a class, and that constraint must appear first. There can be any number of constraints that are interfaces or type parameters.
- c is the special class constraint. This means that the type parameter must be instantiated by a reference type. The special class constraint can appear only first in a constraint list and cannot appear together with a class or with the special struct constraint.
- c is the special struct constraint. This means that the type parameter must be instantiated by a non-nullable value type: a simple type such as int, or a non-nullable struct type. The struct constraint can appear only first in a constraint list and cannot appear together with a constraint that is a class or with
- c is the special new() constraint. This means that the type parameter must be instantiated by a type that has an argumentless constructor. If a type parameter has a struct constraint, it is guaranteed to have an argumentless constructor; in that case the new() constraint is redundant and illegal. 206 illustrates the use of the new() constraint

It is illegal for constraints to be circular as in class<T,U> where T : U : T {. The types T1,...,Tn used when constructing a type must satisfy the parameter-constraints; if parameter Ti is replaced by type Ti throughout the parameter-constraints, for each constraint t : c, where c is a type expression, it must hold that t is convertible to c by an implicit reference conversion or a boxing conversion.

An override method or explicit interface implementation method gets its constraints from the base class method or the interface method and cannot have explicit constraints of its own. A generic method that implements a method described by a base interface must have the same constraints as the interface method.