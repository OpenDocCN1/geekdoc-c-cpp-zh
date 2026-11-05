do with an array:

```
string s = "hello";
char c = s[1]; //Returns 'e'
```

Notice that the return type is char, unlike the Substring method which returns a string type.

You can also use the indexer to iterate through the characters of the string:

```
string s = "hello";
foreach (char c in s)
    Console.WriteLine(c);
/*********** This will print each character on a new line:
h
e
l
l
o
***********/
```

# Section 11.15: Joining an array of strings into a new one

```
var parts = new[] { "Foo", "Bar", "Fizz", "Buzz"};
var joined = string.Join(", ", parts);

//joined = "Foo, Bar, Fizz, Buzz"
```

# Section 11.16: Replacing a string within a string

Using the System.String.Replace method, you can replace part of a string with another string.

```
string s = "Hello World";
s = s.Replace("World", "Universe"); // s = "Hello Universe"
```

All the occurrences of the search string are replaced.

This method can also be used to remove part of a string, using the String.Empty field:

```
string s = "Hello World";
s = s.Replace("ell", String.Empty); // s = "Ho World"
```

# Section 11.17: Changing the case of characters within a String

The System.String class supports a number of methods to convert between uppercase and lowercase characters in a string.

+   - System.String.ToLowerInvariant is used to return a String object converted to lowercase.
+   - System.String.ToUpperInvariant is used to return a String object converted to uppercase.

Note: The reason to use the invariant versions of these methods is to prevent producing unexpected culture-specific letters. This is explained here in detail.

Example:

```
string s = "My String";
```