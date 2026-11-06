# Section 8.4 Pass-by-Reference with Pointers

+   - When calling a function with a variable that the caller wants the called function to modify, the address of the variable may be passed. The called function then uses the indirection operator `(*)` to dereference the pointer and modify the value of the variable in the calling function.
+   - A function receiving an address as an argument must have a pointer as its corresponding parameter.