
## FIGURE 6.1 Demonstration Program for Template Functions

### A Program

```cpp
// File: maximal.cxx
// A demonstration program for a template function called maximal.

#include <cstdlib>   // Provides EXIT_SUCCESS
#include <iostream>  // Provides cout
#include <string>    // Provides string class
using namespace std;

// TEMPLATE FUNCTION used in this demonstration program:
// Note that some compilers require the entire function definition to appear before its use
// (rather than a mere prototype). This maximal function is similar to max from <algorithm>.
template <class Item>
Item maximal(Item a, Item b)
// Postcondition: Returns the larger of a and b.
// Note: Item may be any of the C++ built-in types (int, char, etc.), or a class with
// the > operator and a copy constructor.
{
    if (a > b)
        return a;
    else
        return b;
}

int main( )
{
    string s1("frijoles");
    string s2("beans");
    cout << "Larger of frijoles and beans: " << maximal(s1, s2) << endl;
    cout << "Larger of 10 and 20 : " << maximal(10, 20) << endl;
    cout << "It's a large world." << endl;
    return EXIT_SUCCESS;
}
```

The main program has two different uses of the maximal template function.

### A Sample Dialogue

Larger of frijoles and beans: frijoles
Larger of 10 and 20: 20
It's a large world.

## A Template Function to Swap Two Values

Here is a definition of another template function. The function swaps the values of two variables, as shown here:

```cpp
template <class Item>
void swap(Item& x, Item& y);
// Postcondition: The values of x and y have been interchanged, so that y
// now has the original value of x and vice versa. NOTE: Item may be any
// of the C++ built-in types (int, char, etc.), or a class with an assignment
// operator and a copy constructor.
{
    Item temp = x;
    x = y;
    y = temp;
}
```

In this example, the values of x and y are interchanged by the usual three assignment statements that use an intermediary temporary variable (temp). The example shows two new features. First, notice that the function uses a local variable, temp, whose type is Item. This is fine, so long as the Item type has the necessary constructor (we have indicated this requirement in the documentation).

The second feature of the function is that the underlying data type, Item, is used as a reference parameter. Thus, when swap is called, the actual parameters will have their values interchanged, as shown in this string example:

```cpp
string name1("Castor");
string name2("Pollux");
swap(name1, name2);
cout << name1;
```

## SWAP, MAX, AND MIN FUNCTIONS

The <algorithm> facility in the C++ Standard Library contains the swap function, a max function that is similar to our maximal, and a min function that returns the smaller of two items.

## Parameter Matching for Template Functions

Our next template function searches an array for the biggest item and returns the index of that item. For example, the array could be an array of six integers, shown here:

| 10 | 20 | 30 | 1 | 2 | 3 |
|---|---|---|---|---|---|
| [0] | [1] | [2] | [3] | [4] | [5] |

The biggest value, 30, appears at location [2], so with this array as the argument, our function returns 2. Here is the template function's complete specification:

```cpp
template <class Item>
size_t index_of_maximal(const Item data[], size_t n);
// Precondition: data is an array with at least n items, and n > 0.
// Postcondition: The return value is the index of a maximal item from
// data[0] ... data[n - 1]. Note: Item may be any of the C++ built-in types
// (int, char, etc.), or any class with the > operator defined.
```

Actually, this specification is not exactly what we want. To explain the problem, we need to know a bit more about how the compiler uses template functions.

When a template function is instantiated, the compiler tries to select the underlying data type so that the type of each argument results in an exact match with the type of the corresponding formal parameter. For example, suppose that d is a double variable. You cannot write maximal(d, 1), since there is no way for the compiler to have Item be an exact match with the type of the first argument (double) and also be an exact match with the type of the second argument (int). The compiler does not convert arguments for a template function. The arguments must have an exact match, with no type conversion.

The requirement of an exact match applies to all parameters of a template function. For example, consider the index_of_maximal prototype:

```cpp
template <class Item>
size_t index_of_maximal(const Item data[], size_t n);
```

