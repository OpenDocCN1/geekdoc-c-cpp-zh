```
```c
// Top level program, demo0.c, used to generate demo. It is made up of demo0.c
#include <stdio.h>

// function prototypes
int incrementItem(void);
int decrementItem(void);

// a global static variable
static int count = 0;

// global variables
int gVar0 = 0;
int myArray[10];

void main(void)
{
    // local declaration
    int number = 0;

    // assign a value to the global variable i
    gVar0=3;

    // This line will print 3
    printf ("The value of gVar0 is %i\n", gVar0);

    // Three values are entered into the array myArray[] and printed
    for (gVar0=0; gVar0<3; gVar0++)
    {
        myArray[gVar0]=gVar0;
    }

    for (gVar0=0; gVar0<3; gVar0++)
    {
        printf ("the value of myArray is %i\n", myArray[gVar0]);
    }

    // The function incrementItem is called to increment the variable count the results are printed
    for (gVar0=0; gVar0<3; gVar0++)
    {
        number = incrementItem();
    }

    printf ("The total number of items is: %i\n", number);
    // The function decrementItem is called to decrement the variable count and the results are printed
    for (gVar0=0; gVar0<3; gVar0++)
    {
        number = decrementItem();
    }
    printf ("The value of number is: %i\n", number);
    printf ("The value of count is: %i\n", count);
    return;
}

int incrementItem(void)
{
    count += 1;
    return count;
}

int decrementItem(void)
{
    count -= 1;
    return count;
}
```
```