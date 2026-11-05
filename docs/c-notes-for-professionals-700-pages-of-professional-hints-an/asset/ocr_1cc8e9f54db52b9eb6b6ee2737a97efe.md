# Chapter 14: String Manipulation

# Section 14.1: Replacing a string within a string

Using the System.String.Replace method, you can replace part of a string with another string.

```
string s = "Hello World";
s = s.Replace("World", "Universe"); // s = "Hello Universe"
```

All the occurrences of the search string are replaced:

```
string s = "Hello World";
s = s.Replace("l", "L"); // s = "Hello WorlD"
```

String.Replace can also be used to remove part of a string, by specifying an empty string as the replacement value:

```
string s = "Hello World";
s = s.Replace("ell", String.Empty); // s = "Ho World"
```

# Section 14.2: Finding a string within a string

Using the System.String.Contains you can find out if a particular string exists within a string. The method returns a boolean, true if the string exists else false.

```
string s = "Hello World";
bool stringExists = s.Contains("ello"); //stringExists =true as the string contains the substring
```

Using the System.String.IndexOf method, you can locate the starting position of a substring within an existing string.

Note the returned position is zero-based, a value of -1 is returned if the substring is not found.

```
string s = "Hello World";
int location = s.IndexOf("ello"); // location = 1
```

To find the first location from the end of a string, use the System.String.LastIndexOf method:

```
string s = "Hello World";
int location = s.LastIndexOf("l"); // location = 9
```

# Section 14.3: Removing (Trimming) white-space from a string

The System.String.Trim method can be used to remove all leading and trailing white-space characters from a string:

```
string s = "      String with spaces at both ends      ";
s = s.Trim(); // s = "String with spaces at both ends"
```

In addition:

+   - To remove white-space only from the beginning of a string use: System.String.TrimStart
+   - To remove white-space only from the end of a string use: System.String.TrimEnd