A C-string variable is a partially filled array of characters. Like any other partially filled array, a C-string variable uses positions starting at indexed variable 0 through as many as are needed. However, a C-string variable does not use an int variable to keep track of how much of the array is currently being used. Instead, a string variable places the special symbol '\0' in the array immediately after the last character of the C string. Thus, if s contains the string "Hi Mom!", then the array elements are filled as shown here:

| s[0] | s[1] | s[2] | s[3] | s[4] | s[5] | s[6] | s[7] | s[8] | s[9] |
| H | i |  | M | o | m | ! | \0 | ? | ? |

The character '\0' is used as a sentinel value to mark the end of the C string. If you read the characters in the C string starting at indexed variable s[0], proceed to s[1], and then to s[2], and so forth, you know that when you encounter the symbol '\0', you have reached the end of the C string. Since the symbol '\0' always occupies one element of the array, the length of the longest string that the array can hold is 1 less than the size of the array.

The thing that distinguishes a C-string variable from an ordinary array of characters is that a C-string variable must contain the null character '\0' at the end of the C-string value. This is a distinction in how the array is used rather than a distinction about what the array is. A C-string variable is an array of characters, but it is used in a different way.

C-string variables vs. arrays of characters

# C-String Variable Declaration

A C-string variable is the same thing as an array of characters, but it is used differently. A C-string variable is declared to be an array of characters in the usual way.

# SYNTAX

```
char ArrayName[Maximum_C_string_Size + 1];
```

# EXAMPLE

```
char myCString[11];
```

The + 1 allows for the null character '\0', which terminates any C string stored in the array. For example, the C-string variable myCString in the example can hold a C string that is ten or fewer characters long.

You can initialize a C-string variable when you declare it, as illustrated by the following example:

```
char myMessage[20] = "Hi there.";
```

Initializing C-string variables