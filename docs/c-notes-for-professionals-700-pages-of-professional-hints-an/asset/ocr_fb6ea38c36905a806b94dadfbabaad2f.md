# Chapter 16: String Escape Sequences

# Section 16.1: Escaping special symbols in string literals

# Backslash

```
// The filename will be c:\myfile.txt in both cases
string filename = "c:\\myfile.txt";
string filename = @"c:\myfile.txt";
```

The second example uses a verbatim string literal, which doesn't treat the backslash as an escape character.

# Quotes

```
string text = "\"Hello World!\", said the quick brown fox.";
string verbatimText = @"""Hello World!"", said the quick brown fox.";
```

Both variables will contain the same text.

> "Hello World!", said the quick brown fox.

# Newlines

Verbatim string literals can contain newlines:

```
string text = "Hello\r\nWorld!";
string verbatimText = @"Hello
World!";
```

Both variables will contain the same text.

# Section 16.2: Unicode character escape sequences

```
string sqrt = "\\u221A"; // √
string emoji = "\\U0001F601"; // ?
string text = "\\u0022Hello World\\u0022"; // "Hello World"
string variableWidth = "\\x22Hello World\\x22"; // "Hello World"
```

# Section 16.3: Escaping special symbols in character literals

# Apostrophes

```
char apostrophe = '\';
```

# Backslash

```
char oneBackslash = '\\';
```

# Section 16.4: Using escape sequences in identifiers

Escape sequences are not restricted to string and char literals.