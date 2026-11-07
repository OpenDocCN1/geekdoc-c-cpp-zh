# No Exception

The third possibility is to declare to the user that this function does not throw an exception, which means that the user does not need to use a *try-catch* block. The syntax for this type of a function is shown below. The header of the function uses the *throw* keyword, but the parentheses are empty.

```
type functionName (parameters) throw ();
```

The following shows an example of this specification. If a function is supposed to print two integers, there are no error conditions and exception handling is unnecessary.

```
int print (int first, int second) throw ();   // Function declaration
```

# 14.1.4 Stack Unwinding

One of the most important concepts in exception handling is **stack unwinding**. Stack unwinding is closely related to managing the memory assigned to a program.

# Program Memory

In Chapter 9 we discussed that when a C++ program starts running, the runtime system designates four areas of memory for the program: *code memory*, *static memory*, *stack memory*, and *heap memory*. The code memory (program memory) holds the instructions of the program executed during the program run time. The *static memory* stores the value of static variables and global variables. These values are separated from the local variables. The *stack memory* is a last-in-first-out memory similar to the stacks of trays we see in a restaurant. The last tray pushed into the stack is the first one to be popped out. The *stack memory* is responsible for keeping track of three types of information about each function: values of parameters, values of local variables, and the return address of the calling function in code memory. The *heap memory* is free memory that is used by a program to store information that may outlast the life of a function.

# Pushing and Popping Stack Memory

Exception handling is based on the behavior of stack memory. Each program is made of a set of functions that may call each other. During a function call, data about the calling function, such as parameters, local variables, and the return address, are pushed into stack memory. The return address is used when the function terminates normally or abnormally (by throwing an exception). Figure 14.9 shows how data are pushed into the stack during a function call.

In the example shown in Figure 14.9, the *main* function is pushed into the stack, there are no parameters except the local variable (x), and the address of the instruction that called the *main* function in the RTE is pushed in the stack. When the *main* function calls *function1*, the parameter of the *function1* (xx), the local variable (y), and the address of the function call instruction (107) are pushed into the stack. Similarly, when *function1* calls *function2*, the parameter of *function2* (yy), the local variable of *function2* (z), and the address of the function call (244) are stored in the stack. Now the stack has three entries because of three function calls. Note that each parameter entry can have zero or more parameters and each local-variable record can have zero or more variables.