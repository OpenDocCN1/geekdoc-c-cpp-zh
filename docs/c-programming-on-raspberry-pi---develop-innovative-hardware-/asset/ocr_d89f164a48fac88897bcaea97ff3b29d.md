```
```c
for(k = 0; k < max; k++) ptr[k] = &numbers[k];

for(k = 0; k < max; k++)printf("numbers[%d] = %d\n", k, *ptr[k]);

return 0;
}
```
```

Figure 3.66 Program apointer2.c

# Function pointers

Function pointers are used to point to functions and not data. They can be used in menu type applications. An example is given below.

# Example 3.39

Write a program to operate on two numbers. The required operations are: add, subtract, multiply and divide. Use function pointers as a MENU in your program.

# Solution 3.39

The required program listing is shown in Figure 3.67 (Program: **apointers3.c**). At the beginning of the program, a function pointer called **ptr** is created to point to functions **Add**, **Subtract**, **Multiply**, and **Divide**. The user is prompted to enter two numbers, separated with a space. Four functions are used for addition, subtraction, multiplication, and division. Then a MENU is created with four options and the user is requested to enter a choice. A function is then called based on the user’s choice using the function pointer.

```
```c
/*----------------------------------------------------
                    FUNCTION POINTERS
                    =================

This program is an example of using function pointers

Author: Dogan Ibrahim
File  : apointers3.c
Date  : December 2020
----------------------------------------------------*/
#include <stdio.h>

void Add(float a, float b)
{
    printf("\nThe sum is: %f\n", a + b);
}

void Subtract(float a, float b)
{
```
```