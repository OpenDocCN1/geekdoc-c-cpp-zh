# 10.1. GLOBAL VARIABLES

```
}
while (!done);
}
```

Listing 10.1 (globalecalculator.cpp) uses global variables **result**, **arg1**, and **arg2**. These names no longer appear in the **main** function. The global variables are accessed and/or modified in four different functions: **get_input**, **report**, **add**, and **subtract.

In the course of translating the statements within a machine language, the compiler resolves a local variable it encounters as follows:

+   * If the variable has a local declaration (that is, it is a local variable or parameter), the compiler will use the local variable or parameter, even if a global variable of the same name exists. Local variables, therefore, take precedence over global variables. The local declaration hides the global declaration in the scope of the local variable.

+   * If the variable has no local declaration it is declared as a global variable, the compiler will use the global variable.

+   * If the variable has no local declaration or no global declaration, the variable is undefined, and its use is an error.

In the situation where a local variable hides a global variable of the same name, there is a way to access both the local and like-named global within the local variable's scope. Suppose a program has a global variable **x** and a function with a local variable **x**. The statement

```
x = 10;
```

within the scope of the local variable will assign the local **x**. The following statement will assign the global variable **x** in the scope of the local variable of the name:

```
::x = 10;
```

:: operator is called the scope resolution operator. This special syntax may be used whenever a global variable is accessed within a function, but usually it only when necessary to access a hidden global variable.

If the value of a local variable is used by a statement before that variable has been given a value, either through initialization or assignment, the compiler will issue a warning. For example, the Visual C++ compiler will issue uninitialized() in the following code:

```
void uninitialized() {
  int x; // Declare the variable
cout << x; // Then use it
}
```

The warning is

> warning C4700: uninitialized local variable 'x' used

(The only way to avoid this warning in Visual C++ is to turn off all warnings.) A local variable has an undefined value after it is declared without being initialized. Its value should not be used until it has been properly assigned. Global variables, however, do not need to be initialized before they are used. Numeric

©2014 Richard L. Halverson Draft date: January 26, 2014