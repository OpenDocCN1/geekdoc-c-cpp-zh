For those readers who are unfamiliar with the == syntax of C-based languages, result == evaluates to true if result is equal to number, while result != number does the opposite. Both assignment and equality operators are discussed in the next chapter.

# More Fundamental Types

The fundamental types discussed so far are numeric types. C# includes some additional types as well: bool, char, and string.

# Boolean Type (bool)

Another C primitive is a Boolean or conditional type, bool, which represents true or false in conditional statements and expressions. Allowable values are the keywords true and false. The BCL name for bool is System.Boolean. For example, to compare two strings in a case-insensitive manner, you call the string.Compare() method and pass a bool literal true (see Listing 2.10).

LISTING 2.10: A Case-Insensitive Comparison of Two Strings

```
bool ignoreCase = true;
string option = "/help";
//...
int comparison = string.Compare(option, "/Help", ignoreCase);
bool isRequested = (comparison == 0);
// Displays: Help Requested: True
Console.WriteLine($"Help Requested: {isRequested}");
```

In this case, you case-insensitive comparison of the contents of the variable option with the literal text /Help and assign the result to comparison.

Although theoretically a single bit could hold the value of a Boolean, the size of bool is 1 byte.