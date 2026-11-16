# Scope of Identifiers

Identifiers are variable or function names that are referred to in the program code. The scope of an identifier determines where that identifier can be referred to in the program code.

For example, consider the following code.

```
double average (double, double);

int globalVariable;

int main(void) {
    int localVariable;
    ...
    ...
}

double average(double grade1, double grade2) {
    return (grade1 + grade2) / 2;
}
```

Here, the identifiers (the function and variable names) average, main, globalVariable, localVariable, grade1, and grade2 all have a specific and well-defined scope. We can understand that scope as follows:

+   • Identifiers that are declared before the main() function have a global scope and can be referred to anywhere in the program code. Normally, constants, macros, and functions are declared before the main() function so that they have a global scope and are "visible" throughout the program code. Variables declared before the main() function are referred to as global variables and are generally frowned upon when used in a program.

+   • Identifiers that are declared within a specific function have a local scope and are "visible" only within that specific function. Function parameters are considered local to the function and are not "visible" outside that function. Typically, any variable used in a program should either be declared within a function or passed to a function as a function parameter.