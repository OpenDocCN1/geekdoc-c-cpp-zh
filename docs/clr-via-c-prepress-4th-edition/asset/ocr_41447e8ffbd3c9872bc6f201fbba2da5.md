metadata, and embed the values in the call for you automatically.

# Implicitly Typed Local Variables

C# supports the ability to infer the type of a method’s local variable from the type of expression that is used to initialize it. Here is some sample code demonstrating the use of this feature:

```
```csharp
private static void ImplicitlyTypedLocalVariables() {
    var name = "Jeff";
    ShowVariableType(name);        // Displays: System.String

    // var n = null;            // Error: Cannot assign <null> to an implicitly-typed local variable
    var x = (String)null;    // OK, but not much value
    ShowVariableType(x);        // Displays: System.String

    var numbers = new Int32[] { 1, 2, 3, 4 };
    ShowVariableType(numbers); // Displays: System.Int32[]

    // Less typing for complex types
    var collection = new Dictionary<String, Single>() { { "Grant", 4.0f } };

    // Displays: System.Collections.Generic.Dictionary`2[System.String,System.Single]
    ShowVariableType(collection);

    foreach (var item in collection) {
        // Displays: System.Collections.Generic.KeyValuePair`2[System.String,System.Single]
        ShowVariableType(item);
    }
}

private static void ShowVariableType<T>(T t) {
    Console.WriteLine(typeof(T));
}
```
```

The first line of code inside the `ImplicitlyTypedLocalVariables` method is introducing a new local variable using the C# `var` token. To determine the type of the name variable, the compiler looks at the type of the expression on the right side of the assignment operator (`=`). Since "Jeff" is a string, the compiler infers that name’s type must be String. To prove that the compiler is inferring the type correctly, I wrote the `ShowVariableType` method. This generic method infers the type of its argument, and then it shows the type that it inferred on the console. I added what `ShowVariableType` displayed as comments inside the `ImplicitlyTypedLocalVariables` method for easy reading.

The second assignment (commented out) inside the `ImplicitlyTypedLocalVariables` method would produce a compiler error ("error CS0815: Cannot assign <null> to an implicitly-typed local variable") because null is implicitly castable to any reference type or nullable value type; therefore, the compiler cannot infer a distinct type for it. However, on the third assignment, I show that it is possible to initialize an implicitly typed local variable with null if you