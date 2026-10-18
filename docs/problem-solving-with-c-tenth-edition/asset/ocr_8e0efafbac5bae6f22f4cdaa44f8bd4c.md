# Variable Declarations

All variables must be declared before they are used. The syntax for variable declarations is as follows:

# SYNTAX

```
Type_Name variableName1, variableName2, ...;
```

# EXAMPLES

```
int count, numberOfDragons, numberOfTrolls;
double distance;
```

# Naming Conventions

A naming convention is the set of rules that are used to name identifiers such as variables. In this book, we use the convention that variables start with a lowercase letter. Compound words or phrases are squished together with the first letter of the next word in uppercase. This convention is called camelback or camelcase. Other naming conventions, such as the C-style convention, use an underscore between words, while other naming conventions identify the variable type in the variable name.

Variable declarations provide information the compiler needs in order to implement the variables. Recall that the compiler implements variables as memory locations and that the value of a variable is stored in the memory location assigned to that variable. The value is coded as a string of 0s and 1s. Different types of variables require different sizes of memory locations and different methods for coding their values as a string of 0s and 1s. The computer uses one code to encode integers as a string of 0s and 1s. It uses a different code to encode numbers that have a fractional part. It uses yet another code to encode letters as strings of 0s and 1s. The variable declaration tells the compiler—and, ultimately, the computer—what size memory location to use for the variable and which code to use when representing the variable’s value as a string of 0s and 1s.