# Output

```
Inside the function
Inside try block
There is an uncaught exception in process when message is within the try block
Caught dummy
There is no uncaught exception in process when message is not a part of the try block
```

# How the Program Works

This program contains two different objects of TestClass. One object is initialized before the try block starts and the other is initialized within the try block. When the exception is thrown by the statement

```
throw dummy;
```

the objects defined within the try block have to be destroyed (the stack rewinding process), and so, their destructors are called in the reverse order of their initialization. We have only one object TestObject2 defined within the try block, so its destructor is called. At this point, the exception handling is in process, so the uncaught_exception() function returns true. When the exception is handled by the catch block, it would display "Caught dummy" and then the ExGen() function is over. The destructor for TestObject1 is called next, which now goes out of scope. In this case, the uncaught_exception() would yield false, because now the exception has been handled and no more exception is in process.

Note that *this is used as a string to be printed in the destructor. It is a handy way of finding out which object is going out of scope. The TestClass can be easily converted to a string class with more member functions. We have also seen how destructors are used in such classes. A destructor is needed here because we use dynamic constructor to get the memory, and it is our job then to return that memory when the object goes out of scope.

# 8.14 EXCEPTION HANDLERS AND DEBUGGERS

Some systems such as VC++ have a debugger in place. Sometimes the roles of a debugger and the exception handling system clash and overlap. When an error occurs, the debugger needs all the objects to indicate the user about the problem and the status of all those objects at that point of time.

On the other hand, the exception handling system has to delete those objects because of the compulsion to call the destructors. This system need not be aware of the place where the error has occurred and when the exception was thrown. However, the debugger must be aware of such details and help the user out in such circumstances.

Due to mutually conflicting requirements, the C++ compilers that provide debuggers may not provide all the facilities of exception handling. One must refer to the documentation available with the respective compiler for such details.

# 8.15 DRAWBACKS OF EXCEPTION HANDLING

Uncertain termination is a major drawback of the exception handling mechanism. When library functions are used and the user is unaware of some specific exception, the program would crash if that exception is thrown. Whenever third-party libraries are being used, there is the danger of a program crash. If it cannot be afforded, one cannot use those libraries.

Another disadvantage of exception handling is the overhead. With exception handling, both the executable program code size and the execution time would increase substantially. Simpler