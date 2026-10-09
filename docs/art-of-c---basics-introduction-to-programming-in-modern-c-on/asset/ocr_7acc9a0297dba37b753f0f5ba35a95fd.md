expression is `false`.

For instance, in the following example,

```
```
if (false) {
    Console.WriteLine("I am false");
} else {
    Console.WriteLine("I am true");
}
```
```

It will print out I am true, from the else block, ignoring the statement from the `if` block. In fact, the compiler knows this (because the Boolean expression happens to be a compile time constant `false`), and it will issue a warning about the "unreachable code" since the `if` branch (in this example) will never be executed.

All operating systems, or runtimes, allow passing some kind of arguments to a starting program. These are generally known as the "command line arguments". The C programming language started using a convention where the command line arguments are passed in to the "`main()` function" as the function's arguments.

The exact function signature is not important, but the C's `main()` function accepts the command line arguments (say, multiple arguments separated by spaces) as a list of values, or an "array". Most of the C's descendant languages follow this convention, with minor variations. C# follows more or less the same convention. The command line arguments are passed in as an argument to the `Main()` method (of the "main class"). We will discuss this in more detail in the next lesson.

For the example program using the top level statements, the command line arguments are available as an implicitly defined variable named `args`. The variable `args` is of type `string[]`, that is, an "array of strings".