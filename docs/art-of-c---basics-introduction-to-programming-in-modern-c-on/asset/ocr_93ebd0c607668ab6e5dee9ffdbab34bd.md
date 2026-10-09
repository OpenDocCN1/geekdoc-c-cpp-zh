Although it is beyond the scope of this book, this kind of pattern can be used for "dependency injection" (or, DI for short), if needed. The readers are encouraged to look up on this topic, if interested.

![](bbox=[0.14, 0.15, 0.18, 0.19])

As stated, software development requires a lot of different skills and knowledge beyond mere "programming".

The `Client` encapsulate the functionalities of the "CLI client".

The `System.CommandLine` library more or less requires the program to start as follows:

```
await rootCommand.InvokeAsync(args);
```

We are using the async version of the `Invoke()` method here. As stated, the generated `Main()` method of this program will be an async version. The `rootCommand` is a variable for type `System.CommandLine.RootCommand`.

The client supports a number of different "sub-commands" below the root command.