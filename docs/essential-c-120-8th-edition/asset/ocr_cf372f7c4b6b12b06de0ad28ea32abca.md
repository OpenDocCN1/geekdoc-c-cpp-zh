# Non-Nullable Reference Type Properties with Constructors

+   * The backing field is declared as nullable to avoid the compiler warning that the field is uninitialized.
* The getter returns the field with a null-forgiveness operator—declaring that it is not null thanks to the setter validation.

For a non-nullable property, it is seemingly nonsensical to declare the backing field as null. This is necessary, however, since the compiler is oblivious to non-nullable field/property assignments outside the constructor. Fortunately, this is a case where you, as the programmer, are justified in using the null-forgiveness operator when returning the field because of the not-null check in the setter that ensures the field is null.

# Read-Only Automatically Implemented Reference Type Properties

As pointed out earlier in this section, non-nullable automatically implemented reference-type properties need to be read-only to avoid invalid null assignments. However, you still need to validate any parameters that may be assigned during instantiation, as shown in Listing 6.37.

> Listing 6.37: Validation of Non-Null Reference Type Automatically Implemented Properties

```
public class Employee {
    public Employee(string name) {
        Name = name ?? throw new ArgumentNullException(nameof(name));
    }
    public string Name { get; }
}
```

One could debate whether a private setter should be allowed on non-nullable automatically implemented reference-type properties. While possible, the more appropriate question to ask is your class could mistakenly assign null to the property. If you don't encapsulate the field with validation in a setter, can you be sure you won't mistakenly assign a null value? While the compiler will verify your intent during instantiation, it is questionable that the developer will always remember