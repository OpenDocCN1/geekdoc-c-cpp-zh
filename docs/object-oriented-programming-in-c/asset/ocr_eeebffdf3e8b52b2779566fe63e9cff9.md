```
.....
     /* Function body */
.....
}
```

When the function is called, control is transferred to the first statement in the function body. The other statements in the function body are then executed and control returns to the main program when the closing brace is encountered. C++ is no exception. Functions continue to be the building blocks of C++ programs. In fact, C++ has added many new features to functions to make them more reliable and flexible. Like C++ operators, a C++ function can be overloaded to make it perform different tasks depending on the arguments passed to it. Most of these modifications are aimed at meeting the requirements of object-oriented facilities.

In this chapter, we shall briefly discuss the various new features that are added to C++ functions and their implementation.

# 4.2 The Main Function

C does not specify any return type for the main() function which is the starting point for the execution of a program. The definition of main() would look like this:

```
main()
{
    // main program statements
}
```

This is perfectly valid because the main() in C does not return any value.

In C++, the main() returns a value of type int to the operating system. C++, therefore, explicitly defines main() as matching one of the following prototypes:

```
int main();
int main(int argc, char * argv[]);
```

The functions that have a return value should use the return statement for termination. The main() function in C++ is, therefore, defined as follows:

```
int main()
{
    .....
    .....
    return 0;
}
```

Since the return type of functions is int by default, the keyword int in the main() header is optional. Most C++ compilers will generate an error or warning if there is no return