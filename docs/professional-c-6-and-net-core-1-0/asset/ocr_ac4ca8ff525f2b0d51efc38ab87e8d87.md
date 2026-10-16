Framework? For example, file types (discussed in Chapter 23, “Files and Streams”), wrap a native file handle. This file handle needs to be released. To release this handle early, it’s good to know the `IDisposable` interface and the `using` statement that’s explained in this chapter.

This chapter starts with various aspects of memory management and memory access. A good understanding of memory management and knowledge of the pointer capabilities provided by C# will better enable you to integrate C# code with legacy code and perform efficient memory manipulation in performance-critical systems.

# # Memory Management Under the Hood

One of the advantages of C# programming is that the programmer does not need to worry about detailed memory management; the garbage collector deals with the problem of memory cleanup on your behalf. As a result, you get something that approximates the efficiency of languages such as C++ without the complexity of having to handle memory management yourself as you do in C++. However, although you do not have to manage memory manually, it still pays to understand what is going on behind the scenes. Understanding how your program manages memory under the covers will help you increase the speed and performance of your applications. This section looks at what happens in the computer’s memory when you allocate variables.

> > **NOTE** *The precise details of many of the topics of this section are not presented here. This section serves as an abbreviated guide to the general processes rather than as a statement of exact implementation.*

# ## Value Data Types

Windows uses a system known as *virtual addressing*, in which the mapping from the memory address seen by your program to the actual location in hardware memory is entirely managed by Windows. As a result, each process of a 32-bit application sees 4GB of available memory, regardless of how much hardware memory you actually have in your computer (with 64-bit applications on 64-bit processors this number is greater). This memory contains everything that is part of the program, including the executable code, any DLLs loaded by the code, and the contents of all variables used when the program runs. This 4GB of memory is known as the *virtual address space* or *virtual memory*. For convenience, this chapter uses the shorthand *memory*.