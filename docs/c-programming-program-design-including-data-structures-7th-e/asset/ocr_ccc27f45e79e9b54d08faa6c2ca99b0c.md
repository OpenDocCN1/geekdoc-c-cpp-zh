The function prototype is *not* a definition. It gives the program the name of the function, the number and data types of the parameters, and the data type of the returned value; just enough information to let C++ use the function. It is also a promise that the full definition will appear later in the program. If you neglect to write the definition of the function, the program may compile, but it will not execute.

**Function Prototype:** The function heading, terminated by a semicolon, ;, without the body of the function.

# Syntax: Function Prototype

The general syntax of the function prototype of a value-returning function is:

```
```cpp
functionType functionName(parameter list);
```
```

(Note that the function prototype ends with a semicolon.)

For the function larger, the prototype is:

```
```cpp
double larger(double x, double y);    //function prototype
```
```

> > **NOTE**
> >
> > When writing the function prototype, you do not have to specify the variable name in the parameter list. However, you must specify the data type of each parameter.
> >
> > You can rewrite the function prototype of the function larger as follows:
> >
> > ```cpp
> > double larger(double, double);    //function prototype
> > ```

# FINAL PROGRAM

You now know enough to write the entire program, compile it, and run it. The following program uses the functions larger, compareThree, and main to determine the larger/largest of two or three numbers.

```
```cpp
//Program: Largest of three numbers

#include <iostream>

using namespace std;

double larger(double x, double y);
double compareThree(double x, double y, double z);

int main()
{
    double one, two;

    cout << "Line 2: The larger of 5 and 10 is "
         << larger(5, 10) << endl;              //Line 1
```
```