# Chapter 4 Compound Types

covers by requesting the right number of bytes with new. Finally, the function returns pn, the address of the string copy.

In main(), the return value (the address) is assigned to the pointer name.This pointer points to the block of memory allocated in the getname() function-defined in main(), but the program prints the string and the address of the string.

Next, after it frees the block pointed to by name, main() calls getname() a second time. C++ doesn't guarantee that newly freed memory is the first to be chosen next time memory is used, and in this sample run, it isn't.

Note this that getname() allocates memory and main() frees it. It's usually not a good idea to put new and delete in separate functions because that makes it easier to forget to use delete. But this does separate new from delete to show that it is possible.

To appreciate some of the more subtle aspects of this program, you should know a little about how C++ handles memory. So let's preview some material that's covered fully in Chapter 9.

# Automatic Storage, Static Storage, and Dynamic Storage

C++ has three ways of managing memory for data, depending on the method used to allocate memory: automatic storage, static storage, and dynamic storage, sometimes called the free store or heap. Data allocated in these three ways differ from each other how long they remain in existence.We'll take a quick look at each. (C++11 adds a fourth called thread storage that we'll discuss briefly in Chapter 9.)

# Automatic Storage

Ordinary variables defined inside a function use automatic storage and are called automatic variables. These terms mean that the variables come into existence automatically when the function containing them is invoked, and expire when the function terminates. For example, the temp array in Listing 4.2 exists exists while the getname() function is active. When program control returns to main(), the memory used for temp is freed automatically. If getname() returned the address of temp, the name pointer in main() would be left pointing to a memory location that would soon be reused. One reason you have to use new in getname(). Actually, automatic values are local to the block that contain them. A block is a section of code enclosed between braces. So, all our blocks have even functions.

If you define a variable inside one of those blocks, it exists only while the program is executing statements inside the block.

Automatic variables typically are stored on a stack. This means that when program execution enters a block of code, its variables are added consecutively to the stack in memory and then are freed in reverse order when execution leaves the block. (This is called a last-first-out, or LIFO, process.) So the stack grows and shrinks as execution proceeds.