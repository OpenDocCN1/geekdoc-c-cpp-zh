the memory system. Any arrays or stacks are considered part of the memory subsystem. The C language does not check for, nor prohibit, writing beyond the end of an array or stack into the memory following either data structure. If such memory has been allocated and populated, writing over it can potentially affect the intended or desired operation of the system by corrupting any valid data that had been written there. Whether the memory had been allocated or not, enabling a foreign block of code to be inserted into the memory subsystem can easily bring malware into the system.

When a function is called, a stack frame is created, populated with relevant data including the caller’s return address, register values, and the passed and returned variable values. The stack frame is then pushed onto the stack and the stack pointer incremented to the “next” available stack location. Two potential problems arise here.

The first problem occurs because the C language does not check to see if the stack pointer or other address pointer has gone beyond the valid address/size limit of the stack. The second issue arises when a function returns. On return, the stack pointer is decremented to point to the previous stack frame or, if none, to the original top of the stack. However, the contents of the portion of memory from the just used stack frame are neither erased nor set to NULL. Those values still exist and can be easily read – they have an address in memory and will persist until another function call or operation potentially overwrites them as we see in the code example in Figure 8.39.

```
#include <stdio.h>
#include <stdlib.h>
int f10();
int f1();
int main()
{
    int *intPtr0;
    int myVar0 = 0;
    intPtr0 = &myVar0;
    printf("the value is: %d \n", *intPtr0); // invalid access to local variable in f1()
    // will print: the value is: 9

    myVar0 = f1(); // local variable in f1() overwritten
    printf("the value is: %d \n", myVar0); // will print: the value is: 5
    printf("the value is: %d \n", *intPtr0); // will print: the value is: ?????
    return 0;
}
int f1()
{
    int myVar0 = 9;
    return (&myVar0);
}
int f10()
{
    int myVar1 = 5;
    return (myVar1);
}
```

# Figure 8.39 Persistent Stack Values.

Vulnerable containers are not limited to the stack or the familiar array. A string in C is implemented as a NULL terminated char array. Copying a non-NULL terminated C string, character by character into another container, until a NULL is encountered, could enable the acquisition of all kinds of information.