Since there was no exception in the try block, the catch block will not be executed this time and the control of execution directly jumps to the first statement after the catch block, which is `cout<<"Good Bye"<<endl;`

This prints the message Good Bye on the computer screen.

> **NOTES**
> 
> catch block is executed only if there is an exception generated in the try block. If there is no exception in the try block, all the catch block(s) are skipped.

> **NOTES**
> 
> Always remember to check the boundary conditions before accessing elements of the array in your program to avoid occurrence of **array index out of bounds exception**. It is a good programming practice to have such proactive checks in the program that deals with arrays.

# 17.4.2  NULL pointer exception: An example

Let us assume that we have created a pointer in the program, which points to NULL and no valid data value. In this case, dereferencing a pointer makes no real sense because it is not pointing to any valid memory location. However, if the programmer tries to accidently dereference this pointer, then the results will be erroneous, and this exception is called NULL pointer exception.

In this example, we will demonstrate two things together:

+   1. Handling of NULL pointer exception
+   2. Generating an exception in the called function and handling it in calling function

```
```cpp
#include<iostream.h>
void printData(int *p)
{
    if(p == NULL)
    {
        throw 0;
    }
    else
    {
        cout<<"Data is "<<*p<<endl;
    }
}
void main()
{
    int *p=0;
    int a=10;
    /*Following statement is commented*/
```
```