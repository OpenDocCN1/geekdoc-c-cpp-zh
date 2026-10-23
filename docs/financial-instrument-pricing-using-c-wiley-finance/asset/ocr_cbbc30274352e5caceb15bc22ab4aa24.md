```
// Inform runtime that unmanaged memory has been allocated
GC::AddMemoryPressure(N);

// Release unmanaged memory and inform runtime
delete [] darr;
GC::RemoveMemoryPressure(N);
```

This technique should be useful when a mixture of C++/CLI and native C++ code is being used to manage large data structures such as arrays, vectors and matrices, for example.

Some facts relating to garbage collection are useful to summarise at this stage because of the subtle issues involved when working with the CLI (managed) and CRT (C/C++ Runtime) (unmanaged) heaps:

+   1. The garbage collector tracks and reclaims objects that have been allocated in managed memory. It does not recognise references to objects from unmanaged code.
+   2. The garbage collector only frees an object if it concludes that there are no references to that object.
+   3. The garbage collector does not maintain information about resources (for example, file handles or database connections) held by an object. This issue is resolved by implementing a finaliser in a type that uses unmanaged resources. These unmanaged resources must be released before instances of the type are reclaimed.
+   4. The garbage collector supports object aging using generations. A generation is a unit of measure of the relative age of objects in memory. It is possible to force garbage collection of objects in a range of generations.

The goal of this section was to give an impression of how garbage collection works in .NET and the issues that arise when developing code in a mixed C++ environment.

There are two kinds of destructor in C++/CLI. The first kind is concerned with the deallocation of previously allocated memory while the second type is concerned with the deallocation of managed or unmanaged resources.

An object that is allocated on the CLI heap using gcnew needs to be deallocated. The choices are:

+   Call the delete operator on the handle of a ref class object. Then the managed memory will be immediately deallocated in the reverse order to which it was allocated. In this case the programmer has full control of when objects are finally cleaned up.
+   In some cases the programmer does not care when memory is reclaimed. Then it is not necessary to call the delete operator. The CLR will detect that an object is no longer needed and it will garbage collect the memory in due time. Thus, in most cases the use of the delete operator is not needed.

When we call the delete operator on an object handle the corresponding destructor function (if it exists) is called. In the body of the destructor we normally call the delete operator for any object that the ref class needs to clean up. Finally, if a ref class does not allocate memory then there is no need to create a destructor and in these cases a default destructor will be called. We shall see some examples of use when we create .NET wrappers for native C++ objects.