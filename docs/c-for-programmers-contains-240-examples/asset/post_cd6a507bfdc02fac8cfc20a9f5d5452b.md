
Variables of user-defined type Status can be assigned only one of the three values declared in the enumeration. When the game is won, the program sets variable gameStatus to WON (lines 34 and 55). When the game is lost, the program sets variable gameStatus to LOST (lines 39 and 58). Otherwise, the program sets variable gameStatus to CONTINUE (line 42) to indicate that the dice must be rolled again.

Another popular enumeration is

```
enum Months { JAN = 1, FEB, MAR, APR, MAY, JUN, JUL, AUG,
    SEP, OCT, NOV, DEC };
```

which creates user-defined type Months with enumeration constants representing the months of the year. The first value in the preceding enumeration is explicitly set to 1, so the remaining values increment from 1, resulting in the values 1 through 12. Any enumeration constant can be assigned an integer value in the enumeration definition, and subsequent enumeration constants each have a value 1 higher than the preceding constant in the list until the next explicit setting.

After the first roll, if the game is won or lost, the program skips the body of the while statement (lines 49–59) because gameStatus is not equal to CONTINUE. The program proceeds to the if...else statement in lines 62–65, which prints "Player wins" if gameStatus is equal to WON and "Player loses" if gameStatus is equal to LOST.

After the first roll, if the game is not over, the program saves the sum in myPoint (line 43). Execution proceeds with the while statement, because gameStatus is equal to CONTINUE. During each iteration of the while, the program calls rollDice to produce a new sum. If sum matches myPoint, the program sets gameStatus to WON (line 55), the while-test fails, the if...else statement prints "Player wins" and execution terminates. If sum is equal to 7, the program sets gameStatus to LOST (line 58), the while-test fails, the if...else statement prints "Player loses" and execution terminates.

Note the interesting use of the various program control mechanisms we have discussed. The craps program uses two functions—main and rollDice—and the switch, while, if...else, nested if...else and nested if statements.

## Good Programming Practice 6.3

Using enumerations rather than integer constants can make programs clearer and more maintainable. You can set the value of an enumeration constant once in the enumeration declaration.

## Common Programming Error 6.9

Assigning the integer equivalent of an enumeration constant (rather than the enumeration constant, itself) to a variable of the enumeration type is a compilation error.

## Common Programming Error 6.10

After an enumeration constant has been defined, attempting to assign another value to the enumeration constant is a compilation error.

## 6.9 Storage Classes

The programs you have seen so far use identifiers for variable names. The attributes of variables include name, type, size and value. This chapter also uses identifiers as names for user-defined functions. Actually, each identifier in a program has other attributes, including storage class, scope and linkage.

C++ provides five storage-class specifiers: auto, register, extern, mutable and static. This section discusses storage-class specifiers auto, register, extern and static. Storage-class specifier mutable (discussed in detail in Chapter 22, Other Topics) is used exclusively with classes.

## Storage Class, Scope and Linkage

An identifier’s storage class determines the period during which that identifier exists in memory. Some identifiers exist briefly, some are repeatedly created and destroyed and others exist for the entire execution of a program. First we discuss the storage classes static and automatic.

An identifier’s scope is where the identifier can be referenced in a program. Some identifiers can be referenced throughout a program; others can be referenced from only limited portions of a program. Section 6.10 discusses the scope of identifiers.

An identifier’s linkage determines whether it is known only in the source file where it is declared or across multiple files that are compiled, then linked together. An identifier’s storage-class specifier helps determine its storage class and linkage.

## Storage Class Categories

The storage-class specifiers can be split into two storage classes: automatic storage class and static storage class. Keywords auto and register are used to declare variables of the automatic storage class. Such variables are created when program execution enters the block in which they are defined, they exist while the block is active and they are destroyed when the program exits the block.

## Local Variables

Only local variables of a function can be of automatic storage class. A function’s local variables and parameters normally are of automatic storage class. The storage class specifier auto explicitly declares variables of automatic storage class. For example, the following declaration indicates that double variable x is a local variable of automatic storage class—it exists only in the nearest enclosing pair of curly braces within the body of the function in which the definition appears:

```
auto double x;
```

Local variables are of automatic storage class by default, so keyword auto rarely is used. For the remainder of the text, we refer to variables of automatic storage class simply as automatic variables.

## Performance Tip 6.1

> Automatic storage is a means of conserving memory, because automatic storage class variables exist in memory only when the block in which they are defined is executing.

## Software Engineering Observation 6.6

> Automatic storage is an example of the principle of least privilege, which is fundamental to good software engineering. In the context of an application, the principle states that code should be granted only the amount of privilege and access that it needs to accomplish its designated task, but no more. Why should we have variables stored in memory and accessible when they are not needed?

## Register Variables

Data in the machine-language version of a program is normally loaded into registers for calculations and other processing.

## Performance Tip 6.2

> The storage-class specifier register can be placed before an automatic variable declaration to suggest that the compiler maintain the variable in one of the computer's high-speed hardware registers rather than in memory. If intensely used variables such as counters or totals are maintained in hardware registers, the overhead of repeatedly loading the variables from memory into the registers and storing the results back into memory is eliminated.

## Common Programming Error 6.11

> Using multiple storage-class specifiers for an identifier is a syntax error. Only one storage class specifier can be applied to an identifier. For example, if you include register, do not also include auto.

The compiler might ignore register declarations. For example, there might not be a sufficient number of registers available for the compiler to use. The following definition suggests that the integer variable counter be placed in one of the computer's registers; regardless of whether the compiler does this, counter is initialized to 1:

```
register int counter = 1;
```

The register keyword can be used only with local variables and function parameters.

## Performance Tip 6.3

> Often, register is unnecessary. Optimizing compilers can recognize frequently used variables and may place them in registers without needing a register declaration.

## Static Storage Class

Keywords extern and static declare identifiers for variables of the static storage class and for functions. Static-storage-class variables exist from the point at which the program begins execution and last for the duration of the program. A static-storage-class variable's storage is allocated when the program begins execution. Such a variable is initialized once when its declaration is encountered. For functions, the name of the function exists when the program begins execution, just as for all other functions. However, even though the variables and the function names exist from the start of program execution, this does not mean that these identifiers can be used throughout the program. Storage class and scope (where a name can be used) are separate issues, as we'll see in Section 6.10.

## Identifiers with Static Storage Class

There are two types of identifiers with static storage class—external identifiers (such as global variables and global function names) and local variables declared with the storage-class specifier static. Global variables are created by placing variable declarations outside any class or function definition. Global variables retain their values throughout the execution of the program. Global variables and global functions can be referenced by any function that follows their declarations or definitions in the source file.
