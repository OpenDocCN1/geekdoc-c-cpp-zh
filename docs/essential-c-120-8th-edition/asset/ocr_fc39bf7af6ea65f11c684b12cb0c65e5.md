# Chapter 8: Interfaces

Table 8.1: Default Interface Refactoring Features

| C# 8.0-Introduced Construct | Sample Code |
| --- | --- |
| abstract Modifier | The abstract modifier is only allowable on members without an implementation, the keyword has no effect as such members by default. All abstract members are automatically virtual and explicitly declaring abstract as virtual triggers a compile error. | ```csharp
public interface IPerson {
    // virtual is not allowed on members
    // without implementation
    // virtual / abstract string FirstName
    set { get; set; }
    string LastName { get; set; }
    // abstract is not allowed on members
    // with implementation
    // virtual / abstract string Name => GetName();
    private string GetName() => $"{{FirstName} {LastName}";
}
``` ` |

| Partial Interfaces and Partial Methods | It is now possible to provide partial implementations of a method with no outgoing data (returns or ref/out data) and optionally the fully implemented method in a second definition of the same interface. Partial methods are always private—they do not support access modifiers. | ```csharp
public interface IThing {
    string Value { get; protected set; }
    void SetValue(string value);
    AssertValueIsValid(value);
    Value = value;
}
public interface IThing {
    void AssertValueIsValid(string value);
    // Throw if value is invalid.
    switch(value) {
        case null:
            throw new ArgumentNullException(nameof(value));
        case "":
            throw new ArgumentException("Empty string is invalid", nameof(value));
        case string _ =
            if (string.IsNullOrOrWhiteSpace(value)) {
                throw new ArgumentException("Can't be whitespace", nameof(value));
            }reak;
    }
}
``` `

There are a couple of points to highlight in Table 8.1. First, it is important to note that automatically implemented property support is not available because instance fields (which back an automatically implemented property) are not supported. This is