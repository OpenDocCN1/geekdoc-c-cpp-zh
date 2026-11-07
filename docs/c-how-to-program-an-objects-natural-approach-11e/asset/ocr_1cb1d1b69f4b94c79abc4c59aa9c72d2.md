When an exception is thrown from the constructor for an object created in a *new* expression, the dynamically allocated memory for that object is released.

# ### Do Not Throw Exceptions While Holding a Raw Pointer to Dynamically Allocated Memory

Section 11.5 showed that a `unique_ptr` enables you to ensure that dynamically allocated memory is properly deallocated regardless of whether the `unique_ptr` goes out of scope due to the normal flow of control or an exception. When managing dynamically allocated memory via old-style raw pointers (as might be the case in legacy C++ code), do not allow uncaught exceptions to occur before you release the memory.<sup>39</sup> For example, suppose a function contained the following series of statements:

```
```cpp
int* ptr{new int[100]}; // acquire dynamically allocated memory
processArray(ptr); // assume this function might throw an exception
delete[] ptr; // return the memory to the system
// ...
```
```

A memory leak would occur if `processArray` throws an exception—the code would not reach the `delete[]` statement. To prevent this leak, you’d have to catch the exception and delete the memory before allowing the exception to propagate back to the caller. Instead, you should manage memory with `unique_ptr`, as discussed in Chapter 11.

# ## 12.8.1 *new* Throwing `bad_alloc` on Failure

Figure 12.6 demonstrates *new* throwing `bad_alloc` when *new* fails to allocate memory.<sup>40</sup> The `for` statement (lines 15–19) inside the `try` block iterates through the array of `unique_ptr` objects named *items* and allocates to each element an array of 500,000,000 doubles. Our primary test computer has 32 GB of RAM and eight TB of disk space. We had to allocate enormous numbers of elements to force dynamic memory allocation to fail. We used a separate test machine with 16 GB of RAM and 256 GB of disk space to produce this program’s output and still had to allocate five billion doubles to induce a memory allocation failure. You might be able to specify fewer than 500,000,000 on your system. If *new* fails during a call to `make_unique` and throws a `bad_alloc` exception, the loop terminates. The program continues in line 21, where the `catch` handler catches and processes the exception. Lines 22–23 print “Exception occurred:” followed by the message returned from function `what`. Typically, this is an implementation-defined exception-specific message, such as “bad allocation” or “`std::bad_alloc`”. The output shows that the program performed only 10 iterations of the loop before *new* failed and threw the `bad_alloc` exception. Your output might differ based on your system’s physical memory, the disk space available for virtual memory on your system and the compiler you’re using.

> > 39. C++ Core Guidelines, “E.13: Never Throw While Being the Direct Owner of an Object.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Re-never-throw.

> > 40. This program’s output was produced using Visual C++ on Windows. The executables produced by both g++ and clang++ resulted in the message “killed” rather than a `bad_alloc` exception.