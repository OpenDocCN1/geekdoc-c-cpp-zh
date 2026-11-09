# # Initializing Array Elements

In the previous section, I showed how to create an array object and then I showed how to initialize the elements of the array. C# offers syntax that allows you to do these two operations in one statement. For example:

```
```csharp
String[] names = new String[] { "Aidan", "Grant" };
```
```

The comma-separated set of tokens contained within the braces is called an *array initializer*. Each token can be an arbitrarily complex expression or, in the case of a multi-dimensional array, a nested array initializer. In the example above, I used just two simple **String** expressions.

If you are declaring a local variable in a method to refer to the initialized array, then you can use C#'s implicitly typed local variable (var) feature to simplify the code a little:

```
```csharp
// Using C#'s implicitly typed local variable feature:
var names = new String[] { "Aidan", "Grant" };
```
```

Here, the compiler is inferring that the **names** local variable should be of the **String[]** type since that is the type of the expression on the right of the assignment operator (=).

You can use C#'s implicitly typed array feature to have the compiler infer the type of the array's elements. Notice the line below has no type specified between **new** and **[]**:

```
```csharp
// Using C#'s implicitly typed local variable and implicitly typed array features:
var names = new[] { "Aidan", "Grant", null };
```
```

In the line above, the compiler examines the types of the expressions being used inside the array to initialize the array's elements, and the compiler chooses the closest base class that all the elements have in common to determine the type of the array. In this example, the compiler sees two **Strings** and **null**. Since **null** is implicitly castable to any reference type (including **String**), the compiler infers that it should be creating and initializing an array of **String** references.

If you had this code,

```
```csharp
// Using C#'s implicitly typed local variable & implicitly typed array features: (error)
var names = new[] { "Aidan", "Grant", 123 };
```
```

the compiler would issue the message "**error CS0826: No best type found for implicitly-typed array.**" This is because the base type in common between the two **Strings** and the **Int32** is **Object**, which would mean that the compiler would have to create an array of **Object** references and then box the **123** and have the last array element refer to a boxed **Int32** with a value of 123. The C# compiler team thinks that boxing array elements is too heavy-handed for the compiler to do for you implicitly, and that is why the compiler issues the error.