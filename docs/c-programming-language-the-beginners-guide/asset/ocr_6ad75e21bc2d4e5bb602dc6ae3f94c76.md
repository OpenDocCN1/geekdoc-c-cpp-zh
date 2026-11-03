# Switch/Else Statements

The C language lets you handle complex decisions by stacking a bunch of *if/else* conditions. Sometimes, that structure can get a bit ugly. As an alternative, you can employ the *switch/case* structure, which is yet another decision making tool in the C language.

In this section, we’ll talk about the structure. You’ll see how it is constructed, how it can handle multiple decisions, plus we’ll talk about a few tricks. Take a look at the code below:

```
```c
#include <stdio.h>

int main()
{
    char a;

    printf("Your choice (1,2,3): ");
    scanf("%c", &a);

    switch(a)
    {
        case '1':
            puts("Excellent choice!");
            break;
        case '2':
```
```