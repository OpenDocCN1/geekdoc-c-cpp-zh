
You can initialize a pointer to a function with the name of a function within the declaration of the pointer. The following is an example of this:

```cpp
long sum(long num1, long num2);      // Function prototype
long (*pfun)(long, long) = sum;      // Pointer to function points to sum()
```

In general you can set the `pfun` pointer that you declared here to point to any function that accepts two arguments of type `long` and returns a value of type `long`. In the first instance you initialized it with the address of the `sum()` function that has the prototype given by the first statement.

Of course, you can also initialize a pointer to a function by using an assignment statement. Assuming the pointer `pfun` has been declared as above, you could set the value of the pointer to a different function with these statements:

```cpp
long product(long, long);           // Function prototype
...

pfun = product;                     // Set pointer to function product()
```

As with pointers to variables, you must ensure that a pointer to a function is initialized before you use it to call a function. Without initialization, catastrophic failure of your program is guaranteed.

## Try It Out: Pointers to Functions

To get a proper feel for these newfangled pointers and how they perform in action, try one out in a program.

```cpp
// Ex6_01.cpp
// Exercising pointers to functions
#include <iostream>
using std::cout;
using std::endl;

long sum(long a, long b);             // Function prototype
long product(long a, long b);         // Function prototype

int main(void)
{
    long (*pdo_it)(long, long);      // Pointer to function declaration

    pdo_it = product;
    cout << endl
         << "3*5 = " << pdo_it(3, 5);   // Call product thru a pointer

    pdo_it = sum;                    // Reassign pointer to sum()
    cout << endl
         << "3*(4 + 5) + 6 = "
         << pdo_it(product(3, pdo_it(4, 5)), 6);   // Call thru a pointer,
                                                   // twice

    cout << endl;
    return 0;
}

// Function to multiply two values
long product(long a, long b)
{
    return a*b;
}

// Function to add two values
long sum(long a, long b)
{
    return a + b;
}
```

This example produces the output:

```
3*5 = 15
3*(4 + 5) + 6 = 33
```

### How It Works

This is hardly a useful program, but it does show very simply how a pointer to a function is declared, assigned a value, and subsequently used to call a function.

After the usual preamble, you declare a pointer to a function, `pdo_it`, which can point to either of the other two functions that you have defined, `sum()` or `product()`. The pointer is given the address of the function `product()` in this assignment statement:

```cpp
pdo_it = product;
```

You just supply the name of the function as the initial value for the pointer and no parentheses or other adornments are required. The function name is automatically converted to an address, which is stored in the pointer.

The function `product()` is called indirectly through the pointer `pdo_it` in the output statement.

```cpp
cout << endl
    << "3*5 = " << pdo_it(3, 5);        // Call product thru a pointer
```

You use the name of the pointer just as if it was a function name, followed by the arguments between parentheses exactly as they would appear if you were using the original function name directly.

Just to show that you can do it, you change the pointer to point to the function `sum()`.

```cpp
pdo_it = sum;                        // Reassign pointer to sum()
```

You then use it again in a ludicrously convoluted expression to do some simple arithmetic:

```cpp
cout << endl
    << "3*(4 + 5) + 6 = "
    << pdo_it(product(3, pdo_it(4, 5)), 6);  // Call thru a pointer,
                                        // twice
```

This shows that a pointer to a function can be used in exactly the same way as the function that it points to. The sequence of actions in the expression is shown in Figure 6-1.

![](img/2359b0c604600c58fba3539c738a356e_316_0.png)

Figure 6-1

## A Pointer to a Function as an Argument

Because “pointer to a function” is a perfectly reasonable type, a function can also have a parameter that is a pointer to a function. The function can then call the function pointed to by the argument. Because the pointer can be made to point at different functions in different circumstances, this allows the particular function that is to be called from inside a function to be determined in the calling program. In this case, you can pass a function explicitly as an argument.

### Try It Out: Passing a Function Pointer

You can look at this with an example. Suppose you need a function that processes an array of numbers by producing the sum of the squares of each of the numbers on some occasions, and the sum of the cubes on other occasions. One way of achieving this is by using a pointer to a function as an argument.

```cpp
// Ex6_02.cpp
// A pointer to a function as an argument
#include <iostream>
using std::cout;
using std::endl;

// Function prototypes
double squared(double);
double cubed(double);
double sumarray(double array[], int len, double (*pfun)(double));

int main(void)
{
    double array[] = { 1.5, 2.5, 3.5, 4.5, 5.5, 6.5, 7.5 };
    int len = sizeof array/sizeof array[0];

    cout << endl
         << "Sum of squares = "
         << sumarray(array, len, squared);

    cout << endl
         << "Sum of cubes = "
         << sumarray(array, len, cubed);

    cout << endl;
    return 0;
}

// Function for a square of a value
double squared(double x)
{
    return x*x;
}

// Function for a cube of a value
double cubed(double x)
{
    return x*x*x;
}

// Function to sum functions of array elements
double sumarray(double array[], int len, double (*pfun)(double))
{
    double total = 0.0;                 // Accumulate total in here

    for(int i = 0; i < len; i++)
        total += pfun(array[i]);

    return total;
}
```

If you compile and run this code, you should see the following output:

```
Sum of squares = 169.75
Sum of cubes = 1015.88
```

### How It Works

The first statement of interest is the prototype for the function `sumarray()`. Its third parameter is a pointer to a function that has a parameter of type `double`, and returns a value of type `double`.

```cpp
double sumarray(double array[], int len, double (*pfun)(double));
```

The function `sumarray()` processes each element of the array passed as its first argument with whatever function is pointed to by its third argument. The function then returns the sum of the processed array elements.

You call the function `sumarray()` twice in `main()`, the first time with the function name `squared` as the third argument, and the second time using `cubed`. In each case, the address corresponding to the function name that you use as the argument is substituted for the function pointer in the body of the function `sumarray()`, so the appropriate function is called within the `for` loop.

There are obviously easier ways of achieving what this example does, but using a pointer to a function provides you with a lot of generality. You could pass any function to `sumarray()` that you care to define as long as it takes one `double` argument and returns a value of type `double`.

## Arrays of Pointers to Functions

In the same way as with regular pointers, you can declare an array of pointers to functions. You can also initialize them in the declaration. Here is an example of declaring an array of pointers.

```cpp
double sum(double, double);                 // Function prototype
double product(double, double);             // Function prototype
double difference(double, double);          // Function prototype
double (*pfun[3])(double, double) =
    { sum, product, difference };   // Array of function pointers
```

Each of the elements in the array is initialized by the corresponding function address appearing in the initializing list between braces. To call the function `product()` using the second element of the pointer array, you would write:

```cpp
pfun[1](2.5, 3.5);
```

The square brackets that select the function pointer array element appear immediately after the array name and before the arguments to the function being called. Of course, you can place a function call through an element of a function pointer array in any appropriate expression that the original function might legitimately appear in, and the index value selecting the pointer can be any expression producing a valid index value.

## Initializing Function Parameters

With all the functions you have used up to now, you have had to take care to provide an argument corresponding to each parameter in a function call. It can be quite handy to be able to omit one or more arguments in a function call and have some default values for the arguments that you leave out supplied automatically. You can arrange this by initializing the parameters to a function in its prototype.

For example, suppose that you write a function to display a message, where the displayed message is passed as an argument. Here is the definition of such a function:
