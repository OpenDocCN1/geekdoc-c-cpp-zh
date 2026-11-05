# The example

```
string a = "hello, world";              // hello, world
string b = @"hello, world";             // hello, world
string c = "hello \t world";            // hello    world
string d = @"hello \t world";           // hello \t world
string e = "Joe said \"Hello\" to me";  // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me"; // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt"; // \\server\share\file.txt
string h = @"\\server\share\file.txt";   // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```

shows a variety of string literals. The last string literal, j, is a verbatim string literal that spans multiple lines. The characters between the quotation marks, including white space such as new line characters, are preserved verbatim.

> BRAD ABRAMS In the early days of the C# language design, we experimented with using the backtick (`) character. Personally, I really liked this choice: The backtick is in the quote family and is a grossly underused character. In fact, it was so underused that some international keyboards don't even include a key for it. We were lucky to have such a good, early international following for C#, which allowed us to fix this potential error very early in the design of the language.

Since a hexadecimal escape sequence can have a variable number of hex digits, the string literal "\x123" contains a single character with hex value 123. To create a string containing the character with hex value 12 followed by the character 3, one could write "\x00123" or "\x12" + "3" instead.

> JON SKEET Hexadecimal escape sequences aren't just rare—they're dangerous. While a string such as "\x9Tabbed" is reasonably clear, it's not nearly as obvious that "\x9Badly tabbed" actually begins with the Unicode character U+9BAD.

The type of a string-literal is string.

Each string literal does not necessarily result in a new string instance. When two or more string literals that are equivalent according to the string equality operator (§7.10.7) appear