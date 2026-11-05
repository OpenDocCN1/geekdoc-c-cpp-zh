
> **ERIC LIPPERT** A downside of this implementation technique (and a disadvantage shared by many implementations of many languages that have similar closure semantics) is that two different anonymous functions in the same method that are closed over two different local variables cause the lifetimes of both variables to be extended to match the lifetime of the longest-lived delegate.

Suppose you have two local variables, expensive and cheap, and two delegates, one closed over each variable:

```
D longlived = () => cheap;
D shortlived = () => expensive;
```

The lifetime of expensive is at least as long as the lifetime of the object referred to by longlived, even though expensive is not actually used by longlived. A more sophisticated implementation would partition closed-over variables into separate compiler-generated classes and avoid this problem.

## 6.6 Method Group Conversions

An implicit conversion (§6.1) exists from a method group (§7.1) to a compatible delegate type. Given a delegate type D and an expression E that is classified as a method group, an implicit conversion exists from E to D if E contains at least one method that is applicable in its normal form (§7.5.3.1) to an argument list constructed by use of the parameter types and modifiers of D, as described in the following.

The compile-time application of a conversion from a method group E to a delegate type D is described in the following. Note that the existence of an implicit conversion from E to D does not guarantee that the compile-time application of the conversion will succeed without error.

> **VLADIMIR RESHETNIKOV** In particular, it is possible that overload resolution will pick the best function member containing a delegate type in its signature, while an implicit conversion from a method group, provided as the corresponding argument, to that delegate type will result in a compile-time error. This situation may occur, for instance, because overload resolution cannot find the single best method in that group. Even if the best method is found, constraints on its type parameters might be violated, or the method might not be compatible with the delegate type, or it might be an instance method referenced in a static context.

- A single method M is selected corresponding to a method invocation (§7.6.5.1) of the form E(A), with the following modifications:
  - The argument list A is a list of expressions, each classified as a variable and with the type and modifier (ref or out) of the corresponding parameter in the formal-parameter-list of D.
  - The candidate methods considered are only those methods that are applicable in their normal form (§7.5.3.1), not those applicable only in their expanded form.
- If the algorithm of §7.6.5.1 produces an error, then a compile-time error occurs. Otherwise, the algorithm produces a single best method M having the same number of parameters as D and the conversion is considered to exist.
- The selected method M must be compatible (§15.2) with the delegate type D; otherwise, a compile-time error occurs.
- If the selected method M is an instance method, the instance expression associated with E determines the target object of the delegate.
- If the selected method M is an extension method, which is denoted by means of a member access on an instance expression, that instance expression determines the target object of the delegate.
- The result of the conversion is a value of type D—namely, a newly created delegate that refers to the selected method and target object.

Note that this process can lead to the creation of a delegate to an extension method, if the algorithm of §7.6.5.1 fails to find an instance method but succeeds in processing the invocation of E(A) as an extension method invocation (§7.6.5.2). A delegate thus created captures the extension method as well as its first argument.

> > VLADIMIR RESHETNIKOV If the first parameter of an extension method converted to a delegate type is of a value type or type parameter not known to be a reference type (§10.1.5), a compile-time error occurs.
> >
> > If an instance method declared in System.Nullable<T> is converted to a delegate type, a compile-time error occurs as well.

The following example demonstrates method group conversions:

```
delegate string D1(object o);
delegate object D2(string s);
delegate object D3();
delegate string D4(object o, params object[] a);
```

```
delegate string D5(int i);
class Test
{
    static string F(object o) {...}
    static void G() {
        D1 d1 = F;    // Okay
        D2 d2 = F;    // Okay
        D3 d3 = F;    // Error: not applicable
        D4 d4 = F;    // Error: not applicable in normal form
        D5 d5 = F;    // Error: applicable but not compatible
    }
}
```

The assignment to d1 implicitly converts the method group F to a value of type D1.

The assignment to d2 shows how it is possible to create a delegate to a method that has less derived (contravariant) parameter types and a more derived (covariant) return type.

The assignment to d3 shows how no conversion exists if the method is not applicable.

The assignment to d4 shows how the method must be applicable in its normal form.

The assignment to d5 shows how parameter and return types of the delegate and method are allowed to differ only for reference types.

As with all other implicit and explicit conversions, the cast operator can be used to explicitly perform a method group conversion. Thus the example

```
object obj = new EventHandler(myDialog.OkClick);
```

could instead be written

```
object obj = (EventHandler)myDialog.OkClick;
```

Method groups may influence overload resolution, and participate in type inference. See §7.5 for further details.

The runtime evaluation of a method group conversion proceeds as follows:

- If the method selected at compile time is an instance method, or if it is an extension method that is accessed as an instance method, the target object of the delegate is determined from the instance expression associated with it:
  - The instance expression is evaluated. If this evaluation causes an exception, no further steps are executed.
  - If the instance expression is of a reference-type, the value computed by the instance expression becomes the target object. If the selected method is an instance method and the target object is null, a System.NullReferenceException is thrown and no further steps are executed.
  - If the instance expression is of a value-type, a boxing operation (§4.3.1) is performed to convert the value to an object, and this object becomes the target object.
- Otherwise, the selected method is part of a static method call, and the target object of the delegate is null.
- A new instance of the delegate type D is allocated. If there is not enough memory available to allocate the new instance, a System.OutOfMemoryException is thrown and no further steps are executed.

> > **JON SKEET** The fact that the specification explicitly states that a new instance is created at this point prevents a potential optimization. The Microsoft C# compiler is able to cache delegates created via anonymous functions if they don't capture any variables (including this). The same sort of caching would be feasible for delegates created via any method group conversion that selects a static method—but the specification prohibits it.

- The new delegate instance is initialized with a reference to the method that was determined at compile time and a reference to the target object computed above.

## 7. Expressions

An expression is a sequence of operators and operands. This chapter defines the syntax, order of evaluation of operands and operators, and meaning of expressions.

### 7.1 Expression Classifications

An expression is classified as one of the following:

- A value. Every value has an associated type.
- A variable. Every variable has an associated type—namely, the declared type of the variable.

> > **VLADIMIR RESHETNIKOV** Types of local variables and lambda expression parameters can be inferred by the compiler in many cases, and do not always need to be explicitly specified in declarations.

- A namespace. An expression with this classification can only appear as the left-hand side of a *member-access* (§7.6.4). In any other context, an expression classified as a namespace causes a compile-time error.
- A type. An expression with this classification can only appear as the left-hand side of a *member-access* (§7.6.4), or as an operand for the as operator (§7.10.11), the is operator (§7.10.10), or the typeof operator (§7.6.11). In any other context, an expression classified as a type causes a compile-time error.

> > **VLADIMIR RESHETNIKOV** If an expression is classified as a type and appears as the left-hand side of a *member-access*, it never denotes an array or pointer type. If the expression denotes a type parameter, it always leads to a compile-time error later.
