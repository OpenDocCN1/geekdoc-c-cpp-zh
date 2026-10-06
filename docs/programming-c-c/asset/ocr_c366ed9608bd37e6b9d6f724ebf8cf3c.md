# Functions, Arrays and Strings

A function must always be defined in the global environment that is a function cannot be defined within another function.

Example:

F = factorial (n)

The parameter n is called the actual parameter. The actual parameters should match in type, number and sequence with the formal parameters appearing in the function definition. In the absence of any arguments, an empty pair of parentheses should be given.

The execution of a C program begins from the main() function.

When the compiler encounters functionName(); control of the program jumps to

```
voidfunctionName()
```

And, the compiler starts executing the codes inside functionName().

The control of the program jumps back to the main() function once code inside the function definition is executed.

# How function works in C programming?

![](bbox=[0.19, 0.475, 0.66, 0.675])

Note: Function names are identifiers and should be unique.

There are two types of functions in C:

+   - Built-in (Library) Functions
The system provided these functions and stored in the library. Therefore, it is also called Library Functions, e.g., printf(), scanf(), strcpy(), strlwr, strcmp, strlen, strcat, etc.
- User-defined Functions: These functions are defined by the user at the time of writing the program.