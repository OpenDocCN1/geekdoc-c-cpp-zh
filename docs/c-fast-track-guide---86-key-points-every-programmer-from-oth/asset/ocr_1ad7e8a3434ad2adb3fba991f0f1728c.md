In C#, inheritance allows you to create a new class based on an existing class. However, sometimes you want to prevent this—maybe for security, performance optimization, or to enforce architectural rules. That’s where the sealed keyword comes in.

Declaring a class as sealed tells the compiler: “This class is complete. Nobody can extend it.”

If someone tries to inherit from a sealed class, the compiler throws an error like:

"CS0509: 'Dog': cannot derive from sealed type 'Animal'"

You can use sealed alone, or also to seal methods in derived classes to prevent further overriding. For example:

```
public sealed override void SomeMethod() { }
```

This is especially common in framework code to prevent misuse or unintended behavior through inheritance.

[Supplement]

sealed is often used with classes like System.String, which is sealed to prevent breaking immutability.

If a class is sealed, it cannot also be abstract, since abstract requires inheritance.

Marking a class sealed can allow the JIT compiler to optimize calls (devirtualization), improving performance.