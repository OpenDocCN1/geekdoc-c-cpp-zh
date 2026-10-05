
# How to Use a Dynamic Array

- Define a pointer type: Define a type for pointers to variables of the same type as the elements of the array. For example, if the dynamic array is an array of doubles, you might use the following:

```
typedef double* DoublePtr;
```

- Declare a pointer variable: Declare a pointer variable of this defined type. The pointer variable will point to the dynamically allocated array in memory and will serve as the name of the dynamic array.

```
DoubleArrayPtr a;
```

(Alternatively, without a defined pointer, use double *a);

- Call new: Create a dynamic array using the new operator:

```
a = new double[arraySize];
```

The size of the dynamic array is given in square brackets as in the previous example. The size can be given using an int variable or on lines 13 as in the example. arraySize can be a variable of type whose value is determined while the program is running.

- Use an ordinary array: The pointer variable, such as a, is used just like an ordinary array. For example, the indexed variables are written in the usual way: a[0], a[1], and so forth. The pointer variable should not have any other pointer value assigned to it, but should be used like an array variable.

- Call delete []: When your program is finished with the dynamically allocated array, use delete and empty square brackets along with the pointer variable to eliminate the dynamic array and return the storage that it occupies to the freestore manager for reuse. For example:

```
delete [] a;
```

Be to notice the use of delete in Display 10.9. Since the dynamic array m is an array of arrays, each of the arrays created with new in the for loop on lines 13 and 14 must be returned to the freestore manager with a call to delete [];; then, the array m itself must be returned to the freestore manager with another call to delete {}; For each call to new that created an array. (Since the program ends right after the calls to delete [], we could safely omit the calls to delete [], but we wanted to illustrate its usage.)

# Dynamic Arrays

Display 10.9 A Two-Dimensional Dynamic Array

```cpp
#include <iostream>
using namespace std;

typedef int* IntArrayPtr;
int main() {
    int d1, d2;
    cout << "Enter the row and column dimensions of the array:\n";
    cin >> d1 >> d2;
    IntArrayPtr *m = new IntArrayPtr[d1];
    int i, j;
    for (i = 0; i < d1; i++)
        m[i] = new int[d2];
    // m is now a dl-by-dl array.
    cout << "Enter " << d1 << " rows of "
    cout << " " << d2 << " integers:\n";
    for (i = 0; i < d1; i++)
        for (j = 0; j < d2; j++)
            cout << m[i][j] << " ";
    cout << "\nEchoing the two-dimensional array:\n";
    for (i = 0; i < d1; i++)
        delete[] m[i];
    delete[] m;
    return 0;
}
```

> Note that there must be one call to delete[] for each call to new that created an array. These cases to delete[] are not really needed since the program is ending, but in another context it could be important to include.

Sample Dialogue

Enter the row and column dimensions of the array:
3 4
Enter 3 rows of 4 integers:
1 2 3 4
5 6 7 8
9 0 1 2
Echoing the two-dimensional array:
1 2 3 4
5 6 7 8
9 0 1 2

# 10.3 Classes, Pointers, and Dynamic Arrays

The combinations are endless.

A dynamically allocated array can have a base type that is a class. A class can have a member variable that is a dynamically allocated array. You can combine classes and dynamically allocated arrays in just about any combination. There are a few things to worry about when using classes and dynamically allocated arrays, but the basic techniques are the ones that you have already used. Many of the techniques presented in this section apply to all dynamically allocated structures, such as those we will discuss in Chapter 17, and not just to classes involving dynamic arrays.

# The -> Operator

C++ has an operator that can be used with a pointer to simplify the notation for specifying the members of a struct or a class. The arrow operator, ->, and a dot operator to specify a member of a dynamic struct or class object that is pointed to by a given pointer. For example, you suppose have the following definition:

```cpp
struct Record
{
  int number;
  char grade;
}
```

The following creates a dynamically allocated variable of type Record and sets the member variables of the dynamic struct variable to 2001 and 'A'.

```cpp
Record *ptr;
ptr = new Record;
ptr->number = 2001;
ptr->grade = 'A';
```

The notations

```
p->grade
```

and

```
(*p).grade
```

have the same meaning. However, the first is more convenient and is almost always the notation used.

arrow operator

# The this Pointer

When defining member functions for a class, you sometimes want to refer to the calling object. The this pointer is a constant pointer that points to the object for which the member function is called. It is only available in non-static member functions. For example, consider the following:

```cpp
class Sample {
public:
    int value;
    void setValue(int value) {
        this->value = value;
    }
    int getValue() const {
        return this->value;
    }
};
```

The `this` pointer is used to distinguish between member variables and parameters that have the same name. This is a common practice in C++ programming.

# Overloading the Assignment Operator

The assignment operator can be overloaded to provide custom behavior when assigning one object to another. The default assignment operator performs a shallow copy, which may not be sufficient for classes that manage dynamic resources.

```cpp
Sample& operator=(const Sample& other) {
    if (this != &other) {
        // Perform deep copy here
    }
    return *this;
}
```
