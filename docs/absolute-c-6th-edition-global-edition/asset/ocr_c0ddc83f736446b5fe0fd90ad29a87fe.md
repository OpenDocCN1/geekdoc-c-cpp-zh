The character '\0' is used as a sentinel value to mark the end of the C-string. If you read the characters in the C-string starting at indexed variable a[0], proceed to a[1], then to a[2], and so forth, you know that when you encounter the symbol '\0' you have reached the end of the C-string. Since the symbol '\0' always occupies one element of the array, the length of the longest string that the array can hold is one less than the size of the array.

The thing that distinguishes a C-string variable from an ordinary array of characters is that a C-string variable must contain the null character '\0' at the end of the C-string value. This is a distinction regarding how the array is used rather than a distinction regarding what the array is. A C-string variable is an array of characters, but it is used in a different way.

# C-String Variable Declaration

A C-string variable is the same thing as an array of characters, but it is used differently. A C-string variable is declared to be an array of characters in the usual way.

# SYNTAX

```
char Array_Name[Maximum_C-string_Size + 1];
```

# EXAMPLE

```
char myCString[11];
```

The +1 allows for the null character '\0', which terminates any C-string stored in the array. For example, the C-string variable myCString in the previous example can hold a C-string that is ten or fewer characters long.

You can initialize a C-string variable when you declare it, as illustrated by the following example:

```
char myMessage[20] = "Hi there.";
```

Notice that the C-string assigned to the C-string variable need not fill the entire array. When you initialize a C-string variable, you can omit the array size and C++ will automatically make the size of the C-string variable one more than the length of the quoted string. (The one extra indexed variable is for '\0'.) For example,

```
char shortString[] = "abc";
```

is equivalent to

```
char shortString[4] = "abc";
```

Be sure you do not confuse the following initializations:

```
char shortString[] = "abc";
```

and

```
char shortString[] = { 'a', 'b', 'c' };
```