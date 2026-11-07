
```cpp
{
    antarctica_years_end s01, s02, s03;
    s01.year = 1998;
    antarctica_years_end * pa = &s02;
    pa->year = 1999;
    antarctica_years_end trio[3]; // array of 3 structures
    trio[0].year = 2003;
    std::cout << trio->year << std::endl;
    const antarctica_years_end * arp[3] = {&s01, &s02, &s03};
    std::cout << arp[1]->year << std::endl;
    const antarctica_years_end ** ppa = arp;
    auto ppb = arp; // C++11 automatic type deduction
// or else use const antarctica_years_end ** ppb = arp;
    std::cout << (*ppa)->year << std::endl;
    std::cout << (*(ppb+1))->year << std::endl;
    return 0;
}
```

Here's the output:

```
2003
1999
1998
1999
```

The program compiles and works as promised.

## Array Alternatives

Earlier this chapter mentioned the vector and array template classes as alternatives to the built-in array. Let's take a brief look now at how they are used and at some of the benefits of using them.

### The vector Template Class

The vector template class is similar to the string class in that it is a dynamic array. You can set the size of a vector object during runtime, and you can append new data to the end or insert new data in the middle. Basically, it's an alternative to using new to create a dynamic array. Actually, the vector class does use new and delete to manage memory, but it does so automatically.

At this time we won't venture very deeply into what it means to be a template class. Instead, we'll look at a few basic practical matters. First, to use a vector object, you need to include the vector header file. Second, the vector identifier is part of the std namespace, so you can use a using directive, a using declaration, or std::vector. Third, templates use a different syntax to indicate the type of data stored. Fourth, the vector class uses a different syntax to indicate the number of elements. Here are some examples:

```cpp
#include <vector>
...
using namespace std;
vector<int> vi;       // create a zero-size array of int
int n;
cin >> n;
vector<double> vd(n); // create an array of n doubles
```

We say that `vi` is an object of type `vector<int>` and that `vd` is an object of type `vector<double>`. Because vector objects resize automatically when you insert or add values to them, it’s okay for `vi` to start with 0 size. But for the resizing to work, you would use the various methods that are part of the vector package.

In general, the following declaration creates a vector object `vt` that can hold `n_elem` elements of type `typeName`:

```cpp
vector<typeName> vt(n_elem);
```

The parameter `n_elem` can be an integer constant or an integer variable.

### The array Template Class (C++11)

The vector class has more capabilities than the built-in array type, but this comes at a cost of slightly less efficiency. If all you need is a fixed-size array, it could be advantageous to use the built-in type. However, that has its own costs of lessened convenience and safety. C++11 responded to this situation by adding the array template class, which is part of the std namespace. Like the built-in type, an array object has a fixed size and uses the stack (or else static memory allocation) instead of the free store, so it shares the efficiency of built-in arrays. To this it adds convenience and additional safety. To create an array object, you need to include the array header file. The syntax is a bit different from that for a vector:

```cpp
#include <array>
...
using namespace std;
array<int, 5> ai;   // create array object of 5 ints
array<double, 4> ad = {1.2, 2.1, 3.43, 4.3};
```

More generally, the following declaration creates an array object `arr` with `n_elem` elements of type `typeName`:

```cpp
array<typeName, n_elem> arr;
```

Unlike the case for vector, `n_elem` can’t be a variable.

With C++11, you can use list-initialization with vector and array objects. However, that was not an option with C++98 vector objects.

## Comparing Arrays, Vector Objects, and Array Objects

Perhaps the simplest way to understand the similarities and differences between arrays, vector objects, and array objects is to look at a brief example (Listing 4.24) that uses all three approaches.

### Listing 4.24 choices.cpp

```cpp
// choices.cpp -- array variations
#include <iostream>
#include <vector>    // STL C++98
#include <array>     // C++11
int main()
{
    using namespace std;
// C, original C++
    double a1[4] = {1.2, 2.4, 3.6, 4.8};
// C++98 STL
    vector<double> a2(4);   // create vector with 4 elements
// no simple way to initialize in C++98
    a2[0] = 1.0/3.0;
    a2[1] = 1.0/5.0;
    a2[2] = 1.0/7.0;
    a2[3] = 1.0/9.0;
// C++11 -- create and initialize array object
    array<double, 4> a3 = {3.14, 2.72, 1.62, 1.41};
    array<double, 4> a4;
    a4 = a3;                  // valid for array objects of same size
// use array notation
    cout << "a1[2]: " << a1[2] << " at " << &a1[2] << endl;
    cout << "a2[2]: " << a2[2] << " at " << &a2[2] << endl;
    cout << "a3[2]: " << a3[2] << " at " << &a3[2] << endl;
    cout << "a4[2]: " << a4[2] << " at " << &a4[2] << endl;
// misdeed
    a1[-2] = 20.2;
    cout << "a1[-2]: " << a1[-2] << " at " << &a1[-2] << endl;
    cout << "a3[2]: " << a3[2] << " at " << &a3[2] << endl;
    cout << "a4[2]: " << a4[2] << " at " << &a4[2] << endl;
    return 0;
}
```