When we call the function, the second argument must be a size_t value. Many compilers won't accept any deviation: not an int, not a const size_t, only a size_t value. On such a strict compiler, the following will fail:

```cpp
const size_t SIZE = 5;
double data[SIZE];
...
cout << index_of_maximal(data, SIZE);
cout << index_of_maximal(data, 5);
```

The first function call, with SIZE as the second argument, fails on many compilers because SIZE is declared as const size_t rather than a mere size_t. The second function call, with 5 as the second argument, fails because the compiler takes 5 to be an int rather than a size_t value.

## A Template Function to Find the Biggest Item in an Array

For the index_of_maximal function, we can deal with the problem by slightly changing the specification. The new specification uses two template parameters, one for the data type of the array's components, and a second for the data type of the size of the array, as shown here:

```cpp
template <class Item, class SizeType>
size_t index_of_maximal(const Item data[], SizeType n);
// Precondition: data is an array with at least n items, and n > 0.
// Postcondition: The return value is the index of a maximal item from
// data[0] ... data[n - 1]. Note: Item may be any of the C++ built-in types
// (int, char, etc.), or any class with the > operator defined.
// SizeType may be any of the integer or const integer types.
```

With this template function, we have more flexibility. Both of these are okay:

```cpp
const size_t SIZE = 5;
double data[SIZE];
...
cout << index_of_maximal(data, SIZE);
cout << index_of_maximal(data, 5);
```

SizeType will be const size_t.
SizeType will be int.

Now we can implement the template function. The function uses a local variable, answer, to keep track of the index of the biggest item that has been seen so far. Initially, answer is set to 0, meaning that the biggest item seen so far is at data[0]. Then we step through the rest of the array: data[1], data[2], and so on. If we spot an item that is bigger than data[answer], then we change answer to the index of that bigger item. Notice that it's okay to use size_t for the return type or for a local variable (or, to be more accurate, we have used std::size_t in this case because it is not under the control of a directive to use the namespace std):

```cpp
template <class Item, class SizeType>
std::size_t index_of_maximal(const Item data[], SizeType n)
// Library facilities used: cassert, cstdlib
{
    std::size_t answer;
    std::size_t i;

    assert(n > 0);
    answer = 0;

    for (i = 1; i < n; ++i)
    {
        if (data[answer] < data[i])
            answer = i;
    } // data[answer] is now biggest from data[0]...data[i]

    return answer;
}
```

## MISMATCHES FOR TEMPLATE FUNCTION ARGUMENTS

Each argument to a template function must be an exact match to the data type of the formal parameter, with no type conversions. C++ compilers provide a little leeway on the meaning of “exact match.” For example, with an `int` argument the formal parameter may be any of the following:

- `int` (a value parameter)
- `int&` (a reference parameter)
- `const int&` (a const reference parameter)

But for many compilers, an `int` argument does *not* provide an exact match to `size_t`. With this in mind, we generally will use an extra template parameter for the data type of an integer or `size_t` argument. For example:

```cpp
template <class Item, class SizeType>
std::size_t index_of_maximal(const Item data[], SizeType n);
```

## A Template Function to Insert an Item into a Sorted Array

Our next example defines a template function to insert a new entry into an array that is already sorted from small to large. The insertion must keep all the items in order from small to large. Here is the function’s specification:

```cpp
template <class Item, class SizeType>
void ordered_insert(Item data[], SizeType n, Item entry);
// Precondition: data is a partially filled array containing n items sorted from
// small to large. The array is large enough to hold at least one more item.
// Postcondition: data is a partially filled array containing the n original items
// plus the new entry. These items are still sorted from small to large.
// NOTE: Item may be any of the C++ built-in types (int, char, etc.), or a
// class with the < operator, an assignment operator, and a copy
// constructor. SizeType may be any of the integer or const integer types.
```

For example, suppose that data is this partially filled array of integers, sorted from small to large:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_326_0.png)

We can use the ordered_insert function to insert a new number, as shown here:

```cpp
ordered_insert(data, 3, 15);
```
