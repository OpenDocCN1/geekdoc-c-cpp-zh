
```cpp
// Fig. 8.12: fig08_12.cpp
// Attempting to modify data through a
// nonconstant pointer to constant data.

void f( const int * ); // prototype

int main()
{
    int y;

    f( &y ); // f attempts illegal modification
    return 0; // indicates successful termination
} // end main

// xPtr cannot modify the value of constant variable to which it points
void f( const int *xPtr )
{
    *xPtr = 100; // error: cannot modify a const object
} // end function f
```

*Borland C++ command-line compiler error message:*

```
Error E2024 fig08_12.cpp 18:
    Cannot modify a const object in function f(const int *)
```

*Microsoft Visual C++ compiler error message:*

```
c:\cppf_examples\ch08\Fig08_12\fig08_12.cpp(18) :
    error C3892: '*xPtr' : you cannot assign to a variable that is const
```

*GNU C++ compiler error message:*

```
fig08_12.cpp: In function `void f(const int*)':
fig08_12.cpp:18: error: assignment of read-only location
```

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_345_0.png)

**Fig. 8.12** | Attempting to modify data through a nonconstant pointer to constant data.

As we know, arrays are aggregate data types that store related data items of the same type under one name. When a function is called with an array as an argument, the array is passed to the function by reference. However, objects are always passed by value—a copy of the entire object is passed. This requires the execution-time overhead of making a copy of each data item in the object and storing it on the function call stack. When an object must be passed to a function, we can use a pointer to constant data (or a reference to constant data) to get the performance of pass-by-reference and the protection of pass-by-value. When a pointer to an object is passed, only a copy of the address of the object must be made—the object itself is not copied. On a machine with four-byte addresses, a copy of four bytes of memory is made rather than a copy of a possibly large object.

## Performance Tip 8.1

> If they do not need to be modified by the called function, pass large objects using pointers to constant data or references to constant data, to obtain the performance benefits of pass-by-reference.

## Software Engineering Observation 8.3

Pass large objects using pointers to constant data, or references to constant data, to obtain the security of pass-by-value.

## Constant Pointer to Nonconstant Data

A constant pointer to nonconstant data is a pointer that always points to the same memory location; the data at that location can be modified through the pointer. An example of such a pointer is an array name, which is a constant pointer to the beginning of the array. All data in the array can be accessed and changed by using the array name and array subscripting. A constant pointer to nonconstant data can be used to receive an array as an argument to a function that accesses array elements using array subscript notation. Pointers that are declared const must be initialized when they are declared. (If the pointer is a function parameter, it is initialized with a pointer that is passed to the function.) The program of Fig. 8.13 attempts to modify a constant pointer. Line 11 declares pointer ptr to be of type int * const. The declaration in the figure is read from right to left as “ptr is a constant pointer to a nonconstant integer.” The pointer is initialized with the address of integer variable x. Line 14 attempts to assign the address of y to ptr, but the compiler generates an error message. Note that no error occurs when line 13 assigns the value 7 to

```
// Fig. 8.13: fig08_13.cpp
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
    return 0; // indicates successful termination
} // end main
```

Borland C++ command-line compiler error message:

```
Error E2024 fig08_13.cpp 14: Cannot modify a const object in function main()
```

Microsoft Visual C++ compiler error message:

```
c:\cppfp_examples\ch08\Fig08_13\fig08_13.cpp(14) : error C3892: 'ptr' : you cannot assign to a variable that is const
```

GNU C++ compiler error message:

```
fig08_13.cpp: In function `int main()':
fig08_13.cpp:14: error: assignment of read-only variable `ptr'
```

Fig. 8.13 | Attempting to modify a constant pointer to nonconstant data.

*ptr—the nonconstant value to which ptr points can be modified using the dereferenced ptr, even though ptr itself has been declared const.

## Common Programming Error 8.6

Not initializing a pointer that is declared const is a compilation error.

## Constant Pointer to Constant Data

The least amount of access privilege is granted by a constant pointer to constant data. Such a pointer always points to the same memory location, and the data at that memory location cannot be modified using the pointer. This is how an array should be passed to a function that only reads the array, using array subscript notation, and does not modify the array. The program of Fig. 8.14 declares pointer variable ptr to be of type const int * const (line 14). This declaration is read from right to left as “ptr is a constant pointer to an integer constant.” The figure shows the error messages generated when an attempt is

```
1  // Fig. 8.14: fig08_14.cpp
2  // Attempting to modify a constant pointer to constant data.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  int main()
8  {
9      int x = 5, y;
10
11     // ptr is a constant pointer to a constant integer.
12     // ptr always points to the same location; the integer
13     // at that location cannot be modified.
14     const int *const ptr = &x;
15
16     cout << *ptr << endl;
17
18     *ptr = 7; // error: "*ptr is const; cannot assign new value"
19     ptr = &y; // error: "ptr is const; cannot assign new address"
20     return 0; // indicates successful termination
21  } // end main
```

Borland C++ command-line compiler error message:

```
Error E2024 fig08_14.cpp 18: Cannot modify a const object in function main()
Error E2024 fig08_14.cpp 19: Cannot modify a const object in function main()
```

Microsoft Visual C++ compiler error message:

```
c:\cppfp_examples\ch08\Fig08_14\fig08_14.cpp(18) : error C3892: 'ptr' :
    you cannot assign to a variable that is const
