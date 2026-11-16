
Dereferencing a null pointer crashes the program. The error message varies depending on the operating system, but typically “access violation” or “segmentation fault” errors occur when dereferencing a null pointer.

## Arrays

An **array** is a collection of multiple elements of the same type. The following code declares an array of 10 integers called `a` and then sets the first element in the array (index 0) to 50:

```
int a[10];
a[0] = 50;
```

By default, the elements in an array are uninitialized. While you could manually initialize each element in an array, it’s more convenient to use either the initializer syntax or a loop. The initializer syntax uses braces, like this:

```
int fib[5] = { 0, 1, 1, 2, 3 };
```

Alternatively, you could use a loop. The following initializes each of the 50 elements in `array` to 0:

```
int array[50];
for (int i = 0; i < 50; i++)
{
    array[i] = 0;
}
```

> **warning**
> **ARRAYS DON'T BOUND CHECK:** Requesting invalid indices can lead to memory corruption and other errors. Several tools exist to help find bad memory accesses, such as the AddressSanitizer tool available in Xcode.

C++ stores arrays contiguously in memory. This means that the data for index 0 is right next to the data for index 1, which is right next to index 2, and so on. Table A.4 shows an example of a five-element array in memory. Keep in mind that the variable array (without the subscript) references the memory address of index 0 (in this case, 0xF2E0). Because of this, you can pass a single-dimensional array to a function via a pointer.

### Table A.4 An Array in Memory

| Code | Variable | Memory Address | Value |
|---|---|---|---|
| int array[5] = { 2, 4, 6, 8, 10 }; | array[0] | 0xF2E0 | 2 |
| | array[1] | 0xF2E4 | 4 |
| | array[2] | 0xF2E8 | 6 |
| | array[3] | 0xF2EC | 8 |
| | array[4] | 0xF2F0 | 10 |

## A POINTER BY ANY OTHER NAME...

The C programming language (the precursor to C++) does not support references. Thus, the concept of passing by reference does not exist in C. Instead of using references, you must use pointers. For example, in C, you would write the Swap function as follows:

```
void Swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

Calling this version of Swap then requires the address-of operator:

```
int x = 20;
int y = 37;
Swap(&x, &y);
```

At program execution time, there is no difference between how references and pointers work. However, keep in mind that a reference must refer to something, whereas a pointer can be nullptr.

In C++, many developers prefer passing by reference over passing by pointer. This is because passing by pointer implies that nullptr is a valid parameter. However, for stylistic reasons, this book typically passes dynamically allocated objects by pointer, even in cases where references would work.

You also can declare multidimensional arrays. For example, the following code creates a 2D array of floats with four rows and four columns:

```
float matrix[4][4];
```

To pass a multidimensional array into a function, you must explicitly specify the dimensions, like this:

```
void InvertMatrix(float m[4][4])
{
    // Code here...
}
```

## Dynamic Memory Allocation

As discussed earlier, memory allocation for local variables is automatic in C++. These variables end up in memory on the stack. This is great for temporary variables and function parameters. However, local variables are sometimes not enough.

First, the stack has a limited amount of memory available—typically much less than the amount of memory an average program might want to use. For example, the Microsoft Visual C++ compiler has a default stack size of 1 MB. Such a small amount of memory won’t be enough for all but the simplest games.

Second, local variables have a fixed lifetime. They are only available from the point of declaration until the end of the containing scope. This scope is typically within a function, as global variables are stylistically undesirable.

In dynamic memory allocation, the programmer controls allocation and deallocation of variables in memory. Dynamic allocations go into the heap, which is a separate part of memory. The heap is much larger in size compared to the stack (several gigabytes on current machines), and data on the heap persists until either the programmer deletes the data or the program ends.

Recall that in C++, the `new` and `delete` operators allocate and deallocate memory on the heap. The `new` operator allocates memory for the requested type of variable, and for classes and structs, it calls the constructor. The `delete` operator performs the opposite: It calls the destructor for class/struct types and deallocates the memory for the variable.

For example, this code dynamically allocates memory for a single `int` variable:

```
int* dynamicInt = new int;
```

To free the memory of a dynamically allocated variable, use `delete`:

```
delete dynamicInt;
```

Forgetting to delete a dynamically allocated variable causes a **memory leak**, meaning that the memory is unusable for the remaining life span of the program. For programs that run for a long time, small memory leaks accumulate over time and eventually cause the heap to run out of memory. If the heap runs out of memory, the program will almost always crash soon afterward.

Of course, dynamically allocating just a single integer doesn't take advantage of all the available memory on the heap. You can also dynamically allocate arrays:

Click here to view code image

```
char* dynArray = new char[4*1024*1024];
dynArray[0] = 32; // Set the first element to 32
```

Note that when dynamically allocating an array, you place square brackets immediately after the type and specify the size there. Unlike with a statically allocated array, with a dynamically allocated array, you can specify a size at runtime.

To delete a dynamically allocated array, use `delete[]`:

```
delete[] dynArray;
```

## ASSORTED CLASS TOPICS

Recall that C++ supports object-oriented programming through classes. This section assumes familiarity with the basics of classes in C++: classes versus objects, how to declare a class with member variables and functions, the constructor, and inheritance and polymorphism. It instead focuses on certain topics that cause some issues when using classes in C++.

### References, const, and Classes

Passing objects by value to functions is inefficient. This is because copying the object can be expensive, especially if the object has a lot of data. Thus, a best practice is to pass objects by reference.

However, one issue with references is that they allow the function to modify the parameter. For example, suppose an `Intersects` function takes in two `Circle` objects and returns whether these circles intersect. If the function takes in these circles by reference, it could choose to modify the centers or radii of the circles.

The solution is to instead use a constant (`const`) reference. A **const reference** guarantees that the function can only read from the reference but not write to it. So, a more correct declaration of `Intersects` uses `const` references:

Click here to view code image

![](img/e9afcec1487716b0ef80d7e7c09869c8_981_0.png)

You can also mark member functions as **const member functions** to guarantee that a member function does not modify member data. For example, a `GetRadius` function for `Circle` shouldn't modify member data, which means it should be a `const` member function. To denote that a member function is `const`, add the `const` keyword immediately after the closing parenthesis of the function declaration, as in

### Listing A.1 Circle Class with const Member Function

Click here to view code image

```
class Circle
{
public:
    float GetRadius() const { return mRadius; }

    // Other functions omitted

    // ...

private:
    Point mCenter;
    float mRadius;
};
```

To summarize, the best practices when it comes to references, const, and classes are as follows:

- Pass non-basic types by reference, const reference, or pointers, to avoid making copies.
- Pass by const reference when a function does not need to modify a reference parameter.
- Mark member functions that don't modify data as const.
