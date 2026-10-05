
In the foregoing listings, the memory block was deallocated only at the end of the functions allocated it. However, dynamic memory deallocation is usually conditional (Listing 3.7).

## Listing 3.7 C++ allows deallocation of memory as and when required

```cpp
void abc(int ** p)
{
    if(memory_not_required) {
        delete *ptr;
        *p = NULL;
    }
/* rest of the abc() function */
}
```

A misconception about the delete operator is ‘deleting the pointer’. An uninitiated reader may think that the memory being occupied by the pointer gets removed if the delete operator is used on the pointer. In reality, nothing of this happens.

When the delete operator is used on a pointer, the pointer continues to occupy its block of memory and continues to have the same value that is the address of the first byte of the block of memory. Thus, the pointer continues to point at same block of memory. This will lead to runtime errors if the pointer is dereferenced.

We see in Listing 3.7 that the pointer being pointed at by ‘p’ was deliberately nullified after the pointer was pointing at had been deallocated. This is a very common practice to indicate that the pointer (the whose address is passed from the calling function) no longer points to a dynamically allocated block of memory. In other words, it is highly desirable that either the pointer points at a valid block of memory or be NULL. It is not possible to ensure this due to the low level of representation of pointers. A pointer is unlikely to be NULL at the time of creation. But that does not mean that the value contains is the address of some valid block of memory. There is no guaranteed initialization of data. This problem is solved by the use of constructors, which have been discussed in Chapter 4.

A multiple block of memory is deallocated by suffixing the delete operator with an empty pair of square brackets followed by the pointer that points at the multiple block of memory, as shown in Listing 3.8.

## Listing 3.8 Deallocating memory that was allocated for an array

```cpp
int * Iptr;
...
ptr = new int[10];
...
delete[] Iptr;
```

If we write `delete Iptr` instead of `delete[] Iptr`, only the first four bytes of the block of 40 bytes at which Iptr is pointing, will be deallocated. Using `delete[]` deallocates the entire block of 40 bytes. The syntax for using the delete operator to allocate an array is as follows:

```cpp
delete [] <ptr>;
```

The size of the array to be created is passed as a parameter to the new operator. But while deallocating the memory allocated for the array, the size is not passed (the square brackets are empty). How does the compiler know how much memory is to be deallocated? The answer is that when the new operator executes to allocate a block of array, the OS stores the size passed. Figure 3.4 shows the size of the memory block, which is captured during run time, prefixed to the memory block itself. When the delete operator is used followed by the empty pair of square brackets, the compiler uses the size stored and deallocates the entire block correctly.

![](img/5bfa77b13fdaa376725789bb8c00ee79_101_0.png)

Figure 3.4 Size of the allocated memory is prefixed to the memory block

Blocks of memory containing arrays of other types can also be deallocated similarly. For example, see Listing 3.9.

## Listing 3.9 Deallocating memory that was allocated for an array of objects

```cpp
Distance * dptr; // creates an array of 5 objects at
dptr = new Distance[5]; // the class Distance
...
delete[] dptr; // de-allocates the memory allocated for the entire array
```

## 3.4 set_new_handler() Function

We already know that the new operator attempts to capture more chunks of memory from the heap during run time. But what happens if no more memory is available to satisfy this attempt? We get an out-of-memory condition. 

The new operator, when faced with an out-of-memory condition, calls a global function and then throws an exception of type `bad_alloc` (the chapter on exception dealing with the mechanism of throwing and catching exceptions). This global function is known as the new handler function.

We can specify our own handler function also! We can specify that the new operator, upon encountering an out-of-memory condition, calls a function of your choice. We can do this by calling the `set_new_handler()` function and passing the name of the desired function as a parameter to it. The prototype of the `set_new_handler()` function clarifies this. The prototype is in the `new.h` header file.

```cpp
new_handler set_new_handler(new_handler);
```

Obviously, `new_handler` is a data type. It is a function pointer. The first argument of the `set_new_handler()` is a function pointer. If we pass the name of our desired function as a parameter to the `set_new_handler()` function, all subsequent out-of-memory conditions cause the new operator to call it. Our desired function becomes the new handler. Moreover, when the `set_new_handler()` function is called, it returns a pointer to the previous new function.

An illustrative example follows in Listing 3.10.

## Listing 3.10 Specifying a new handler function

```cpp
/* Beginning of newHandler.cpp */
#define BIG_NUMBER 9999999
#include<new.h> // for set_new_handler

void newHandler() {
    // handle out-of-memory
}

int main() {
    set_new_handler(newHandler);
    int *p = new int[BIG_NUMBER];
    ...
    return 0;
}
```
