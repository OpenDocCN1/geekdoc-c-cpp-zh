```
sb.Capacity = 100;
```

The following table lists the main StringBuilder methods.

| Method | Description |
|---|---|
| Append | Appends a string to the current string. |
| AppendFormat | Appends a string that has been formatted from a format specifier. |
| Insert | Inserts a substring into the current string. |
| Remove | Removes characters from the current string. |
| Replace | Replaces all occurrences of a character with another character or a substring with another substring in the current string. |
| ToString | Returns the current string cast to a System.String object (overridden from System.Object). |

Several overloads of many of these methods exist.

> **NOTE** AppendFormat is actually the method that is ultimately called when you call Console.WriteLine, which is responsible for determining what all the format expressions like {0:D} should be replaced with. This method is examined in the next section.

There is no cast (either implicit or explicit) from StringBuilder to String. If you want to output the contents of a StringBuilder as a String, you must use the ToString method.

Now that you have been introduced to the StringBuilder class and have learned some of the ways in which you can use it to increase performance, be aware that this class does not always deliver the increased performance you are seeking. Basically, you should use the StringBuilder class when you are manipulating multiple strings. However, if you are just doing something as simple as concatenating two strings, you will find that System.String performs better.

# String Formats

In previous chapters you’ve seen passing variables to strings with the $ prefix. This chapter examines what’s behind this new feature of C# 6 and covers all the other functionality offered by format strings.

# String Interpolation

C# 6 introduces string interpolation by using the $ prefix for strings. The following example creates the string s2 using the $ prefix. This prefix allows having placeholders in curly brackets to reference results from code. {s1} is a placeholder in the string, where the compiler puts into the value of variable s1 into the string s2 (code file