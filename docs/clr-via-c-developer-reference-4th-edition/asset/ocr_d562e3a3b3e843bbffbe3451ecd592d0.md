# CHAPTER 21
The Managed Heap and Garbage Collection

+   In this chapter:
Managed Heap Basics ................................................................ 505
Generations: Improving Performance ....................................... 513
Working with Types Requiring Special Cleanup ................ 525
Monitoring and Controlling the Lifetime of Objects
Manually ................................................................................... 545

In this chapter, I'll discuss how managed applications construct new objects, how the managed heap controls the lifetime of these objects, and how the memory for these objects gets reclaimed. In short, I'll explain how the garbage collector in the common language runtime (CLR) works, and I'll explain various performance issues related to it. I'll also discuss how to design applications so that they use most efficiently.

# Managed Heap Basics

Every program uses resources of one sort or another, be they files, memory buffers, screen space, network connections, database resources, and so on. In fact, in an object-oriented environment, every type identifies some resource available for a program's use. To use any of these resources requires memory to be allocated to represent the type. The following steps are required to access a resource:

+   1. Allocate memory for the type that represents the resource (usually accomplished by using C#'s new operator).
2. Initialize the memory to set the initial state of the resource and to make the resource usable. The type's instance constructor is responsible for setting this initial state.
3. Use the resource by accessing the type's members (repeating as necessary).
4. Tear down the state of a resource to clean up.
5. Free the memory. The garbage collector is solely responsible for this step.