
If a member is a method or event, or if it is a constant, field or property of either a delegate type (§15) or the type dynamic (§4.7), then the member is said to be invocable.

Member lookup considers not only the name of a member but also the number of type parameters the member has and whether the member is accessible. For the purposes of member lookup, generic methods and nested generic types have the number of type parameters indicated in their respective declarations and all other members have zero type parameters.

A member lookup of a name N with K type parameters in a type T is processed as follows:

- First, a set of accessible members named N is determined:
  - If T is a type parameter, then the set is the union of the sets of accessible members named N in each of the types specified as a primary constraint or secondary constraint (§10.1.5) for T, along with the set of accessible members named N in object.
  - Otherwise, the set consists of all accessible (§3.5) members named N in T, including inherited members and the accessible members named N in object. If T is a constructed type, the set of members is obtained by substituting type arguments as described in §10.3.2. Members that include an override modifier are excluded from the set.
- Next, if K is zero, all nested types whose declarations include type parameters are removed. If K is not zero, all members with a different number of type parameters are removed. Note that when K is zero, methods having type parameters are not removed, since the type inference process (§7.5.2) might be able to infer the type arguments.
- Next, if the member is invoked, all non-invocable members are removed from the set.
- Next, members that are hidden by other members are removed from the set. For every member S.M in the set, where S is the type in which the member M is declared, the following rules are applied:
  - If M is a constant, field, property, event, or enumeration member, then all members declared in a base type of S are removed from the set.
  - If M is a type declaration, then all non-types declared in a base type of S are removed from the set, and all type declarations with the same number of type parameters as M declared in a base type of S are removed from the set.
  - If M is a method, then all non-method members declared in a base type of S are removed from the set.
- Next, interface members that are hidden by class members are removed from the set. This step only has an effect if T is a type parameter and T has both an effective base class other than object and a non-empty effective interface set (§10.1.5). For every member S.M in the set, where S is the type in which the member M is declared, the following rules are applied if S is a class declaration other than object:
  - If M is a constant, field, property, event, enumeration member, or type declaration, then all members declared in an interface declaration are removed from the set.
  - If M is a method, then all non-method members declared in an interface declaration are removed from the set, and all methods with the same signature as M declared in an interface declaration are removed from the set.
- Finally, having removed hidden members, the result of the lookup is determined:
  - If the set consists of a single member that is not a method, then this member is the result of the lookup.
  - Otherwise, if the set contains only methods, then this group of methods is the result of the lookup.
  - Otherwise, the lookup is ambiguous, and a binding-time error occurs.

For member lookups in types other than type parameters and interfaces, and member lookups in interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effect of the lookup rules is simply that derived members hide base members with the same name or signature. Such single-inheritance lookups are never ambiguous. The ambiguities that can possibly arise from member lookups in multiple-inheritance interfaces are described in §13.2.5.

## 7.4.1 Base types

For purposes of member lookup, a type T is considered to have the following base types:

- If T is object, then T has no base type.
- If T is an enum-type, the base types of T are the class types System.Enum, System.ValueType, and object.
- If T is a struct-type, the base types of T are the class types System.ValueType and object.
- If T is a class-type, the base types of T are the base classes of T, including the class type object.
- If T is an interface-type, the base types of T are the base interfaces of T and the class type object.
- If T is an array-type, the base types of T are the class types System.Array and object.
- If T is a delegate-type, the base types of T are the class types System.Delegate and object.

## 7.5 Function members

Function members are members that contain executable statements. Function members are always members of types and cannot be members of namespaces. C# defines the following categories of function members:

- Methods
- Properties
- Events
- Indexers
- User-defined operators
- Instance constructors
- Static constructors
- Destructors

Except for destructors and static constructors (which cannot be invoked explicitly), the statements contained in function members are executed through function member invocations. The actual syntax for writing a function member invocation depends on the particular function member category.

The argument list (§7.5.1) of a function member invocation provides actual values or variable references for the parameters of the function member.

Invocations of generic methods may employ type inference to determine the set of type arguments to pass to the method. This process is described in §7.5.2.

Invocations of methods, indexers, operators and instance constructors employ overload resolution to determine which of a candidate set of function members to invoke. This process is described in §7.5.3.

Once a particular function member has been identified at binding-time, possibly through overload resolution, the actual run-time process of invoking the function member is described in §7.5.4.

| Construct | Example | Description |
|---|---|---|
|  | `T.E += value` | The add accessor of the event E in the class or struct T is invoked. A binding-time error occurs if E is not static. |
|  | `T.E -= value` | The remove accessor of the event E in the class or struct T is invoked. A binding-time error occurs if E is not static. |
|  | `e.E += value` | The add accessor of the event E in the class, struct, or interface given by the type of e is invoked with the instance expression e. A binding-time error occurs if E is static. |
|  | `e.E -= value` | The remove accessor of the event E in the class, struct, or interface given by the type of e is invoked with the instance expression e. A binding-time error occurs if E is static. |
| Indexer access | `e[x, y]` | Overload resolution is applied to select the best indexer in the class, struct, or interface given by the type of e. The **get** accessor of the indexer is invoked with the instance expression e and the argument list (x, y). A binding-time error occurs if the indexer is write-only. |
| Indexer access | `e[x, y] = value` | Overload resolution is applied to select the best indexer in the class, struct, or interface given by the type of e. The **set** accessor of the indexer is invoked with the instance expression e and the argument list (x, y, value). A binding-time error occurs if the indexer is read-only. |
| Operator invocation | `-x` | Overload resolution is applied to select the best unary operator in the class or struct given by the type of x. The selected operator is invoked with the argument list (x). |
| Operator invocation | `x + y` | Overload resolution is applied to select the best binary operator in the classes or structs given by the types of x and y. The selected operator is invoked with the argument list (x, y). |
| Instance constructor invocation | `new T(x, y)` | Overload resolution is applied to select the best instance constructor in the class or struct T. The instance constructor is invoked with the argument list (x, y). |

### 7.5.1 Argument lists

Every function member and delegate invocation includes an argument list which provides actual values or variable references for the parameters of the function member. The syntax for specifying the argument list of a function member invocation depends on the function member category:

- For instance constructors, methods, indexers and delegates, the arguments are specified as an *argument-list*, as described below. For indexers, when invoking the **set** accessor, the argument list additionally includes the expression specified as the right operand of the assignment operator.
- For properties, the argument list is empty when invoking the **get** accessor, and consists of the expression specified as the right operand of the assignment operator when invoking the **set** accessor.
- For events, the argument list consists of the expression specified as the right operand of the **+=** or **-=** operator.
