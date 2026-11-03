| Function | Description |
|---|---|
| `tan()` | Calculates the tangent value of an angle. Accepts the angle value in radians. |
| `tanh()` | Calculates the tangent hyperbolic value. |

| `string.h` | `string.h` |
|---|---|
| `strcat()` | Function to concatenate(merge) strings. |
| `strcmp()` | Function to compare two strings. |
| `strcpy()` | Function to copy a string to another string |
| `stricmp()` | Function to compare two strings ignoring their case. |
| `strlen()` | Function to calculate the length of the string |
| `strlwr()` | Converts the given string to lowercase |
| `strrev()` | Function to reverse the given string. |
| `strupr()` | Converts the given string to uppercase |
| `strdup` | Duplicates a string. |
| `strnicmp()` | Compares the first n characters of one string to another without being case sensitive. |
| `strncat()` | Adds the first n characters at the end of second string. |
| `strncpy()` | Copies the first n characters of a string into another. |
| `strchr()` | Finds the first occurrence of the character. |
| `strrchr()` | Finds the last occurrence of the character. |
| `strstr()` | Finds the first occurrence of string in another string. |
| `strset()` | Sets all the characters of the string to a given character. |
| `strnset()` | Sets first n characters of the string to a given character. |

# 2. User Defined Functions -

Functions defined by us are known as User Defined Functions. main() function is also user defined function because the definition of main() is defined by us.

e.g.

```
int power(int, int);
main()
{
        int n, p, ans;
        printf("Enter number and its power");
        scanf("%d%d", &n, &p);
```