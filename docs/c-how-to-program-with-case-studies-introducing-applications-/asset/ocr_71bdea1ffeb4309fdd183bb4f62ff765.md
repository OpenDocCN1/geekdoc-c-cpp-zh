+   - An array name can be treated as a pointer and used in pointer arithmetic expressions that do not attempt to modify the pointer's value.
+   - Pointers can be subscripted (p. 334) like arrays. This is referred to as pointer/subscript notation.
+   - A parameter of type const char * typically represents a constant string.

# Section 7.10 Arrays of Pointers

+   - Arrays may contain pointers (p. 338). A common use of an array of pointers is to form an array of strings (p. 338). Each element is a string, but a C string is essentially a pointer to its first character. So, each element is actually a pointer to the first character of a string.

# Section 7.12 Function Pointers

+   - A function pointer (p. 347) contains the address of a function in memory. A function name is really the starting address in memory of the code that performs the function's task.
+   - Pointers to functions can be passed to functions, returned from functions, stored in arrays assigned to other function pointers and compared with one another for equality or inequality.
+   - A pointer to a function is dereferenced to call the function. A function pointer can be used directly as the function name when calling the function.
+   - A common use of function pointers is in menu-driven systems.

# Self-Review Exercises

7.1 Answer each of the following:

+   - a) A pointer variable contains as its value another variable's ______.
+   - b) Three values can be used to initialize a pointer—__________, __________ and __________.
+   - c) The only integer that can be assigned to a pointer is __________.

7.2 State whether the following are true or false. If the answer is false, explain why.

+   - a) A pointer that's declared to be void can be dereferenced.
+   - b) Pointers of different types may not be assigned to one another without a cast operation.

7.3 Answer each of the following. Assume that single-precision floating-point numbers are stored in four bytes, and that the array's starting address is location 1002500 in memory. Each part of the exercise should use the results of previous parts where appropriate.