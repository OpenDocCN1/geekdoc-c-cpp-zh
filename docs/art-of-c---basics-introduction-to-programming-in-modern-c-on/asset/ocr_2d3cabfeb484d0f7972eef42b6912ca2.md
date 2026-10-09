member methods and properties of a type. Namely, `public`, `internal`, `protected`, `protected internal`, `private protected`, and `private`.

C# provides a number of operators for checking types and casting objects between different types. We explored the some basics of the `is` and `as` operators. Although we did not cover in this lesson, C# also has an operator, `typeof`, to get the `System.Type` instance for a given type name. The `object.GetType()` method, available in all objects, can also be used to get the type of an object.

We also learned basic usages of the functional style methods (e.g., `List<T>.ForEach()`) and the lamdba expressions. The `List<T>.ForEach()` method, as well as many of the LINQ extension methods, takes a delegate as one of its arguments.