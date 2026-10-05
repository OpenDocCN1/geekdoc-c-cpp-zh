Each time a recursive function calls itself, new memory is allocated from the stack to store its variables. In our example, three different num variables were created, each with a different value. A simple way to describe this is to consider that each num is piled on top of the other (e.g., as dishes piled on top of each other) and at the end of the recursion we access the num created last (e.g., we get the dish at the top of the pile). For static variables no new memory is allocated, as all functions share the same stack. The information for which part of the code is left unexecuted is also stored in the stack. That code will be executed when the function calls itself again, that is, when the recursion ends.

In our example, the value of each num is stored in the stack and each cout will be executed in the opposite order from the function calls, that is, from the last to the first one. This will happen when show() does not call itself, that is, when num becomes 1.

The size of the stack might not be large enough to store the information associated with each function call. For example, if the user enters a large value, say 100000, the execution of the program may terminate abruptly and the Stack overflow appear, which indicates that there is no other available memory in the stack. The default stack size depends on the implementation.

> Be careful when using a recursive function, because it calls many times, its execution may take considerable time and the repeated calls may deplete the stack memory.

In practice, recursion is often used to implement math algorithms or operations in data structures. In general, an individual task is a smaller version of the original task to be performed, it is a candidate to be implemented using a recursive function. For example, we will use recursion in Chapter 14 to implement several functions in a binary search tree. However, if you can write equivalent code, better. For example, use an iteration loop instead. Although the recursive code might be easier to read and write, the loop performance would probably be better as it avoids consecutive function calls and memory allocations in the stack.

# EXERCISES

C.11.29 What is the output of the following program?

```
#include <iostream>

int a = 4;

int main()
{
    if(a == 0)
        return 0;
    else
    {
        std::cout << a-- << ' ';
        main();
    }
    return 0;
```

**Answer:** Note that main() can also be called recursively. In each call, a is decremented by 1. The program stops calling main() once a becomes 0. Therefore, the program displays: 4 3 2 1