
rule simply permits access to the static members and nested types of E where a compile-time error would otherwise have occurred. [Example:

```
struct Color
{
    public static readonly Color white = new Color(...);
    public static readonly Color Black = new Color(...);
    public Color Complement() {...}
}
class A
{
    public Color Color;            // Field Color of type Color
    void F() {
        Color = Color.Black;       // Refs Color.Black static member
        Color = Color.Complement(); // Invokes Complement() on Color field
    }
    static void G() {
        Color c = Color.White;     // Refs Color.White static member
    }
}
```

Within the A class, those occurrences of the Color identifier that reference the Color type are underlined, and those that reference the Color field are not underlined. end example]

## 12.7.6 Invocation expressions

### 12.7.6.1 General

An invocation-expression is used to invoke a method.

```
invocation-expression:
    primary-expression ( argument-list_opt )
```

An invocation-expression is dynamically bound (§12.3.3) if at least one of the following holds:

- The primary-expression has compile-time type dynamic.
- At least one argument of the optional argument-list has compile-time type dynamic.

In this case, the compiler classifies the invocation-expression as a value of type dynamic. The rules below to determine the meaning of the invocation-expression are then applied at run-time, using the run-time type instead of the compile-time type of those of the primary-expression and arguments that have the compile-time type dynamic. If the primary-expression does not have compile-time type dynamic, then the method invocation undergoes a limited compile-time check as described in §12.6.5.

The primary-expression of an invocation-expression shall be a method group or a value of a delegate-type. If the primary-expression is a method group, the invocation-expression is a method invocation (§12.7.6.2). If the primary-expression is a value of a delegate-type, the invocation-expression is a delegate invocation (§12.7.6.4). If the primary-expression is neither a method group nor a value of a delegate-type, a binding-time error occurs.

The optional argument-list (§12.6.2) provides values or variable references for the parameters of the method.

The result of evaluating an invocation-expression is classified as follows:

- If the invocation-expression invokes a method or delegate that returns void, the result is nothing. An expression that is classified as nothing is permitted only in the context of a statement-expression (§13.7) or as the body of a lambda-expression (§12.16). Otherwise a binding-time error occurs.
- Otherwise, the result is a value, with an associated type of the return type of the method or delegate. If the invocation is of an instance method, and the receiver is of a class type T, the associated type is picked from the first declaration or override of the method found when starting with T and searching through its base classes.

### 12.7.6.2 Method invocations

For a method invocation, the *primary-expression* of the *invocation-expression* shall be a method group. The method group identifies the one method to invoke or the set of overloaded methods from which to choose a specific method to invoke. In the latter case, determination of the specific method to invoke is based on the context provided by the types of the arguments in the *argument-list*.

The binding-time processing of a method invocation of the form M(A), where M is a method group (possibly including a *type-argument-list*), and A is an optional *argument-list*, consists of the following steps:

- The set of candidate methods for the method invocation is constructed. For each method F associated with the method group M:
  - If F is non-generic, F is a candidate when:
    - M has no type argument list, and
    - F is applicable with respect to A (§12.6.4.2).
  - If F is generic and M has no type argument list, F is a candidate when:
    - Type inference (§12.6.3) succeeds, inferring a list of type arguments for the call, and
    - Once the inferred type arguments are substituted for the corresponding method type parameters, all constructed types in the parameter list of F satisfy their constraints (§9.4.5), and the parameter list of F is applicable with respect to A (§12.6.4.2).
  - If F is generic and M includes a type argument list, F is a candidate when:
    - F has the same number of method type parameters as were supplied in the type argument list, and
    - Once the type arguments are substituted for the corresponding method type parameters, all constructed types in the parameter list of F satisfy their constraints (§9.4.5), and the parameter list of F is applicable with respect to A (§12.6.4.2).
- The set of candidate methods is reduced to contain only methods from the most derived types: For each method C.F in the set, where C is the type in which the method F is declared, all methods declared in a base type of C are removed from the set. Furthermore, if C is a class type other than object, all methods declared in an interface type are removed from the set. [Note: This latter rule only has an effect when the method group was the result of a member lookup on a type parameter having an effective base class other than object and a non-empty effective interface set. end note]
- If the resulting set of candidate methods is empty, then further processing along the following steps are abandoned, and instead an attempt is made to process the invocation as an extension method invocation (§12.7.6.3). If this fails, then no applicable methods exist, and a binding-time error occurs.
- The best method of the set of candidate methods is identified using the overload resolution rules of §12.6.4. If a single best method cannot be identified, the method invocation is ambiguous, and a binding-time error occurs. When performing overload resolution, the parameters of a generic method are considered after substituting the type arguments (supplied or inferred) for the corresponding method type parameters.
- Final validation of the chosen best method is performed:
  - The method is validated in the context of the method group: If the best method is a static method, the method group shall have resulted from a *simple-name* or a *member-access* through a type. If the best method is an instance method, the method group shall have resulted from a *simple-name*, a member-access through a variable or value, or a base-access. If neither of these requirements is true, a binding-time error occurs.
  - If the best method is a generic method, the type arguments (supplied or inferred) are checked against the constraints (§9.4.5) declared on the generic method. If any type argument does not satisfy the corresponding constraint(s) on the type parameter, a binding-time error occurs.

Once a method has been selected and validated at binding-time by the above steps, the actual run-time invocation is processed according to the rules of function member invocation described in §12.6.6.

> [Note: The intuitive effect of the resolution rules described above is as follows: To locate the particular method invoked by a method invocation, start with the type indicated by the method invocation and proceed up the inheritance chain until at least one applicable, accessible, non-override method declaration is found. Then perform type inference and overload resolution on the set of applicable, accessible, non-override methods declared in that type and invoke the method thus selected. If no method was found, try instead to process the invocation as an extension-method invocation. end note]

### 12.7.6.3 Extension method invocations

In a method invocation (§12.6.6.2) of one of the forms

```
expr . identifier ( )
expr . identifier ( args )
expr . identifier < typeargs > ( )
expr . identifier < typeargs > ( args )
```

if the normal processing of the invocation finds no applicable methods, an attempt is made to process the construct as an extension method invocation. If expr or any of the args has compile-time type dynamic, extension methods will not apply.

The objective is to find the best type-name C, so that the corresponding static method invocation can take place:

```
C . identifier ( expr )
C . identifier ( expr , args )
C . identifier < typeargs > ( expr )
C . identifier < typeargs > ( expr , args )
```

An extension method C₁ . Mⱼ is eligible if:

- C₁ is a non-generic, non-nested class
- The name of Mⱼ is identifier
- Mⱼ is accessible and applicable when applied to the arguments as a static method as shown above
- An implicit identity, reference or boxing conversion exists from expr to the type of the first parameter of Mⱼ.

The search for C proceeds as follows:

- Starting with the closest enclosing namespace declaration, continuing with each enclosing namespace declaration, and ending with the containing compilation unit, successive attempts are made to find a candidate set of extension methods:
  - If the given namespace or compilation unit directly contains non-generic type declarations C₁ with eligible extension methods Mⱼ, then the set of those extension methods is the candidate set.
