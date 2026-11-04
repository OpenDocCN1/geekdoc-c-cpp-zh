value of the variable i to 1.” This is not a compiler bug because, by definition, once you have “undefined behavior” there is no such thing as a compiler bug. At that point there are no requirements on what code the compiler generates.

There are some additional interesting scenarios when you want to read strings and numbers from the command line, some of which are described here:

[https://stackoverflow.com/questions/20867382/c-programming-scanf-not-working-correctly](https://stackoverflow.com/questions/20867382/c-programming-scanf-not-working-correctly)

# ## READING MULTIPLE STRINGS FROM THE COMMAND LINE

Listing 2.22 displays the contents of `FirstLastName.c` that illustrates how to prompt users to enter the first name and the last name of a person.

***LISTING 2.22: FirstLastName.c***

```
```c
#include <stdio.h>
#include <string.h>

char first[100];
char last[100];
char full[200];

int main()
{
    printf("Enter first name: ");
    fgets(first, sizeof(first), stdin);

    // see comment below about this snippet:
    // first[strlen(first)-1] = '\0';
```
```