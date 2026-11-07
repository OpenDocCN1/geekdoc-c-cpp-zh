```
```c
// calculate and return cube of integer argument
int cubeByValue(int n) {
    return n * n * n; // cube local variable n and return result
}
```
```

The original value of number is 5  
The new value of number is 125

**Fig. 7.2**   Cube a variable using pass-by-value. (Part 2 of 2.)

# Pass-By-Reference

Line 12 of Fig. 7.3 passes the variable number’s address to function cubeByReference (lines 17–19)—passing the address enables pass-by-reference. The function’s parameter is a pointer to an int called nPtr (line 17). The function uses the expression *nPtr to dereference the pointer and cube the value to which it points (line 18). It assigns the result to *nPtr—which is really the variable number in main—thus changing number’s value in main. Use pass-by-value unless the caller explicitly requires the called function to modify the argument variable’s value in the caller. This prevents accidental modification of the caller’s arguments and is another example of the principle of least privilege.

```
```c
// fig07_03.c
// Cube a variable using pass-by-reference with a pointer argument.

#include <stdio.h>

void cubeByReference(int *nPtr); // function prototype

int main(void) {
    int number = 5; // initialize number

    printf("The original value of number is %d", number);
    cubeByReference(&number); // pass address of number to cubeByReference
    printf("\nThe new value of number is %d\n", number);
}

// calculate cube of *nPtr; actually modifies number in main
void cubeByReference(int *nPtr) {
    *nPtr = *nPtr * *nPtr * *nPtr; // cube *nPtr
}
```
```

The original value of number is 5  
The new value of number is 125

**Fig. 7.3**   Cube a variable using pass-by-reference with a pointer argument.

# Use a Pointer Parameter to Receive an Address

A function receiving an address as an argument must receive it in a pointer parameter. For example, in Fig. 7.3, function cubeByReference’s header (line 17) is

```
```c
void cubeByReference(int *nPtr) {
```
```