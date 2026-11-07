```
```cpp
// Fig. 8.10: fig08_10.cpp
// Attempting to modify data through a
// nonconstant pointer to constant data.

void f( const int * ); // prototype

int main()
{
    int y;

    f( &y ); // f attempts illegal modification
} // end main

// xPtr cannot modify the value of constant variable to which it points
void f( const int *xPtr )
{
    *xPtr = 100; // error: cannot modify a const object
} // end function f
```
```

*Microsoft Visual C++ compiler error message:*

```
```text
c:\cpphtp8_examples\ch08\Fig08_10\fig08_10.cpp(17) :
    error C3892: 'xPtr' : you cannot assign to a variable that is const
```
```

*GNU C++ compiler error message:*

```
```text
fig08_10.cpp: In function 'void f(const int*)':
fig08_10.cpp:17: error: assignment of read-only location
```
```

**Fig. 8.10** | Attempting to modify data through a nonconstant pointer to constant data.

As you know, arrays are aggregate data types that store related data items of the same type under one name. When a function is called with an array as an argument, the array is passed to the function by reference. However, by default, objects are passed by value—a copy of the entire object is passed. This requires the execution-time overhead of making a copy of each data item in the object and storing it on the function call stack. When a pointer to an object is passed, only a copy of the address of the object must be made—the object itself is not copied.

![](bbox=[0.16, 0.735, 0.214, 0.771])

> > **Performance Tip 8.1**
> > 
> > If they do not need to be modified by the called function, pass large objects using pointers to constant data or references to constant data, to obtain the performance benefits of pass-by-reference.

![](bbox=[0.16, 0.824, 0.214, 0.861])

> > **Software Engineering Observation 8.3**
> > 
> > Pass large objects using pointers to constant data, or references to constant data, to obtain the security of pass-by-value.

# *Constant Pointer to Nonconstant Data*

A constant pointer to nonconstant data is a pointer that always points to the same memory location; the data at that location can be modified through the pointer. An example of