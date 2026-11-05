
- Otherwise, both operands are converted to type int.

*Note:* The first rule disallows any operations that mix the `decimal` type with the `double` and `float` types. The rule follows from the fact that there are no implicit conversions between the `decimal` type and the `double` and `float` types. *end note*

*Note:* Also note that it is not possible for an operand to be of type `ulong` when the other operand is of a signed integral type. The reason is that no integral type exists that can represent the full range of `ulong` as well as the signed integral types. *end note*

In both of the above cases, a cast expression can be used to explicitly convert one operand to a type that is compatible with the other operand.

*Example:* In the following code

```
decimal AddPercent(decimal x, double percent) => x * (1.0 + percent / 100.0);
```

a binding-time error occurs because a `decimal` cannot be multiplied by a `double`. The error is resolved by explicitly converting the second operand to `decimal`, as follows:

```
decimal AddPercent(decimal x, double percent) => x * (decimal)(1.0 + percent / 100.0);
```

*end example*

**End of informative text.**

### 11.4.8 Lifted operators

**Lifted operators** permit predefined and user-defined operators that operate on non-nullable value types to also be used with nullable forms of those types. Lifted operators are constructed from predefined and user-defined operators that meet certain requirements, as described in the following:

- For the unary operators +, ++, -, --, !, and ~, a lifted form of an operator exists if the operand and result types are both non-nullable value types. The lifted form is constructed by adding a single ? modifier to the operand and result types. The lifted operator produces a null value if the operand is null. Otherwise, the lifted operator unwraps the operand, applies the underlying operator, and wraps the result.
- For the binary operators +, -, *, /, %, &, |, ^, <<, and >>, a lifted form of an operator exists if the operand and result types are all non-nullable value types. The lifted form is constructed by adding a single ? modifier to each operand and result type. The lifted operator produces a null value if one or both operands are null (an exception being the & and | operators of the bool? type, as described in §11.12.5). Otherwise, the lifted operator unwraps the operands, applies the underlying operator, and wraps the result.
- For the equality operators == and !=, a lifted form of an operator exists if the operand types are both non-nullable value types and if the result type is bool. The lifted form is constructed by adding a single ? modifier to each operand type. The lifted operator considers two null values equal, and a null value unequal to any non-null value. If both operands are non-null, the lifted operator unwraps the operands and applies the underlying operator to produce the bool result.
- For the relational operators <, >, <=, and >=, a lifted form of an operator exists if the operand types are both non-nullable value types and if the result type is bool. The lifted form is constructed by adding a single ? modifier to each operand type. The lifted operator produces the value false if one or both operands are null. Otherwise, the lifted operator unwraps the operands and applies the underlying operator to produce the bool result.

## 11.5 Member lookup

### 11.5.1 General

A member lookup is the process whereby the meaning of a name in the context of a type is determined. A member lookup can occur as part of evaluating a simple_name (§11.7.4) or a member_access (§11.7.6) in an expression. If the simple_name or member_access occurs as the primary_expression of an invocation_expression (§11.7.8.2), the member is said to be invoked.

If a member is a method or event, or if it is a constant, field or property of either a delegate type (§19) or the type dynamic (§8.2.4), then the member is said to be invocable.

Member lookup considers not only the name of a member but also the number of type parameters the member has and whether the member is accessible. For the purposes of member lookup, generic methods and nested generic types have the number of type parameters indicated in their respective declarations and all other members have zero type parameters.

A member lookup of a name N with K type arguments in a type T is processed as follows:

- First, a set of accessible members named N is determined:
  - If T is a type parameter, then the set is the union of the sets of accessible members named N in each of the types specified as a primary constraint or secondary constraint (§14.2.5) for T, along with the set of accessible members named N in object.
  - Otherwise, the set consists of all accessible (§7.5) members named N in T, including inherited members and the accessible members named N in object. If T is a constructed type, the set of members is obtained by substituting type arguments as described in §14.3.3. Members that include an override modifier are excluded from the set.
- Next, if K is zero, all nested types whose declarations include type parameters are removed. If K is not zero, all members with a different number of type parameters are removed. When K is zero, methods having type parameters are not removed, since the type inference process (§11.6.3) might be able to infer the type arguments.
- Next, if the member is invoked, all non-invocable members are removed from the set.
- Next, members that are hidden by other members are removed from the set. For every member S.M in the set, where S is the type in which the member M is declared, the following rules are applied:
  - If M is a constant, field, property, event, or enumeration member, then all members declared in a base type of S are removed from the set.
  - If M is a type declaration, then all non-types declared in a base type of S are removed from the set, and all type declarations with the same number of type parameters as M declared in a base type of S are removed from the set.
  - If M is a method, then all non-method members declared in a base type of S are removed from the set.
- Next, interface members that are hidden by class members are removed from the set. This step only has an effect if T is a type parameter and T has both an effective base class other than object and a non-empty effective interface set (§14.2.5). For every member S.M in the set, where S is the type in which the member M is declared, the following rules are applied if S is a class declaration other than object:
  - If M is a constant, field, property, event, enumeration member, or type declaration, then all members declared in an interface declaration are removed from the set.
  - If M is a method, then all non-method members declared in an interface declaration are removed from the set, and all methods with the same signature as M declared in an interface declaration are removed from the set.
- Finally, having removed hidden members, the result of the lookup is determined:
  - If the set consists of a single member that is not a method, then this member is the result of the lookup.
  - Otherwise, if the set contains only methods, then this group of methods is the result of the lookup.
  - Otherwise, the lookup is ambiguous, and a binding-time error occurs.

For member lookups in types other than type parameters and interfaces, and member lookups in interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effect of the lookup rules is simply that derived members hide base members with the same name or signature. Such single-inheritance lookups are never ambiguous. The ambiguities that can possibly arise from member lookups in multiple-inheritance interfaces are described in §17.4.6.

> Note: This phase only accounts for one kind of ambiguity. If the member lookup results in a method group, further uses of method group may fail due to ambiguity, for example as described in §11.6.4.1 and §11.6.2. end note

### 11.5.2 Base types

For purposes of member lookup, a type T is considered to have the following base types:

- If T is object or dynamic, then T has no base type.
- If T is an enum_type, the base types of T are the class types System.Enum, System.ValueType, and object.
- If T is a struct_type, the base types of T are the class types System.ValueType and object. Note: A nullable_value_type is a struct_type (§8.3.1). end note
- If T is a class_type, the base types of T are the base classes of T, including the class type object.
- If T is an interface_type, the base types of T are the base interfaces of T and the class type object.
- If T is an array_type, the base types of T are the class types System.Array and object.
- If T is a delegate_type, the base types of T are the class types System.Delegate and object.

## 11.6 Function members

### 11.6.1 General

Function members are members that contain executable statements. Function members are always members of types and cannot be members of namespaces. C# defines the following categories of function members:

- Methods
