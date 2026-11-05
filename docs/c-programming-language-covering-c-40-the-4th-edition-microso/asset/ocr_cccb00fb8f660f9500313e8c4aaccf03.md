The last expression causes a compile-time error because neither int nor string is implicitly convertible to the other, so there is no best common type. An explicitly typed array creation expression must be used in this case—for example, specifying the type to be object[]. Alternatively, one of the elements can be cast to a common base type, which would then become the inferred element type.

Implicitly typed array creation expressions can be combined with anonymous object initializers (§7.6.10.6) to create anonymously typed data structures. For example:

```
var contacts = new[] {
    new {
        Name = "Chris Smith",
        PhoneNumbers = new[] { "206-555-0101", "425-888-8888" }
    },
    new {
        Name = "Bob Harris",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```

# 7.6.10.5 Delegate Creation Expressions

A delegate-creation-expression is used to create a new instance of a delegate-type.

```
delegate-creation-expression:
    new delegate-type ( expression )
```

The argument of a delegate creation expression must be a method group, an anonymous function, or a value of either the compile-time type dynamic or a delegate-type. If the argument is a method group, it identifies the method and, for an instance method, the object for which to create a delegate. If the argument is an anonymous function, it directly defines the parameters and method body of the delegate target. If the argument is a value, it identifies a delegate instance of which to create a copy.

If the expression has the compile-time type dynamic, the delegate-creation-expression is dynamically bound (§7.2.2), and the rules below are applied at runtime using the runtime type of the expression. Otherwise, the rules are applied at compile time.

The binding-time processing of a delegate-creation-expression of the form new D(E), where D is a delegate-type and E is an expression, consists of the following steps:

+   - If E is a method group, the delegate creation expression is processed in the same way as a method group conversion (§6.6) from E to D.
+   - If E is an anonymous function, the delegate creation expression is processed in the same way as an anonymous function conversion (§6.5) from E to D.