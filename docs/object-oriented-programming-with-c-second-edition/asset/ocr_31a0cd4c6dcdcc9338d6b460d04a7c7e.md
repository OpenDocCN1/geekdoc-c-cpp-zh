```
*/
void abc() 
{
int * IPtr;
IPtr = new int;
/*
rest of the abc() function
*/
}
/*End of memleak.cpp*/
```

The following statement executes from within the abc() function which is called from the main() function.

**Statement:** IPtr = new int;

As a result, the following scenario emerges.

![](bbox=[0.348, 0.366, 0.755, 0.493])

The new operator allocates memory in the heap to hold one integer type value. Suppose the block from the byte with address 5972 to the byte gets allocated. The new operator returns the base address of the block 5972. This value gets stored in IPtr. After abc() finishes execution, memory for IPtr is deallocated. But, the memory in the heap area remains locked up as an orphan (unreferenced) locked up of memory.

![](bbox=[0.388, 0.606, 0.663, 0.693])

**Figure 3.3** Memory leak

As it can be seen from Figure 3.3, after the abc() function terminates, four bytes of memory are lost. They have not been returned to the OS, they remain locked up. This is known as a memory leak. If more memory is required, the OS will **not** allocate this block of memory. Moreover, this block of memory cannot be accessed since the only pointer (IPtr) that was pointing at it has itself been removed from the stack.

This block of memory is no longer of any use and can be returned to the OS. A dynamically allocated block of memory can be deallocated by passing the pointer pointing to operate as the `delete` operator. For example, the following statement should be inserted before the end of the abc() function in Listing 3.5.

```
delete IPtr;
```