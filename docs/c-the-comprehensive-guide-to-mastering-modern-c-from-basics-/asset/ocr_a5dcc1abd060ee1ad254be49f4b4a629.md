+   - Smart pointers unique_ptr and shared_ptr
Pointer types of the standard library following the RAII concept, which save you from explicit the deallocation.
- move
Turning a named value into a temp-value, making it movable.
- C-array
A C-array contains multiple elements of the same type and is declared with square brackets.
- Pointer arithmetic
Addition, increment, and similar operations with raw pointers in a C-array.
- C-array decay
A C-array loses its size information when passed to a function.
- Iterator
The abstract concept of pointers, applied to standard containers.

Through character strings, you have already had a bit to do with pointers. You have always passed their literals around as const char*. And when you call main with arguments, the arguments are packed into a C-array of this type—that is, const char[]. In this chapter, you will learn more about these constructs. They are not easy to understand but enable all sorts of useful things. However, you must use them correctly so that they do