```
```c
printf("\na++ = %d",a++);
printf("\na = %d",a);

getch();
}

Output
a = 10
++a = 11
a = 11
a++ = 11
a = 12
```
```

# EXAMPLE A.8 Write a program to perform bitwise AND and OR operations.

```
```c
Program
/*Program for demonstrating the use of bitwise operators*/
#include <stdio.h>
#include <conio.h>

void main()
{
    char a='A',b='B';
    clrscr();

    printf("\na & b = %c",a&b);/*Using bitwise & operator*/
    printf("\na | b = %c",a|b);/*Using bitwise | operator*/

    getch();
}

Output
a & b = @
a | b = C
```
```

# EXAMPLE A.9 Write a program to demonstrate the use of sizeof operator.

```
```c
Program
/*Program for demonstrating the use of sizeof operator*/
#include <stdio.h>
#include <conio.h>

void main()
{
    char a;
    int b;
```
```