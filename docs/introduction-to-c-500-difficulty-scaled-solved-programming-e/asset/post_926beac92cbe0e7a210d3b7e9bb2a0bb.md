
# 25 • Namespaces, Type Cast Operators, and Smart Pointers 833

```cpp
int main()
{
    auto sp = make_shared<int>(10);
    weak_ptr<int> wp(sp); /* The reference counter for the allocated
    memory is not increased. */

    shared_ptr<int> ptr = wp.lock(); /* Alternatively, we could write:
    auto ptr = wp.lock(); and ptr and sp point to the same memory. */
    if(ptr)
        cout << *ptr << '\n';
    else
        cout << "Not valid memory\n";
    return 0;
}
```

When it is declared it is initialized with sp. As we said, the reference counter for this memory does not increase, it retains 1. The direct access through wp is not allowed. We first use the lock(), which returns a shared_ptr object. If the memory pointed by the weak_ptr has not been released, the object (e.g. ptr) has a valid value and we can safely use it to access the memory. Otherwise, lock() returns an empty shared_ptr object. That is, with weak_ptr and lock() we first check if the memory can be managed and then access it. Thus, the program displays 10. In general, weak_ptr is used in advanced cases.

## THE volatile QUALIFIER

The volatile qualifier is rarely used. Typically, it is used in code that communicates with the hardware of the system. It is used to inform the compiler that the value of a variable may change, even if it does not appear to change within the program. In fact, it prevents the compiler from performing optimizations which may be undesirable. Let's look at an example:

```cpp
int out = 0;
while(out != 200)
{
    ... // The value of out does not change inside the program.
}
```

The condition checks if the value of out is not less than 200. Because the value of out seems to remain the same, an optimizing compiler might replace this loop with an infinite loop, such as while(1). However, if out can be modified by a "hidden" entity, such as the system hardware, this optimization would affect the behaviour of the program. To prevent the compiler from optimizing the code we use the volatile qualifier in its declaration, that is, volatile int out;

![](img/25e0e40b08b8016a58f1aab13ac2e812_848_0.png)

## Introduction to Standard Template Library

In this chapter we'll make a brief introduction to Standard Template Library (STL) and its most important features. The STL is part of the C++ standard library; it was designed by Alex Stepanov and contains a large collection of standard algorithms, iterators, containers, and function objects. All these have been designed in a uniform way based on the principles of generic programming. The classes and algorithms it provides can be used in a wide range of applications and saves us from a lot of work. However, a full description of STL would require a separate book. The next challenge for you is to find a book that focuses on STL and read about it. It is very useful to know the tools it offers; it will make your work simpler, safer, and more flexible. The goal of this chapter is to give you an idea about its features and design philosophy. We'll briefly discuss the most important STL components: algorithms, iterators, and containers.

## ALGORITHMS

STL provides a great number of algorithms that can be applied to containers. Most of them are declared in the `<algorithm>` file. The design philosophy is to provide a generic way to operate on the data stored in any container, irrespective of how they are stored or what type of the container. For that reason, the algorithms have been implemented as function templates in order to operate in a simple, elegant, and generic way, which does not depend on the container to be applied. For example, the `find()` function can be used to find a value in a `vector` or `set` container or find a value in a `vector` that contains string elements.

The STL approach is that these functions are not defined as members of the containers, but externally. That is, instead of `find()` for each container, a single non-member `find()` is defined which can be used by all containers. As we'll see later, important that, STL uses iterators to traverse the container. This practice does not increase the complexity of code, and the repetition of similar code is avoided. However, there are cases where the STL defines a function in a container that particular container may be more efficient than the generic function. In general, whenever a container provides a member function that is functionally equivalent to a generic function, it'd be better to use the function.

When we discuss about iterators, which are generalizations of pointers, we will see that the STL functions, besides the containers, can also be applied to non-STL containers, such as array arrays. In general, the first two arguments of most functions are iterators that indicate the range of the elements which will be applied. Let's look briefly at some of them.

## The for_each() Function

The for_each() function works with any container. It takes three parameters. The first is an input iterator which denotes the initial position (e.g. first), the second is an input iterator which denotes the final position without including it (e.g. last), and the third is a pointer to a function. The for_each() function applies the function to the specified range, which is [first, last]. Let's look at an example of its use:

```cpp
#include <iostream> // Example 26.1
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {10, 20, 30, 40, 50}; /* Create a vector with the elements. */
    std::for_each(v.begin(), v.end(), [](int n) {
        std::cout << n << " ";
    });
    return 0;
}
```

The for_each() function works with any container. It takes three parameters. The first is an input iterator which denotes the initial position (e.g. first), the second is an input iterator which denotes the final position without including it (e.g. last), and the third is a pointer to a function. The for_each() function applies the function to the specified range, which is [first, last]. Let's look at an example of its use:

```cpp
#include <iostream> // Example 26.1
#include <vector>
#include <algorithm>

void show(int n) {
    std::cout << n << " ";
}

int main() {
    std::vector<int> v = {10, 20, 30, 40, 50};
    std::for_each(v.begin(), v.end(), show);
    return 0;
}
```

## The find() Function

The find() function works with any container and it is used to search for a value in a container. It takes three parameters. The first two are iterators (e.g. first, last) that indicate the range, which is [first, last]. The third is the value to be searched. If the value is found, find() returns an iterator that points to its position. If not, it returns the second argument (e.g. last). Let's look at an example using an array and vector:

```cpp
#include <iostream> // Example 26.2
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    int *p, arr[] = {10, 20, 30, 40, 50};

    p = find(arr, arr+5, 30);
    if(p != arr+5) cout << "Element " << *p << " found in position " << p-arr-1 << '\n';
    else cout << "Element not found\n';

    vector<int> v(arr, arr+5);
    vector<int>::iterator it;
    it = find(v.begin(), v.end(), 30);
    if(it != v.end()) cout << "Element " << *it << " found in position " << it-v.begin()+1 << '\n';
    else cout << "Element not found\n";

    return 0;
}
```

To give an idea how find() might be defined in STL, here is an implementation example:

```cpp
template <typename Iterator, typename T>
Iterator find(Iterator start, Iterator end, const T& val) {
    for(Iterator p = start; p != end; ++p)
        if(*p == val)
            return p;
    return end;
}
```

In the first call of find() the Iterator is replaced with int*, while in the second call with the iterator member of the vector class.
