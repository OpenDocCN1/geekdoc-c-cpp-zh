```
// Fig. 8.13: fig08_13.cpp
// Sizeof operator when used on a built-in array's name
// returns the number of bytes in the built-in array.
#include <iostream>
using namespace std;

size_t getSize(double*); // prototype

int main() {
    double numbers[20]; // 20 doubles; occupies 160 bytes on our system

    cout << "The number of bytes in the array is " << sizeof(numbers);

    cout << "\nThe number of bytes returned by getSize is "
         << getSize(numbers) << endl;
}

// return size of ptr
size_t getSize(double* ptr) {
    return sizeof(ptr);
}
```

```
The number of bytes in the array is 160
The number of bytes returned by getSize is 4
```

Fig. 8.13 **sizeof** operator when applied to a built-in array’s name returns the number of bytes in the built-in array.

The number of *elements* in a built-in array can be determined using the results of two `sizeof` operations. For example, to determine the number of elements in the built-in array `numbers`, use the following expression (which is evaluated at *compile time*):

```
sizeof numbers / sizeof(numbers[0])
```

The expression divides the number of bytes in `numbers` (160, assuming 8-byte `double`s) by the number of bytes in the built-in array’s