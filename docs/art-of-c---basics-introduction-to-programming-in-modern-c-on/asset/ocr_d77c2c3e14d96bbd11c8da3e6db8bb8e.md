The following keyword references are mostly adopted from the C# language reference website.

# ## Abstract Modifier (abstract)

The `abstract` modifier indicates that the thing being modified has a missing or incomplete implementation. The abstract modifier can be used with classes/records, methods, properties, indexers, and events. Use the `abstract` modifier in a class/record declaration to indicate that a class/record is intended only to be a base class of other classes/records, not instantiated on its own.

Members marked as abstract must be implemented by non-abstract classes that derive from the abstract class.

Abstract classes have the following features:

+   - An abstract class cannot be instantiated.
- An abstract class may contain abstract methods and accessors.
- It is not possible to modify an abstract class with the `sealed` modifier because the two modifiers have opposite meanings. The `sealed` modifier prevents a class from being inherited and the `abstract` modifier requires a class to be inherited.
- A non-abstract class derived from an abstract class must include actual implementations of all inherited abstract methods and accessors.

Use the `abstract` modifier in a method or property declaration to indicate that the method or property does not contain implementation.

Abstract methods have the following features:

+   - An abstract method is implicitly a virtual method.
- Abstract method declarations are only permitted in abstract classes.
- Because an abstract method declaration provides no actual implementation,