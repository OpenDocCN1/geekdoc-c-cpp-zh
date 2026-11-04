```
```c
char *names[4] = {"John", "James", "Mark", "Mary"};
```
```

In the above declaration, **names[0]** points to string **John**, **names[1]** points to string **James**, **names[2]** points to string **Mark**, and so on. An example is given below.

# Example 3.37

Write a program to show how the array of pointers can be used. Declare a function to change an array element.

# Solution 3.37

Figure 3.65 shows the program listing (Program: **apointers.c**). An array of pointers is declared in the main program with 5 names. Function **Chng** changes the third element of this array from **Jane** to **Susan**. The program displays the following:

+   - John
+   - Smith
+   - Susan
+   - Mark
+   - Mary

```
```c
/*--------------------------------------------------
                         ARRAY OF POINTERS
                         ================

This program is an example of array of pointers

Author: Dogan Ibrahim
File  : apointers.c
Date  : December 2020
--------------------------------------------------*/

#include <stdio.h>
#include <ctype.h>

void Chng(char *s[])
{
    s[2] = "Susan";
}

int main(void)
{
    char *names[5] = {"John", "Smith", "Jane", "Mark", "Mary"};
    int k;

    Chng(names);
}
```
```