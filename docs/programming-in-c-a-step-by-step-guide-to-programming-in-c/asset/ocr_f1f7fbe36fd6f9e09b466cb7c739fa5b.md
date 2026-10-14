(True/False)
10._________ variables retain their values throughout the life of the program. As a result, if a function is exited and then reentered later, the static variables defined within that function will retain their previous values.
11.By default, a static variable is initialized to _______.

# 6.6 External Variables

It is possible to split a function up into several source files, for easier maintenance. When several source files are combined into one program the compiler must have a way of correlating the variables which might be used to communicate between the several source files. Furthermore, if a variable is going to be useful for communication, there must be exactly one of it: you wouldn't want one function in one source file to store a value in one variable named **externvar**, and then have another function in another source file read from a *different* variable named **externvar**. Therefore, a variable should have exactly one *defining instance*, in one place in one source file. If the same variable is to be used anywhere else (i.e. in some other source file or files), the variable is declared in those other file(s) with an *external declaration*, which is not a defining instance. The external declaration says the compiler that the variable will be used in this source file but defined in some other source file. Thus the compiler doesn't allocate space for that variable with this source file.

To make a variable as an external declaration, which is defined somewhere else; you precede it with the keyword **extern**:

```
extern int j;
```

Program 6.4: Program to illustrate the concept of external variables.