# OBJECT-ORIENTED PROGRAMMING HAND ON LAB

Experiment-1 : Program illustrating function overloading feature.

```
/*Program : Illustrating function overloading */

#include <iostream.h>
#include <conio.h>

void main()
{
    void show(int);
    void show(float);
    void show(char);
    void show(char*);

    int x = 10;
    float y = 23.45;
    char ch = 'p';

    char * s = "overload";

    clrscr();
    show(x);
    show(y);
    show(ch);
    show(s);
    getch();
}
```