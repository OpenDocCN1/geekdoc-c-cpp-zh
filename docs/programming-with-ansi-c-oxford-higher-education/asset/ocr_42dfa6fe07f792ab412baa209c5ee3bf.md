A library user must be aware of the type and nature of exceptions thrown by the functions he/she uses. If the user fails to take account of an exception, the program may terminate abnormally.

A polymorphic object, when thrown, can be caught by its own catch statement or the base class from which it is derived.

When we have two exceptions thrown at the same point of time, the program terminates abnormally.

programs such as Program 8.1. However, it becomes complicated if a function called from the try block throws an exception in the body of the function itself and does not have an appropriate catch block in its body. The programmer needs to provide an error handler in this case. One may assume that such cases are rare but it is not so. Most of the exceptions are thrown by the functions and are not caught by them. The onus is on the calling function to decide what to do when a specific exception is thrown.

Take the case of the new operator. The library implementation of new does not have a catch for a case when memory is not allocated. The operator new just throws an exception of type bad_alloc. It is up to the programmer to provide a catch block for it. If third-party functions are called in a program, a user needs to be aware of the exceptions that might be thrown from those functions and must provide appropriate error handlers for them. Failing to provide a proper exception handler leads to sudden crashes of programs much to the dislike of the users. Thus, it is imperative appropriate handlers are written when exceptions are expected.

In the real sense, the exception handling mechanism is an error-reporting mechanism from the library creator to the user, as mentioned earlier. Both the designers and the programmers are unaware of each other. Exception handling is a standardized mechanism to help them communicate about anomalies. It is imperative that the user of library functions be able to know the type and nature of the exceptions thrown from those functions.

# 8.5.2 Finding Proper Handlers for Polymorphic Objects

It will be seen in Chapter 9 that it is possible to inherit a class into another class. It is possible to access a derived class object by a base class pointer. The object pointed to by such a pointer is known as a polymorphic object. Whenever a polymorphic object of a derived class is thrown, it can be caught either by the base class or by the derived class. This is a challenging task. We defer this discussion until we study inheritance in Chapter 9.

# 8.5.3 Backtracking until Beginning of try Block

It is important to understand that when an exception is thrown, the control, before being passed to the catch block, travels backwards in the try block, and destroys all the objects generated in due course. This helps in restoring consistency, which was discussed earlier. A programmer must take care while writing destructors for objects (if a destructor is required for properly destroying the object) and place them in the try block to ensure consistency. It is also important to note that these destructors should not throw exceptions themselves in such cases. If one exception is not handled and another exception is thrown, the system has no other option but to terminate the program abnormally, as it is not capable of handling more than one exception at the same point of time.

# 8.6 THROWING WITHIN AND OUTSIDE FUNCTIONS

We have seen that we can throw an exception in the function that is caught outside the function under consideration but handled in the calling function. If this exception is not caught by the calling function, it may be caught by a function that has called this calling function. This is true for any level of hierarchy.