Function `realloc` takes two arguments—a pointer to the original object (`ptr`) and the new size of the object (size). If `ptr` is 0, `realloc` works identically to `malloc`. If `size` is 0 and `ptr` is not 0, the memory for the object is freed. Otherwise, if `ptr` is not 0 and size is greater than zero, `realloc` tries to allocate a new block of memory. If the new space cannot be allocated, the object pointed to by `ptr` is unchanged. Function `realloc` returns either a pointer to the reallocated memory or a null pointer.

> **Common Programming Error F.2.**
> 
> *Runtime errors may occur if you use the `delete` operator on a pointer resulting from `malloc`, `calloc` or `realloc`, or if you use `realloc` or `free` on a pointer resulting from the `new` operator.*

![](bbox=[0.159, 0.232, 0.217, 0.277])

# F.11 Unconditional Branch: goto

Throughout the text we’ve stressed the importance of using structured programming techniques to build reliable software that is easy to debug, maintain and modify. In some cases, performance is more important than strict adherence to structured-programming techniques. In these cases, some unstructured programming techniques may be used. For example, we can use break to terminate execution of a repetition structure before the loop-continuation condition becomes false. This saves unnecessary repetitions of the loop if the task is completed before loop termination.

Another instance of unstructured programming is the `goto` statement—an unconditional branch. The result of the `goto` statement is a change in the flow of control of the program to the first statement after the label specified in the `goto` statement. A label is an identifier followed by a colon. A label must appear in the same function as the `goto` statement that refers to it. Figure F.7 uses `goto` statements to loop 10 times and print the counter value each time. After initializing count to 1, the program tests count to determine whether it is greater than 10. (The label start is skipped, because labels do not perform any action.) If so, control is transferred from the `goto` to the first statement after the label end. Otherwise, count is printed and incremented, and control is transferred from the `goto` to the first statement after the label start.

```
// Fig. F.7: figF_07.cpp
// Using goto.
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    int count = 1;

start: // label
    // goto end when count exceeds 10
    if ( count > 10 )
        goto end;
```

Fig. F.7 | Using goto. (Part 1 of 2.)