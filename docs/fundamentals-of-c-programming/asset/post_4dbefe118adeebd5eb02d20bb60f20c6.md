
Figure 11.7 Incrementing a pointer to an array

```cpp
int a[] = { 2, 4, 6, 8 }, *p;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_328_0.png)

```cpp
p = a;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_328_1.png)

```cpp
p++;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_328_2.png)

```cpp
*p = 7;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_328_3.png)

## 11.2. ARRAYS

represents the element at index 5 within the array pointed to by p.

Listing 11.14 (pointerprint2.cpp) uses pointers in a different way to traverse an array.

```cpp
Listing 11.14: pointerprint2.cpp

#include <iostream>

int main() {
    int a[] = { 2, 4, 6, 8, 10, 12, 14, 16, 18, 20 },
        *begin, *end, *cursor;

    begin = a;             // begin points to the first element of array a
    end = a + 10;          // end points to just after the last element

    // Print out the contents of the array
    cursor = begin;
    while (cursor != end) {
        std::cout << *cursor << ' ';  // Print the element
        cursor++;                     // Increment cursor so it points to the next element
    }
    std::cout << '\n';
}
```

In Listing 11.14 (pointerprint2.cpp), the code

```cpp
cursor = begin;
while (cursor != end) {
    std::cout << *cursor << ' ';  // Print the element
    cursor++;                     // Increment cursor so it points to the next element
}
```

can be expressed more succinctly as a for loop:

```cpp
for (cursor = begin; cursor != end; cursor++)
    std::cout << *cursor << ' ';  // Print the element
```

If pointer p points to an array, the element at index i can be accessed as either p[i] or *(p + i). The expression *(p + i) dereferences the address that is i positions away from the address referenced by p.

Sometimes pointer notation is used to represent an array parameter to a function. The array print function that begins

```cpp
void print(const int a[], int n)
```

could instead be written

```cpp
void print(const int *a, int n)
```

where a is a pointer to an array. The compiler treats the two forms identically in the machine language it produces.

Listing 11.15 (recursivearrayprint.cpp) uses two array printing functions, iterative_print and recursive_print. Both use the pointer notation when declaring their array parameters.

Listing 11.15: recursivearrayprint.cpp

```cpp
#include <iostream>
/*
 * iterative_print(a,n)
 *
 * Prints the contents of array a
 * a is the array to print; a is not modified
 * n is number of elements in a
 */
void iterative_print(const int *a, int n) {
    for (int i = 0; i < n; i++)
        std::cout << a[i] << ' ';
}
/*
 * recursive_print(a,n)
 *
 * Prints the contents of array a
 * a is the array to print; a is not modified
 * n is number of elements in a
 */
void recursive_print(const int *a, int n) {
    if (n > 0) {
        std::cout << *a << ' ';     // Print the first element of the array
        recursive_print(a + 1, n - 1); // Print rest of the array
    }
}
int main() {
    int list[] = { 23, -3, 4, 215, 0, -3, 2, 23, 100, 88, -10 };
    iterative_print(list, 11);
    recursive_print(list, 11);
}
```

The function iterative_print uses a loop, while recursive_print uses recursion instead. Inside the recursive_print function, the expression a + 1 points to the second element in array a. a + 1 essentially represents the rest of the array—everything except for the first element. The statement recursive_print(a + 1, n - 1);

calls the function recursively, passing the remainder of the array (a + 1) with a length that is one less (n - 1) than before. The recursion terminates when the array's length is zero.

Instead of passing a pointer to an array and the array's size, we can pass two pointers. The first pointer points to the beginning of the array and another pointer points just past the end of the array. The following print function illustrates:

```cpp
void print(int *begin, int *end) {
    for (int *elem = begin; elem != end; elem++)
        std::cout << *elem << ' ';
    std::cout << '\n';
}
```

Notice that this code does not appear to be using arrays at all! This code takes advantage of pointer arithmetic to move the elem pointer from the first element to each successive element in the array. Since the memory devoted to an array is a continuous, contiguous block of memory addresses, pointer arithmetic simply redirects a pointer from one element in an array to another element in that array. Listing 11.16 (pointerarithmetic.cpp) provides some more examples of pointer arithmetic in action.

