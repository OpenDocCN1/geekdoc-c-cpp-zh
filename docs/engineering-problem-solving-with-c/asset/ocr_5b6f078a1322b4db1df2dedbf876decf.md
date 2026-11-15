We will test this function with the following driver program:

```
```cpp
#include<iostream> //Required for cin, cout.
using namespace std;

//Function prototype
void swapIntegers(int&, int&);
int main()
{
    //Declare variables.
    int a, b;

    //Get values for a and b.
    cout << "Enter two integer values: ";
    cin >> a >> b;

    //Print values of a and b before the swap
    cout << "Before swap:\n a is " << a << " b is " << b << endl;

    //Call swap function and print values
    swapIntegers(a,b);
    cout << "After call to swapIntegers\na is " << a
         << " b is " << b << endl;

    //Exit main
    return 0;
}
```
```

A sample run of our driver program produces the following results:

enter two integer values: 5 10
Before swap:
a is 5 b is 10
After call to swapIntegers
a is 10 b is 5

![](bbox=[0.58, 0.6, 0.88, 0.69])

To further illustrate pass by reference, we provide a trace of the execution of our program. Omitting the cout statements. Note that directed arrows are used to indicate that the formal parameters reference, or point to the function arguments when pass by reference is used.

# Program Trace

![](bbox=[0.23, 0.8, 0.87, 0.95])