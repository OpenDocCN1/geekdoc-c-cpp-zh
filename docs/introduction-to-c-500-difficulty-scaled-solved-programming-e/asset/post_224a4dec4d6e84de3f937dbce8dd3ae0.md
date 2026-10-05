
As you see, there are not many things left to do with ptr. Essentially, what is left is to test the pointer value. And yes, that's a very rare declaration to see in practice. Here is an example to have in mind something similar:

```cpp
const char* const days[] = {"Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"};
```

The outer const prevents the modification of the strings, while the inner prevents the pointers to point somewhere else. We'll discuss array pointers later in this chapter.
Here is a question for you, is the following code correct?

```cpp
const int i = 10;
int *p = &i;
```

Of course, the second statement won't compile. Why? If allowed, we could use the pointer to change the value of i (e.g., *p = 2;) and violate its const nature. The address of a const variable can only be stored in a pointer to const. That, we must write: const int *p;

# POINTER ARITHMETIC

Pointer arithmetic refers to the application of some arithmetic operations on pointers. The allowed operations are presented next.

# Pointers and Integers

The standard says that adding or subtracting an integer from a pointer is guaranteed to produce reliable results only if the pointer points to an array, otherwise the result is undefined. Suppose a pointer variable ptr points to an element of an array. The addition of a positive integer n in an assignment such as:

```cpp
ptr = ptr + n;
```

increases the value by n*size of the pointer's data type and makes the pointer to the address of the n-th element after one. For example, if ptr points to the array arr[i] and n is 3, ptr will point to arr[3]. In Chapter 2, ptr is declared as a pointer of int or float, its value is increased by n*4, since the size of both types is four. If it is a char array, its value is increased by n*1, while if it is a double array, it is increased by n*8. After adding the integer to the pointer, the pointer must point to an array element or the first place past the end which is considered a valid result. Let's see the following program:

```cpp
#include <iostream> // Example 8.8
int main()
{
    int *ptr, arr[] = {1, 2, 3};

    ptr = &arr[0];
    *ptr = 10;
    std::cout << "Addr: " << ptr << " " << arr[0] << '\n';
```

# 180 Introduction to C++

```cpp
ptr = ptr+2;
*ptr = 20;
std::cout << "Addr: " << ptr << " " << arr[2] << '\n';
return 0;
}
```

Since ptr points to the address of arr[0], arr[0] becomes 10. Then, ptr is increased by 8, not by 2, because it is declared as a pointer to int. Thus, ptr points to arr[2], arr[2] becomes 20. Therefore, the program displays the values 10 and 20 and two addresses with the second being 8 places greater than the one.

Similar to the addition, subtracting a positive integer from a pointer in an assignment such as:

```cpp
ptr = ptr - n;
```

decreases the pointer value by n*size of int and makes the pointer points to the address of the n-th element before the one it points. For example, if we write the following code:

```cpp
ptr = &arr[2];
cout << "Addr: " << ptr << '\n';
ptr = ptr-2;
cout << "Addr: " << ptr << '\n';
```

the second address will be larger than the first. In case of addition, the result is considered valid the pointer to element within the array or to the next place past the end. For example:

```cpp
int arr[] = {10, 20, 30};
int *p1 = arr+3; /* Valid, the pointer points to the next place past the end of the array. */
int *p2 = arr-2; // Non valid.
int *p3 = arr-1; // Non valid.
```

Although the assignment with the address past the end of the array is valid, in case of p1, do not attempt to dereference this address because it is out of bounds. For example, do not write *p1 = 2; the behaviour of the pointer is unpredictable.

Note that if the pointer does not point to an array element, the use of ++ and -- operators produce a valid result. The pointer is increased or decreased by the size of the type it points to. For example:

```cpp
#include <iostream> // Example 8.9
int main() {

double *ptr = &i;
ptr++;
std::cout << "Addr: " << ptr << '\n';
ptr--;
std::cout << "Addr: " << ptr << '\n';
return 0;
}
```

The program displays two addresses with the first being 8 places greater than the one. As we'll see in next examples, the ++ and -- operators are often combined with the * indirection operator to process array elements. The value of the expression depends on the operator precedence.

# 8 Pointers 181

Because these combinations are often used, I put them all together for quick reference. For example, let's see the four combinations of * and ++; the same are for --:

- `i = (*ptr)++;` first value of *ptr is assigned to i and then ptr is increased by one.
- `i = (*ptr--);` first value of *ptr is assigned to i and then ptr is decreased by one type.
- `i = ++ptr;` first value of ptr is increased by one and then *ptr is assigned to i.
- `i = ptr++;` first value of *ptr is assigned to i and then ptr is increased by its type.

