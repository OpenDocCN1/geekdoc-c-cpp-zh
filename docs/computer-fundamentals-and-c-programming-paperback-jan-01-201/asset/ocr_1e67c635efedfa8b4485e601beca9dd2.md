# TABLE 13.2　String-Handling (`string.h`) Functions

| Function | Significance |
|---|---|
| `size_t strlen(const char *s)` | Returns length of *s*. |
| `char *strcpy(char *dest, const char *src)` | Copies *src* to *dest*, returns pointer to *dest*. |
| `char *strcat(char *dest, const char *src)` | Appends *src* to *dest*, returns pointer to *dest*. |
| `int strcmp(const char *s1, const char *s2)` | Compares *s1* to *s2*, returns -ve, 0 or +ve integer depending on whether *s1* <, =, or > than *s2*. |
| `char *strchr(const char *s, int c)` | Searches *c* in *s*, returns pointer to first occurrence of *c* in *s* or NULL if *c* not found in *s*. |
| `char *strrchr(const char *s, int c)` | As above, but returns pointer to last occurrence of *c* in *s* or NULL if *c* not found in *s*. |
| `char *strstr(const char *s1, const char *s2)` | Searches *s2* in *s1*, returns pointer to *s2* or NULL if *s2* not found in *s1*. |

C doesn’t allow a string *src* to be copied to *dest* using the assignment *dest = src* because that would mean having the same pointer value in both variables. A string is copied with the **strcpy** function. All characters of *src*, including the '\0', are copied to *dest*, and **strcpy** returns a pointer to *dest*. Note that the destination string is always the first argument for functions that use two strings.

# 13.9.3　The strcat Function

Prototype: `char *strcat(char *dest, const char *src);`

```
```c
printf("Enter second string: ");
scanf("%[^\n]", stg3);
strcat(stg3, stg1);
printf("Concatenated string: %s\n", stg3);
```

Assuming stg1 is Burundi ...
... if user enters Congo ...
... stg3 is CongoBurundi
... after concatenation
```

You can’t use the + operator to concatenate two strings. The expression *dest + src* is invalid because that implies adding two pointers, which is not permitted in C. Strings are concatenated with the **strcat** function. The function overwrites the NUL at the end of *dest* with the string *src* and then writes a separate NUL at the end of the concatenated string. **strcat** returns a pointer to *dest*.

# 13.9.4　The strcmp Function

Prototype: `int strcmp(const char *s1, const char *s2);`

```
```c
if (strcmp(s1, s2) == 0)
    printf("The two strings are equal\n");
else if (strcmp(s1, s2) > 0)
    printf("s1 is greater than s2\n");
else
    printf("s1 is less than s2\n");
```
```