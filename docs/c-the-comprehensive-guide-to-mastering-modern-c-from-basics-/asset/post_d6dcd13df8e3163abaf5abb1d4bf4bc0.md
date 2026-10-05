
```cpp
std::vector<int> quis{1,4,9,16,25};
for(unsigned idx=0; idx<quis.size(); ++idx) // returns the count
    std::cout << quis[idx] << " "; // [idx] or at(idx) gets an element
    std::cout << std::endl;
}
```

# Listing 6.11 Accessing the elements by index.

In C++, however, you should use iterators instead of an index. They can be used more widely, may be easier for the compiler to handle, and all, are the same for all containers.

```cpp
// https://godbolt.org/z/1WG8zvhYe
#include <vector>
#include <iostream> // cout, endl
int main() {
    std::vector<int> quis{1,4,9,16,25};
    for(auto it = quis.begin(); it!=quis.end(); ++it) // between begin() and end() {
        std::cout << *it << " "; // with *it you get from the iterator to the element
        std::cout << std::endl;
    }
}
```

# Listing 6.12 The use of the iterators for a loop.

Just like containers, iterators are a general idea. They work closely with containers and are also explained in detail in Chapter 24. For now, I will summarize them for you in the shortest possible way:

- `quis.begin()` and `quis.end()`: Return iterators for the start and end of the container, similar to how they and `size()` provide the bounds of the indexes.
- `auto it = quis.begin()`: Defines an iterator and initializes it to the start of the container.
- `it != quis.end()`: Checks if you are at the end. Always check with "not equal," never with "less."
- `*it`: Goes from the iterator to the element. You "dereference" the iterator.

### The Standard Library Contains Many Containers
The other containers and plenty of instructions on how to use them can be found in Chapter 24.

# 6.5 Algorithms

In addition to the capabilities of the containers, there are **algorithms**. Most of them can be found in the `<algorithm>` header. There is a long list of auxiliary functions that help you to solve specific problems using general methods.

All these algorithms consistently work on iterators, which is why they work on (almost) all containers. It is important to know that the power of the containers is not exhausted by their methods.

In the following example, a vector is filled with an algorithm, and then elements meeting a specific criterion are counted.

```cpp
// https://godbolt.org/z/4G67rso8T
#include <vector>
#include <algorithm>             // count_if
#include <numeric>                // iota
#include <iostream>
bool even(int n) { return n==0; }  // test for even
int main() {
    std::vector<int> data(100);          // 100 x zero
    std::iota(data.begin(), data.end(), 0); // 0, 1, 2, ... 99
    // counts even numbers
    std::cout << std::count_if(data.begin(), data.end(), even);
}
```

**Listing 6.13** Counting with an algorithm.

# 6.6 Pointers and C-Arrays

In discussing the built-in data types, I have so far omitted two very important types: pointers and C-arrays. These two are closely related, which is why I treat them together. There are two reasons that this happens so late:

- They have their own principles and bring with them a huge range of things that you need to understand to use them effectively.
- For the tasks they solve, they are only the second-best option in modern C++. Since C++11 at the latest, there is usually a better alternative in the language or the standard library.

Therefore, I will give you a brief introduction to pointers and C-arrays. You will learn more in Chapter 20—and you will learn more there about the alternatives.

# 6.6.1 Pointer Types

A pointer is the C variant of a reference, which is still used frequently in C++ due to historical reasons. It is an indirection to the actual value. Therefore, every type can also exist as a pointer—even pointers themselves, meaning that a pointer can point to a pointer. A pointer represents an address in memory, and the computer can perform calculations with it: it can form differences, increment, and so on. Therefore, pointers are well-suited for large and dynamic memory amounts. With the address operator `&`, you determine the address of an object and obtain a pointer type. You can recognize it by an asterisk `*` following the type. For example, after `int x=12;` you can determine the address with `int* p = &x;`. This int points to an int value, and a `char*` points to a char value. Only the pointer type `void*` is flexible in what it points to—and is therefore unsafe and should be avoided. If a pointer points to nowhere, it has the special value `nullptr`.

# 6.6.2 C-Arrays

C-arrays are denoted with square brackets `[]`. In the declaration, these are placed after the variable name. For example, `int nums[10]` stores 10 int values directly next to each other. The type of `nums` is `int[10]`—so long as...

# 7.0 Functions

You have already seen some functions, and you have already written some of yourself—primarily the main() function, because you can't do without main(). In this chapter, I want to explain the possibilities you have with functions, especially when you write them yourself.

A function is something that you can call from another location. Functions can also have a return value. A function that does not have a return value is said to return `void`. In addition to calculating the return value, parameters can also be changed if you allow it.

# 7.1 Declaration and Definition of a Function

When you write a function and immediately specify what its program code looks like—that is, with the instructions in the curly brackets—then this is the definition of the function. However, you can also first tell the compiler that a certain function exists somewhere; where exactly, it should figure out later. Then you omit the brackets and only name the function header—and you have a declaration.
