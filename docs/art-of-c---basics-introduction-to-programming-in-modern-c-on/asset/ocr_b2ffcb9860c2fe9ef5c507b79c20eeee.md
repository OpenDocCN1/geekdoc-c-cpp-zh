![](bbox=[0.12, 0.12, 0.15, 0.15])

In the C convention, the first element of the command line argument array, argv, is the name of the program. C#, however, does not follow that convention. The args array contains only the command line arguments explicitly provided by the user. If none is provided, then it is an "empty array".

An "array" is a built-in type in C#. It is a collection type, so to speak. A variable of an array type stores a sequence of (zero or more) values of a given "element type" (e.g. string in this example) in a consecutive space in memory.

The values of its elements, which are variables themselves, can be accessed using the "index notation". For example, one can access the third element of an array arr as arr[2], assuming that arr has more than 2 elements. Note that the index is "zero-based". That is, the first element of arr is arr[0].

An array is a "reference type", as we will discuss further throughout this book.

One thing to note is that an array has a "readonly property" called Length. One can read the length of an array variable (i.e., the number of elements in the array) using the "dot notation". For example,

```
```
var length = args.Length;
Console.WriteLine($"The arr's length is {length}.");
```
```

The variable name is initialized with a value "you" (a string literal) in line 1 of the example code. The if statement next checks if the predefined array args has any elements (as made available to the given program by the .NET runtime or the operating system), and if so, then it updates the value of the string variable name.

Note that even though we use an "implicit variable declaration" using the keyword var, the type of name is string because it is initialized with a string value. We could have more explicitly declared name as a string variable as follows: