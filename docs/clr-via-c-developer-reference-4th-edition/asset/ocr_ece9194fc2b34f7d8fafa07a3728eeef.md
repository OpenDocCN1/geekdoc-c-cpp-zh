# Chars, Strings, and Working with Text

+   In this chapter:
Characters. ..................................................................... 317
The System.String Type ................................................................... 320
Constructing a String Efficiently. ........................................ 336
Obtaining a String Representation of an Object: ToString ................. 339
Parsing a String to Obtain an Object: Parse. ................................ 348
Encodings: Converting Between Characters and Bytes. ............... 350
Secure Strings ................................................................................... 357

In this chapter, I'll explain the mechanics of working with individual characters and strings in the Microsoft .NET Framework. I'll start by talking about the System.Char structure and the various ways that you can manipulate a character. I'll go over the more useful System.String class, which allows you to work with immutable strings. (Once created, strings cannot be modified in any way.) After examining strings, I'll show you how to perform various operations efficiently to build a string dynamically via the System.Text.StringBuilder class. With the string basics out of the way, I'll describe how to format objects into strings and how to persist or transmit strings using various encodings. Finally, I'll discuss the System.Security.SecureString class, which can be used to protect sensitive data such as passwords and credit card information.

# Characters

In the .NET Framework, characters are always represented in 16-bit Unicode code values, easing the development of global applications. A character is represented with an instance of the System.Char structure (a value type). The System.Char type is pretty simple. It offers two read-only fields: MinValue, defined as '\0', and MaxValue, defined as '\ffff'.

Given an instance of a Char, you can call the static GetUnicodeCategory method, which returns a value of the System.Globalization.UnicodeCategory enumerated type. This value indicates whether the character is a control character, a currency symbol, a lowercase letter, an uppercase letter, a punctuation character, a math symbol, or another character (as defined by the Unicode standard).