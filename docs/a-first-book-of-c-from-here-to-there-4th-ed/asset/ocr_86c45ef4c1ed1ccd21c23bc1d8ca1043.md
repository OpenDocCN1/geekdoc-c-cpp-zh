value, three distinct functions must be written to handle each case correctly. Therefore, if the function name abs() is used, these three functions would have the following prototypes:

```
void abs(int);
void abs(float);
void abs(double);
```

Clearly, each of these functions performs essentially the same operation but on different parameter data types. A much cleaner solution is writing a general function that handles all three parameter data types, but the compiler can set parameters, variables, and even return type based on the data type used when the function is called. You can write this type of function in C++ by using a function template, which is a single, complete function that serves as a model for a family of functions. The function from the family that's actually created depends on subsequent function calls. To make this concept more concrete, take a look at a function template that computes and displays the absolute value of a passed argument:

```
template <class T>
void showabs(T number)
{
    if (number < 0)
        number = -number;
    cout << "The absolute value of the number "
         << " is " << number << endl;
    return;
}
```

For the moment, ignore the first line, template <class T>, and look at the second line, consisting of the function header void showabs(T number). Notice that this function header has the same syntax used for all function definitions, except the T where a data type is usually placed. For example, if the function header were void showabs(int number), you should recognize it as a function named showabs() that expects one integer argument to be passed to it and returns no value. Similarly, if the function header were void showabs(double number), you should recognize it as a function that expects one double-precision argument to be passed to it when the function is called.

The advantage of using the T in the function template header is that it represents a general data type that's replaced by an actual data type, such as int, float, double, and so forth, when the compiler encounters an actual function call. For example, if a function call with an integer argument is encountered, the compiler uses the function template to construct a function that expects an integer parameter. Similarly, if a call is made with a double-precision argument, the compiler constructs a function that expects a double-precision parameter. As a specific example, take a look at Program 6.3.