# Sealed Classes

Designing a class correctly so that others can extend it via derivation can be a tricky task that requires testing with examples to verify the derivation will work successfully. Listing 7.8 shows how to avoid unexpected derivation scenarios and problems by marking classes as sealed.

Listing 7.8: Preventing Derivation with Sealed Classes

```
public sealed class CommandLineParser
{
    //...
}

// ERROR: Sealed classes cannot be derived from
public sealed class DerivedCommandLineParser
{
    //...
}
```

Sealed classes include the sealed modifier, so they cannot be derived from. The string type is an an example of a type that uses the sealed modifier to prevent derivation.

# Overriding the Base Class

All members of a base class are inherited in the derived class, except for constructors and destructors. However, sometimes the base class does not have the optimal implementation of a particular member. Consider the Name property on PdaItem, for example. The implementation is probably acceptable when inherited by the Appointment class. For the Contact class, however, the Name property should return the FirstName and LastName properties combined. Similarly, When Name is assigned, it should be split across FirstName and LastName. In other words, the base class property declaration is appropriate for the derived class, but the implementation is not always valid. A mechanism is needed for overriding the base class implementation with a custom implementation in the derived class.