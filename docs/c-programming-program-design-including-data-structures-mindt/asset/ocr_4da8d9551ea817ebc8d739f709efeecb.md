```
```cpp
double poolCapacity(double len, double wid, double dep)
{
    return 1000.00;
}
```
```

This allows the function `poolCapacity` to be called while the program is being coded. Ultimately, the stub for function `poolCapacity` is replaced with a function that properly calculates the amount of water needed to fill the pool based on the values of the parameters. In the meantime, the function stub allows work to continue on other parts of the program that call the function `poolCapacity`.

Because a stub looks a lot like a viable function, it must be properly documented in a way that would remind you to replace it with the actual definition. If you forget to replace a stub with the actual definition, the program will generate erroneous results, which sometimes might be embarrassing.

Before we look at some programming examples, another concept about functions is worth mentioning: function overloading.

# Function Overloading: An Introduction

In a C++ program, several functions can have the same name. This is called **function overloading**, or **overloading a function name**. Before we state the rules to overloading a function, let us define the following:

Two functions are said to have **different formal parameter lists** if both functions have

+   - A different number of formal parameters or
+   - The same number of formal parameters and the data types of the formal parameters, in the order listed, differ in at least one position.

For example, consider the following function headings:

```
```cpp
void functionOne(int x)
void functionTwo(int x, double y)
void functionThree(double y, int x)
int functionFour(char ch, int x, double y)
int functionFive(char ch, int x, string name)
```
```

These functions all have different formal parameter lists.

Now consider the following function headings:

```
```cpp
void functionSix(int x, double y, char ch)
void functionSeven(int one, double u, char firstCh)
```
```

The functions `functionSix` and `functionSeven` both have three formal parameters, and the data type of the corresponding parameters is the same. Therefore, these functions have the same formal parameter list. Note that it is the *data types* and not the *parameter names* or the *return type* that are examined.

To overload a function name, any two definitions of the function must have different formal parameter lists.