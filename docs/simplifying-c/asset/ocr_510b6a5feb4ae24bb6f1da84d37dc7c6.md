![](bbox=[0.15, 0.14, 0.85, 0.39])

It can be seen in Figure 2 that the different components of a C function are function prototype, caller function, function call, actual parameter, formal parameter, return type, and called function. The next section discusses about the components of C function in detail.

# ### The Function Prototype

C language does not allow us to use any identifier before it has been declared. The declaration of an identifier has two scopes, namely, global and local. If an identifier is declared above all the functions used in the C program, then the identifier can be used and modified within all the functions below. Such an identifier is said to have a global scope. Similarly, an identifier may have a scope that is limited to a function. In such a case, the identifier can only be used and modified within the function that it is declared.

A function prototype is an indication to the C compiler that a function with the specified parameter can be referenced in the main function or any other function, before being defined in the program. In most of the cases, the executable statements of the function whose prototype is defined are written after the completion of the main function. For example, the declaration float add (float, float); refers to a function called add. The function add takes two float parameters as input and return one float parameter as an output. Almost all the header files available in C language library contain the prototype of the readily available C functions.

Note that if the function executable statements are defined before they are accessed, then we do not need a prototype statement for such functions.

# ### The Caller Function and Called Function

A function once defined can be used as a normal executable statement within the C program. In Figure 2, we have defined two functions, namely, main and add. Here, the function add is used in the function main, hence the function main is referred to as a caller function, while function add is referred to as a called function.