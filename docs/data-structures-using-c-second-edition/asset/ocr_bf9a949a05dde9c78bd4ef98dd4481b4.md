```
if(str[i] == str[j])
{
    i++;
    j--;
}
else
    break;
}
if(i>j)
    printf("\n PALINDROME");
else
    printf("\n NOT A PALINDROME");
return 0;
```

Output
Enter the string: madam
PALINDROME

# 4.4 POINTERS AND STRINGS

In C, strings are treated as arrays of characters that are terminated with a binary zero character (written as '\0'). Consider, for example,

```
char str[10];
str[0] = 'H';
str[1] = 'I';
str[2] = '!';
str[3] = '\0';
```

C provides two alternate ways of declaring and initializing a string. First, you may write

```
char str[10] = { 'H', 'I', '!', '\0'};
```

But this also takes more typing than is convenient. So, C permits

```
char str[10] = "HI";
```

When the double quotes are used, a null character ('\0') is automatically appended to the end of the string.

When a string is declared like this, the compiler sets aside a contiguous block of the memory, i.e., 10 bytes long, to hold characters and initializes its first four characters as HI\0.

Now, consider the following program that prints a text.

```
#include <stdio.h>
int main()
{
    char str[] = "Hello";
    char *pstr;
    pstr = str;
    printf("\n The string is : ");
    while(*pstr != '\0')
    {
        printf("%c", *pstr);
        pstr++;
    }
    return 0;
}
```

Output
The string is: Hello