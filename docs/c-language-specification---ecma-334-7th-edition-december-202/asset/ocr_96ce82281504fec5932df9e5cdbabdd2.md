```
{
    Name = "Bob Harris",
    PhoneNumbers = new[] { "650-555-0199" }
};
```

*end example*

# 12.8.16.6 Delegate creation expressions

A *delegate_creation_expression* is used to obtain an instance of a *delegate_type*.

```
delegate_creation_expression
  : 'new' delegate_type '(' expression ')'
  ;
```

The argument of a delegate creation expression shall be a method group, an anonymous function, or a value of either the compile-time type *dynamic* or a *delegate_type*. If the argument is a method group, it identifies the method and, for an instance method, the object for which to create a delegate. If the argument is an anonymous function it directly defines the parameters and method body of the delegate target. If the argument is a value it identifies a delegate instance of which to create a copy.

If the *expression* has the compile-time type *dynamic*, the *delegate_creation_expression* is dynamically bound (§12.8.16.6), and the rules below are applied at run-time using the run-time type of the *expression*. Otherwise, the rules are applied at compile-time.

The binding-time processing of a *delegate_creation_expression* of the form new D(E), where D is a *delegate_type* and E is an *expression*, consists of the following steps:

+   - If E is a method group, the delegate creation expression is processed in the same way as a method group conversion (§10.8) from E to D.
+   - If E is an anonymous function, the delegate creation expression is processed in the same way as an anonymous function conversion (§10.7) from E to D.
+   - If E is a value, E shall be compatible (§20.2) with D, and the result is a reference to a newly created delegate with a single-entry invocation list that invokes E.

The run-time processing of a *delegate_creation_expression* of the form new D(E), where D is a *delegate_type* and E is an *expression*, consists of the following steps:

+   - If E is a method group, the delegate creation expression is evaluated as a method group conversion (§10.8) from E to D.
+   - If E is an anonymous function, the delegate creation is evaluated as an anonymous function conversion from E to D (§10.7).
+   - If E is a value of a *delegate_type*:
+     - E is evaluated. If this evaluation causes an exception, no further steps are executed.
+     - If the value of E is null, a System.NullReferenceException is thrown and no further steps are executed.
+     - A new instance of the delegate type D is allocated. If there is not enough memory available to allocate the new instance, a System.OutOfMemoryException is thrown and no further steps are executed.
+     - The new delegate instance is initialized with a single-entry invocation list that invokes E.