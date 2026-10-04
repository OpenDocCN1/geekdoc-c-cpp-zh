Like delegates, an interface with generic type parameters can have its type parameters be variant or covariant. Here is an example of an interface with a covariant generic type parameter.

```
public interface IEnumerator<out T> : IEnumerator {
    Boolean MoveNext();
    T Current { get; }
}
```

Because T is covariant, it is possible to have an IEnumerable of of the following code compile and run successfully.

```
// Int32 Count(IEnumerable<object> collection) { ... }
```

```
// The call below passes an IEnumerable<String> to Count
Int32 c = Count(new[] { "Grant" });
```

> **Important** Sometimes developers ask why they must explicitly put in or out on generic type parameters. They think the compiler should be able to examine the delegate or interface declaration and automatically detect what generic type parameters can be variant and covariant. Although it is true that the compiler could detect this automatically, the C# team believes that you are declaring a contract that you should be explicit about what you want to do. For example, it would be bad if the compiler determined that a generic type parameter could be contravariant and then, in the future, a member to an interface that had the type parameter used in an output position. When you compile, the compiler would determine that the type parameter should be invariant, but all code sites that reference the other members might now produce errors if they used the fact that the type parameter had been contravariant.
For reason, the compiler forces you to be explicit when declaring a generic type parameter. If you attempt to use this type parameter in a context that doesn't match how you declared it, the compiler issues an error letting you know that you are attempting to break the contract. If you then decide to break the contract by adding in or out on generic type parameters, you should expect to have some of the code sites using the old contract.

# Generic Methods

When you define a generic class, struct, or interface, methods defined in these types can refer to a type parameter specified by the type. A type parameter can be used as a method's parameter, a method's return type, or as a local variable inside the method. However, the CLR also supports the ability for a method to specify its very own type parameters. And these type parameters can also be used for parameters, return types, or local variables.