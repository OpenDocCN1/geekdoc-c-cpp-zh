```
char *strchr(const char * s, int c);
```

This function returns a pointer to the first location in the string s that holds the character c. (The terminating null character is part of the string, so it can be searched for.) The function returns the null pointer if the character is not found.

```
char *strpbrk(const char * s1, const char * s2);
```

This function returns a pointer to the first location in the string s1 that holds any character found in the s2 string. The function returns the null pointer if no character is found.

```
char *strrchr(const char * s, int c);
```

This function returns a pointer to the last occurrence of the character c in the string s. (The terminating null character is part of the string, so it can be searched for.) The function returns the null pointer if the character is not found.

```
char *strstr(const char * s1, const char * s2);
```

This function returns a pointer to the first occurrence of string s2 in string s1. The function returns the null pointer if the string is not found.

```
size_t strlen(const char * s);
```

This function returns the number of characters, not including the terminating null character, found in the string s.

Note that these prototypes use the keyword const to indicate which strings are not altered by a function. For example, consider the following:

```
char *strcpy(char * restrict s1, const char * restrict s2);
```

It means s2 points to a string that can’t be changed, at least not by the strcpy() function, but s1 points to a string that can be changed. This makes sense, because s1 is the target string, which gets altered, and s2 is the source string, which should be left unchanged.

The keyword restrict, discussed in Chapter 12, indicates restrictions on how the function arguments should be used, for example, not copying a string into itself.

The size_t type, as discussed in Chapter 5, “Operators, Expressions, and Statements,” is whatever type the sizeof operator returns. C states that the sizeof operator returns an integer type, but it doesn’t specify which integer type, so size_t can be unsigned int on one system and unsigned long on another. The string.h file defines size_t for a particular system or else refers to another header file having the definition.

As mentioned earlier, Reference Section V lists all the functions in the string.h family. Many implementations provide additional functions beyond those required by the ANSI standard. You should check the documentation for your implementation to see what is available.