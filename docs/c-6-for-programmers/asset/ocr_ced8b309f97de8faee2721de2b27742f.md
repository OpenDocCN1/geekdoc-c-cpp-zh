```
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32

Console.Write("Array intArray contains: ");
DisplayArray(intArray); // pass an int array argument
Console.Write("Array doubleArray contains: ");
DisplayArray(doubleArray); // pass a double array argument
Console.Write("Array charArray contains: ");
DisplayArray(charArray); // pass a char array argument
}

// output array of all types
private static void DisplayArray<T>(T[] inputArray)
{
    foreach (var element in inputArray)
    {
        Console.Write($"{element} ");
    }
    Console.WriteLine();
}
```

```
Array intArray contains: 1 2 3 4 5 6
Array doubleArray contains: 1.1 2.2 3.3 4.4 5.5 6.6 7.7
Array charArray contains: H E L L O
```

**Fig. 18.3** | Using a generic method to display arrays of different types. (Part 2 of 2.)

Line 23 begins method `DisplayArray`'s declaration, which is `static` so that `Main` can call `DisplayArray`. All generic method declarations have a type-parameter list delimited by angle brackets (`<T>` in this example) that follows the method's name. Each type-parameter list contains one or more type parameters, separated by commas (e.g., `Dictionary<K, V>`). A type parameter is an identifier that's used in place of actual type names. The type parameters can be used to declare the return type, the parameter types and local variable types in a generic method declaration; the type parameters act as placeholders for type arguments that represent the types of data that will be passed to the generic method.

The type-parameter names throughout the method declaration (if any) must match those declared in the type-parameter list. Also, a type parameter can be declared *only once* in the type-parameter list but can appear *more than once* in the method's parameter list. Type-parameter names need *not* be unique among separate generic methods.

> **Common Programming Error 18.1**
> 
> If you forget to include the type-parameter list when declaring a generic method, the compiler will not recognize the type-parameter names when they're encountered in the method. This results in compilation errors.

Method `DisplayArray`'s type-parameter list (line 23) declares type parameter `T` as the placeholder for the array-element type that `DisplayArray` will output. Note that `T` appears in the parameter list as the array-element type (line 23). This is the same location where the overloaded `DisplayArray` methods of Fig. 18.1 specified `int`, `double` or `char` as the element type. The remainder of `DisplayArray` is identical to the version presented in