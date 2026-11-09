
System.Diagnostics.Contracts.ContractReferenceAssemblyAttribute applied to the assembly's assembly definition metadata table. The CCRewrite.exe tool and the CCCheck.exe tool can use contract reference assemblies as input when these tools are performing their instrumentation and analysis.

The last tool, the Code Contract Document Generator tool (CCDocGen.exe), adds contract information to the XML documentation files already produced by the C# compiler when you use the compiler's /doc:File switch. This XML file, enhanced by the CCDocGen.exe tool, can be processed by Microsoft's Sandcastle tool to produce MSDN-style documentation that will now include contract information.

## Chapter 21: The Managed Heap and Garbage Collection

- In this chapter:
  - Managed Heap Basics ........ 502
  - Generations: Improving Performance ........ 510
  - Working with Types Requiring Special Cleanup ........ 522
  - Monitoring and Controlling the Lifetime of Objects Manually ........ 542

In this chapter, I’ll discuss how managed applications construct new objects, how the managed heap controls the lifetime of these objects, and how the memory for these objects gets reclaimed. In short, I’ll explain how the garbage collector in the common language runtime (CLR) works, and I’ll explain various performance issues related to it. I’ll also discuss how to design applications so that they use memory most efficiently.

### Managed Heap Basics

Every program uses resources of one sort or another, be they files, memory buffers, screen space, network connections, database resources, and so on. In fact, in an object-oriented environment, every type identifies some resource available for a program’s use. To use any of these resources requires memory to be allocated to represent the type. The following steps are required to access a resource:

1. Allocate memory for the type that represents the resource (usually accomplished by using C#’s new operator).
2. Initialize the memory to set the initial state of the resource and to make the resource usable. The type’s instance constructor is responsible for setting the initial state.
3. Use the resource by accessing the type’s members (repeating as necessary).
4. Tear down the state of a resource to clean up.
5. Free the memory. The garbage collector is solely responsible for this step.

This seemingly simple paradigm has been one of the major sources of problems for programmers that must manually manage their memory, for example, native C++ developers. Programmers responsible for managing their own memory routinely forget to free memory causing a memory leak. In addition, these programmers frequently use memory after having released it, causing their program to experience memory corruption resulting in bugs and security holes. Furthermore, these two bugs are worse than most others because you can’t predict the consequences or the timing of them. For other bugs, when you see your application misbehaving, you just fix the line of code that is not working.

As long as you are writing verifiably type-safe code (avoiding C#’s unsafe keyword), then it is impossible for your application to experience memory corruption. It is still possible for your application to leak memory but it is not the default behavior. Memory leaks typically occur because your application is storing objects in a collection and never removes objects when they are no longer needed.

To simplify things even more, most types that developers use quite regularly do not require Step 4 (tear down the state of the resource to clean up). And so, the managed heap, in addition to abolishing the bugs I mentioned, also provides developers with a simple programming model: allocate and initialize a resource and use it as desired. For most types, there is no need to clean up the resource and the garbage collector will free the memory.

When consuming instances of types that require special cleanup, the programming model remains as simple as I’ve just described. However, sometimes, you want to clean up a resource as soon as possible, rather than waiting for a GC to kick in. In these classes, you can call one additional method (called `Dispose`) in order to clean up the resource on your schedule. On the other hand, implementing a type that requires special cleanup is quite involved. I describe the details of all this in the “Working with Types Requiring Special Cleanup” section later in this chapter. Typically, types that require special cleanup are those that wrap native resources like files, sockets, or database connections.

#### Allocating Resources from the Managed Heap

The CLR requires that all objects be allocated from the managed heap. When a process is initialized, the CLR allocates a region of address space for the managed heap. The CLR also maintains a pointer, which I’ll call `NextObjPtr`. This pointer indicates where the next object is to be allocated within the heap. Initially, `NextObjPtr` is set to the base address of the address space region.

As region fills with non-garbage objects, the CLR allocates more regions and continues to do this until the whole process’s address space is full. So, your application’s memory is limited by the process’s virtual address space. In a 32-bit process, you can allocate close to 1.5 gigabytes and in a 64-bit process you can allocate close to 8 terabytes.

C#’s new operator causes the CLR to perform the following steps:

1. Calculate the number of bytes required for the type’s fields (and all the fields it inherits from its base types).
2. Add the bytes required for an object’s overhead. Each object has two overhead fields: a type object pointer and a sync block index. For a 32-bit application, each of these fields requires 32 bits, adding 8 bytes to each object. For a 64-bit application, each field is 64 bits, adding 16 bytes to each object.
3. The CLR then checks that the bytes required to allocate the object are available in the region. If there is enough free space in the managed heap, the object will fit, starting at the address pointed to by `NextObjPtr`, and these bytes are zeroed out. The type’s constructor is called (passing `NextObjPtr` for the `this` parameter), and the new operator returns a reference to the object. Just before the reference is returned, `NextObjPtr` is advanced past the object and now points to the address where the next object will be placed in the heap.

Figure 21-1 shows a managed heap consisting of three objects: A, B, and C. If another object were to be allocated, it would be placed where `NextObjPtr` points to (immediately after object C).

![](img/3f2c86949cdef7e2f9e27c37c607b28e_503_0.png)

**FIGURE 21-1** Newly initialized managed heap with three objects constructed in it.

For the managed heap, allocating an object simply means adding a value to a pointer—this is blazingly fast. In many applications, objects allocated around the same time tend to have strong relationships to each other and are frequently accessed around the same time. For example, it’s very common to allocate a `FileStream` object immediately before a `BinaryWriter` object is created. Then the application would use the `BinaryWriter` object, which internally uses the `FileStream` object. Since the managed heap allocates these objects next to each other in memory, you get excellent performance when accessing these objects due to locality of reference. Specifically, this means that your process’s working set is small, which means your application runs fast with less memory. It’s also likely that your code and all the data it accesses reside in the CPU’s cache. The result is that your application will access these objects with phenomenal speed because the CPU will be able to perform most of its manipulations without having cache misses that would force slower access to RAM.

So far, it sounds like the managed heap provides excellent performance characteristics. However, what I have just described is assuming that memory is infinite and that the CLR can always allocate new objects at the end. However, memory is not infinite and so the CLR employs a technique known as garbage collection (GC) to “delete” objects in the heap that your application no longer requires access to.
