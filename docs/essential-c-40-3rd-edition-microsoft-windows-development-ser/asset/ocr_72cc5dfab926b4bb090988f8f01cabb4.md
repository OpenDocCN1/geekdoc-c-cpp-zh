NOTE

Although nothing in the language requires it, a good guideline is for value types to be immutable: Once you have instantiated a value type, you should not be able to modify the same instance. In scenarios where modification is desirable, you should create a new instance. Listing 8.1 supplies a Move() method that doesn’t modify the instance of Angle, but instead returns an entirely new instance.

# Initializing structs

In addition to properties and fields, structs may contain methods and constructors. However, default (parameterless) constructors are not allowed. Sometimes (for instance, when instantiating an array) a value type’s constructor will not be called because all array memory is initialized with zeroes instead. To avoid the inconsistency of default constructors being called only sometimes, C# prevents explicit definition of default constructors altogether. Because the compiler’s implementation of an instance field assignment at declaration time is to place the assignment into the type’s constructor, C# prevents instance field assignment at declaration time as well (see Listing 8.2).

# LISTING 8.2: Initializing a struct Field within a Declaration, Resulting in an Error

```
struct Angle
{
    // ...

    // ERROR: Fields cannot be initialized at declaration time
    // int _Hours = 42;
    // ...
}
```

This does not eliminate the need to initialize the field. In fact, just as with classes, the compiler will issue a warning on struct fields that remain uninitialized after instantiation if they also cannot be accessed from outside the assembly (because they are decorated with internal or private modifiers, for example).

Fortunately, C# supports constructors with parameters and they come with an interesting initialization requirement. They must initialize all fields within the struct. Failure to do so causes a compile error. The constructor in Listing 8.3 that initializes the property rather than the field, for example, produces a compile error.