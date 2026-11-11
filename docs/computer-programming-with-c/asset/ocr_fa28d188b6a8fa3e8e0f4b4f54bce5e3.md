This is a valid combination of functions that can coexist in the program because the data type of one argument is different in both of the functions. The first function takes both the arguments of type `int`, whereas the second function takes one argument of type `int` and the other of type `float`. Hence, these two functions with same name can exists in the same program because their signature is different.

# Example 3:

```
void area(int,float);
void area(float,int);
```

This is a valid combination of functions that can coexist in the program because the order of arguments is different in first and second `area()` functions. Hence, the two functions have a different function signature even if their names are same.

# Example 4:

```
float f1(int,int);
float f2(int,int);
```

This is a valid combination of functions which can coexist in the program because the names of two functions are different. The name of the first function is `f1()` and second function is `f2()`. In this case, it does not matter whether the arguments are same or different.

When a function with same name is defined multiple times in the program with different signatures, then the function name is said to be **overloaded**. For example, let us consider the code below which has two functions with the same name `area()`. Even if the name of the two functions is same, the arguments that each of the `area()` function takes is different. One of the `area()` function takes a single argument of type float, whereas the other area function takes two arguments of type integer, and hence, they have a different signature and can be safely written in the same program. If we observe the set of operations in each of the functions, we see that the `area()` function that takes only one argument actually calculates the area of circle by considering the argument passed to it as a radius value. Also, the area function that takes two arguments actually calculates the area of rectangle by considering the arguments passed to it as a length and breadth values, respectively.

# DEFINITION

When a function with same name is defined multiple times in the program with different signatures, then the function name is said to be **overloaded**.

```
#include<iostream.h>
void area(float r)
{
float area= 3.14*r*r;
cout<<"Area of circle is "<<area<<endl;
}
void area(int l,int b)
{
int area=l*b;
```