# Subtracting and Comparing Pointers

The result of pointer subtraction is valid only if both pointers point to elements of the same array or the place right after the end. The result is the number of elements between them. If the value of the subtracted pointer is greater, the result would be a negative sign. For example, if p1 points to the second element and p2 points to the fifth element of the same array, the result of p2-p1 is -3. The result of comparing two pointers with == and != operators is reliable. Using relational operators <, <= and >=, the result is valid if both point to members of the same object including the next past end, otherwise it is undefined. For example, the result of p2 > p1 is 1.

# EXERCISES

S.8.6 Use the p1, p2, and p3 pointers and complete the following program to read the grades of student. If all grades are greater than equal to 5, the program should display names in ascending order. Otherwise, the program should display their average. The variables i, j, and k should be used only once.

```cpp
#include <iostream>
int main()
{
    float *p1, *p2, *p3, i, j, k;
    ...
}
```

Answer:

```cpp
#include <iostream>
using std::cout;
using std::cin;

int main()
{
    float *p1, *p2, *p3, i, j, k;

    p1 = &i;
    p2 = &j;
    p3 = &k;

    cout << "Enter grades: ";
    cin >> *p1 >> *p2 >> *p3;

    if (*p1 >= 5) && (*p2 >= 5) && (*p3 >= 5)
    {
        if (*p1 <= *p2 && *p1 <= *p3)
        {
            cout << *p1;
            cout << ' ' << *p2 << ' ' << *p3;
            else
            cout << ' ' << *p3 << ' ' << *p2;
        }
        else if (*p2 <= *p1 && *p2 <= *p3)
        {
            cout << *p2;
            if (*p1 < *p3)
                cout << ' ' << *p1 << ' ' << *p3;
            else
                cout << ' ' << *p3 << ' ' << *p1;
        }
        else
        {
            cout << *p3;
            if (*p1 < *p2)
                cout << ' ' << *p2 << ' ' << *p1;
            else
                cout << ' ' << *p1 << ' ' << *p2;
        }
    }
    else
    cout << "Avg: " << (*p1 + *p2 + *p3)/3 << '\n';
    return 0;
}
```

C.8.7 Use the p1, p2, and p3 pointers and complete the following program to read two integers and display the sum of the integers between them. For example, if the user enters 6 and 10, the program should display 24 (7+8+9). The program should force the user to enter numbers less than 100 and the first integer than the second. The variables i, j, and sum should be used only once.

```cpp
#include <iostream>
int main()
{
    int *p1, *p2, *p3, i, j, sum;
    ...
}
```

Answer:

```cpp
#include <iostream>
int main()
{
    int *p1, *p2, *p3, i, j, sum;
    p1 = &i;
    p2 = &j;
    p3 = &sum;
    *p3 = 0;

    do {
      std::cout << "Enter two numbers (a < b < 100): ";
      std::cin >> *p1 >> *p2;
      while(*p1 >= *p2 || *p2 > 100) {
        (*p1)++;
        while(*p1 < *p2) {
          *p3 += *p1;
          (*p1)++;
        }
        std::cout << "Sum: " << *p3 << '\n';
        return 0;
      }
}
```

# 8 • Pointers 183

Break time. We reach one of the most important sections. Listen to Passenger from Iggy Pop (Stooges), and get on board. Pay extra attention.

# POINTERS AND ARRAYS

The elements of an array are stored in successive memory locations, with the first one stored at the lowest memory address. The type of the array defines the distance of elements in memory. For example, in a char array, the distance is one byte, while in an int array the distance equals the size of int (e.g., four bytes).

> Tip The close relationship between pointers and arrays is based on the fact that the name of an array can be used as a pointer to its first element.

In a similar way, arr+1 can be used as a pointer to the second element, arr+2 as a pointer to the third element, and so on. In general, the following expressions are equivalent:

```cpp
arr == &arr[0]
arr + 1 == &arr[1]
arr + 2 == &arr[2]
...
arr + n == &arr[n]
```

Again, the following program outputs four times the same value:

```cpp
#include <iostream> // Example 8.10
int main() {
  int *ptr, arr[5];

  ptr = arr;
  std::cout << ptr << ' ' << &arr[0] << ' ' << ' ' << arr << ' ' << ' ' << << ' ' << &arr << '\n';
  return 0;
}
```
