Implicitly typed array creation expressions can be combined with anonymous object initializers (§11.7.15.7) to create anonymously typed data structures.

*Example:*

```
var contacts = new[]
{
    new
    {
        Name = "Chris Smith",
        PhoneNumbers = new[] { "206-555-0101", "425-882-8080" }
    },
    new
    {
        Name = "Bob Harris",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```

*end example*

# 11.7.15.6 Delegate creation expressions

A *delegate_creation_expression* is used to obtain an instance of a *delegate_type*.

```
delegate_creation_expression
    ; 'new' delegate_type '(' expression ')'
    ;
```

The argument of a delegate creation expression shall be a method group, an anonymous function, or a value of either the compile-time type *dynamic* or a *delegate_type*. If the argument is a method group, it identifies the method and, for an instance method, the object for which to create a delegate. If the argument is an anonymous function it directly defines the parameters and method body of the delegate target. If the argument is a value it identifies a delegate instance of which to create a copy.

If the *expression* has the compile-time type *dynamic*, the *delegate_creation_expression* is dynamically bound (§11.7.15.6), and the rules below are applied at run-time using the run-time type of the *expression*. Otherwise, the rules are applied at compile-time.

The binding-time processing of a *delegate_creation_expression* of the form new D(E), where D is a *delegate_type* and E is an *expression*, consists of the following steps:

+   - If E is a method group, the delegate creation expression is processed in the same way as a method group conversion (§10.8) from E to D.
+   - If E is an anonymous function, the delegate creation expression is processed in the same way as an anonymous function conversion (§10.7) from E to D.
+   - If E is a value, E shall be compatible (§19.2) with D, and the result is a reference to a newly created delegate that has a single-entry invocation list that invokes E.

The run-time processing of a *delegate_creation_expression* of the form new D(E), where D is a *delegate_type* and E is an *expression*, consists of the following steps:

+   - If E is a method group, the delegate creation expression is evaluated as a method group conversion (§10.8) from E to D.
+   - If E is an anonymous function, the delegate creation is evaluated as an anonymous function conversion from E to D (§10.7).