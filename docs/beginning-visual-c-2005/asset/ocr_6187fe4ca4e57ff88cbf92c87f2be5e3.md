As long as the function header and function prototype indicate the return type appropriately, you have no problem— or at least no apparent problem. Assuming that the variable value is of type double, the prototype of a function called treble, which might contain the above return statement, could be as follows:

```
double* treble(double data);
```

I have defined the parameter list arbitrarily here.

So let’s look at a function that returns a pointer. It’s only fair that I warn you in advance — this function doesn’t work, but it is educational. Let’s assume that you need a function that returns a pointer to a memory location containing three times its argument value. Our first attempt the implement such a function might look like this:

```
// Function to treble a value - mark 1
double* treble(double data)
{
    double result = 0.0;

    result = 3.0*data;
    return &result;
}
```

# Try It Out    Returning a Bad Pointer

You could create a little test program to see what happens (remember that the treble function won’t work as expected):

```
//Ex5_11.cpp
#include <iostream>
using std::cout;
using std::endl;

double* treble(double);            // Function prototype

int main(void)
{
    double num = 5.0;               // Test value
    double* ptr = 0;                // Pointer to returned value

    ptr = treble(num);

    cout << endl
         << "Three times num = " << 3.0*num;

    cout << endl
         << "Result = " << *ptr;     // Display 3*num

    cout << endl;
    return 0;
```