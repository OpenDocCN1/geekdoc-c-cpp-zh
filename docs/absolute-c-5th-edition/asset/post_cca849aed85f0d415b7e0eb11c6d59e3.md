
## Display 10.7 A Dynamically Allocated Array (part 2 of 2)

```cpp
36 //Uses the library <iostream>:
37 void fillArray(int a [], int size)
38 {
39     cout << "Enter " << size << " integers\n";
40     for (int index = 0; index < size; index++)
41         cin >> a[index];
42 }
```

```cpp
43 int search(int a [], int size, int target)
44 {
45     int index = 0;
46     while (a[index] != target && (index < size))
47         index++;
48     if (index == size) if (target is not in a)
49         index = -1;
50     return index;
51 }
```

Sample Dialogue

> This program searches a list of numbers.
How many numbers will be on the list? 5
Enter 5 integers.
1 2 3 4 5
Enter a value to search for: 3
3 is element 2 in the array.

delete [] The delete statement, which destroys the dynamically allocated array pointed to by a[] in Display 10.7. Since the program is about to end anyway, we did not really need this delete statement; if the program went to do other things, however, you would want a delete statement so that the memory used by this dynamically allocated array was returned to the freedom manager. The delete statement is similar to the delete statement you saw earlier, except that with a dynamically allocated array you must include an empty pair of square brackets like:

```cpp
delete [] a;
```

The square brackets tell C++ that a dynamically allocated array variable is being eliminated, so the system checks the size of the array and removes that many indexed variables. If you omit the square brackets you will not be eliminating the entire array. For example.

```cpp
delete a;
```

# CHAPTER 10 Pointers and Dynamic Arrays

is legal, but the error is not detected by most compilers. The C++ standard says that what happens when you do this is "undefined." That means that the compiler can do anything that is convenient (for the compiler writer, for you). Always use the

```cpp
delete [] arrayPtr;
```

syntax when you are deleting memory that was allocated with something like

```cpp
arrayPtr = new MyType[
```

Also note the position of the square brackets in the delete statement

```cpp
delete [] arrayPtr; //Correct
delete arrayPtr[]; //ILLEGAL!
```

You create a dynamically allocated array with a call to new using a pointer, such as the pointer in Display 10.7. After the call to new, you should not assign any other pointer value to this variable because can confuse the system when the memory for the dynamic array is returned to the freestore manager with a call to delete.
Dynamically allocated arrays are created using new and a pointer variable. When your program is finished using a dynamically allocated array, you should return the array memory to the freestore manager with a call to delete. Other than that, a dynamically allocated array can be used just like any other array.

# EXAMPLE: A Function That Returns an Array

In C++ an array type is not allowed as the return type of a function. For example, the following is illegal:

```cpp
int someFunction( ); //ILLEGAL
```

If you want to create a function similar to this, you must return a pointer to the array base type and use the pointer point to the array. So, the function declaration would be follows:

```cpp
int* someFunction( ); //Legal
```

An example of a function that returns a pointer to an array is given in Display 10.8.

# Dynamic Arrays 443

```cpp
#include <iostream>
using namespace std;

int* doubler(int, int size);
//Precondition: size is the size of the array a.
//All indexed variables of a have values.
//Returns: a pointer to an array of the same size as a in which
//each indexed variable is double the corresponding element in a.

int main() {
    int a[] = {1, 2, 3, 4, 5};
    int* b;

    b = doubler(a, 5);

    int i;
    cout << "Array a:\n";
    for (i = 0; i < 5; i++)
        cout << a[i] << " ";
    cout << endl;
    cout << "Array b:\n";
    for (i = 0; i < 5; i++)
        cout << b[i] << " ";
    cout << endl;

    delete b;
    return 0;
}

int* doubler(int a[], int size) {
    int* temp = new int[size];
    for (i = 0; i < size; i++)
        temp[i] = 2*a[i];

    return temp;
}
```

Display 10.8 Returning a Pointer to an Array

> This call to delete is not really needed since in another context it could be important to include this delete.

Sample Dialogue
Array a:
1 2 3 4 5
Array b:
2 4 6 8 10

# CHAPTER 10

# Self-Test Exercises

- 9. Write a type definition for pointer variables that will be used to point to dynamically allocated arrays. The array elements are to of type char. Call the type JSONArray.
- 10. Note the position of the square brackets in the delete statement. Why is `delete arrayPtr[];` illegal?
- 11. If a function returns a pointer to an array, how should the caller manage the memory allocated for that array?
- 12. What is the output of the following code?
```cpp
int a[] = {1, 2, 3, 4, 5};
int* p = a;
for (int i = 0; i < 5; i++)
    cout << p[i] << " ";
```

# Pointer Arithmetic

This pointer arithmetic gives you an alternative to manipulate arrays. For example, if arraySize is the size of the dynamic array pointed to by d, then the following will output the contents of the array:

```cpp
for (int i = 0; i < arraySize; i++)
    cout << *(d + i);
```

The previous is equivalent to:

```cpp
for (int i = 0; i < arraySize; i++)
    cout << d[i];
```

You may not perform multiplication or division of pointers. All you can do is add an integer to a pointer, subtract an integer from a pointer, or subtract two pointers of the same type. When you subtract two pointers, the result is the number of indexed variables between the two. Remember, for subtraction of two pointers, these values must point into the same array makes little sense to subtract a pointer that points into one array from another that points into a different array.

You can also use the increment and decrement operators, ++ and --, to perform pointer arithmetic. For, d++ will advance the value of d so that it contains the address of the next indexed variable, and d-- will change d so that it contains the address of the previous indexed variable.

# Multidimensional Dynamic Arrays

You can have multidimensional dynamic arrays. You just need to remember that multidimensional dynamic arrays are arrays of arrays or arrays of arrays and so forth. For example, to create a two-dimensional dynamic array of integers, you must remember to create a one-dimensional dynamic array of pointers of type int*, which is the type for a one-dimensional dynamic array of ints. You create a dynamic array of ints for each element of the array.

A type definition may help keep things straight. The following is the variable type for an ordinary multidimensional dynamic array of ints:

```cpp
typedef int* IntArrayPtr;
```

To obtain a three-by-four array of ints, you want an array whose base type is IntArrayPtr. For example,

```cpp
IntArrayPtr *m = new IntArrayPtr[3];
```

This is an array of three pointers, each which can name a dynamic array of ints, as follows:

```cpp
for (int i = 0; i < 3; i++)
    m[i] = new int[4];
```

The resulting m is a three-by-four dynamic array. A simple program to illustrate this is given in Display 10.9.
