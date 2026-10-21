formatting statements to be specified before output or input. Most of the cases, however, need formatting.

+   - There are two different ways of formatting in C++, namely, using ios member functions and using manipulators.
+   - The ios functions return the original format, whereas manipulators are more flexible and are easy to use.
+   - The function width() is similar to setw() manipulator, fill() is similar to setfill() manipulator, and so on.

+   - The ios functions include the setf() function. This function can be used for a variety of purposes. It has two versions, one with a single argument and the other with two arguments.
+   - There is a member function flags(), which returns flag settings.
+   - It is also possible to construct our own manipulators and use them wherever needed in the program.

# KEYWORDS

Device drivers These are routines written by the device manufacturer to make it work when plugged with the computer.

Format functions from ios These functions are defined in the ios_base class and are useful in formatting. Being member functions, they are called by following a dot (.) after the cout object.

Manipulators These are functions that are non-members but provide similar formatting mechanism as ios functions.

Namespace This is a kind of enclosure for functions, classes, and variables to separate them from other entities.

Shorthand manipulators There are some manipulators that work as a shorthand to the longer versions, for example, using boolalpha for setiosflags(ios::boolalpha). These are called shorthand manipulators.

Stream A stream is a conceptual pipe-like structure, which can have one end attached to the program and the other end attached by default to a keyboard, screen, or file. It is possible to change where one end is pointing to, while keeping the other end as it is.

# EXERCISES

# Multiple Choice Questions

1. C++ I/O is __________ to use compared to C I/O.
(a) easier
(b) harder
(c) moderate
(d) never easy

2. Which of the following functions is used to specify the precision of the floating number?
(a) width()
(b) precision()
(c) setf()
(d) unsetf()

3. Which of the following functions undo the operations done by setf()?
(a) width()
(b) precision()
(c) setf()
(d) unsetf()

4. After every set and respective display, we have a call to the __________ function to revoke the effect of applying the format flag.
(a) setf()
(b) unsetf()
(c) clear()
(d) Any of the above

5. __________ are conceptually pipe-like constructs for providing I/O.
(a) Files
(b) Devices
(c) Both
(d) None

6. What will be the output from the following statements? (S indicates space)
cout.width(5);
cout << "C++";
cout.width(5);
cout << "C++";
(a) SSSSSSC++C++
(b) SSC++SSC++
(c) SSSSSC++C++
(d) SSSSSC++SSSSSC++

7. We can write __________ and use it in the program.
(a) our own manipulator
(b) our own ios function