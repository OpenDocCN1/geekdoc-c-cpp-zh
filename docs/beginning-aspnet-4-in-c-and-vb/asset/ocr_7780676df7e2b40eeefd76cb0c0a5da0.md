You can also explicitly set the capacity at any time, though an exception will be raised if you set it to a value less than the current length of the string or a value that exceeds the maximum capacity:

```
StringBuilder sb = new StringBuilder("Hello");
sb.Capacity = 100;
```

The following table lists the main StringBuilder methods.

| METHOD | PURPOSE |
|---|---|
| Append() | Appends a string to the current string. |
| AppendFormat() | Appends a string that has been worked out from a format specifier. |
| Insert() | Inserts a substring into the current string. |
| Remove() | Removes characters from the current string. |
| Replace() | Replaces all occurrences of a character with another character or a substring with another substring in the current string. |
| ToString() | Returns the current string cast to a System.String object (overridden from System.Object). |

Several overloads of many of these methods exist.

![](bbox=[0.12, 0.63, 0.82, 0.75])

There is no cast (either implicit or explicit) from StringBuilder to String. If you want to output the contents of a StringBuilder as a String, you must use the ToString() method.

Now that you have been introduced to the StringBuilder class and have learned some of the ways in which you can use it to increase performance, you should be aware that this class will not always give you the increased performance you are looking for. Basically, the StringBuilder class should be used when you are manipulating multiple strings. However, if you are just doing something as simple as concatenating two strings, you will find that System.String will be better-performing.

# Format Strings

So far, a large number of classes and structs have been written for the code samples presented in this book, and they have normally implemented a ToString() method in order to display the contents of a given variable. However, quite often users might want the contents of a variable to be displayed in different, often culture- and locale-dependent ways. The .NET base class, System.DateTime, provides the most obvious example of this. For example, you might want to display the same date as 10 June 2010, 10 Jun 2010, 6/10/10 (USA), 10/6/10 (UK), or 10.06.2010 (Germany).

Similarly, the Vector struct in Chapter 7, “Operators and Casts,” implements the Vector.ToString() method to display the vector in the format (4, 56, 8). There is, however, another very common way of writing vectors, in which this vector would appear as 4i + 56j + 8k. If you want the classes that you write to be user-friendly, they need to support the facility to display their string representations in any of the formats that users are likely to want to use. The .NET runtime defines a standard way in which this should be done: the IFormattable interface. Showing how to add this important feature to your classes and structs is the subject of this section.