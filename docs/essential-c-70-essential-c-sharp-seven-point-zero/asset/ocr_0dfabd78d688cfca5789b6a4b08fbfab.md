# **Allocating on the Stack**

You should use the *fixed* statement on an array to prevent the garbage collector from moving the data. However, an alternative is to allocate the array on the call stack. Stack allocated data is not subject to garbage collection or to the finalizer patterns that accompany it. Like referent types, the requirement is that the *stackalloc* data is an array of unmanaged types. For example, instead of allocating an array of bytes on the heap, you can place it onto the call stack, as shown in Listing 21.16.

+   **LISTING 21.16: Allocating Data on the Call Stack**

```csharp
byte* bytes = stackalloc byte[42];
```

Because the data type is an array of unmanaged types, the runtime can allocate a fixed buffer size for the array and then restore that buffer once the pointer goes out of scope. Specifically, it allocates sizeof(T) * E, where E is the array size and T is the referent type. Given the requirement of using *stackalloc* only on an array of unmanaged types, the runtime restores the buffer back to the system by simply unwinding the stack, thereby eliminating the complexities of iterating over the f-reachable queue (see, in Chapter 10, the section titled “Garbage Collection” and the discussion of finalization) and compacting reachable data. Therefore, there is no way to explicitly free *stackalloc* data.

The stack is a precious resource. Although it is small, running out of stack space will have a big effect—namely, the program will crash. For this reason, you should make every effort to avoid running out stack space. If a program does run out of stack space, the best thing that can happen is for the program to shut down/crash immediately. Generally, programs have less than 1MB of stack space (possibly a lot less). Therefore, take great care to avoid allocating arbitrarily sized buffers on the stack.

# **Dereferencing a Pointer**

Accessing the data stored in a variable of a type referred to by a pointer requires that you dereference the pointer, placing the indirection operator prior to the expression. *byte data = *pData;*, for example, dereferences the location of the *byte* referred to by *pData* and produces a variable of type *byte*. The variable provides read/write access to the single *byte* at that location.