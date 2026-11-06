# Section 17.9 Class `unique_ptr`
and Dynamic Memory Allocation

+   - If an exception occurs after successful memory allocation but before the `delete` statement executes, a memory leak could occur.
+   - The C++ Standard Library provides class template `unique_ptr` (p. 772) to deal with memory leaks.
+   - An object of class `unique_ptr` maintains a pointer to dynamically allocated memory. A `unique_ptr`’s destructor performs a `delete` operation on the `unique_ptr`’s pointer data member.
+   - Only one `unique_ptr` at a time can refer to the managed dynamic memory.
+   - Class template `unique_ptr` provides overloaded operators `*` and `->` so that a `unique_ptr` object can be used just as a regular pointer variable is. A `unique_ptr` also transfers ownership of the dynamic memory it manages via its copy constructor and overloaded assignment operator.