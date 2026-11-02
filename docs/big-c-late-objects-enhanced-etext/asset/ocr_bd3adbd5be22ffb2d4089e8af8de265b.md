# 8.2.2 Reading Characters

Instead of reading an entire word, you can read one character at a time by calling the get function:

```
```
char ch;
in_file.get(ch);
```
```

The get function returns the "not failed" condition. The following loop processes all characters in a file:

```
```
while (in_file.get(ch))
{
    Process the character ch.
}
```
```

The get function reads white space characters. This is useful if you need to process characters such as spaces, tabs, or newlines. On the other hand, if you are not interested in white space, use the >> operator instead.

```
```
in_file >> ch; // ch is set to the next non-white space character
```
```

If you read a character and you regretted it, you can unget it, so that the next input operation can read it again. However, you can unget only the last character. This is called one-character lookahead. You get a chance to look at the next character in the input stream, and you can make a decision whether you want to consume it or put it back.

You can get individual characters from a stream and unget the last one.

A typical situation for lookahead is to look for numbers:

```
```
char ch;
in_file.get(ch);
if (isdigit(ch))
{
    in_file.unget(); // Put the digit back so that it is part of the number
    int n;
    in_file >> n; // Read integer starting with ch
}
```
```

The isdigit function is one of several useful functions that categorize characters—see Table 1. All return true or false as to whether the argument passes the test. You must include the <cctype> header to use these functions.

Table 1 Character Functions in <cctype>

| Function | Accepted Characters |
|---|---|
| isdigit | 0...9 |
| isalpha | a...z, A...Z |
| islower | a...z |
| isupper | A...Z |
| isalnum | a...z, A...Z, 0...9 |
| isspace | White space (space, tab, newline, and the rarely used carriage return, form feed, and vertical tab) |