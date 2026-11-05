# Chapter 55: Naming Conventions

This topic outlines some basic naming conventions used when writing in the C# language. Like all conventions, they are not enforced by the compiler, but will ensure readability between developers.

For comprehensive .NET framework design guidelines, see docs.microsoft.com/dotnet/standard/design-guidelines.

# Section 55.1: Capitalization conventions

The following terms describe different ways to case identifiers.

# Pascal Casing

The first letter in the identifier and the first letter of each subsequent concatenated word are capitalized. You can use Pascal case for identifiers of three or more characters. For example: BackColor

# Camel Casing

The first letter of an identifier is lowercase and the first letter of each subsequent concatenated word is capitalized. For example: backColor

# Uppercase

All letters in the identifier are capitalized. For example: IO

# Rules

When an identifier consists of multiple words, do not use separators, such as underscores ("_") or hyphens ("-"), between words. Instead, use casing to indicate the beginning of each word.

The following table summarizes the capitalization rules for identifiers and provides examples for the different types of identifiers:

| Identifier | Case | Example |
|---|---|---|
| Local variable | Camel | carName |
| Class | Pascal | AppDomain |
| Enumeration type | Pascal | ErrorLevel |
| Enumeration values | Pascal | FatalError |
| Event | Pascal | ValueChanged |
| Exception class | Pascal | WebException |
| Read-only static field | Pascal | RedValue |
| Interface | Pascal | IDisposable |
| Method | Pascal | ToString |
| Namespace | Pascal | System.Drawing |
| Parameter | Camel | typeName |
| Property | Pascal | BackColor |

More information can be found on MSDN.