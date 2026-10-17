```
```cpp
double* pvalue = NULL;

if( !(pvalue = new double ))
{
    cout << "Error: out of memory." <<endl;
    exit(1);
}
```
```

The **malloc()** function from C, still exists in C++, but it is recommended to avoid using malloc() function. The main advantage of new over malloc() is that new doesn't just allocate memory, it constructs objects which is prime purpose of C++.

At any point, when you feel a variable that has been dynamically allocated is not anymore required, you can free up the memory that it occupies in the free store with the delete operator as follows:

```
```cpp
delete pvalue;        // Release memory pointed to by pvalue
```
```

Let us put above concepts and form the following example to show how new and delete work:

```
```cpp
#include <iostream>

using namespace std;

int main ()
{
    double* pvalue = NULL;  // Pointer initialized with null
    pvalue = new double;    // Request memory for the variable

    *pvalue = 29494.99;     // Store value at allocated address
    cout << "Value of pvalue : " << *pvalue << endl;

    delete pvalue;          // free up the memory.

    return 0;
}
```
```

If we compile and run above code, this would produce the following result: