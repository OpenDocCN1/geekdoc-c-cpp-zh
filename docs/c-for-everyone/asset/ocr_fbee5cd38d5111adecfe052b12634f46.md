![](bbox=[0.34, 0.09, 0.8, 0.19])

This array can hold strings with a length of at most 39, because one character is required for the null terminator.

Now copy the first name, using `strncpy`:

```
strncpy(name, first, NAME_SIZE - 1);
```

You must be careful not to overrun the target array. It is unlikely that a first name is longer than 39 characters, but a hacker could supply a longer input in order to overwrite memory.

Now, if there is still room, add a space and the last name, again being careful not to overrun the array boundaries.

```
int length = strlen(name);
if (length < NAME_SIZE - 1)
{
    strcat(name, " ");
    int n = NAME_SIZE - 2 - length; // Leave room for space, null terminator
    if (n > 0)
    {
        strncpy(name, last, n);
    }
}
```

As you can see, the C string code is over three times as long as the code using C++ strings, and it is not as capable—if the target array is not long enough to hold the result, it is truncated.

### Table 4  C String Functions

In this table, s and t are character arrays; n is an integer.

| Function | Description |
|---|---|
| `strlen(s)` | Returns the length of s. |
| `strcpy(t, s)` | Copies the characters from s into t. |
| `strncpy(t, s, n)` | Copies at most n characters from s into t. |
| `strcat(t, s)` | Appends the characters from s after the end of the characters in t. |
| `strncat(t, s, n)` | Appends at most n characters from s after the end of the characters in t. |
| `strcmp(s, t)` | Returns 0 if s and t have the same contents, a negative integer if s comes before t in lexicographic order, a positive integer otherwise. |