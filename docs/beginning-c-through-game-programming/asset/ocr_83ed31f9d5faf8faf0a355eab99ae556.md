An important point to understand here is that the two previous statements free the memory on the heap, but they do not directly affect the local variables pHeap and pHeap2. This creates a potential problem because pHeap and pHeap2 now point to memory that has been returned to the heap, meaning that they point to memory that the computer can use in some other way at any given time. Pointers like this are called dangling pointers and they are quite dangerous. You should never attempt to dereference a dangling pointer. One way to deal with dangling pointers is to assign 0 to them, and that's what I do with the following lines, which reassign both dangling pointers so they no longer point to some memory to which they should not point.

```
pHeap = 0;
pHeap2 = 0;
```

Another good way to deal with a dangling pointer is to assign a valid memory address to it.

# Trap

> Using delete on a dangling pointer can cause your program to crash. Be sure to set a dangling pointer to 0 or reassign it to point to a new, valid chunk of memory.

# Avoiding Memory Leaks

One problem with allowing a programmer to allocate and free memory is that he might allocate memory and lose any way to get at it, thus losing any way to ever free it. When memory is lost like this, it's called a memory leak. Given a large enough leak, a program might run out of memory and crash. As a game programmer, it's your responsibility to avoid memory leaks.

I've written two functions in the Heap program that purposely create memory leaks in order to show you what not to do when using dynamic memory. The first function is leak1(), which simply allocates a chunk of memory on the heap for an int value and then ends.

```
```cpp
void leak1()
{
    int* drip1 = new int(30);
}
```
```