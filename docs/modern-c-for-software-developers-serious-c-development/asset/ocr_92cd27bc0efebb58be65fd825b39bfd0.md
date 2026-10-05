```
ss.str(std::string());
```

or:

```
ss.clear()
```

# erase

Erases the portion of a string value that begins at the character position pos and spans len characters (or until the end of the string, if either the content is too short or len is string::npos):

```
string& erase (size_t pos = 0, size_t len = npos);
```

returns a pointer to the erased string.

# find

The string::find(string) function returns the index of first occurrence of a substring substr in a given string, if there is an occurrence of the substring in the string. If the given substring is not present in this string, find() returns -1. The syntax is:

```
str.find(substr)
```

We can also specify the search starting position in this string and the search interval for the substring.

```
str.find(substr, start, n)
```

start is optional. And if start is provided, n is optional.