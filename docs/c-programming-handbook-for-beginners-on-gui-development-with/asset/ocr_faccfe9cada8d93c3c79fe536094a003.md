std::vector , std::map ), algorithms (e.g., sorting, searching), and iterators. Here’s an example of using a vector to store and manipulate a list of integers:

```
cpp
Copy code
#include <vector>
#include <algorithm>

std::vector<int> numbers = {5, 3, 8, 1, 4};
std::sort(numbers.begin(), numbers.end());
```

In this example, the std::vector container is used to store a dynamic array of integers. The std::sort algorithm is then applied to sort the vector in ascending order.

# String Manipulation:

The <string> library provides a rich set of functions for manipulating strings. Understanding string manipulation is vital for handling user input and displaying text in your Qt applications. Here’s an example of using strings:

```
cpp
Copy code
std::string greeting = "Hello, ";
std::string name = "World!";
std::string message = greeting + name; // Concatenation
```

This code concatenates two strings, resulting in the message "Hello, World!".

# Memory Management

Memory management is a critical aspect of C++ programming. Unlike languages with automatic garbage collection, C++ requires developers to manage memory manually, using techniques like dynamic allocation and deallocation.