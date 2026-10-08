# CHAPTER 9 Value-Returning Functions

+   * You call a function by including its name and actual arguments (if any) in a statement.

+   * Unless specified otherwise, variables in C++ are passed to a function by value, which means that the value stored in the variable is passed.

+   * A program will have one function prototype for each function defined below the main function. Functions defined above the main function in a program do not need a function prototype.

+   * A variable's scope, which can be either local or global, indicates where in a program it can be used. A variable's lifetime extends how long the variable remains in the computer's internal memory.

+   * Local variables are used only within the function in which they are declared or whose parameterList they appear, and they remain in memory until the function ends. Global variables, which you should avoid using, can be used anywhere in the program. Unlike local variables, global variables remain in memory until the program ends.

+   * If more than one memory location has the same name and appears in a statement, the computer uses the position of the statement within the program to determine which memory location to use. For clarity, you should use unique variable names within a program.

#  Terms

**Actual functions**—an item of information passed (sent) to a function when the function is called (invoked)

**Built-in functions**—blocks of code that perform a task and are included in libraries that come with the C++ language; examples include the `pow`, `sqrt`, `rand`, and `time` functions

**Formal parameters**—the memory locations listed in a function header's parameterList; a formal parameter stores an item of information passed to a function when the function is invoked (called)

**Function prototype**—a statement that specifies the function's name, the data of its return value (if any), the data type and (optionally) name of each of its formal parameters (if any); for every function that is defined below the `main` function in a program

**Global variables**—variables that are declared outside of any function in a program; global variables can be used by any statement declaration in the program, and they remain in memory until the program ends; you should avoid using global variables in a program

**Lifetime**—indicates how long an item, such as a variable, remains in the computer's internal memory

**Local variables**—variables that are either declared within a function or appear in the function header's parameterList; local variables can be used only by the function in which they are declared or in whose parameterList they appear; local variables remain in memory until the function ends

**Passing by reference**—refers to the process of passing a variable's address to a function