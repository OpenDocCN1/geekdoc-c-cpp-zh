# 16.5 Comparing strings

Line 41 tests string3 and string4 equal to illustrate that comparisons are indeed case sensitive. Here, static method Equals is used to compare the values of two strings. "Happy Birthday" does not equal "happy birthday", so the comparison fails, and the message "string3 does not equal string4" is output (line 47).

Lines 51–60 use method CompareTo to compare strings. The method returns 0 if the strings are equal, a negative value if the string that CompareTo is less than the string that was passed as an argument and a positive value if the string that invokes CompareTo is greater than the string that passed as an argument.

Notice that CompareTo considers string3 to be greater than string4. The only difference between these two strings is that string3 contains two uppercase letters in positions where string4 contains lowercase letters. The sorting rules vary by culture and sensitive.

# Determining Whether a String Begins or Ends with a Specified String

Figure 16.4 tests whether a string begins or ends with a given string. Method StartWith determines whether a string starts with the string passed to the method as an argument. Method EndWith determines whether a string ends with the string passed to the method as an argument.

```
// Fig. 16.4: StringStartEnd.cs
// Demonstrating StartWith and EndWith methods.
using System;
class StringStartEnd
{
    static void Main()
{
        string[] strings = {"started"
```

Fig. 16.4 | Demonstrating StartWith and EndWith methods. (Part 1 of 2).