
- Properties
- Events
- Indexers
- User-defined operators
- Instance constructors
- Static constructors
- Finalizers

Except for finalizers and static constructors (which cannot be invoked explicitly), the statements contained in function members are executed through function member invocations. The actual syntax for writing a function member invocation depends on the particular function member category.

The argument list (§11.6.2) of a function member invocation provides actual values or variable references for the parameters of the function member.

Invocations of generic methods may employ type inference to determine the set of type arguments to pass to the method. This process is described in §11.6.3.

Invocations of methods, indexers, operators, and instance constructors employ overload resolution to determine which of a candidate set of function members to invoke. This process is described in §11.6.4.

Once a particular function member has been identified at binding-time, possibly through overload resolution, the actual run-time process of invoking the function member is described in §11.6.6.

Note: The following table summarizes the processing that takes place in constructs involving the six categories of function members that can be explicitly invoked. In the table, e, x, y, and value indicate expressions classified as variables or values, T indicates an expression classified as a type, F is the simple name of a method, and P is the simple name of a property.

| Construct | Example | Description |
|---|---|---|
| Method invocation | F(x, y) | Overload resolution is applied to select the best method F in the containing class or struct. The method is invoked with the argument list (x, y). If the method is not static, the instance expression is this. |
| Method invocation | T.F(x, y) | Overload resolution is applied to select the best method F in the class or struct T. A binding-time error occurs if the method is not static. The method is invoked with the argument list (x, y). |
| Method invocation | e.F(x, y) | Overload resolution is applied to select the best method F in the class, struct, or interface given by the type of e. A binding-time error occurs if the method is static. The method is invoked with the instance expression e and the argument list (x, y). |
| Property access | P | The get accessor of the property P in the containing class or struct is invoked. A compile-time error occurs if P is write-only. If P is not static, the instance expression is this. |

|  | Syntax | Description |
|---|---|---|
|  | `P = value` | The set accessor of the property P in the containing class or struct is invoked with the argument list (value). A compile-time error occurs if P is read-only. If P is not static, the instance expression is this. |
|  | `T.P` | The get accessor of the property P in the class or struct T is invoked. A binding-time error occurs if P is not static or if P is write-only. |
|  | `T.P = value` | The set accessor of the property P in the class or struct T is invoked with the argument list (value). A binding-time error occurs if P is not static or if P is read-only. |
|  | `e.P` | The get accessor of the property P in the class, struct, or interface given by the type of e is invoked with the instance expression e. A binding-time error occurs if P is static or if P is write-only. |
|  | `e.P = value` | The set accessor of the property P in the class, struct, or interface given by the type of e is invoked with the instance expression e and the argument list (value). A binding-time error occurs if P is static or if P is read-only. |
| Event access | `E += value` | The add accessor of the event E in the containing class or struct is invoked. If E is not static, the instance expression is this. |
|  | `E -= value` | The remove accessor of the event E in the containing class or struct is invoked. If E is not static, the instance expression is this. |
|  | `T.E += value` | The add accessor of the event E in the class or struct T is invoked. A binding-time error occurs if E is not static. |
|  | `T.E -= value` | The remove accessor of the event E in the class or struct T is invoked. A binding-time error occurs if E is not static. |
|  | `e.E += value` | The add accessor of the event E in the class, struct, or interface given by the type of e is invoked with the instance expression e. A binding-time error occurs if E is static. |
|  | `e.E -= value` | The remove accessor of the event E in the class, struct, or interface given by the type of e is invoked with the instance expression e. A binding-time error occurs if E is static. |
| Indexer access | `e[x, y]` | Overload resolution is applied to select the best indexer in the class, struct, or interface given by the type of e. The get accessor of the indexer is invoked with the instance expression e and the argument list (x, y). A binding-time error occurs if the indexer is write-only. |
|  | `e[x, y] = value` | Overload resolution is applied to select the best indexer in the class, struct, or interface given by the type of e. The set accessor of the indexer is invoked with the instance expression e and the argument list (x, y, value). A binding-time error occurs if the indexer is read-only. |

| Invocation | Operator or syntax | Description |
|---|---|---|
| Operator invocation | `-x` | Overload resolution is applied to select the best unary operator in the class or struct given by the type of `x`. The selected operator is invoked with the argument list `(x)`. |
| Operator invocation | `x + y` | Overload resolution is applied to select the best binary operator in the classes or structs given by the types of `x` and `y`. The selected operator is invoked with the argument list `(x, y)`. |
| Instance constructor invocation | `new T(x, y)` | Overload resolution is applied to select the best instance constructor in the class or struct `T`. The instance constructor is invoked with the argument list `(x, y)`. |

## 11.6.2 Argument lists

### 11.6.2.1 General

Every function member and delegate invocation includes an argument list, which provides actual values or variable references for the parameters of the function member. The syntax for specifying the argument list of a function member invocation depends on the function member category:

- For instance constructors, methods, indexers and delegates, the arguments are specified as an *argument_list*, as described below. For indexers, when invoking the set accessor, the argument list additionally includes the expression specified as the right operand of the assignment operator.
  *Note:* This additional argument is not used for overload resolution, just during invocation of the set accessor, and *note*
- For properties, the argument list is empty when invoking the get accessor, and consists of the expression specified as the right operand of the assignment operator when invoking the set accessor.
- For events, the argument list consists of the expression specified as the right operand of the `+=` or `-=` operator.
- For user-defined operators, the argument list consists of the single operand of the unary operator or the two operands of the binary operator.

The arguments of properties (§14.7), events (§14.8), and user-defined operators (§14.10) are always passed as value parameters (§14.6.2.2). The arguments of indexers (§14.9) are always passed as value parameters (§14.6.2.2) or parameter arrays (§14.6.2.5). Reference and output parameters are not supported for these categories of function members.

The arguments of an instance constructor, method, indexer, or delegate invocation are specified as an *argument_list*:

```
argument_list
    : argument (',' argument)*
    ;

argument
    : argument_name? argument_value
    ;

argument_name
    : identifier ':'
    ;

argument_value
  : expression
  | 'ref' variable_reference
  | 'out' variable_reference
  ;
```

An argument_list consists of one or more arguments, separated by commas. Each argument consists of an optional argument_name followed by an argument_value. An argument with an argument_name is referred to as a named argument, whereas an argument without an argument_name is a positional argument. It is an error for a positional argument to appear after a named argument in an argument_list.

The argument_value can take one of the following forms:

- An expression, indicating that the argument is passed as a value parameter (§14.6.2.2).
- The keyword ref followed by a variable_reference (§9.5), indicating that the argument is passed as a reference parameter (§14.6.2.3). A variable shall be definitely assigned (§9.4) before it can be passed as a reference parameter.
- The keyword out followed by a variable_reference (§9.5), indicating that the argument is passed as an output parameter (§14.6.2.4). A variable is considered definitely assigned (§9.4) following a function member invocation in which the variable is passed as an output parameter.

The form determines the parameter-passing mode of the argument: value, reference, or output, respectively.

Passing a volatile field (§14.5.4) as a reference parameter or output parameter causes a warning, since the field may not be treated as volatile by the invoked method.

### 11.6.2.2 Corresponding parameters

For each argument in an argument list there has to be a corresponding parameter in the function member or delegate being invoked.

The parameter list used in the following is determined as follows:

- For virtual methods and indexers defined in classes, the parameter list is picked from the first declaration or override of the function member found when starting with the static type of the receiver, and searching through its base classes.
- For partial methods, the parameter list of the defining partial method declaration is used.
- For all other function members and delegates there is only a single parameter list, which is the one used.

The position of an argument or parameter is defined as the number of arguments or parameters preceding it in the argument list or parameter list.

The corresponding parameters for function member arguments are established as follows:

- Arguments in the argument_list of instance constructors, methods, indexers and delegates:
  - A positional argument where a parameter occurs at the same position in the parameter list corresponds to that parameter, unless the parameter is a parameter array and the function member is invoked in its expanded form.
