One interesting thing about the type `MD5` is that an instance of `MD5` needs to be “disposed of” after use. Many functions and methods use system resources (memory being the most common such resources) and they need to be cleaned up (e.g., while the program is running).

![](bbox=[0.13, 0.26, 0.22, 0.34])

.NET is a managed platform. .NET, in particular, handles the memory management on behalf of a running program. It periodically checks the memory usage and it cleans up any “no-longer used” memories. This is known as the “garbage collection”.

Although the C# programming language itself does not have such a concept, it does not have any support for the memory management (outside the “unsafe” use), and therefore C# programs can only run on the managed platforms like .NET.

The main program calls the `CryptoMD5.Hash()` static method three times with three different input strings. It just prints out the input strings and their hashed values (as text) for visual inspection, and it terminates.

Note the use of the `nameof()` operator. It returns the string representation of a name used in the program.

As stated, most names used in a program are “dummy” names. That is, changing the names (as long as they are done consistently across the entire program) does not affect the workings of the program. We could have just as well used a name `firstUserInput` instead of `input1`, for instance.

A minor problem occurs, however, when you change the names in most part of the program, but not in the string literals. For instance, in this sample code, we print out the text, `input1 = hello world.` The string `input1` is tied to the variable name in the program. But, the compiler cannot know this relationship. If one changes the variable name `input1` to `text1` across all its uses in a program, then the program will still work. The only place we can notice that something happened is the string output. In the output, we may still print out `input1 = hello world.` although we changed its variable name to `text1`.