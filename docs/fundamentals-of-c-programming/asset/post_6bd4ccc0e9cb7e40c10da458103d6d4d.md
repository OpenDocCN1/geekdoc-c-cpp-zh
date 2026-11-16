
## Figure 18.1 Memory leak

- 1. Before the call to calc, variable p does not exist

- 2. During the execution of calc, variable p is alive and points to dynamically allocated memory

![](img/e84ad11adb18201d71595b31ce6c9eff_556_0.png)

- 3. After calc returns, variable p goes away, but the memory allocated on its behalf remains

![](img/e84ad11adb18201d71595b31ce6c9eff_556_1.png)

```
// Do some stuff
// ...
int *p = new int[n];
// ...
// Do some stuff with p
// ...
// Exit function without deleting p's memory
}
```

If a program calls function calc enough times, the program will eventually run out of memory. Figure 18.1 shows how memory is stranded when local pointers go out of scope at the end of a function's execution.

In the calc function p is a local variable. As such, p lives on the stack. When a particular call to calc completes, the function's clean up code automatically releases the space held by the variable p. This is because all functions automatically manage the memory for their parameters and local variables. The problem is p is assigned via new to point to memory allocated from the heap, not the stack. Function executions manage the stack memory only. When the function's execution completes, p is gone, and the memory to which p pointed is not deallocated automatically. Worse yet, the heap memory formerly referenced by the local variable p now is unreachable because no other variables that remain viable know anything about it.

A correctly written calc function has two options in this case:

- 1. free up p's allocated memory with delete before returning,

- 2. return p to the function's caller and let the caller call delete when finished with the object calc created.

Option 1 is the easiest solution. The `calc` function needs a dynamically allocated array, creates it, uses it, and then deallocates it before returning. Within this single function definition we can see a `new` and later its corresponding `delete`—a perfect matched pair. Unfortunately, this is not a common case.

Option 2 is the more common occurrence. Dynamic memory allocation from the heap enables an executing program to add extra data at run time that persists across function calls. In theory the process is simple:

- 1. code in need of what the `calc` function can offer would call `calc` to obtain a dynamically allocated object and

- 2. `delete` the object when finished with it.

The problem here is we cannot see the `new` paired with the `delete`. The `new` is hidden in `calc`, and the caller must exercise `delete`. The programmer of the calling code must be self disciplined and remember to use `delete` appropriately.

- The `delete` operator never should be used to free up memory that was not allocated by a previous call to `new`. This code fragment illustrates one such example:

```
int list[10], *p = list; // p points to list
// ...
// Do some stuff
// ...
delete [] p; // Logic error, attempt to deallocate p's memory
```

The space referenced by pointer `p` was not allocated by `new`, so `delete` should not be used to attempt to free up its memory.

Attempting to `delete` memory not allocated with `new` results in undefined behavior and represents a logic error.

- `delete` must not be used to deallocate the same memory more than once. This can happen when two pointers refer to the same memory. Such pointers are called *aliases*. The following code fragment illustrates the situation:

```
int *p = new int[10], *q = p; // q aliases p
// ...
// Do some stuff with p and/or q
// ...
delete [] p; // Free up p's memory
// ...
// Do some other stuff
// ...
delete [] q; // Logic error, q's memory already freed!
```

Since pointer `p` and pointer `q` point to the same memory, they are aliases of each other. Deallocate the memory referenced by one of them, and the other's memory is also deallocated, since it is the same memory.

Multiple `delete`s of the same memory results in undefined behavior and represents a logic error.

- Never attempt to access memory previously deallocated via `delete`. Attempting to access deleted memory results in undefined behavior and represents a logic error. The code fragment

```
int *list = new int[10];
// ...
// Use list, then
// ...
delete [] list; // Deallocate list's memory
// ...
// Sometime later
// ...
int x = list[2]; // Logic error, but sometimes works!
```

illustrates how such a situation can arise. For efficiency reasons the delete operator in many implementations marks heap space as "available" without modifying the contents of that memory. Careless programmers can accidentally use the memory of a deleted pointer obliviously as if it were still live. The problem manifests itself when the freed up memory eventually gets reallocated elsewhere via a call to new. The result is that programs seem to "work" for a while and mysteriously fail at unpredictable times. Debugging such situations can be very difficult. The problem often happens because of aliasing:

```
int *list = new int[10];
// ...
int *arr = list; // arr aliases list
// ...
delete [] list; // Deallocate list's memory
// ...
// Sometime later
// ...
int x = arr[2]; // Same problem!
```

We declared list's memory, not arr's memory, didn't we? No, since arr is an alias for list, arr references memory previously deallocated with delete.

Aliasing is a problem because of our concept of variables. When we have two variables with different names it is natural to assume they represent two different objects. This is known as value semantics. Pointers and references introduce the possibility of aliasing: they use reference semantics. Reference semantics enable useful techniques such as call-by-reference and the traversal of dynamic data structures like linked lists, but reasoning about the identity of objects using reference semantics requires extra caution.

It seems simple enough to make sure every new has exactly one corresponding delete, but in practice it can be very difficult to determine exactly when to use delete. Suppose, for example, you obtain a dynamically allocated object from a function call, as in the following:

```
Widget *p = get_widget();
```

Quite possibly the get_widget function allocates a Widget object via new and simply returns a pointer to the object. In this case we can use

```
delete p;
```

when we are finished using the object to which p points. What if, however, the get_widget function is managing some resource created elsewhere; that is, get_widget returns a pointer to an object it does not create? Listing 18.1 (howtodelete.cpp) provides a rudimentary example.

## Listing 18.1: howtodelete.cpp

```
#include <iostream>

struct Widget {
    int value;
    Widget(int value): value(value) {
        std::cout << "Creating widget " << value << '\n';
    }
    ~Widget() {
        std::cout << "Destroying widget " << value << '\n';
    }
};

Widget global_w(5);

Widget *get_widget1() {
    // Caller must deallocate the returned object
    Widget *w = new Widget(10); // Allocation each call
    return w;
}

Widget *get_widget2() {
    // Caller must NOT deallocate the returned object
    // as it points to a global variable not dynamically
    // allocated
    return &global_w; // No allocation
}

void process() {
    Widget *p1 = get_widget1();
    std::cout << "p1->value = " << p1->value << '\n';
    Widget *p2 = get_widget2();
    std::cout << "p2->value = " << p2->value << '\n';
    delete p1; // Must delete p1
    delete p2; // But do not delete p2!
}

int main() {
    std::cout << "Entering main\n";
    process();
    std::cout << "Leaving main\n";
}
```

The author of the process function in Listing 18.1 (howtodelete.cpp) correctly assumes that the get_widget1 function returns a dynamically allocated object that callers (in this case process) must eventually deallocate. The statement

```
delete p1;
```

correctly frees up the object get_widget1 created. The author of the process function also mistakenly assumes that the get_widget2 function returns a dynamically allocated object that callers must eventually deallocate. Not wanting to risk a memory leak, the process author adds the statement

```
delete p2;
```
