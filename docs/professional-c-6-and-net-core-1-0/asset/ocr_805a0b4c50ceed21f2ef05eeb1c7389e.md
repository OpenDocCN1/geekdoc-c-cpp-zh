is usually pointless; instead, you should have the application gracefully exit.

+   - `EndOfStreamException`—The usual cause of an `EndOfStreamException` is an attempt to read past the end of a file. A *stream* represents a flow of data between data sources. Streams are covered in detail in Chapter 25, “Networking.”

+   - `OverflowException`—An example when this occurs is if you attempt to cast an `int` containing a value of `-40` to a `uint` in a `checked` context.

The other exception classes shown in Figure 14.1 are not discussed here. They are just shown to illustrate the hierarchy of exception classes.

The class hierarchy for exceptions is somewhat unusual in that most of these classes do not add any functionality to their respective base classes. However, in the case of exception handling, the common reason for adding inherited classes is to indicate more specific error conditions. Often, it isn’t necessary to override methods or add any new ones (although it is not uncommon to add extra properties that carry extra information about the error condition). For example, you might have a base `ArgumentException` class intended for method calls whereby inappropriate values are passed in, and an `ArgumentNullException` class derived from it, which is intended to handle a `null` argument if passed.

# Catching Exceptions

Given that the .NET Framework includes a selection of predefined base class exception objects, this section describes how you use them in your code to trap error conditions. In dealing with possible error conditions in C# code, you typically divide the relevant part of your program into blocks of three different types:

+   - `try` blocks encapsulate the code that forms part of the normal operation of your program and that might encounter some serious error conditions.

+   - `catch` blocks encapsulate the code dealing with the various error conditions that your code might have encountered by working through any of the code in the accompanying `try` block. This block could also be used for logging errors.

+   - `finally` blocks encapsulate the code that cleans up any resources or takes any other action that you normally want handled at the end of a `try` or `catch` block. It is important to understand that the `finally` block is executed whether an exception is thrown. Because the purpose of the `finally` block is to contain cleanup code that should always be executed, the compiler flags an error if you place a `return` statement inside a `finally` block. An example of using the `finally` block is closing any connections that were opened in the `try` block. Understand that the `finally` block is completely optional. If your