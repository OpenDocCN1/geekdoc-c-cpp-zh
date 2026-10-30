# Working with Strings

Visual Basic provides many methods for working with text strings. Strings in Visual Studio are immutable, which means that once a string is created, it cannot be changed. Although many programs in this text seem to modify a string, actually a new string is created and the old string is discarded.

For string handling, you can use any of the many methods of the String class. You can also use the StringBuilder class, which is more efficient if you are building or modifying strings, since the string can be changed in memory. In other words, a StringBuilder is mutable (changeable) and a String is immutable.

Here is a partial list of the methods in the String class. For shared methods, you don’t need to specify a String instance; for nonshared methods, you must attach the method to the String instance. For example:

Shared Method

```
If Compare(AString, BString) > 0 Then
    ...
```

Nonshared Method

```
If MyString.EndsWith("ed") Then
    ...
```

| Method | Returns |
|---|---|
| Compare(AString, BString) (Shared) | Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| Compare(AString, BString, IgnoreCaseBoolean) (Shared) | Case insensitive if IgnoreCaseBoolean is True.
Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| Compare(AString, AStartInteger, BString, BStartInteger, LengthInteger) (Shared) | Compare substrings; start position indicates beginning character to compare for a length of LengthInteger.
Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| Compare(AString, AStartInteger, BString, BStartInteger, LengthInteger, IgnoreCaseBoolean) (Shared) | Case insensitive if IgnoreCaseBoolean is True.
Compare substrings; start position indicates beginning character to compare for a length of LengthInteger.
Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |