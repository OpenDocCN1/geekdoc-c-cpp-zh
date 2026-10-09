universe. ☺

We use certain encoding schemes to represent Unicode characters on computer (e.g., for storage and transmission). Two of the most popular encoding methods for Unicode are UTF-8 and UTF-16. The English alphabets, and most of the Latin alphabets, require only 1 byte. And, UTF-8 is the most popular, and fairly efficient, encoding method when transmitting or storing the data in Unicode characters.

Without going into too much detail, C# internally uses one or two values of the `char` type (of 2 bytes) to store a single Unicode character, using UTF-16. In many cases, a single `char` in C# corresponds to a single Unicode character (e.g., from the "Basic Multilingual Plane" (BMP)). In some cases, however, a single `char` is not enough for certain Unicode characters (e.g., a character that requires an additional 2 bytes from a "Surrogate Plane").

In this sample code, we use the function `char.ConvertFromUtf32()` to get a certain smiley character (\u1F642). This static method from `System.Char` in .NET returns a `string`, not a `char`, because some Unicode characters cannot be represented by a single `char`.

Normally, any Unicode character from the BMP (that requires only 2 bytes) can be represented by using the "\u" character escape syntax in C#.

For example, `\u0041` represents a character `'A'`. (A hexadecimal number `0x41` is 65 in base 10. Note that we use *four* hexadecimal digits for two bytes in this notation regardless of the integer value of the char.)

For any other characters, we will need to rely on some API methods provided by .NET. Note that the `string? ConvertFromUtf32(int)` method takes an `int` argument, not a `char`.

In this particular example, the integer `0x1F642` does not fit into a `char` type. An explicit casting to `char` would have been a compile time error.