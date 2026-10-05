# Exception Handling

In order to overcome this problem, classes whose objects function like pointers should be devised. Obviously, such objects will have pointers embedded in memory. Memory will be allocated dynamically for these pointers during the lifetime of the objects. This memory will be deallocated through the destructor. Thus, when the object is destroyed, the memory locked up and referenced by the embedded pointer will be destroyed.

# Summary

Statements to detect conditions that prohibit further execution of the library function and should be placed within the library function itself. Statements to take appropriate action when such conditions are detected and should be placed in the functions that call these library functions.

append the try block with a series of catch blocks, one for each of the exceptions expected to be thrown.

Since the number of fundamental data types is limited, it is better to throw objects of exception classes created specifically for the purpose. These objects can be initialized with appropriate information before being thrown by the library functions. This information can be accessed within the corresponding catch block of the application program.

Exception handling enables the library function to notify the detected invalid conditions to the user using the throw statement. The program terminates prematurely if the application ignores such notifications. Application program can catch notifications in a try block and take appropriate action in a catch block.

Uncaught exceptions can be caught by the catch(...). Exceptions can be re-thrown. During unwinding of the stack, memory acquired by the objects themselves is destroyed. However, the memory acquired dynamically by the pointers embedded in these objects remains locked up. This is a limitation of exception handling.

Library functions announce the list of all possible exceptions that they throw by enrolling them in their headers. Appropriately, the application program should call these functions in a try block and

# Key Terms

+   exception handling
C-style solutions for exception handling
try
catch

+   throw
catching uncaught exceptions
exception classes
unwinding of the stack

# Exercises

+   1. What is exception handling? The need is for exception handling?
2. What is the negative impact if the library programmer simply terminates an application upon detecting an error condition?
3. Which three keywords are provided by C++ for implementing exception handling?
4. What happens if the application does not catch the exception thrown by a library function?

+   5. Explain how the stack is unwound when an exception is thrown.
6. What is the need to catch objects instead of values of fundamental types?
7. Why are nested exception classes needed?
8. How are uncaught exceptions caught?
9. What is the limitation of exception handling in C++?