c:\cppfp_examples\ch08\Fig08_14\fig08_14.cpp(19) : error C3892: 'ptr' :
    you cannot assign to a variable that is const
```

# GNU C++ compiler error message:

```
fig08_14.cpp: In function `int main()':
fig08_14.cpp:18: error: assignment of read-only location
fig08_14.cpp:19: error: assignment of read-only variable `ptr'
```

Fig. 8.14 | Attempting to modify a constant pointer to constant data. (Part 2 of 2.)

made to modify the data to which ptr points (line 18) and when an attempt is made to modify the address stored in the pointer variable (line 19). Note that no errors occur when the program attempts to dereference ptr, or when the program attempts to output the value to which ptr points (line 16), because neither the pointer nor the data it points to is being modified in this statement.

## 8.6 Selection Sort Using Pass-by-Reference

In this section, we define a sorting program to demonstrate passing arrays and individual array elements by reference. We use the selection sort algorithm, which is an easy-to-program, but unfortunately inefficient, sorting algorithm. The first iteration of the algorithm selects the smallest element in the array and swaps it with the first element. The second iteration selects the second-smallest element (which is the smallest element of the remaining elements) and swaps it with the second element. The algorithm continues until the last iteration selects the second-largest element and swaps it with the second-to-last index, leaving the largest element in the last index. After the iᵗʰ iteration, the smallest i items of the array will be sorted into increasing order in the first i elements of the array.

As an example, consider the array

34 56 4 10 77 51 93 30 5 52

A program that implements the selection sort first determines the smallest value (4) in the array, which is contained in element 2. The program swaps the 4 with the value in element 0 (34), resulting in

4 56 34 10 77 51 93 30 5 52

[Note: We use bold to highlight the values that were swapped.] The program then determines the smallest value of the remaining elements (all elements except 4), which is 5, contained in element 8. The program swaps the 5 with the 56 in element 1, resulting in

4 5 34 10 77 51 93 30 56 52

On the third iteration, the program determines the next smallest value, 10, and swaps it with the value in element 2 (34).

4 5 10 34 77 51 93 30 56 52

The process continues until the array is fully sorted.

4 5 10 30 34 51 52 56 77 93

Note that after the first iteration, the smallest element is in the first position. After the second iteration, the two smallest elements are in order in the first two positions. After the third iteration, the three smallest elements are in order in the first three positions.