Here's some sample output:

```
a1[2]: 3.6 at 0x28cc8
a2[2]: 0.142857 at 0xca0328
a3[2]: 1.62 at 0x28ccc8
a4[2]: 1.62 at 0x28cca8
a1[-2]: 20.2 at 0x28ccc8
a3[2]: 20.2 at 0x28ccc8
a4[2]: 1.62 at 0x28cca8
```

## Program Notes

First, notice that whether we use a built-in array, a vector object, or an array object, we can use the standard array notation to access individual members. Second, you can see from the addresses that array objects use the same region of memory (the stack, in this case) as the built-in array, whereas the vector object is stored in a different region (the free store, or heap). Third, note that you can assign an array object to another array object. For built-in arrays, you have to copy the data element-by-element.

Next, and this deserves special attention, note this line:

```
    a1[-2] = 20.2;
```

What does an index of -2 mean? Recall that this translates to the following:

```
    *(a1-2) = 20.2;
```

Expressing this in words, see where a1 points, move backward two double elements, and put 20.2 there. That is, store the information at a location outside of the array. C++, like C, does not check for such out-of-range errors. In this particular case, that location turned out to be in the array object a3. Another compiler placed the wayward 20.2 in a4, and other compilers might make yet other bad choices. This is an example of the unsafe behavior of built-in arrays.

Do the vector and array objects protect against this behavior? They can if you let them. That is, you still can write unsafe code, such as the following:

```
    a2[-2] = .5;    // still allowed
    a3[200] = 1.4;
```

However, you have alternatives. One is using the `at()` member function. Just as you can use the `getline()` member function with the `cin` object, you can use the `at()` member function with objects of the vector or array type:

```
    a2.at(1) = 2.3;  // assign 2.3 to a2[1]
```

The difference between using bracket notation and the `at()` member function is that if you use `at()`, an invalid index is caught during runtime and the program, by default, aborts. This added checking does come at the cost of increased run time, which is why C++ gives you the option of using either notation. More than that, these classes offer ways of using objects that reduce the chances of accidental range errors. For example, the classes have `begin()` and `end()` member functions that let you delimit the range without accidentally exceeding the bounds. But we'll save that discussion until Chapter 16.

## Summary

Arrays, structures, and pointers are three C++ compound types. An array can hold several values, all of the same type, in a single data object. By using an index, or subscript, you can access the individual elements in an array.

A structure can hold several values of different types in a single data object, and you can use the membership operator (.) to access individual members. The first step in using structures is to create a structure template that defines what members the structure holds. The name, or tag, for this template then becomes a new type identifier. You can then declare structure variables of that type.

A union can hold a single value, but it can be of a variety of types, with the member name indicating which mode is being used.

Pointers are variables that are designed to hold addresses. We say a pointer points to the address it holds. The pointer declaration always states to what type of object a pointer points. Applying the dereferencing operator (*) to a pointer yields the value at the location to which the pointer points.

A string is a series of characters terminated by a null character. A string can be represented by a quoted string constant, in which case the null character is implicitly understood. You can store a string in an array of char, and you can represent a string with a pointer-to-char that is initialized to point to the string. The strlen() function returns the length of a string, not counting the null character. The strcpy() function copies a string from one location to another. When using these functions, you include the cstring or the string.h header file.

The C++ string class, supported by the string header file, offers an alternative, more user-friendly means to deal with strings. In particular, string objects are automatically resized to accommodate stored strings, and you can use the assignment operator to copy a string.

The new operator lets you request memory for a data object while a program is running. The operator returns the address of the memory it obtains, and you can assign that address to a pointer. The only means to access that memory is to use the pointer. If the data object is a simple variable, you can use the dereferencing operator (*) to indicate a value. If the data object is an array, you can use the pointer as if it were an array name to access the elements. If the data object is a structure, you can use the pointer dereferencing operator (->) to access structure members.

Pointers and arrays are closely connected. If ar is an array name, then the expression ar[i] is interpreted as *(ar + i), with the array name interpreted as the address of the first element of the array. Thus, the array name plays the same role as a pointer. In turn, you can use a pointer name with array notation to access elements in an array allocated by new.

The new and delete operators let you explicitly control when data objects are allocated and when they are returned to the memory pool. Automatic variables, which are those declared within a function, and static variables, which are defined outside a function or with the keyword static, are less flexible. An automatic variable comes into being
