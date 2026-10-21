# Notes

+   1. It is possible to have an operator implemented as a function in C++. In that case, there will be no advantage if the function is not defined inline.
+   2. Unlike malloc(), new can be overloaded such that class objects can be given memory as per the need and at the place the user wants it. When new is overloaded for any class, calling new with the object of that class follows the process defined by the developer of that class and not by the conventional memory management defined by C++.

# 2.9.5 Significance of delete Operator

The delete operation does not seem to be important when used in programs. The use of delete is not important in places where the machine is shut down at the end of the day, for example, an educational institute. However, there are places where the machine is not shut down daily and the programs continue to run without any halt for a very long period, for example, web servers and related components. In such cases, the memory space occupied by the new variables will continue to increase while the program is running unless they are deleted periodically. At some point of time, the memory will be exhausted and the program will crash. On the other hand, if the machine is shut down, the space occupied is released automatically and there will be no problem of insufficient memory.

# Note

Web servers run for long periods. In such programs, if the objects introduced by new do not have a corresponding delete to be used when they go out of scope, the memory occupied by such objects is not regained and the program crashes when the memory is full. C++11, obviously inspired by Java, added garbage collection; it is a process by which the memory wasted by such objects that have gone out of scope can be reclaimed and problems such as mentioned here can be avoided.

# 2.9.6 New Casting Operators, typeid, and throw

C++ has new function-like castings as well as old C-style castings. To convert an int variable into a float in C, FloatVar = (float) IntVar; is used. However, in C++, this is written as

```
FloatVar = float(IntVar);
```

which is more readable. The old C-style casting is still available and is very popular among programmers.

Four new casting operators have been recently added by the C++ Standardization Committee for providing better casting operations than that offered by the old C-style casting. These are dynamic cast, reinterpret cast, static cast, and const cast. The old C-style cast is still valid in C++, though using new casting operators is recommended. These are discussed in Sections 11.2–11.5 in Chapter 11. typeid also is used in the context of RTTI and throw is used when exception handling is used to trap errors in C++.

The following code illustrates how try, throw, and catch can be used in a given circumstance. The block covered by try is monitored by C++ during the execution of the program. When a throw statement is encountered, the control gets permanently transferred to the corresponding catch statement. In the following case, if throw error1 is executed, the control gets transferred to catch(ErrorType1 er), and if throw error2 is executed, the control gets transferred to catch(ErrorType2 er) block.

```
try
{
    ErrorType1 error1;
```