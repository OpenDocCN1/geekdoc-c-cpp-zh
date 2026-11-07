```
The values stored in character array s are:
integer: 31298
double: 87.375
```

**Fig. 8.10**  |  Using function sscanf. (Part 2 of 2.)

# ✓ Self Check

+   1. *(Multiple Choice)* Which function is described by “Prints the character stored in its parameter and returns it as an integer?”
+      a) getchar.
+      b) sprintf.
+      c) puts.
+      d) putchar.
+   
+   **Answer:** d.

2. *(True/False)* Function getchar reads a character from the standard input and returns it as a char.

**Answer:** False. Actually, getchar returns an int to support the end-of-file indicator, which is -1.

# 8.6 String-Manipulation Functions of the String-Handling Library

The string-handling library (<string.h>) provides useful functions for:

+   - manipulating string data (copying strings and concatenating strings),
+   - comparing strings,
+   - searching strings for characters and other strings,
+   - tokenizing strings (separating strings into logical pieces), and
+   - determining the length of strings.

This section presents the string-handling library’s string-manipulation functions, which are summarized in the following table. Other than strncpy, each function appends the null character to its result.

| Function prototype | Function description |
|---|---|
| `char *strcpy(char *s1, const char *s2)` | Copies string s2 into array s1 and returns s1. |
| `char *strncpy(char *s1, const char *s2, size_t n)` | Copies at most n characters of string s2 into array s1 and returns s1. |
| `char *strcat(char *s1, const char *s2)` | Appends string s2 to array s1 and returns s1. String s2’s first character overwrites s1’s terminating null character. |