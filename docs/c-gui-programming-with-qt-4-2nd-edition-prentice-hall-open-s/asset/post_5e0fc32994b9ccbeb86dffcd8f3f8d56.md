
of object. Here's the definition of a function that receives its parameters by call-by-value:

```cpp
#include <cstdlib>

double manhattanDistance(Point2D a, Point2D b)
{
    return std::abs(b.x() - a.x()) + std::abs(b.y() - a.y());
}
```

We would then invoke the function as follows:

```cpp
Point2D broadway(12.5, 40.0);
Point2D harlem(77.5, 50.0);
double distance = manhattanDistance(broadway, harlem);
```

C programmers avoid needless copy operations by declaring their parameters as pointers instead of as values:

```cpp
double manhattanDistance(const Point2D *ap, const Point2D *bp)
{
    return std::abs(bp->x() - ap->x()) + std::abs(bp->y() - ap->y());
}
```

They must then pass addresses instead of values when calling the function:

```cpp
double distance = manhattanDistance(&broadway, &harlem);
```

C++ introduced references to make the syntax less cumbersome and to prevent the caller from passing a null pointer. If we use references instead of pointers, the function looks like this:

```cpp
double manhattanDistance(const Point2D &a, const Point2D &b)
{
    return std::abs(b.x() - a.x()) + std::abs(b.y() - a.y());
}
```

The declaration of a reference is similar to that of a pointer, with & instead of *. When we actually use the reference, we can forget that it is a memory address and treat it like an ordinary variable. In addition, calling a function that takes references as arguments doesn't require any special care (no & operator).

All in all, by replacing Point2D const with const Point2D & in the parameter list, we reduced the overhead of the function call: Instead of copying 256 bits (the size of four doubles), we copy 64 or 128 bits, depending on the platform's pointer size.

The previous example used const, preventing the function from modifying the objects associated with the references. When this kind of side effect is desired, we can pass a non-const reference or pointer. For example:

```cpp
void transpose(Point2D &point)
{
  double oldX = point.x();
  point.setX(point.y());
  point.setY(oldX);
}
```

In some cases, we have a reference and need to call a function that takes a pointer, or vice versa. To convert a reference to a pointer, we can simply use the unary & operator:

```cpp
Point2D point;
Point2D &ref = point;
Point2D *ptr = &ref;
```

To convert a pointer to a reference, there is the unary * operator:

```cpp
Point2D point;
Point2D ptr = &ref;
Point2D &ref = ptr;
```

References and pointers are represented the same way in memory, and they can often be used interchangeably, which begs the question of when to use which. On the one hand, references have a more convenient syntax; on the other hand, pointers can be reassigned at any time to point to another object, they can hold a null value, and their more explicit syntax is often a blessing. For these reasons, pointers tend to prevail, with references used exclusively for declaring function parameters in conjunction with const.

# Arrays

Arrays in C++ are declared by specifying the number of items in the variable name. Two-dimensional arrays are possible using an array of arrays. Here's the definition of a one-dimensional array containing ten items:

```cpp
int fibonacci[10];
```

The items are accessible as fibonacci[0], fibonacci[1], ..., fibonacci[9]. Often we want to initialize the array we define:

```cpp
int fibonacci[10] = { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 };
```

In such cases, we can omit the array size since the compiler can deduce it from the number of initializers:

```cpp
int fibonacci[] = { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 };
```

Static initialization also works for complex types, such as Point2D:

```cpp
Point2D triangle[] = {
  Point2D(0.0, 0.0), Point2D(1.0, 0.0), Point2D(0.5, 0.8)
};
```

If we have no intention of altering the array later on, we can make it const:

```cpp
const int fibonacci[] = { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 };
```

To find out how many items an array contains, we can use the size operator as follows:

```cpp
int n = sizeof(fibonacci) / sizeof(fibonacci[0]);
```

The size operator returns the size of its argument in bytes. The number of items in an array is its size in bytes divided by the size of one of its items. Because this is cumbersome, a common alternative is to declare a constant and use it for defining the array:

```cpp
enum { Fibonacci = 10 };
const int fibonacci[Fibonacci] = { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 };
```

It would have been tempting to declare the constant as a const int variable. Unfortunately, some compilers have issues with const variables as array specifiers. We will explain the enum keyword later in this appendix.

Iterating through an array is normally done using an integer. For example:

```cpp
for (int i = 0; i < Fibonacci; ++i)
    std::cout << fibonacci[i] << std::endl;
```

It is also possible to traverse the array using a pointer:

```cpp
const int ptr = &fibonacci[0];
while (ptr != &fibonacci[10]) {
  std::cout << ptr << std::endl;
  ++ptr;
}
```

We initialize the pointer with the address of the first item and loop until we reach the "one past the last" item (the "eleventh" item, fibonacci[10]). At each iteration, the ++ operator advances the pointer to the next item.

Instead of &fibonacci[0], we could have written fibonacci. This is because the name of an array used is automatically converted into a pointer to the first item in the array. Similarly, we could substitute fibonacci + 10 for &fibonacci[10]. This works the other way as well: we can retrieve the contents of the current item using either *ptr or ptr[0] and access the next item using *(ptr + 1) or ptr[1]. This principle is sometimes called "equivalence of pointers and arrays".

To prevent what it considers to be a gratuitous inefficiency, C++ does not let us pass arrays by function value. Instead, they must be passed by address. For example:

```cpp
#include <iostream>
void printIntegerTable(const int *table, int size)
{
  for (int i = 0; i < size; ++i)
      std::cout << table[i] << std::endl;
}
```

```cpp
int main()
{
    const int fibonacci[10] = { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 };
    printIntegerTable(fibonacci, 10);
    return 0;
}
```

Ironically, C++ doesn't give us any choice about whether we want to pass the array by address or by value. To prevent what it considers to be a gratuitous inefficiency, C++ does not let us pass arrays by function value. Instead, they must be passed by address. For example:

```cpp
#include <iostream>
void printIntegerTable(const int *table, int size)
{
  for (int i = 0; i < size; ++i)
      std::cout << table[i] << std::endl;
}
```

```cpp
int main()
{
    const int fibonacci[10] = { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 };
    printIntegerTable(fibonacci, 10);
    return 0;
}
```

To create an array of variable size, we have several options. Some compilers allow variables in that context, but this feature should not be relied upon in portable programs. We can dynamically allocate the array:

```cpp
int *fibonacci = new int[n];
```

When we have finished using the array, we should release the memory it consumes using the delete [] operator:

```cpp
delete [] fibonacci;
```

We can use the standard vector<T> class:

```cpp
#include <vector>
```

```cpp
std::vector<int> fibonacci(n);
```

Items are accessible using the [] operator, just like with a C++ array. With vector<T> T is the type of the items stored in the vector, we can resize the array at any time using resize() and we can copy it using the assignment operator. Classes that contain angle brackets (<>) in their name are called template classes.

We can use Qt's QVector<T> class:

```cpp
#include <QVector>
```

```cpp
QVector<int> fibonacci(n);
```

QVector<T>'s API is very similar to that of vector<T>, but it also supports implicit data sharing ("copy on write") iteration using Qt's foreach keyword and uses speed optimization. Chapter 11 presents Qt's container classes and explains how they relate to the Standard C++ containers.

# Character Strings

The most basic way to represent character strings in C++ is to use an array of chars terminated by a null byte ('\0'). The following four functions demonstrate how these kinds of strings work:

```cpp
void hello1() {
    const char str[] = {
        'H', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd', '\0'
    };
    std::cout << str << std::endl;
}
