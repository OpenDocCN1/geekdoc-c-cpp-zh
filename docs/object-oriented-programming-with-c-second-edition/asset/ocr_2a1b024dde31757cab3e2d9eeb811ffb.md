# Object-Oriented Programming with C++

the output would be

$ 20

User-defined manipulators enable modularity. A user-defined manipulator can be used throughout an application to format the output in a uniform manner. If a change is required, it needs to be carried out at only one place—the definition of the manipulator—and again the change occurs uniformly throughout the application.

# 7.14 Command Line Arguments

Command line arguments are values that are passed to executables when they are run from the command line. As we know, after successfully compile and link a C++ program we get an executable file. These executable programs can be run from the command line of your computer's operating system.

How do we pass command line arguments to executables? Let us understand this with the help of an example.

Suppose the name of an executable that has been generated from a C++ program is 'test. exe'. We can run this executable by typing the following command on the command line and hitting the enter key:

```
test.exe
```

We can also run the executable by issuing the following command:

```
test.exe
```

We follow the first method for running the executable. (Note that the above two methods would work if the operating system on your computer is not Windows. The method may change for a different operating system. Please consult the operating system's documentation or your lab instructor if the operating system on your computer is not Windows. For the purpose of this book, we will assume that the operating system on your computer is Windows.)

Suppose we want to pass the strings 'abc' and 'def' as command line arguments to the executable. We can do this by calling the executable from the command line as:

```
test def
```

Note that 'abc' and 'def' have been passed as parameters to the command for executing the executable file.
Why are command line arguments important? Why should a C++ programmer write programs that can read the values of command line arguments? Consider a very simple program (Listing 7.29) that adds up two numbers and displays the result.

# Listing 7.29 The programmer can decide the values to be added

```
/*Beginning of add.cpp*/
/
A program in which two numbers are added but it is the
programmer, and not the programmer's user, who decides the
values to be added.
*/
#include <iostream>
void main()
{
```