of type `const int* const` (line 12). This declaration is read from *right to left* as “*ptr* is a constant pointer to an integer constant.” The figure shows the Xcode LLVM compiler’s error messages that are generated when an attempt is made to modify the data to which *ptr* points (line 16) and when an attempt is made to modify the address stored in the pointer variable (line 17)—these show up on the lines of code with the errors in the Xcode text editor. In line 14, no errors occur when the program attempts to dereference *ptr*, or when the program attempts to output the value to which *ptr* points, because *neither* the pointer *nor* the data it points to is being modified in this statement.

```
```cpp
// Fig. 8.12: fig08_12.cpp
// Attempting to modify a constant pointer to constant data.
#include <iostream>
using namespace std;

int main() {
    int x{5}, y;

    // ptr is a constant pointer to a constant integer.
    // ptr always points to the same location; the integer
    // at that location cannot be modified.
    const int* const ptr{&x};

    cout << *ptr << endl;

    *ptr = 7; // error: *ptr is const; cannot assign new value
    ptr = &y; // error: ptr is const; cannot assign new address
}
```
```

*Xcode LLVM compiler error message:*

```
```text
Read-only variable is not assignable
Read-only variable is not assignable
```
```

# Fig. 8.12 Attempting to modify a constant pointer to constant data.