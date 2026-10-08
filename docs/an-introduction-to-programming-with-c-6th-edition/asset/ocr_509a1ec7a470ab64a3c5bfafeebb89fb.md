# Void Functions

+   * Variables can be passed to functions either by value (the default) or by reference.
* When you pass a variable by value, only a copy of the value inside the variable is passed to the receiving function. The receiving function is not given access to a variable passed by value, so it cannot change the variable's contents.
* When you pass a variable by value, the computer uses the data type and name of the corresponding formal parameter to create a separate memory location where to store a copy of the value.
* When you pass a variable by reference, the variable's address in memory is passed to the receiving function, allowing the receiving function to change the variable's contents. Only variables can be passed by reference.
* When you pass a variable by reference, the computer locates the variable in memory and assigns the name of its corresponding formal parameter to the memory location. Therefore, the variable will have two names: one assigned by the calling function and the other assigned by the receiving function.
* To pass a variable by reference in a C++ program, you include the address-of-operator (&) before the name of the corresponding formal parameter in the function header. If the function definition appears below the main function in the program, you must also include the address-of-operator in the function prototype. The address-of-operator tells the computer to pass the variable's address rather than its contents.

# Key Terms

&the address-of-operator

**Address-of-operator**—the ampersand; tells the computer to pass a variable's address in memory rather than its contents

**Passing by reference**—refers to the process of passing a variable's address to a function

**Void functions**—functions that do not return a value after completing their assigned task

# Review Questions

+   1. Which of the following is false?
  a. A void function does not return a value after completing its assigned task.
  b. A void call can typically appears as its own statement in a C++ program.
  c. A void function cannot receive any items of information when it is called.
  d. A void function header begins with the keyword void.