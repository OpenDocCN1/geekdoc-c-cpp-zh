
non-empty effective interface set (§15.2.5). For every member S.M in the set, where S is the type in which the member M is declared, the following rules are applied if S is a class declaration other than object:

- If M is a constant, field, property, event, enumeration member, or type declaration, then all members declared in an interface declaration are removed from the set.
- If M is a method, then all non-method members declared in an interface declaration are removed from the set, and all methods with the same signature as M declared in an interface declaration are removed from the set.

Finally, having removed hidden members, the result of the lookup is determined:

- If the set consists of a single member that is not a method, then this member is the result of the lookup.
- Otherwise, if the set contains only methods, then this group of methods is the result of the lookup.
- Otherwise, the lookup is ambiguous, and a binding-time error occurs.

For member lookups in types other than type parameters and interfaces, and member lookups in interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effect of the lookup rules is simply that derived members hide base members with the same name or signature. Such single-inheritance lookups are never ambiguous. The ambiguities that can possibly arise from member lookups in multiple-inheritance interfaces are described in §18.4.6. [Note: This phase only accounts for one kind of ambiguity. If the member lookup results in a method group, further uses of method group may fail due to ambiguity, for example as described in §12.6.4.1 and §12.6.6.2. end note]

## 12.5.2 Base types

For purposes of member lookup, a type T is considered to have the following base types:

- If T is object or dynamic, then T has no base type.
- If T is an enum-type, the base types of T are the class types System.Enum, System.ValueType, and object.
- If T is a struct-type, the base types of T are the class types System.ValueType and object. [Note: A nullable-value-type is a struct-type (§9.3.1). end note]
- If T is a class-type, the base types of T are the base classes of T, including the class type object.
- If T is an interface-type, the base types of T are the base interfaces of T and the class type object.
- If T is an array-type, the base types of T are the class types System.Array and object.
- If T is a delegate-type, the base types of T are the class types System.Delegate and object.

## 12.6 Function members

### 12.6.1 General

Function members are members that contain executable statements. Function members are always members of types and cannot be members of namespaces. C# defines the following categories of function members:

- Methods
- Properties
- Events
- Indexers
- User-defined operators
- Instance constructors
- Static constructors
- Finalizers

Except for finalizers and static constructors (which cannot be invoked explicitly), the statements contained in function members are executed through function member invocations. The actual syntax for writing a function member invocation depends on the particular function member category.

The argument list (§12.6.2) of a function member invocation provides actual values or variable references for the parameters of the function member.

Invocations of generic methods may employ type inference to determine the set of type arguments to pass to the method. This process is described in §12.6.3.

Invocations of methods, indexers, operators, and instance constructors employ overload resolution to determine which of a candidate set of function members to invoke. This process is described in §12.6.4.

Once a particular function member has been identified at binding-time, possibly through overload resolution, the actual run-time process of invoking the function member is described in §12.6.6.

[Note: The following table summarizes the processing that takes place in constructs involving the six categories of function members that can be explicitly invoked. In the table, e, x, y, and value indicate expressions classified as variables or values, T indicates an expression classified as a type, F is the simple name of a method, and P is the simple name of a property.]

| Construct | Example | Description |
|---|---|---|
| Method invocation | F(x, y) | Overload resolution is applied to select the best method F in the containing class or struct. The method is invoked with the argument list (x, y). If the method is not static, the instance expression is this. |
| Method invocation | T.F(x, y) | Overload resolution is applied to select the best method F in the class or struct T. A binding-time error occurs if the method is not static. The method is invoked with the argument list (x, y). |
| Method invocation | e.F(x, y) | Overload resolution is applied to select the best method F in the class, struct, or interface given by the type of e. A binding-time error occurs if the method is static. The method is invoked with the instance expression e and the argument list (x, y). |
| Property access | P | The get accessor of the property P in the containing class or struct is invoked. A compile-time error occurs if P is write-only. If P is not static, the instance expression is this. |
| Property access | P = value | The set accessor of the property P in the containing class or struct is invoked with the argument list (value). A compile-time error occurs if P is read-only. If P is not static, the instance expression is this. |
| Property access | T.P | The get accessor of the property P in the class or struct T is invoked. A compile-time error occurs if P is not static or if P is write-only. |
| Property access | T.P = value | The set accessor of the property P in the class or struct T is invoked with the argument list (value). A compile-time error occurs if P is not static or if P is read-only. |

end note]

### 12.6.2 Argument lists

### 12.6.2.1 General

Every function member and delegate invocation includes an argument list, which provides actual values or variable references for the parameters of the function member. The syntax for specifying the argument list of a function member invocation depends on the function member category:

- For instance constructors, methods, indexers and delegates, the arguments are specified as an *argument-list*, as described below. For indexers, when invoking the *set* accessor, the argument list additionally includes the expression specified as the right operand of the assignment operator. [Note: This additional argument is not used for overload resolution, just during invocation of the set accessor. end note]
- For properties, the argument list is empty when invoking the *get* accessor, and consists of the expression specified as the right operand of the assignment operator when invoking the *set* accessor.
- For events, the argument list consists of the expression specified as the right operand of the *+=* or *-=* operator.
- For user-defined operators, the argument list consists of the single operand of the unary operator or the two operands of the binary operator.

The arguments of properties (§15.7), events (§15.8), and user-defined operators (§15.10) are always passed as value parameters (§15.6.2.2). The arguments of indexers (§15.9) are always passed as value parameters (§15.6.2.2) or parameter arrays (§15.6.2.5). Reference and output parameters are not supported for these categories of function members.

The arguments of an instance constructor, method, indexer, or delegate invocation are specified as an *argument-list*:

```
argument-list:
    argument
    argument-list , argument

argument:
    argument-nameopt argument-value

argument-name:
    identifier :

argument-value:
    expression
    ref variable-reference
    out variable-reference
```

An *argument-list* consists of one or more *arguments*, separated by commas. Each argument consists of an optional *argument-name* followed by an *argument-value*. An argument with an *argument-name* is referred to as a *named argument*, whereas an argument without an *argument-name* is a *positional argument*. It is an error for a positional argument to appear after a named argument in an *argument-list*.

The *argument-value* can take one of the following forms:

- An *expression*, indicating that the argument is passed as a value parameter (§15.6.2.2).
- The keyword *ref* followed by a *variable-reference* (§10.5), indicating that the argument is passed as a reference parameter (§15.6.2.3). A variable shall be definitely assigned (§10.4) before it can be passed as a reference parameter.
