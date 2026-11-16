
### Figure 11.6 A simple array with three elements

```
int list[3];
list[0] = 5;
list[1] = -3;
list[2] = 12;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_323_0.png)

```
int list[3]; // Declare list to be an array of three ints
list[0] = 5 ; // Make the first element 5
list[1] = -3 ; // Make the second element -3
list[2] = 12 ; // Make the last element 12
```

This code fragment shows that the square brackets used after the point of declaration allow us to access an individual element based on that element's position within the block of memory assigned to the array. This syntax is identical to that used with vector objects. As with vectors, the very first element in an array appears at index 0.

After executing these assignment statements, the list array conceptually looks like Figure 11.6.

The array square brackets operator has two distinct meanings depending on the context:

- 1. At the array's declaration, for example,
  `double nums[10];`
  the number within the square brackets specifies the number of elements that the array can hold. The compiler uses this number along with the type of the array to determine how much memory to allocate for the array.

- 2. After the array's declaration, for example,
  `nums[3] = 10.45;`
  the number within the square brackets represents an index locating a specific element within the memory allocated to the array.

![](img/e84ad11adb18201d71595b31ce6c9eff_323_1.png)

Unlike with vectors, the compiler will insist that the programmer use an integral value for an index; for example, the following statement:

```
numbers[1.3] = 5;
```

is illegal if numbers is an array. Identically to vectors, the programmer must ensure that the array index is within the bounds of the array. Accessing an element via an index outside the bounds of an array results in undefined behavior.

We can pass an array to a function, as shown in Listing 11.11 (arraytofunc.cpp), the array-based version of Listing 11.7 (vectortofunc.cpp).

```
Listing 11.11: arraytofunc.cpp
#include <iostream>
/*
 * print(a, n)
 *
 * Prints the contents of an int array
 * a is the array to print
 * n is the size of the array
 */
void print(int a[], int n) {
    for (int i = 0; i < n; i++) {
        std::cout << a[i] << " ";
    }
    std::cout << '\n';
}
/*
 * sum(a, n)
 *
 * Adds up the contents of an int array
 * a is the array to sum
 * n is the size of the array
 */
int sum(int a[], int n) {
    int result = 0;
    for (int i = 0; i < n; i++)
        result += a[i];
    return result;
}
int main() {
    int list[] = { 2, 4, 6, 8 };
    // Print the contents of the array
    print(list, 4);
    // Compute and display sum
    std::cout << sum(list, 4) << '\n';
    // Zero out all the elements of list
    for (int i = 0; i < 4; i++)
        list[i] = 0;
    // Reprint the contents of the array
    print(list, 4);
    // Compute and display sum
    std::cout << sum(list, 4) << '\n';
}
```

As shown in the print function's definition:

void print(int a[], int n)

empty square brackets follow the name of an array formal parameter. The programmer can supply a number within the square brackets, but the compiler will ignore it. When calling a function that accepts an array parameter, as in

```
print(list, 4);
```

the programmer must pass the array's size along with the array name. This is because an array simply references a block of memory and has no notion of its size.

An undecorated array name by itself in C++ source code behaves like a constant pointer to the beginning element of the array. Consequently, when an array is passed as an actual parameter during a function call, as in Listing 11.11 (arrayfunc.cpp):

```
print(list, 4);
```

the function is passed the address of the array—the array's address is bound to the formal parameter. So, while the function cannot affect the address of the array itself, the function has total access to the array's contents. In Listing 11.12 (cleararray.cpp), the function clear modifies the contents of any array sent to it, making all the elements zero.

### Listing 11.12: cleararray.cpp

```
#include <iostream>

/*
 * print(a, n)
 *
 * Prints the contents of an int array
 * a is the array to print
 * n is the size of the array
 */
void print(int a[], int n) {
    for (int i = 0; i < n; i++) {
        std::cout << a[i] << " ";
    }
    std::cout << '\n';
}

/*
 * clear(a, n)
 *
 * Makes all the elements of array a zero
 * a is the array to zero out
 * n is the size of the array
 */
