# 11.1. VECTORS

the compiler will alert us to that fact. To see why you should not take this warning lightly, consider the following code that we might expect to print:

```
unsigned u = 0;
int i = 0;
while (i < u - 1) {
    cout << i << endl;
    i++;
}
```

but it is printed that many unsigned values as the system supports! This is because even 0 is not less than -1,-1 is a signed value, not an unsigned value. The unsigned data type cannot represent signed numbers. An attempt to compute unsigned 0 minus 1 on a 32-bit system produces 4,294,967,295, which is definitely not zero. To be safe, assign the value of the size to an int variable or use unsigned variables to control loop iterations. Better yet, use range-for whenever possible.

The empty method is a convenience method; if vec is a vector, the expression vec.empty() != 0. That empty method does not make the vector empty; it returns true if the vector is empty and false if it is not.

The clear method removes all the elements from a vector leaving it. Invoking clear on an initially empty vector has no effect. The vector's size method will return zero, its empty method will return true, and a call to its operator[] method with any index of zero will exhibit undefined behavior.

# 11.1.4 Vectors and Functions

A function can accept a vector as a parameter in Listing 11.7 (vectortofunc.cpp)

Listing 11.7: vectortofunc.cpp
#include <iostream>
#include <vector>

using namespace std;

/*
* print(v)
* Prints the contents of an int vector
* v is the vector to print
*/
void print(vector<int> v) {
    for (int elem : v)
        cout << elem << " ";
    cout << endl;
}

/
* sum(v)
* Adds the contents of an int vector
* v is the vector to sum
* Returns the sum of all the elements
* zero if the vector is empty.