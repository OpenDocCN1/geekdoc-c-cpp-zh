same string. That way, if the same string literal containing thousands of characters was placed multiple times in the code, the resultant assembly would reflect the size of only one of them.

# ADVANCED TOPIC

# UTF-8 String Literals

Earlier in the chapter, we mentioned that characters in .NET are Unicode. Specifically, they are UTF-16 and requiring two bytes per character (or symbol). Therefore, the strings that are comprised of characters are all Unicode (UTF-8) as well.

Occasionally, especially working with extremely defined formats, C# 11 allows specification of UTF-8 string literals with a suffix following its closing quote—u8. However, the data type is not a .NET string (System.String). Rather the data type is a generic ReadOnlySpan<byte>. An example of such a string declaration and assignment, would be:

```
ReadOnlySpan<byte> rates = "€ rates"u8;
```

# String Interpolation

As discussed in Chapter 1, strings can support embedded expressions when using the string interpolation format.⁴The string interpolation syntax fixes a string literal with a dollar symbol and then embeds the expressions within curly brackets. Listing 2.15 is an example in which firstName and lastName are simple expressions that refer to variables.

LISTING 2.15: String Interpolation

```
Console.WriteLine($"Your full name is {firstName} {lastName}.");
```

+   4. Starting in C# 6.0