# Working with Pointers to Functions

LISTING 16.2 ptrfunc2c: Using a Pointer to a Function to Call Different Functions Depending on Program Circumstances

```
/* ptrfunc2c--Using a pointer to call different functions. */
#include <stdio.h>

/* The function prototypes. */
void func1(int x);
void one(void);
void two(void);
void other(void);
int main( void )\n{
    int nbr;
    for (;;) {
        puts("\nenter an integer between 1 and 10
```