# PROGRAMMING TIP

# USE EXIT_SUCCESS IN A MAIN PROGRAM

When the temperature program finishes, it executes the statement:

```
return EXIT_SUCCESS;
```

This return statement ends the main program and also sends the value of the constant EXIT_SUCCESS back to your computer's operating system. The operating system is the software that is responsible for running all programs on your computer. Although you may not realize it, the operating system is able to take further actions based on the return value from a main program. For example, the return value of EXIT_SUCCESS tells the operating system that the program ended normally, and the operating system can then proceed with its next task. Other return values tell the operating system about abnormal terminations such as problems opening files or running out of memory. The EXIT_SUCCESS constant is defined in cstdlib (or stdlib.h). For most operating systems, this constant is defined as zero (which is why you may have used return 0 in other programming).

By the way, a program can also return another constant, EXIT_FAILURE, as a simple way of indicating non-normal completion.

# C++ FEATURE

# EXCEPTION HANDLING

The C++ language provides built-in support for handling unusual situations, known as “exceptions,” which may occur during the execution of your program. Exception handling is commonly used to handle run-time errors. It is a very good alternative to traditional techniques of error handling, which are often inadequate, error-prone, and ad hoc. Once you have a program working for the core situation where things always go as planned, you can use the C++ exception handling facilities to add code for unusual cases. Please refer to Appendix L for more information about these facilities. In order to focus on data structures, formal exception handling is not incorporated into the examples in this book.

# Self-Test Exercises for Section 1.1

Each section of this book finishes with a few self-test exercises. Answers to these exercises are given at the end of each chapter.

+   1. What are two considerations for selecting good subtasks?

+   2. What are the elements of a C++ function prototype?

+   3. This exercise refers to a function that Jervis has written for you to use. The prototype and precondition/postcondition contract are shown at the top of the next page.