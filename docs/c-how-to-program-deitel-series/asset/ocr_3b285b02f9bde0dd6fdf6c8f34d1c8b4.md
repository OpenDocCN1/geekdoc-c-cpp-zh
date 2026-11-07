a constant pointer to a nonconstant integer.” The pointer is initialized with the address of integer variable x. Line 14 attempts to assign the address of y to ptr, but the compiler generates an error message. No error occurs when line 13 assigns the value 7 to *ptr—the nonconstant value to which ptr points can be modified using the dereferenced ptr, even though ptr itself has been declared const.

```
```cpp
// Fig. 8.11: fig08_11.cpp
// Attempting to modify a constant pointer to nonconstant data.

int main()
{
    int x, y;

    // ptr is a constant pointer to an integer that can
    // be modified through ptr, but ptr always points to the
    // same memory location.
    int * const ptr = &x; // const pointer must be initialized

    *ptr = 7; // allowed: *ptr is not const
    ptr = &y; // error: ptr is const; cannot assign to it a new address
} // end main()
```
```

> you cannot assign to a variable that is const

Fig. 8.11  |  Attempting to modify a constant pointer to nonconstant data.

# 8.6.4 Constant Pointer to Constant Data

The minimum access privilege is granted by a constant pointer to constant data. Such a pointer always points to the same memory location, and the data at that location cannot be modified via the pointer. This is how a built-in array should be passed to a function that only reads from the built-in array, using array subscript notation, and does not modify the built-in array. The program of Fig. 8.12 declares pointer variable ptr to be of type const int * const (line 13). This declaration is read from right to left as “ptr is a constant pointer to an integer constant.” The figure shows the Xcode LLVM compiler’s error messages that are generated when an attempt is made to modify the data to which ptr points (line 17) and when an attempt is made to modify the address stored in the pointer variable (line 18)—these show up on the lines of code with the errors in the Xcode text editor. In line 15, no errors occur when the program attempts to dereference ptr, or when the program attempts to output the value to which ptr points, because neither the pointer nor the data it points to is being modified in this statement.

```
```cpp
// Fig. 8.12: fig08_12.cpp
// Attempting to modify a constant pointer to constant data.
#include <iostream>
```
```

Fig. 8.12  |  Attempting to modify a constant pointer to constant data. (Part 1 of 2.)