orderby, join, let, and additional from clauses.

> NOTE The variable query just has the LINQ query assigned to it. The query is not performed by this assignment, but rather as soon as the query is accessed using the foreach loop. This is discussed in more detail later in the section “Deferred Query Execution.”

# Extension Methods

The compiler converts the LINQ query to invoke method calls instead of the LINQ query. LINQ offers various extension methods for the IEnumerable<T> interface, so you can use the LINQ query across any collection that implements this interface. An extension method is defined as a static method whose first parameter defines the type it extends, and it is declared in a static class.

Extension methods make it possible to write a method to a class that doesn’t already offer the method at first. You can also add a method to any class that implements a specific interface, so multiple classes can make use of the same implementation.

For example, wouldn’t you like to have a Foo method with the String class? The String class is sealed, so it is not possible to inherit from this class; but you can create an extension method, as shown in the following code:

```
public static class StringExtension
{
    public static void Foo(this string s)
    {
        WriteLine($"Foo invoked for {s}");
    }
}
```

The Foo method extends the string class, as is defined with the first parameter. For differentiating extension methods from normal static methods, the extension method also requires the this keyword with the first parameter.

Indeed, it is now possible to use the Foo method with the string type:

```
string s ="Hello";
s.Foo();
```

The result shows Foo invoked for Hello in the console, because Hello is the string passed to the Foo method.

This might appear to be breaking object-oriented rules because a new method is defined for a type without changing the type or deriving from it. However, this is not the case. The extension method cannot access private members of the type it extends. Calling an extension method is just a new syntax for invoking a static method. With the string you can get the same result by calling the method Foo this way: