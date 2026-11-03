The code shown in Listing 20-4 doesn't contain any surprises; most of it should be familiar if you've worked through this chapter straight from the beginning. The only new item is at Line 23, the free() function.

The free() function releases the allocated memory, making it available for malloc() or something else to use. Its argument is a pointer, the address of memory to free. Like malloc(), calloc(), and realloc(), the free() function is prototyped in the stdlib.h header file.

Exercise 20-9: Type the source code from Listing 20-4 into a new project. Build and run.

You may have noticed that no earlier listings in this chapter use the free() function to release allocated memory. The reason is that memory was allocated in the main() function, and the operating system releases all the program's memory when the program quits. Even in Listing 20-5, the free() function is redundant.

Where the free() function is vital is in functions or elsewhere that temporary memory is allocated. When the program is done using the memory, it must be freed or else it accumulates and hogs system resources. An example of using free() in this manner is provided later in this chapter, in Listing 20-8.

# Lists That Link

At the intersection of Structure Street and Pointer Place, you find a topic known as the linked list. It's an array of structures, like a database. The big difference is that each structure is carved out of memory one at a time, like hewing blocks of marble to build an elaborate temple. It's a marvelously nerdy topic and an excellent demonstration of how pointers can be useful. Linked lists put the malloc() function to the test.

# Allocating space for a structure

As a C language data storage thingy, a structure can be allocated storage just like any other C language data type. The malloc() function uses the structure's definition to allocate memory. The address returned is assigned to a structure pointer variable. The operation works as you'd expect — except for one thing: Instead of a period used to reference structure members, allocated structures use the structure pointer operator, which looks like this: -> .