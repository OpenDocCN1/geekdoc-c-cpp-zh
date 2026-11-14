# EXAMPLE 11.1

The software listing in Figure 11.14 gives a first cut at the design of a simple operating system kernel.

```
```
// Building a simple OS kernel - step 1
#include <stdio.h>
// Declare the prototypes for the tasks
void get( void* aNumber); // input task
void increment( void* aNumber); // computation task
void display( void* aNumber); // output task
void main(void)
{
int i=0; // queue index
int data; // declare a shared data
int* aPtr = &data; // point to it
void (*queue[3])(void*); // declare queue as an array of pointers to
// functions taking an arg of type void*
queue[0] = get; // enter the tasks into the queue
queue[1] = increment;
queue[2] = display;
while(1)
{
queue[i]( (void*) aPtr); // dispatch each task in turn
i = (i+1)%3;
}
return;
}
void get( void* aNumber) // perform input operation
{
printf( "Enter a number: 0. 9" );
*(int*) aNumber = getchar(); // discard cr
getchar(); // convert to decimal from ascii
*(int*) aNumber -= '0';
return;
}
void increment( void* aNumber) // perform computation
{
int* aPtr = (int*) aNumber;
(*aPtr)++;
return;
}
void display( void* aNumber) // perform output operation
{
printf( "The result is: %d\n", *(int*)aNumber);
return;
}
```
```

Figure 11.14 A Simple Operating System Kernel