```
```cpp
// Fig. 8.14: Fig08_14.cpp
// sizeof operator used to determine standard data type sizes.
#include <iostream>
using namespace std;

int main() {
    char c; // variable of type char
    short s; // variable of type short
    int i; // variable of type int
    long l; // variable of type long
    long long ll; // variable of type long long
    float f; // variable of type float
    double d; // variable of type double
    long double ld; // variable of type long double
    int array[20]; // built-in array of int
    int* ptr{array}; // variable of type int*

    cout << "sizeof c = " << sizeof c
         << "\nsizeof(char) = " << sizeof(char)
         << "\nsizeof s = " << sizeof s
         << "\nsizeof(short) = " << sizeof(short)
         << "\nsizeof i = " << sizeof i
         << "\nsizeof(int) = " << sizeof(int)
         << "\nsizeof l = " << sizeof l
         << "\nsizeof(long) = " << sizeof(long)
         << "\nsizeof ll = " << sizeof ll
         << "\nsizeof(long long) = " << sizeof(long long)
         << "\nsizeof f = " << sizeof f
         << "\nsizeof(float) = " << sizeof(float)
         << "\nsizeof d = " << sizeof d
         << "\nsizeof(double) = " << sizeof(double)
         << "\nsizeof ld = " << sizeof ld
         << "\nsizeof(long double) = " << sizeof(long double)
         << "\nsizeof array = " << sizeof array
         << "\nsizeof ptr = " << sizeof ptr << endl;
}
```
```

```
```
sizeof c = 1    sizeof(char) = 1
sizeof s = 2    sizeof(short) = 2
sizeof i = 4    sizeof(int) = 4
sizeof l = 8    sizeof(long) = 8
sizeof ll = 8   sizeof(long long) = 8
sizeof f = 4    sizeof(float) = 4
sizeof d = 8    sizeof(double) = 8
sizeof ld = 16  sizeof(long double) = 16
sizeof array = 80
sizeof ptr = 8
```
```

**Fig. 8.14** `sizeof` operator used to determine standard data type sizes.