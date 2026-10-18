A default argument is checked for type at the time of declaration and evaluated at the time of call. One important point to note is that only the trailing arguments can have default values and therefore we must add defaults from _right to left._ We cannot provide a default value to a particular argument in the middle of an argument list. Some examples of function declaration with default values are:

Default arguments are useful in situations where some arguments always have the same value. For instance, bank interest may remain the same for all customers for a particular period of deposit. It also provides a greater flexibility to the programmers. A function can be written with more parameters than are required for its most common application. Using default arguments, a programmer can use only those arguments that are meaningful to a particular situation. Program 4.2 illustrates the use of default arguments.

# Program 4.2 Default Arguments

```
#include<iostream>
#include<conio.h>

using namespace std;

int main( )
{
    float amount;
    float value(float p, int n, float r-0.15); //prototype
    void println(char ch-‘*’,int len-40); //prototype
    println();
    //use default values for arguments
```