```cpp
Listing 11.16: pointerarithmetic.cpp

#include <iostream>

int main() {
    // Make an array
    int arr[] = {10, 20, 30, 40, 50};
    int *p = arr;    // p points to the first element
    std::cout << *p << '\n';   // Prints 10, does not change p
    std::cout << *p++ << '\n'; // Prints 10, does not change p
    std::cout << p[1] << '\n'; // Prints 20, does not change p
    std::cout << *p << '\n';   // Prints 20, does not change p
    p++;             // Advances p to the next element
    std::cout << *p << '\n';   // Prints 30, does not change p
    p += 2;          // Advance p two places
    std::cout << *p << '\n';   // Prints 40, does not change p
    std::cout << p[0] << '\n'; // Prints 40, does not change p
    std::cout << p[1] << '\n'; // Prints 50, does not change p
    p--;             // Moves p back one place
    std::cout << *p << '\n';   // Prints 30, does not change p
}
```

Listing 11.16 (pointerarithmetic.cpp) prints

![](img/e84ad11adb18201d71595b31ce6c9eff_331_0.png)

Figure 11.8 illustrates how Listing 11.16 (pointerarithmetic.cpp) works.

Listing 11.16 (pointerarithmetic.cpp) also shows how we can use the square bracket array access operator with a pointer. The expression p[i] refers to the element in memory i positions from the location pointed to by p.

Going back to the print function that uses pointers:

```cpp
void print(int *begin, int *end) {
    for (int *elem = begin; elem != end; elem++)
        std::cout << *elem << ' ';
    std::cout << '\n';
}
```

the pointer elem first points to the same element to which begin points (that is, the first element in the array), and within the loop it moves to the next element repeatedly until it passes the last element. A caller could invoke the function as

Figure 11.8 Pointer arithmetic. Incrementing pointer p moves it to the next element in the array.

```cpp
int arr[] = {10, 20, 30, 40, 50};
int *p = arr;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_332_0.png)

```cpp
p++;
```

![](img/e84ad11adb18201d71595b31ce6c9eff_332_1.png)

```cpp
int list[25];                 // Allocate a static array
for (int i = 0; i < 25; i++) {
    list[i] = rand() % 1000;  // Fill with pseudorandom values
    print(list, list + 25);   // Print the elements of list
}
```

The advantage of the begin/end pointer approach is that it allows a programmer to pass a *slice* of the array to the function; for example, if we wish to print the elements of the array from index 3 to index 7, we would call the function as

```cpp
print(list + 3, list + 8);   // Print elements at indices 3, 4, 5, 6, 7
```

### 11.2.3 Dynamic Arrays

Programmers need not worry about managing the memory used by static arrays. The compiler and run-time environment automatically ensure the array has enough space to hold all of its elements. The space held by local arrays is freed up automatically when the local array goes out of the scope of its declaration. Global arrays live for the lifetime of the executing program. Memory management for static arrays, therefore, works just like scalar variables.

Static arrays have a significant limitation: The size of a static array is determined at compile time. The programmer may change the size of the array in the source code and recompile the program, but once the program is compiled into an executable program any static array's size is fixed. For many applications the circumstances of the executing program must determine the size of an array. Static arrays lack such flexibility.

One approach to implementing a flexibly-sized array defines the array to hold as many items as it conceivably will ever need. Listing 11.17 (largearrayaverage.cpp) uses this approach.

```cpp
Listing 11.17: largearrayaverage.cpp
#include <iostream>
// Maximum number of expected values is 1,000,000
const int MAX_NUMBER_OF_ENTRIES = 10000000;
double numbers[MAX_NUMBER_OF_ENTRIES];
int main() {
    double sum = 0.0;
    int size;   // Actual number of entries
    // Get effective size of the array
    std::cout << "Please enter number of values to process: ";
    std::cin >> size;
    if (size > 0) {   // Nothing to do with no entries
        std::cout << "Please enter " << size << " numbers: ";
        // Allow the user to enter in the values.
        for (int i = 0; i < size; i++) {
            std::cin >> numbers[i];
            sum += numbers[i];
        }
        std::cout << "The average of ";
        for (int i = 0; i < size - 1; i++)
```
