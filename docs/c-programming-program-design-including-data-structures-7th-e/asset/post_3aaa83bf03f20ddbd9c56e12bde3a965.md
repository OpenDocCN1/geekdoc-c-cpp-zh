
```cpp
int larger(int x, int y);
char larger(char first, char second);
double larger(double u, double v);
string larger(string first, string second);
```

If the call is `larger(5, 3)`, for example, the version having `int` parameters is executed. If the call is `larger('A', '9')`, the version having `char` parameters is executed, and so on.

Function overloading is used when you have the same action for different sets of data. Of course, for function overloading to work, you must give a separate definition for each function.

## Functions with Default Parameters

**NOTE** This section is not needed until Chapter 10.

This section discusses functions with default parameters. Recall that when a function is called, the number of actual and formal parameters must be the same. C++ relaxes this condition for functions with default parameters. You specify the value of a default parameter when the function name appears for the first time, usually in the prototype. In general, the following rules apply for functions with default parameters:

- If you do not specify the value of a default parameter, the default value is used for that parameter.
- All of the default parameters must be the far-right parameters of the function.
- Suppose a function has more than one default parameter. In a function call, if a value to a default parameter is not specified, then you must omit all of the arguments to its right.
- Default values can be constants, global variables, or function calls.
- The caller has the option of specifying a value other than the default for any default parameter.
- You cannot assign a constant value as a default value to a reference parameter.

Consider the following function prototype:

```cpp
void funcExp(int t, int u, double v, char w = 'A', int x = 67,
             char y = 'G', double z = 78.34);
```

The function `funcExp` has seven parameters. The parameters `w`, `x`, `y`, and `z` are default parameters. If no values are specified for `w`, `x`, `y`, and `z` in a call to the function `funcExp`, their default values are used.

Suppose you have the following statements:

```cpp
int a, b;
char ch;
double d;
```

The following function calls are legal:

1. `funcExp(a, b, d);`
2. `funcExp(a, 15, 34.6, 'B', 87, ch);`
3. `funcExp(b, a, 14.56, 'D');`

In statement 1, the default values of `w`, `x`, `y`, and `z` are used. In statement 2, the default value of `w` is replaced by `'B'`, the default value of `x` is replaced by `87`, the default value of `y` is replaced by the value of `ch`, and the default value of `z` is used. In statement 3, the default value of `w` is replaced by `'D'`, and the default values of `x`, `y`, and `z` are used.

The following function calls are illegal:

1. `funcExp(a, 15, 34.6, , 46.7);`
2. `funcExp(b, 25, 48.76, 'D', 4567, , 78.34);`

In statement 1, because the value of `w` is omitted, all other default values must be omitted. In statement 2, because the value of `y` is omitted, the value of `z` should be omitted, too.

The following are illegal function prototypes with default parameters:

1. `void funcOne(int x, double z = 23.45, char ch, int u = 45);`
2. `int funcTwo(int length = 1, int width, int height = 1);`
3. `void funcThree(int x, int& y = 16, double z = 34);`

In statement 1, because the second parameter `z` is a default parameter, all other parameters after `z` must also be default parameters. In statement 2, because the first parameter is a default parameter, all parameters must be default parameters. In statement 3, a constant value cannot be assigned to `y` because `y` is a reference parameter.

Example 6-19 further illustrates functions with default parameters.

### EXAMPLE 6-19

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

int volume(int l = 1, int w = 1, int h = 1);
void funcOne(int& x, double y = 12.34, char z = 'B');
```

> **NOTE**
> In programs in this book, and as is recommended, the definition of the function `main` is placed before the definition of any user-defined functions. You must, therefore, specify the default value for a parameter in the function prototype and in the function prototype only, *not* in the function definition because this must occur at the first appearance of the function name.

## PROGRAMMING EXAMPLE: Classify Numbers

In this example, we use functions to rewrite the program that determines the number of odds and evens from a given list of integers. This program was first written in Chapter 5.

The main algorithm remains the same:

1. Initialize the variables, `zeros`, `odds`, and `evens` to 0.
2. Read a number.
3. If the number is even, increment the even count, and if the number is also zero, increment the zero count; otherwise, increment the odd count.
4. Repeat Steps 2 and 3 for each number in the list.

The main parts of the program are: initialize the variables, read and classify the numbers, and then output the results. To simplify the function `main` and further illustrate parameter passing, the program includes:

- A function `initialize` to initialize the variables, such as `zeros`, `odds`, and `evens`.
- A function `getNumber` to get the number.
- A function `classifyNumber` to determine whether the number is odd or even (and whether it is also zero). This function also increments the appropriate count.
- A function `printResults` to print the results.

Let us now describe each of these functions.

### initialize

The function `initialize` initializes variables to their initial values. The variables that we need to initialize are `zeros`, `odds`, and `evens`. As before, their initial values are all zero. Clearly, this function has three parameters. Because the values of the formal parameters initializing these variables must be passed outside of the function, these formal parameters must be reference parameters. Essentially, this function is:

```cpp
void initialize(int& zeroCount, int& oddCount, int& evenCount)
{
    zeroCount = 0;
    oddCount = 0;
    evenCount = 0;
}
```

### getNumber

The function `getNumber` reads a number and then passes this number to the function `main`. Because you need to pass only one number, this function has only one parameter. The formal parameter of this (void) function must be a reference parameter because the number read is passed outside of the function. Essentially, this function is:

```cpp
void getNumber(int& num)
{
    cin >> num;
}
```

You can also write the function `getNumber` as a value-returning function. See the note at the end of this programming example.

### classifyNumber

The function `classifyNumber` determines whether the number is odd or even, and if the number is even, it also checks whether the number is zero. It also updates the values of some of the variables, `zeros`, `odds`, and `evens`. This function needs to know the number to be analyzed; therefore, the number must be passed as a parameter. Because this function also increments the appropriate count, the variables (that is, `zeros`, `odds`, and `evens` declared in `main`) holding the counts must be passed as parameters to this function. Thus, this function has four parameters.

Because the number will only be analyzed and not altered, you need to pass only its value. Thus, the formal parameter corresponding to this variable is a value parameter. After analyzing the number, this function increments the values of some of the variables, `zeros`, `odds`, and `evens`. Therefore, the formal parameters corresponding to these variables must be reference parameters. The algorithm to analyze the number and increment the appropriate count is the same as before. The definition of this function is:

```cpp
void classifyNumber(int num, int& zeroCount, int& oddCount,
                    int& evenCount)
{
    switch (num % 2)
    {
    case 0:
        evenCount++;
        if (num == 0)
            zeroCount++;
        break;
    case 1:
    case -1:
        oddCount++;
    } //end switch
} //end classifyNumber
```

### printResults

The function `printResults` prints the final results. To print the results (that is, the number of zeros, odds, and evens), this function must have access to the values of the variables `zeroCount`, `odds`, and `evens` declared in the function `main`. Therefore, this function has three parameters. Because this function doesn’t change the values of
