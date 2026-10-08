3. Write C code to print the character arrays stored in Question 2, left-justified.
4. Write C code to print the characters stored in Question 2, right-justified.

# 9.2 Introduction to Strings

A string constant in C is zero or more characters including blanks, enclosed between two double quotes. For example "axcmn" and "x5*mc" are string constants. If there are no characters between double quotation marks (""), it is a null string. String constants are used in every input/output statement that has a format, but they can also be stored in character arrays and given names. A string stored in a character array differs from character data stored in a character array in that a string is treated as a single value, must be shorter than the declared size of the array, and must be followed by a special character known as the null terminating character ('\0').

| Character array | String |
|---|---|
| 7 9 4 | 7 9 4 \0 |
| J | o | e | s | J | o | e | s \0 |

String variables can be initialized when they are declared, either by specifying the individual elements of the variable, or by using a string constant.

Character array

String

```
char IDnum[3] = {'7','9','4'};
char ID[4] = {'7','9','4','\0'};
or char ID[4] = "794";
```

char name[8] = {'J','o','n','e','s','s'};

```
char strname[8] = 
{'J','o','n','e','s','s','\0'};
nor char strname[8] = "Jones";
```

Here IDnum and name are character arrays. Initializing them places the characters in the array, left-justified with blanks filled on the right. ID and strname are strings. If they are initialized character-by-character, the null terminating character must