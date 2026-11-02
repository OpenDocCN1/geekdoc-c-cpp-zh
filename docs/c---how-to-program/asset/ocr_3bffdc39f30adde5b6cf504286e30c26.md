```
```
The values stored in character array s are:
integer: 31298
double: 87.375
```
```

Fig. 8.13 | Using function sscanf. (Part 2 of 2.)

# # 8.6 String-Manipulation Functions of the String-Handling Library

The string-handling library (<string.h>) provides many useful functions for manipulating string data (copying strings and concatenating strings), comparing strings, searching strings for characters and other strings, tokenizing strings (separating strings into logical pieces) and determining the length of strings. This section presents the string-manipulation functions of the string-handling library. The functions are summarized in Fig. 8.14. Every function—except for strncpy—appends the null character to its result. [Note: Each of these functions has a more secure version described in the optional Annex K of the C11 standard. We mention these in the Secure C Programming section of this chapter.]

| Function prototype | Function description |
|---|---|
| `char *strcpy(char *s1, const char *s2)` | Copies string s2 into array s1. The value of s1 is returned. |
| `char *strncpy(char *s1, const char *s2, size_t n)` | Copies at most n characters of string s2 into array s1 and returns s1. |
| `char *strcat(char *s1, const char *s2)` | Appends string s2 to array s1. The first character of s2 overwrites the terminating null character of s1. The value of s1 is returned. |
| `char *strncat(char *s1, const char *s2, size_t n)` | Appends at most n characters of string s2 to array s1. The first character of s2 overwrites the terminating null character of s1. The value of s1 is returned. |

Fig. 8.14 | String-manipulation functions of the string-handling library.

Functions strncpy and strncat specify a parameter of type size_t. Function strncpy copies its second argument (a string) into its first argument—a character array that *you must ensure is large enough* to store the string and its terminating null character, which is also copied. Function strncpy is equivalent to strcpy, except that strncpy specifies the number of characters to be copied from the string into the array. *Function strncat does not necessarily copy the terminating null character of its second argument.* This occurs only if the number of characters to be copied is more than the length of the string. For example, if "test" is the second argument, a *terminating null character* is written only if the third argument to strncat is at least 5 (four characters in "test" plus a terminating null character). If the third argument is larger than 5, some implementations append null characters to the array until the total number of characters specified by the third argument are written and others stop after writing the first null character.