void clear(int a[], int n) {
    for (int i = 0; i < n; i++)
        a[i] = 0;
}

int main() {
    int list[] = { 2, 4, 6, 8 };
    // Print the contents of the array
    print(list, 4);
    // Zero out the array
    clear(list, 4);
    // Reprint the contents of the array
    print(list, 4);
}
```

The output of Listing 11.12 (cleararray.cpp) is

```
2 4 6 8
0 0 0 0
```

The clear function actually modifies the contents of main's list array. The function works on the array's actual elements, not copies of its elements.

Arrays, therefore, by default are passed by reference with respect to the elements they contain. By default, an array's contents are open to corruption by errant functions. In order to protect an array so that a function may read its contents but not modify its contents, the parameter must be declared const, as in

```
int sum(const int a[], int n)
```

In Listing 11.11 (arrayofunc.cpp) there is no reason why the print and sum functions should be able to modify the contents of their array parameters, so the const specifier should be added to their definitions.

As a general rule, all functions that accept array parameters should declare the array contents as const unless they need to modify the elements of the array.

> As a general rule, all functions that accept array parameters should declare the array contents as const unless they need to modify the elements of the array. For example, use
> `int sum(const int a[], int n)`
> rather than
> `int sum(int a[], int n)`
> if the sum function must be able to examine the contents of the array but is not intended to modify its contents.

C++ does not directly support empty arrays. A physical array must contain at least one element. Sometimes it is appropriate to consider an array that is conceptually empty: for example, what if we wish to pass an "empty" array to the sum function? We can pass 0 as the second parameter since empty array contains no elements, but what should we pass as the first parameter? Any array will do, but there is no need create a real array when none truly is needed. Instead, we may use nullptr:

```
quantity = sum(nullptr, 0);
```

If you scrutinize the body of the sum function, you will see that this call will assign to quantity the correct answer, namely zero.

## 11.2.2 Pointers and Arrays

An array name used in C++ source code references a location in memory, the address of the first element (element at index 0) in the array. In this way an array name is similar to a constant pointer (see Section 10.7 for more information about C++ pointers). Because of this, we can treat in some ways an array identifier like a pointer. Similarly, we can direct a pointer to point to an array, and then treat the pointer itself as if it were an array.

Listing 11.13 (pointerprint.cpp) uses a pointer to traverse an array.

```
Listing 11.13: pointerprint.cpp
#include <iostream>

int main() {
    int a[] = { 2, 4, 6, 8, 10, 12, 14, 16, 18, 20 },
        *p;

    p = &a[0]; // p points to first element of array a

    // Print out the contents of the array
    for (int i = 0; i < 10; i++) {
        std::cout << *p << ' '; // Print the element p points to
        p++; // Increment p so it points to the next element
    }
    std::cout << '\n';
}
```

The statement
p = &a[0];
sets p to point to the first element of array a. A shorter way to accomplish the same thing is
p = a;

since a is itself a reference to the array's location in memory. This assignment statement clearly demonstrates the association between array variables and pointer variables. Note that the opposite assignment (a = p) is impossible, because array a declared as above may not appear by itself on the left side of the assignment operator.

Pointer variables can participate in addition and subtraction expressions. The statement
p++;
changes the address stored in p so subsequently the pointer will point to the next integer position in memory. If p is assigned to array a, incrementing p redirects it to point to a's next element. 1 In Figure 11.7, pointer p is assigned to array a and then incremented to refer to various elements within a.

The expression
p[0]
is another way to write
*p

so the array indexing operator ([]) can be used with pointers. The expression
p[5]

1 Each byte in memory has a unique numeric address. Since most C++ types require more than one byte of storage, incrementing a pointer by 1 does not simply add 1 to the address it holds. The amount added depends on the type of the pointer, for example, on systems using 32-bit (4 byte) integers, adding 1 to an integer pointer variable increments its address by 4, not 1. The compiler knows the type of the pointer variable because programmers must declare all variables. The compiler, therefore, can automatically adjust the arithmetic to work properly. If a pointer points to memory within an array and is of the same type as the array, incrementing the pointer correctly repositions the pointer to point to the next element in the array.
