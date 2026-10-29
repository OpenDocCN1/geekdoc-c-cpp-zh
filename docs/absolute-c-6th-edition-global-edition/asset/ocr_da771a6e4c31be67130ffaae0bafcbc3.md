# Sample Dialogue:

```
8
22
4
The minimum from threaded min-search is 4
```

The code sends in the array to be searched, an array for results, an ID, and bounds for each thread to search. Each thread then searches its portion of the array, finds the minimum, and uses its ID to determine a unique spot to place its result in the results array.

# Smart Pointers

Chapters 10 and 17 describe the benefits of pointers but also illustrate the pitfalls if memory management is not performed correctly. Dangling pointers or memory leaks can result in errors that are difficult to find. C++11 includes a new class called shared_ptr that simplifies memory management and sharing of objects in memory.

The shared_ptr class is a template that is a wrapper around an object allocated from the free store. The wrapper uses reference counting to track how many other pointers reference the object. The counter starts at 0. The counter is incremented by one every time a new variable references the object. Similarly, the counter is decremented by one every time a variable ceases to reference the object (e.g., it is deleted or reassigned). If the counter reaches 0, then the object can be safely deleted and the allocated memory returned to the free store. This is all performed automatically, which frees the programmer from having to write his or her own memory management code!

As an example, consider the following code, which implements a simple linked list of the Node class. The class simply stores an integer. The code is written using the “old” format of linking classes via pointer and does not explicitly free the memory that is allocated in the list’s function. This means that the program has a memory leak when execution returns to the main function. This could cause memory problems if the program did not immediately exit.

```
// Linked list of a simple Node class using traditional pointers.
// Note that this version has a memory leak when execution returns to
// main.
#include <iostream>
using namespace std;

// A simple Node class. A full-featured class would have
// several more functions.
class Node
{
private:
        int num;
        Node *next;
```