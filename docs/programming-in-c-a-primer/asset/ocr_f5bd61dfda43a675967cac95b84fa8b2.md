This statement converts the number 123 to a string ‘123’ and then assigns the string value to the string variable numStr.

# 10.2.6 Verbatim Strings

Strings can also be created using what are known as verbatim strings. Verbatim strings are those that start with the @ symbol. This symbol tells the compiler that the string should be used verbatim even if it includes escape characters.

```
string s1 = @ "\EBG\Csharp\string.cs";
```

In order to obtain the same output without using the symbol @, the input string should be written as follows:

```
string s1 = "\\EBG\\Csharp\\string.cs";
```

We may also use the escape characters such as n and t in @ - quoted strings. They will not be processed during output and appear in the text as such.

Note that if an ordinary string contains an embedded n, the string that follows n will be displayed on the next line when the string is processed for output.

# 10.3 STRING METHODS

String objects are immutable, meaning that we cannot modify the characters contained in them. However, since the string is an alias for the predefined System.String class in the Common Language Runtime (CLR), there are many built-in operations available that work with strings. All operations produce a modified version of the string rather than modifying the string on which the method is called.

Table 10.1 lists various methods that could be used for various operations such as comparison, appending, inserting, conversion, copying, indexing, joining, splitting, padding, trimming, removing, replacing and searching. We have already used some methods like Concat and Copy in the previous section.

# Table 10.1 String class methods

| METHOD | OPERATION |
|---|---|
| Compare () | Compares two strings |
| CompareTo () | Compares the current instance with another instance |
| ConCat () | Concatenates two or more strings |
| Copy() | Creates a new string by copying another |
| CopyTo () | Copies a specified number of characters to an array of Unicode characters |
| EndsWith () | Determines whether a substring exists at the end of the string |
| Equals() | Determines if two strings are equal |
| IndexOf () | Returns the position of the first occurrence of a substring |
| Insert () | Returns a new string with a substring inserted at a specified location |
| Join () | Joins an array of strings together |
| LastIndexOf () | Returns the position of the last occurrence of a substring |
| PadLeft () | Left-aligns the strings in a field |
| PadRight () | Right-aligns the string in a field |
| Remove () | Deletes characters from the string |