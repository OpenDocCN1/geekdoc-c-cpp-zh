When we declare char as “string[]”, memory space will be allocated as per the requirement during execution of the program.

A string in the C language is simply an array of characters. Strings must have a NULL or \0 character after the last character to show where the string ends. A string can be declared as a character array or with a string pointer. First we take a look at a character array example:

```
```c
char mystr[15];
```
```

As you can see the character array is declared in the same way as a normal array. This array can hold only 14 characters, because we must leave room for the NULL character

```
```c
#include <stdio.h>
int main()
{
    char name[15];
    printf("Enter name: ");
    scanf("%s", name);
    printf("Your name is %s.", name);
    return 0;
}
```
```

# ### Output:

```
```
Enter name
Shrutkirti
Your name is Shrutkirti
```
```

# ## 5.8.2 Declaration

Declaring a string is as simple as declaring a one-dimensional array. Below is the basic syntax for declaring a string.

```
```c
char str_name[size];
```
```

In the above syntax str_name is any name given to the string variable and size is used define the length of the string, i.e the number of characters strings will store. Please keep in mind that there is an extra terminating character which is the Null character (‘\0’) used to indicate termination of string which differs strings from normal character arrays.

# ## 5.8.3 Initialization

Consider the following declaration and initialization that creates a string consisting of the word "Program". To hold the null character at the end of the array, the size of the character array containing the string is one more than the number of characters in the word "Programming"

```
```c
char word[8] = {‘P’, ‘r’, ‘o’, ‘g’, ‘r’, ‘a’, ‘m’, ‘\0’};
```
```

The above array can also be initialized as follows

```
```c
char word[ ] = “Program”;
```
```