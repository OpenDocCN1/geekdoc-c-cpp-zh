
```cpp
int b = 200;

cout << "Before swap, value of a :" << a << endl;
cout << "Before swap, value of b :" << b << endl;

// calling a function to swap the values.
swap(a, b);

cout << "After swap, value of a :" << a << endl;
cout << "After swap, value of b :" << b << endl;

return 0;
}
```

When the above code is put together in a file, compiled and executed, it produces the following result:

```text
Before swap, value of a :100
Before swap, value of b :200
After swap, value of a :100
After swap, value of b :200
```

Which shows that there is no change in the values though they had been changed inside the function.

## Call by Pointer

The **call by pointer** method of passing arguments to a function copies the address of an argument into the formal parameter. Inside the function, the address is used to access the actual argument used in the call. This means that changes made to the parameter affect the passed argument.

To pass the value by pointer, argument pointers are passed to the functions just like any other value. So accordingly you need to declare the function parameters as pointer types as in the following function **swap()**, which exchanges the values of the two integer variables pointed to by its arguments.

```cpp
// function definition to swap the values.
void swap(int *x, int *y)
{
    int temp;

    temp = *x; /* save the value at address x */
    *x = *y;   /* put y into x */
    *y = temp; /* put x into y */

    return;
}
```

To check the more detail about C++ pointers, kindly check C++ Pointers chapter.

For now, let us call the function **swap()** by passing values by pointer as in the following example:

```cpp
#include <iostream>

using namespace std;

// function declaration
void swap(int *x, int *y);

int main ()
{
    // local variable declaration:
    int a = 100;
    int b = 200;

    cout << "Before swap, value of a :" << a << endl;
    cout << "Before swap, value of b :" << b << endl;

    /* calling a function to swap the values.
     * &a indicates pointer to a ie. address of variable a and
     * &b indicates pointer to b ie. address of variable b.
     */
    swap(&a, &b);

    cout << "After swap, value of a :" << a << endl;
    cout << "After swap, value of b :" << b << endl;

    return 0;
}
```

When the above code is put together in a file, compiled and executed, it produces the following result:

```text
Before swap, value of a :100

Before swap, value of b :200

After swap, value of a :200

After swap, value of b :100
```

## Call by Reference

The **call by reference** method of passing arguments to a function copies the reference of an argument into the formal parameter. Inside the function, the reference is used to access the actual argument used in the call. This means that changes made to the parameter affect the passed argument.

To pass the value by reference, argument reference is passed to the functions just like any other value. So, accordingly you need to declare the function parameters as reference types as in the following function **swap()**, which exchanges the values of the two integer variables pointed to by its arguments.

```cpp
// function definition to swap the values.

void swap(int &x, int &y)
{
    int temp;

    temp = x; /* save the value at address x */

    x = y;    /* put y into x */

    y = temp; /* put x into y */

    return;
}
```

For now, let us call the function **swap()** by passing values by reference as in the following example:

```cpp
#include <iostream>

using namespace std;

// function declaration

void swap(int &x, int &y);

int main ()
{
    // local variable declaration:
    int a = 100;
    int b = 200;

    cout << "Before swap, value of a :" << a << endl;
    cout << "Before swap, value of b :" << b << endl;

    /* calling a function to swap the values using variable reference.*/
    swap(a, b);

    cout << "After swap, value of a :" << a << endl;
    cout << "After swap, value of b :" << b << endl;

    return 0;
}
```

When the above code is put together in a file, compiled and executed, it produces the following result:

```text
Before swap, value of a :100

Before swap, value of b :200

After swap, value of a :200

After swap, value of b :100
```

By default, C++ uses **call by value** to pass arguments. In general, this means that code within a function cannot alter the arguments used to call the function and above mentioned example while calling max() function used the same method.

## Default Values for Parameters

When you define a function, you can specify a default value for each of the last parameters. This value will be used if the corresponding argument is left blank when calling to the function.

This is done by using the assignment operator and assigning values for the arguments in the function definition. If a value for that parameter is not passed when the function is called, the default given value is used, but if a value is specified, this default value is ignored and the passed value is used instead. Consider the following example:

```cpp
#include <iostream>

using namespace std;


int sum(int a, int b=20)
{
    int result;


    result = a + b;


    return (result);
}


int main ()
{
    // local variable declaration:
    int a = 100;
    int b = 200;
    int result;


    // calling a function to add the values.
    result = sum(a, b);
    cout << "Total value is :" << result << endl;


    // calling a function again as follows.
    result = sum(a);
    cout << "Total value is :" << result << endl;


    return 0;
}
```

When the above code is compiled and executed, it produces the following result:

```text
Total value is :300
Total value is :120
```

```cpp
cout << "double d :" << d << endl;

    return 0;
}
```

When the above code is compiled and executed, it produces the following result:

```text
short  s :10
int    i :-1000
long   l :1000000
float  f :230.47
double d :30949.4
```

## Math Operations in C++

In addition to the various functions you can create, C++ also includes some useful functions you can use. These functions are available in standard C and C++ libraries and called **built-in** functions. These are functions that can be included in your program and then use.

C++ has a rich set of mathematical operations, which can be performed on various numbers. Following table lists down some useful built-in mathematical functions available in C++.

To utilize these functions you need to include the math header file **<cmath>**.

| S.N. | Function & Purpose |
|------|--------------------|
| 1 | **double cos(double);**<br>This function takes an angle (as a double) and returns the cosine. |
| 2 | **double sin(double);**<br>This function takes an angle (as a double) and returns the sine. |
| 3 | **double tan(double);**<br>This function takes an angle (as a double) and returns the tangent. |
| 4 | **double log(double);**<br>This function takes a number and returns the natural log of that number. |
| 5 | **double pow(double, double);**<br>The first is a number you wish to raise and the second is the power you wish to raise it to. |
| 6 | **double hypot(double, double);**<br>If you pass this function the length of two sides of a right triangle, it will return you the length of the hypotenuse. |
| 7 | **double sqrt(double);**<br>You pass this function a number and it gives you the square root. |
| 8 | **int abs(int);**<br>This function returns the absolute value of an integer that is passed to it. |
| 9 | **double fabs(double);**<br>This function returns the absolute value of any decimal number passed to it. |
| 10 | **double floor(double);**<br>Finds the integer which is less than or equal to the argument passed to it. |

Following is a simple example to show few of the mathematical operations:

```cpp
#include <iostream>
#include <cmath>

using namespace std;

int main ()
{
    // number definition:
    short s = 10;
    int   i = -1000;
    long  l = 100000;
    float f = 230.47;
```
