files are in UTF-8 by default. UTF-8 encoding system is backwards compatible with ASCII. (meaning: If a file only contain characters in ASCII, then encoding the file using UTF-8 results the same byte sequence as using ASCII as encoding scheme.)

+   5. With UTF-16, every char is encoded into at least 2 bytes, and commonly used characters in Unicode are exactly 2 bytes. For Asian languages containing lots of Chinese characters, such as Chinese & Japanese, UTF-16 creates smaller file size.
+   6. There's also UTF-32, which always uses 4 bytes per character. It creates larger file size, but is simpler to parse. Currently, UTF-32 is not being used much.

# 2.2 Token

# Concept

+   1. Token is the smallest individual unit that is made up of valid characters in C#.
+   2. Tokens are valid words that are the basic building blocks of C# Programming.

# Explanation

+   3. Token is formed and defined using the C# grammar.
+   4. Tokens are generally any unit that is not whitespace or a comment.
+   5. Every C# program is basically collection of tokens.
+   6. There are 5 kinds of tokens namely, identifiers, keywords, literals, operators, and punctuators.
+   7. White space and comments are not tokens, though they act as separators or delimters for tokens.

![](bbox=[0.12, 0.78, 0.92, 0.92])

# Example

```
class Tokens
{
    static void Main()
    {

```