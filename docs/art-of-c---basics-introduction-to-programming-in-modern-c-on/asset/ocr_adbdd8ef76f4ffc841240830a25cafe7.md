This feature is officially called the "static using". The author prefers to call it the `using static` declaration because that is how he uses it when he programs. The terminologies are important, but only to the extent that they help clarify the underlying concepts and/or as long as they facilitate easier communications.

Throughout this book, we will just use the terms that make sense (although they may not be the "official" terms). At the end of the day, it is the program that speaks, not the names that we attach to the parts of the program.

Now, as for the static method `WriteLine()` of the `Console` class defined in the `System` namespace, it takes one argument of the `string` type (in this example), and it prints out the given argument(s) to the terminal. "Hello World!!!" (with a pair of double quotes) is a "string literal". It represents a specific (constant) value of the `type` `string`.

That’s all there is to it. If you build and run the program, then it prints out the given `string` (Hello World!!! in this case, without the double quotes) to the console, and since there is nothing more to do, the program terminates.

One thing to note is that many statements in C# end with a semicolon (;). It is required in many types of statements. (Also, a "block" can terminate a statement instead of the semicolon.)

At the risk of stating the obvious, the semicolon is required at the end of a statement in a C# program. It is not the end of a line where we need to use a semicolon. (Just to reiterate, some types of statements in C# require (explicit or implicit) "blocks" and those types of statements do not end with semicolons.)