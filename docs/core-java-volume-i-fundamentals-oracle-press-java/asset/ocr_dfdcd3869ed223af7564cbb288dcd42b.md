This call compiles and runs without error. Elsewhere, casting the result of `get` to a `String` will cause an error.

Generics offer a better solution: *type parameters*. The `ArrayList` class now has a type parameter that indicates the element type:

```
`var files = new ArrayList<String>();`
```

This makes your code easier to read. You can tell right away that this particular array list contains `String` objects.

# **NOTE:**

If you declare a variable with an explicit type instead of `var`, you can omit the type parameter in the constructor by using the “diamond” syntax:

```
`ArrayList<String> files = new ArrayList<>();`
```

The omitted type is inferred from the type of the variable.

Java 9 expands the use of the diamond syntax to situations where it was previously not accepted. For example, you can now use diamonds with anonymous subclasses:

```
    ArrayList<String> passwords = new ArrayList<>() // diamond OK
    in Java 9
        {
            public String get(int n) { return
    super.get(n).replaceAll(".", "*"); }
        };
```

The compiler can make good use of the type information too. No cast is required for calling `get`. The compiler knows that the return type is `String`, not `Object`: