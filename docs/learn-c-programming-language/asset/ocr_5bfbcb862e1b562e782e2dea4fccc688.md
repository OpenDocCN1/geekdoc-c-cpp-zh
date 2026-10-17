Second point to remember is that C++ does not advocate to return the address of a local variable to outside of the function so you would have to define the local variable as **static** variable.

Now, consider the following function, which will generate 10 random numbers and return them using an array and call this function as follows:

```
```cpp
#include <iostream>

#include <ctime>

using namespace std;

// function to generate and retrun random numbers.
int * getRandom( )
{
    static int  r[10];

    // set the seed
    srand( (unsigned)time( NULL ) );
    for (int i = 0; i < 10; ++i)
    {
        r[i] = rand();
        cout << r[i] << endl;
    }

    return r;
}

// main function to call above defined function.
int main ()
{
    // a pointer to an int.
    int *p;
```
```