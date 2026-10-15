# Phase 5: Loading

Before a program can be executed, it must first be placed in memory. This is done by the loader, which takes the executable image from disk and transfers it to memory. Additional components from shared libraries that support the program are also loaded.

# Phase 6: Execution

Finally, the computer executes the program.

# Problems That May Occur at Execution Time

Each of the preceding phases can fail because of various errors that we discuss throughout the book. This would cause the C++ program to display an error message. If this occurs, you would have to return to the edit phase, make the necessary corrections and proceed through the remaining phases again to determine that the corrections fix the problem(s).

Most programs in C++ input and/or output data. Certain C++ functions take their input from cin (the standard input stream; pronounced “see-in”), which is normally the keyboard, but cin can be redirected to another device. Data is often output to cout (the standard output stream; pronounced “see-out”), which is normally the computer screen, but cout can be redirected to another device. When we say that a program prints a result, we normally mean that the result is displayed on a screen. Data may be output to other devices, such as disks and hardcopy printers. There is also a standard error stream referred to as cerr. The cerr stream (normally connected to the screen) is used for displaying error messages. It is common for users to assign cout to a device other than the screen while keeping cerr assigned to the screen, so that normal outputs are separated from errors.

# Common Programming Error 1.1

Errors such as division by zero occur as a program runs, so they are called runtime errors or execution-time errors. Fatal runtime errors cause programs to terminate immediately without having successfully performed their jobs. Nonfatal runtime errors allow programs to run to completion, often producing incorrect results. [Note: On some systems, divide-by-zero is not a fatal error. Please see your system documentation.]

# 1.6 Notes About C++ and C++ for Programmers

Experienced C++ programmers sometimes take pride in being able to create weird, contorted, convoluted uses of the language. This is a poor programming practice. It makes programs more difficult to read, more likely to behave strangely, more difficult to test and debug, and more difficult to adapt to changing requirements. The following is our first Good Programming Practice.

# Good Programming Practice 1.1

Write your C++ programs in a simple and straightforward manner. This is sometimes referred to as KIS (“keep it simple”). Do not “stretch” the language by trying bizarre usages.

You have heard that C and C++ are portable languages, and that programs written in C and C++ can run on many different computers. Portability is an elusive goal. The ANSI C standard document contains a lengthy list of portability issues, and complete books have been written that discuss portability.