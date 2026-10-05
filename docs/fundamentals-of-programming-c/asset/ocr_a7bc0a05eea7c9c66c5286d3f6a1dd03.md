# 11.1. VECTORS

Programmers use the shorter syntax exactly, but the longer expression illustrates the fact that the square bracket `{}` operator is really a class method.

As we have seen, a programmer must be vigilant about avoiding an out-of-bounds index with the `operator[]` method. The vector class provides an additional method, `at`, that provides bounds checking. Checking expression `vec[x]` in and itself provides no bounds checking and so may prevent undefined behavior. The functionally equivalent `vec.at(x)` will ensure that the index `x` is within the bounds of the vector. If `x` is outside the range of indices, it is guaranteed to produce a run-time error. (vectorofbounds2.cpp) Listing 11.6 is a variation of Listing 11.4 that uses the `at` method of the `operator[]` method.

# Listing 11.6: vectorofbounds2.cpp

```
#include <iostream>
#include <vector>
using namespace std;
int main() {
    const int SIZE = 3;
    vector<int> a(5, 5);
    // Print the contents of the vector
    cout << "a contains";
    for (int i = 0; i < SIZE; i++)
        cout << a.at(i) << " ";
    cout << endl;
    // Change all 5s in vector to 8s
    for (int i = 0; i < SIZE; i++) // Bug: should be
        a.at(i) = 8;
    // Reprint the contents of the vector
    cout << "a contains";
    for (int i = 0; i < SIZE; i++)
        cout << a.at(i) << " ";
    cout << endl;
}
```

When compiled and executing Listing 11.6 (vectorofbounds2.cpp) is guaranteed to produce a run-time error.

The size method returns the number of elements in a vector. The following code prints the contents of vector list:

```
int n = list.size();
for (int i = 0; i < n; i++)
    cout << list[i] << " ";
cout << endl;
```

The exact type that the size method returns is a `vector<int>::size_type`. This type is compatible with the `unsigned` type and may be assigned to an `int` variable as shown above. We can avoid the additional local variable `n` as follows:

```
for (unsigned i = 0; i < list.size(); i++)
    cout << list[i] << " ";
cout << endl;
```

Notice that i's declared type is `unsigned`, not `int`. This prevents a warning when comparing i to list.size(). A comparison between signed and unsigned integer types is potentially dangerous, and