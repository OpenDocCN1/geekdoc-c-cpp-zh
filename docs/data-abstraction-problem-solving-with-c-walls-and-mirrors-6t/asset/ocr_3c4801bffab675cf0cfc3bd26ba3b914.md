# # Exceptions

# ## Contents

+   - C3.1 Background 228
+   - C3.1.1 A Problem to Solve 228
+   - C3.2 Assertions 229
+   - C3.3 Throwing Exceptions 230
+   - C3.4 Handling Exceptions 233
+   - C3.4.1 Multiple catch Blocks 235
+   - C3.4.2 Uncaught Exceptions 236
+   - C3.5 Programmer-Defined Exception Classes 239

# ## Prerequisites

+   - C++ Interlude 1
+   - C++ Classes

Exceptions provide a mechanism in C++ and other programming languages for interrupting program execution when errors, unusual circumstances, or other events occur. An **exception** is an object that signals the rest of the program that something unexpected has happened. Our code can react appropriately to the exception based on its type and what the exception can tell us via its methods. We **handle** the exception when we detect and react to it.

Some exceptions indicate mistakes in your code. By correcting those mistakes, you avoid the exceptions and no longer have to worry about them. In fact, your final code gives no indication that an exception could occur. Furthermore, if your code is entirely correct, an exception will not occur. On the other hand, you can intentionally cause an exception. In fact, the programmers who wrote the code for the C++ Standard Library did so. At the very least, we need to know about exceptions so we can use the methods in the Standard Library.

What should we do when an exception occurs? Should we ever intentionally cause an exception in our own programs, and if so, how would we do so? These are some of the questions that this interlude will answer. This knowledge will be particularly important when we implement the ADT stack in the next chapter.