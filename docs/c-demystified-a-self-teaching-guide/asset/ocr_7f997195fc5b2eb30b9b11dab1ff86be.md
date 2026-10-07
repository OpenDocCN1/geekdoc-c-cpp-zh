# Useful C-String and C++ String Functions

The string standard library provides a number of functions that are useful when working with null terminated character arrays, C-strings. The string standard library provides a number of functions that are useful when working with the C++ string class. This section will discuss the functions you use with a C-string and the C++ string class, respectively, to perform several common tasks.

# Determining the Length of a String

You use the strlen function to determine the length of a C-string. The strlen function takes one argument, which may be a character array, a pointer to a character array, or a literal string. This function returns an integer representing the number of characters, not including the null character. The following code fragment illustrates the use of strlen

```
int len;
len = strlen("Jeff") // len is 4
char* stinkody = "Dante";
len = strlen(stinkody); // len is 5
char name[80] = "Devvie";
len = strlen(name); // len is 6
char crazydog = "Micaela";
len = strlen(crazydog); // len is 7
```

The strlen function is particularly useful in determining the length of a character array. For example, the following code fragment illustrates the use of the strlen and isdigit functions to validate a security string, which to be valid, must be exactly 11 characters long and consist of three digits, a dash, two digits, and four digits:

```
bool isValid(char* strInput)
{
    if (!strlen(strInput) == 11)
        return false;
    for (int x = 0; x < 11; x++)
    {
        if (x == 3 || x == 6)
        {
            if (strInput[x] != '-')
                return false;
        } else
        {
            if (!isdigit(strInput[x]))
                return false;
        }
    }
    return true;
}
```

The C++ class member functions are comparable to the effect of strlen length and size. Neither has any arguments, and both return an integer representing the length of the string. The following code fragment illustrates the use of the length and size member: