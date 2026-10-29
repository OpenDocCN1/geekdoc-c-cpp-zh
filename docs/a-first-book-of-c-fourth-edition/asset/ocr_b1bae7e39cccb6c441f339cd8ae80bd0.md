The register variables have the same time duration as auto variables; that is, a local register variable is created when the function declaring it is entered and is destroyed when the function finishes execution. The only difference between register and auto variables is where storage for the variable is located.

Storage for all variables (local and global), except register variables, is reserved in the computer’s memory. Most computers also have a few high-speed storage areas, called registers, located in the CPU that can also be used for variable storage. Because registers are in the CPU, they can be accessed faster than the normal storage areas in the computer’s memory. Also, computer instructions referencing registers typically require less space than instructions referencing memory locations because there are fewer registers than memory locations that can be accessed. When the compiler substitutes a register’s location for a variable during program compilation, the instruction needs less space than address memory having millions of locations.

Besides decreasing a compiled C++ program’s size, using register variables can increase the program’s execution speed if your computer supports this data type. Variables declared with the register storage category are switched to auto automatically if your compiler doesn’t support register variables or if the declared register variables exceed the computer’s register capacity. Application programs intended to run on different types of computers shouldn’t use register variables, however. The only restriction in using the register storage category is that a register variable’s address can’t be taken by using the address operator, &. This concept is easier to understand when you realize that registers don’t have standard memory addresses.

# Global Variable Storage Categories

Global variables are created by definition statements external to a function. By their nature, these externally defined variables don’t come and go with the calling of a function. After a global variable is created, it exists until the program in which it’s declared has finished running. Therefore, global variables can’t be declared as auto or register variables that are created and destroyed as the program is running. Global variables can be declared with the static or extern storage category (but not both). The following are examples of declaration statements including these two category descriptions:

```
extern int sum;
extern double volts;
static double current;
```

The static and extern storage categories affect only the scope, not the lifetime, of global variables. As with static local variables, all global variables are initialized to 0 at compile time. The purpose of the extern storage category is to extend a global variable’s scope beyond its normal boundaries. To understand this concept, first note that all the programs written so far have been contained in one file. Therefore, when you have saved or retrieved programs, you have needed to give the computer only a single name for your program. C++ doesn’t require doing this, however.

Large programs typically consist of many functions stored in multiple files. For example, Figure 6.13 shows the three functions main(), func1(), and func2() stored in one file and the two functions func3() and func4() stored in a second file.