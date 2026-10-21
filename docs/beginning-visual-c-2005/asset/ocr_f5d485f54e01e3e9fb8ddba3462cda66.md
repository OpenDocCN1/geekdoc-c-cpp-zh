# Returning a Reference

You can also return a reference from a function. This is just as fraught with potential errors as returning a pointer, so you need to take care with this too. Because a reference has no existence in its own right (it’s always an alias for something else), you must be sure that the object that it refers to still exists after the function completes execution. It’s very easy to forget this when you use references in a function because they appear to be just like ordinary variables.

References as return types are of primary significance in the context of object-oriented programming. As you will see later in the book, they enable you to do things that would be impossible without them. (This particularly applies to “operator overloading,” which I’ll come to in Chapter 9.) The principal characteristic of a reference-type return value is that it’s an lvalue. This means that you can use the result of a function that returns a reference on the left side of an assignment statement.

# Try It Out Returning a Reference

Next, look at one example that illustrates the use of reference return types, and also demonstrates how a function can be used on the left of an assignment operation when it returns an lvalue. This example assumes that you have an array containing a mixed set of values. Whenever you want to insert a new value into the array, you want to replace the element with the lowest value.

```
// Ex5_12.cpp
// Returning a reference
#include <iostream>
#include <iomanip>
using std::cout;
using std::endl;
using std::setw;

double& lowest(double values[], int length); // Prototype of function
                                         // returning a reference

int main(void)
{
    double array[] = { 3.0, 10.0, 1.5, 15.0, 2.7, 23.0,
                       4.5, 12.0, 6.8, 13.5, 2.1, 14.0 };
    int len = sizeof array/sizeof array[0];  // Initialize to number
                                         // of elements

    cout << endl;
    for(int i = 0; i < len; i++)
        cout << setw(6) << array[i];

    lowest(array, len) = 6.9;               // Change lowest to 6.9
    lowest(array, len) = 7.9;               // Change lowest to 7.9

    cout << endl;
    for(int i = 0; i < len; i++)
        cout << setw(6) << array[i];

    cout << endl;
```