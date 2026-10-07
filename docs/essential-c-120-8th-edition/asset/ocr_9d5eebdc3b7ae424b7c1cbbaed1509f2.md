# Chapter 23: Platform Interoperability and Unsafe Code

Potentially you might need to fix an object in place in one method body and have it remain fixed until another method is called; this is not possible with the fixed statement. If you are in this unfortunate situation, you can use methods on the GCHandle object to fix an object in place indefinitely. You should do so only if it is absolutely necessary, however fixing an object for a long time makes it highly likely that the garbage collector will be unable to efficiently compact memory.

# Allocating on the Stack

You should use the fixed statement on an array to prevent the garbage collector from moving the data. However, an alternative is to allocate the array on the call stack. Stack allocated data is not subject to garbage collection or to the finalizer patterns that accompany it. Like reference types, the requirement is that the stackalloc is an array of unmanaged types. For example, instead of allocating an array of bytes on the heap, you can place it onto the call stack, as shown in Listing 23.16.

> LISTING 23.16: Allocating Data on the Call Stack

```
byte* bytes = stackalloc byte[42];
```

The data type is an array of unmanaged types, the runtime allocate a fixed buffer size for the array and restore buffer before the pointer gets out of scope. Specifically, it allocates sizeof(T) * E, where E is the array size and T is the reference type. Given the requirement of using stackalloc only on an array of unmanaged types, the runtime restores the buffer to the system by simply unwinding the stack, thereby eliminating the complexities of iterating over the f-reachable queue (the "Garbage Collection" section and discussion of finalization in Chapter 10) and compacting data. Thus, there is no way to explicitly free stackalloc data.

The stack is a precious resource. Although it is small, running out of stack space will have a big effect—namely, the program will crash. For this reason, you should make every effort to avoid running out stack space. Back space, the best thing that can happen is for the program to shut down/crash immediately. Generally, programs have less than 1MB of stack space (and possibly a