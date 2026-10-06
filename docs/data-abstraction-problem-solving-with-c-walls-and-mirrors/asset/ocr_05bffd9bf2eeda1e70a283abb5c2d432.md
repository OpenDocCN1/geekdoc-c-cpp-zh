the output parameter larger. The & that follows larger's data type int indicates that larger is a reference parameter. Thus, computeMax will access and alter the argument that corresponds to larger, whereas the function will make and use copies of the values of the arguments that correspond to the value parameters x and y.

The following statements demonstrate how to computeMax:

If a function's output is a large object, the objects you will encounter in this book, you might not want the function to copy it. Thus, you would not pass the argument by value. If it is an input argument, you would not want the function to alter it. A constant reference parameter is a reference parameter that is tagged as const. The function uses the actual argument is passed to it, not a copy of it, and cannot modify it.

For example, the function f that has

```
void f(const int &x, int y, int &z)
```

x is a constant reference parameter, y is a value parameter, and z is a reference parameter. Here x and y are input parameters because z is an output parameter. Note that z can also be an input parameter. That is, the argument corresponding to z can both provide a value to the function and return a value from the function. Such arguments must be passed by reference.

> Note: Use reference parameters with caution, as you might inadvertently change an argument. On the other hand, constant reference parameters are safe to use.

If you write another function f that calls computeMax, you must either define the place of f after the definition of computeMax or precede f's with a function declaration for computeMax. For example, you can use either of the following statements to declare the function computeMax:

```
void computeMax(int x, int y, int &max);
```

or

```
void computeMax(int, int, int&);
```

A function declaration provides the data types of the function's parameters and its return type. Parameter names are optional in a function declaration, although they are helpful stylistically. However, parameter names are required in the function's definition. Although a function declaration ends with a semicolon, it does not appear in a function definition.

A typical C++ program contains a function declaration for every function used in the program, with comments that describe each function's purpose, parameters, and assumptions. The program in Listing A-1 demonstrates the placement of a function declaration, function definition, and main function: