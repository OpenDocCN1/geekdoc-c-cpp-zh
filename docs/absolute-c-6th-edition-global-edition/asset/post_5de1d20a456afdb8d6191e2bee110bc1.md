
## Display 10.8 Returning a Pointer to an Array

```
#include <iostream>
using namespace std;

int* doubler(int a[], int size);
//Precondition: size is the size of the array a.
//All indexed variables of a have values.
//Returns: a pointer to an array of the same size as a in which
//each indexed variable is double the corresponding element in a.

int main()
{
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

    delete[] b;
    return 0;
}

int* doubler(int a[], int size)
{
    int* temp = new int[size];

    for (int i =0; i < size; i++)
        temp[i] = 2*a[i];

    return temp;
}
```

This call to delete is not really needed since the program is ending, but in another context it could be important to include this delete.

Sample Dialogue

```
Array a:
1 2 3 4 5
Array b:
2 4 6 8 10
```

## Self-Test Exercises

9. Write a type definition for pointer variables that will be used to point to dynamically allocated arrays. The array elements are to be of type char. Call the type CharArray.

10. Suppose your program contains code to create a dynamically allocated array as follows:

```
int *entry;
entry = new int[10];
```

so that the pointer variable entry is pointing to this dynamically allocated array. Write code to fill this array with ten numbers typed in at the keyboard.

11. Suppose your program contains code to create a dynamically allocated array as in Self-Test Exercise 10, and suppose the pointer variable entry has not had its (pointer) value changed. Write code to destroy this dynamically allocated array and return the memory it uses to the freestore manager.

12. What is the output of the following code fragment?

```
int a[10];
int arraySize = 10;
int *p = a;
int i;
for (i = 0; i < arraySize; i++)
    a[i] = i;
for (i = 0; i < arraySize; i++)
    cout << p[i] << " ";
cout << endl;
```

## Pointer Arithmetic

You can perform a kind of arithmetic on pointers, but it is an arithmetic of addresses, not an arithmetic of numbers. For example, suppose your program contains the following code:

```
typedef double* DoublePtr;
DoublePtr d;
d = new double[10];
```

After these statements, d contains the address of the indexed variable d[0]. The expression d + 1 evaluates to the address of d[1], d + 2 is the address of d[2], and so forth. Notice that although the value of d is an address and an address is a number, d + 1 does not simply add 1 to the number in d. If a variable of type double requires eight bytes (eight memory locations) and d contains the address 2000, then d + 1 evaluates to the memory address 2008. Of course, the type double can be replaced by any other type, and then pointer addition moves in units of variables for that type.

addresses, not numbers

This pointer arithmetic gives you an alternative way to manipulate arrays. For example, if arraySize is the size of the dynamically allocated array pointed to by d, then the following will output the contents of the dynamic array:

```
for (int i = 0; i < arraySize; i++)
    cout << *(d + i)<< " ";
```

The previous is equivalent to the following:

```
for (int i = 0; i < arraySize; i++)
    cout << d[i] << " ";
```

You may not perform multiplication or division of pointers. All you can do is add an integer to a pointer, subtract an integer from a pointer, or subtract two pointers of the same type. When you subtract two pointers, the result is the number of indexed variables between the two addresses. Remember, for subtraction of two pointer values, these values must point into the same array! It makes little sense to subtract a pointer that points into one array from another pointer that points into a different array.

You can also use the increment and decrement operators, ++ and --, to perform pointer arithmetic. For example, d++ will advance the value of d so that it contains the address of the next indexed variable, and d-- will change d so that it contains the address of the previous indexed variable.

## Multidimensional Dynamic Arrays

You can have multidimensional dynamic arrays. You just need to remember that multidimensional dynamic arrays are arrays of arrays or arrays of arrays of arrays and so forth. For example, to create a two-dimensional dynamic array you must remember that it is an array of arrays. To create a two-dimensional array of integers, you first create a one-dimensional dynamic array of pointers of type int*, which is the type for a one-dimensional array of ints. Then you create a dynamic array of ints for each element of the array.

A type definition may help to keep things straight. The following is the variable type for an ordinary one-dimensional dynamic array of ints:

```
typedef int* IntArrayPtr;
```

To obtain a three-by-four array of ints, you want an array whose base type is IntArrayPtr. For example,

```
IntArrayPtr *m = new IntArrayPtr[3];
```

This is an array of three pointers, each of which can name a dynamic array of ints, as follows:

```
for {int i = 0; i < 3; i++}
m[i] = new int[4];
```

The resulting array m is a three-by-four dynamic array. A simple program to illustrate this is given in Display 10.9.

## How to Use a Dynamic Array

- **Define a pointer type:** Define a type for pointers to variables of the same type as the elements of the array. For example, if the dynamic array is an array of doubles, you might use the following:
  
  ```
  typedef double* DoubleArrayPtr;
  ```

- **Declare a pointer variable:** Declare a pointer variable of this defined type. The pointer variable will point to the dynamically allocated array in memory and will serve as the name of the dynamic array.
  
  ```
  DoubleArrayPtr a;
  ```
  (Alternatively, without a defined pointer type, use double *a;).

- **Call new:** Create a dynamic array using the new operator:
  
  ```
  a = new double [arraySize];
  ```
  
  The size of the dynamic array is given in square brackets as in the previous example. The size can be given using an int variable or other int expression. In the previous example, arraySize can be a variable of type int whose value is determined while the program is running.

- **Use like an ordinary array:** The pointer variable, such as a, is used just like an ordinary array. For example, the indexed variables are written in the usual way: a[0], a[1], and so forth. The pointer variable should not have any other pointer value assigned to it, but should be used like an array variable.

- **Call delete []:** When your program is finished with the dynamically allocated array variable, use delete and empty square brackets along with the pointer variable to eliminate the dynamic array and return the storage that it occupies to the freestore manager for reuse. For example,
  
  ```
  delete [] a;
  ```

Be sure to notice the use of delete in Display 10.9. Since the dynamic array m is an array of arrays, each of the arrays created with new in the for loop on lines 13 and 14 must be returned to the freestore manager with a call to delete []; then, the array m itself must be returned to the freestore manager with another call to delete []. There must be a call to delete [] for each call to new that created an array. (Since the program ends right after the calls to delete [], we could safely omit the calls to delete [], but we wanted to illustrate their usage.)

## Display 10.9 A Two-Dimensional Dynamic Array

```
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
    // m is now a d1-by-d2 array.

    cout << "Enter " << d1 << " rows of "
         << d2 << " integers each:\n";
    for (i = 0; i < d1; i++)
        for (j = 0; j < d2; j++)
            cin >> m[i][j];

    cout << "Echoing the two-dimensional array:\n";
    for (i = 0; i < d1; i++) {
        for (j = 0; j < d2; j++)
            cout << m[i][j] << " ";
        cout << endl;
    }

    for (i = 0; i < d1; i++)
        delete[] m[i];
    delete [] m;

    return 0;
}
```

Note that there must be one call to delete[] for each call to new that created an array. (These calls to delete[] are not really needed since the program is ending, but in another context it could be important to include them.)

## Sample Dialogue

```
Enter the row and column dimensions of the array:
3 4
Enter 3 rows of 4 integers each:
1 2 3 4
5 6 7 8
9 0 1 2
Echoing the two-dimensional array:
1 2 3 4
5 6 7 8
9 0 1 2
```
