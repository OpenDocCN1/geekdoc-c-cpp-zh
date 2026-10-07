# Chapter 4 Compound Types

```
char boss[8] = "Bozo";
```

| B | o | z | o | \0 | \0 | \0 |
|---|---|---|---|---|---|---|
| | | | null character | remaining |
| | | | automatically added at end | set to \0 |

Figure 4.2 Initializing an array to a string.

Note that a string constant (with double quotes) is not interchangeable with a character constant (with single quotes). A character, such as 'S', is a shorthand notation for the code. On an ASCII system, 'S' is just another way of writing 83. Thus, the following statement assigns the value 83 to shirt_size:

```
char shirt_size = 'S'; // this is fine
```

But "S" is not a character constant; it represents the string consisting of two characters, the S and \0 characters. Even worse, "S" represents the memory address at which the string is stored. A statement like the following assigns a memory address to shirt_size:

```
char shirt_size = "S"; // illegal type mismatch
```

Because an is a separate type in C++, a C++ compiler won't allow this sort of nonsense. (We'll return to this point later in this chapter we've discussed pointers.)

# Concatenating String Literals

Sometimes a string may be too long to fit on one line of code. C++ enables you to concatenate string literals—that is, to combine two quoted strings into one. Indeed, any two strings separated only by whitespace (spaces, tabs, and newlines) are automatically joined into one. Thus, the following output statements are equivalent to each other:

```
cout << "I'd give my right arm to be " " a great violinist.\\n"
cout << "I'd give my right arm to be a great violinist.\\n"
cout << "I'd give my right arm ar"
m" to be a great violinist.\\n";
```

Note that join adds any spaces to the joined strings.The first character of the second string immediately follows the last character, \0, of the first string. The \0 character from the first is replaced by the first character of the last string.