String is a special type of array that is used to store a group of characters. Therefore, strings are also known as character arrays. Similar to arrays, elements of a string are also stored in a contiguous memory location.

The C language provides various standard library functions to manipulate a string. Some of the important library functions for string manipulation are strcat(), strcmp(), strlen(), and strcpy(). The strcat() function concatenates a string with another string. The strcmp() function is used to compare two strings. The strlen() function returns the length of a string. The strcpy() function copies the content of a string into another. To use these functions in a program, we need to include the <string.h> header in it.

In this chapter, we learn about strings as well as how to display them using pointers and the printf() function. Next, we learn about some standard string library functions, such as strcat(), strcmp(), strlen(), strcpy(), strncpy(), strncat(), strchr(), and strcspn().

# Strings

A string is a one-dimensional array of characters, which is terminated by a NULL character ('\0'). Each character in a string occupies one byte of memory and the last character should always be '\0'. It might look like '\0' contains two characters, but '\' is used as an escape sequence, which signifies that the character after '\' is a special character. Note that '\0' and '0' are not similar characters because '\0' has an ASCII value 0; whereas, '0' has an ASCII value 48. Consider the code, given in Listing 3.1, to understand more about the NULL character:

Listing 3.1: Understanding the NULL Character in a String

```
```
#include<stdio.h>

int main()
{
    char a[] = "Tanuman";
    int i=0;

    while(a[i]!='\0')
    {
        printf("%c",a[i++]);
    }

    getch();
    return 0;
}
```
```

In Listing 3.1, we can notice that the string has been displayed without considering its length. This is done because all the strings are automatically terminated by a NULL character; therefore, there is no need to check the length of the string. This implies that we do not need to define the NULL character explicitly in a string, as the compiler always puts a NULL character at the end of a string.

Output of the preceding program is as follows:

```
```
Tanuman
```
```

Let's now learn how to display a string using pointers and the printf() function.

Listing 3.2 displays a string using a pointer:

Listing 3.2: Displaying a String Using a Pointer

```
```
#include<stdio.h>

int main()
{
    char a[] = "Tanuman";
    char *ptr;
```
```