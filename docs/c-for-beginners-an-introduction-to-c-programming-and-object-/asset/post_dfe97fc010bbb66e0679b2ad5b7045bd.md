
```cpp
}
cout << endl << "Sum: " << (x + y + z) << endl;
}
```

A function that accepts 2 integer values and returns the quotient of division in float form. The function should have float return type:

```cpp
float divide(int a, int b)
{
    float quotient = (a * 1.0) / b;
    return quotient;
}
```

### 9.1.1 Function Prototyping

Function Prototyping is a process of declaring a function before defining it. This is always not mandatory but is a good programming practice. Function prototyping tells the compiler what kind of functions are present.

Syntax:

```cpp
<return data type> <function name> ( <parameters or parameter's type> );
```

Prototyping statement should be placed before the function definition, preferably on the first few lines, after *using namespace std;* statement. The prototype for the divide function from the previous example is as follows:

```cpp
float divide(int a, int b);
// OR
float divide(int, int);
```

## 9.2 Function Call

A function definition contains a set of operation that a function performs. However, that code remains inactive unless a call is made to that function. Calling a function is also known as invoking a function. The general syntax is:

```cpp
<function name> ( <parameters> );
```

Let us recall the definition of *display_sum* function explained as an example in *Section 9.1:*

```cpp
void display_sum(int x, int y, int z)
{
    cout << endl << "Sum: " << (x + y + z) << endl;
}
```

If we had to call this function, we would use the following statement:

```cpp
display_sum(4, 5, 10);
```

The *display_sum* function accepts 3 integer values as parameters hence integer values of **4, 5 and 10** are passed as *function arguments* to it during the function call. These values will be received by x, y and z respectively.

If a function is returning a value, there should be a variable to receive that value. General Syntax:

```cpp
<variable> = <function name> ( <parameters> );
```

```cpp
cout << "quotient: " << divide(44, 5);
```

Let us put `display_message`, `display_sum` and `divide` functions in a C++ code and make different calls to them in order to demonstrate the usage of functions:

```cpp
#include <iostream>

using namespace std;

float divide(int, int);
void display_sum(int x, int y, int z);
void display_message();

float divide(int a, int b)
{
    float quotient = (a * 1.0) / b;
    return quotient;
}

void display_sum(int x, int y, int z)
{
    cout << endl << "Sum: " << (x + y + z) << endl;
}

void display_message()
{
    cout << " " << endl << " " << endl;
}

int main()
{
    // declare a variable to store quotient
    float quotient;
    cout << endl << endl
         << "The main() function includes the main"
         << " and display message function" << endl;
    display_message();
    cout << endl << endl
         << "Calling display_sum function. " << endl;
    display_sum(4, 5, 10);

    cout << endl << endl
         << "Calling divide function. " << endl;
    quotient = divide(44, 5);

    cout << endl << endl
         << "Quotient: " << quotient
         << endl;

    cout << endl << endl
         << "Passing 23 and 8: " << divide(23, 8) << endl;

    return 0;
}
```

## Output:

![](img/cda5b023e23ffd0b87fc37b1da33973d_92_0.png)

While passing values to a function as arguments, there are three methods – pass by value, pass by reference and pass by pointer. We will look at pass by value and pass by reference in this chapter and pass by pointer will be explained in the *Pointers* chapter.

### 9.2.1 Pass by Value

With this method, the value of the variable is passed to the function. In the function definition, the passed values are accepted in different variables. Hence, any changes made to the received variable in the function definition do not reflect back to the calling function. The examples explained so far were using pass by value method.

Here is an example which accepts a float value, multiplies itself by 10 and returns the new value:

```cpp
float multiply_by_10(float num)
{
    num = num * 10;
    return num;
}
```

Function call:

```cpp
float number = 1.2;
float x = multiply_by_10(number);
```

In the function call, a float variable called *number* having a value of *1.2* is passed to the function *multiply_by_10*. Inside the function, there is a parameter called *num* which receives this value, in the body of the function, the value of this variable is increased by a factor of 10 and returned back to the calling function. Because pass by value method is used to call the function, the value of *number* will be unaltered in the calling function.

### 9.2.2 Pass by Reference

In this method, when a value is passed to a function, it is received in the function using a reference variable. A reference variable in a function definition is denoted by a prefixed *ampersand symbol (&).* Any changes made to those variables will be reflected back in the calling function. Rest of the procedures remains the same including the function call. Let us slightly modify the *multiply_by_10* function from the previous section:

```cpp
void multiply_by_10(float &num)
{
    num = num * 10;
}
```

Any changes that are made to *num* will be reflected back in the calling function, hence there is no need to return a value.

Function call:

```cpp
float number = 1.2;
multiply_by_10(number);
```

While making the function call, the value of the variable *number* is not passed, instead a *reference to that variable* is passed. The function definition increases the value of the parameter by a factor 10. Since pass by reference method is used, the local variable *number* will now hold a value of 12.

In order to better understand this concept, let us write a C++ program with two functions to swap two input values. One using the pass by value method and the other with pass by reference method:

```cpp
#include <iostream>

using namespace std;

void swap_by_value(int, int);
void swap_by_reference(int &, int &);

void swap_by_value(int x, int y)
{
    int temp = x;
    x = y;
    y = temp;
    // Display x and y
    cout << endl << endl << "Inside swap_by_value" << endl
         << endl
         << "x: " << x << "    y: " << y << endl;
}

void swap_by_reference(int &x, int &y)
{
    // Swap x and y
    int temp = x;
    x = y;
    y = temp;

    cout << endl << endl << "Inside swap_by_reference" << endl
         << endl
         << "x: " << x << " y: " << y << endl;
}

int main()
{
    // Declare 2 integers to accept and store user input
    int x, y;
    // Ask the user to enter a number
```

You can set certain parameters of a function to have default values. While calling a function, if the parameter which has been set as default is not passed, its default value will be used. There are a few rules to be followed while setting default arguments:

- 1. Only the last parameter(s) can be set as default.
- 2. If a parameter has been set as default, all the following parameters must be set as default.

General syntax for setting default arguments is:

```cpp
<return type> <function name> (<parameter 1>, ...
<parameter n> = <value>)
{
    // Function Body
}
```

Example:

Let us define a function which accepts 3 parameters, returns their product. Out of the 3 parameters, the last one will be the default argument:

```cpp
int multiply(int a, int b, int c = 10)
{
    return (a * b * c);
}
```

This function can be called by passing 2 or 3 arguments. Since the third parameter c is set to 10, if two arguments are passed,

```cpp
// Two arguments
int sum(int a, int b)
{
    return (a + b);
}

// Three arguments
int sum(int a, int b, int c)
{
    return (a + b + c);
}

// Four arguments
int sum(int a, int b, int c, int d)
{
    return (a + b + c + d);
}
```

As seen, there are 3 definitions having the same name – sum but different number of arguments in each definition. Let us see how each of these functions can be called:

```cpp
// sum with 2 arguments
int x = sum(4, 5);
// sum with 3 arguments
int x = sum(10, 20, 30);
// sum with 4 arguments
int x = sum(150, 690, 55, 340);
```

### 9.4.2 Different types of Arguments

Functions can be overloaded by changing the types of parameters each definition accepts. Logically speaking, changing the data types of function parameters may have to be followed by changing the return type of the function. Different return type is not a criterion for function overloading. For example, if there are two definitions of *sum* function, one takes *two integers* and the other takes *two floats* as input parameters. The one that takes
