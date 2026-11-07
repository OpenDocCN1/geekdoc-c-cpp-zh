
## 13 Data Structures: Standard Library Containers and Iterators

![](img/7b5e2088e71c7f78681d4ddbcf104c06_755_0.png)

### Objectives

In this chapter, you’ll:

- Learn more about the C++ standard library’s reusable containers, iterators, and algorithms.
- Understand how containers relate to C++20 ranges.
- Use I/O stream iterators to read values from the standard input stream and write values to the standard output stream.
- Use iterators to access container elements.
- Use the vector, list and deque sequence containers.
- Use ostream_iterators with the std::copy and std::ranges::copy algorithms to output container elements in a single statement.
- Use the set, multiset, map and multimap ordered associative containers.
- Understand the differences between the ordered and unordered associative containers.
- Use the stack, queue and priority_queue container adaptors.
- Use the bitset “near container” to manipulate a collection of bit flags.

### Outline

- 13.1  Introduction
- 13.2  A Brief Intro to Big O
- 13.3  A Brief Intro to Hash Tables
- 13.4  Introduction to Containers
  - 13.4.1  Common Nested Types in Sequence and Associative Containers
  - 13.4.2  Common Container Member Functions
  - 13.4.3  Requirements for Container Elements
- 13.5  Working with Iterators
  - 13.5.1  Using istream_iterator for Input and ostream_iterator for Output
  - 13.5.2  Iterator Categories
  - 13.5.3  Container Support for Iterators
  - 13.5.4  Predefined Iterator Type Names
  - 13.5.5  Iterator Operators
- 13.6  A Brief Introduction to Algorithms
- 13.7  Sequence Containers
- 13.8  vector Sequence Container
  - 13.8.1  Using vectors and Iterators
  - 13.8.2  vector Element-Manipulation Functions
- 13.9  list Sequence Container
- 13.10  deque Sequence Container
- 13.11  Associative Containers
  - 13.11.1  multiset Associative Container
  - 13.11.2  set Associative Container
  - 13.11.3  multimap Associative Container
  - 13.11.4  map Associative Container
- 13.12  Container Adaptors
  - 13.12.1  stack Adaptor
  - 13.12.2  queue Adaptor
  - 13.12.3  priority_queue Adaptor
- 13.13  bitset Near Container
- 13.14  Wrap-Up
- Exercises

### 13.1 Introduction

The standard library defines powerful, template-based, reusable components that implement many common data structures and algorithms used to process those data structures. We began introducing templates in Chapters 5–6 and use them extensively here and in Chapters 14 and 15. Historically, the features presented in this chapter were referred to as the Standard Template Library or STL.¹ In the C++ standard document, they are simply referred to as part of the C++ standard library.

### Containers, Iterators and Algorithms

This chapter introduces three key standard library components—containers (templated data structures), iterators and algorithms. We’ll introduce containers, container adaptors and near containers.

### Common Member Functions Among Containers

Each container has associated member functions—a subset of these is defined in all containers. We’ll illustrate most of this common functionality in our examples of array (introduced in Chapter 6), vector (also introduced in Chapter 6 and covered in more depth here), list (Section 13.9) and deque (pronounced “deck”; Section 13.10).

### Iterators

Iterators, which have properties similar to pointers, are used to manipulate container elements. Built-in arrays also can be manipulated by standard library algorithms using pointers as iterators. We’ll see that manipulating containers via iterators provides tremendous expressive power when combined with standard library algorithms—sometimes reducing many lines of code to a single statement.

1. The STL was developed by Alexander Stepanov and Meng Lee at Hewlett-Packard and is based on their generic programming research, with significant contributions from David Musser. https://en.wikipedia.org/wiki/History_of_the_Standard_Template_Library; Accessed April 18, 2023.

### Algorithms

Standard library algorithms (which we’ll cover in Chapter 14) are function templates that perform common data manipulations, such as searching, sorting, copying, transforming and comparing elements or entire containers. The standard library provides over 100 algorithms:

- 90 in the `<algorithm>` header’s `std` namespace—82 also are overloaded in the `std::ranges` namespace for use with C++20 ranges.
- 11 in the `<numeric>` header’s `std` namespace,
- 14 in the `<memory>` header’s `std` namespace—all 14 also are overloaded in the `std::ranges` namespace for use with C++20 ranges and
- 2 in the `<cstdlib>` header.

For the complete list of algorithms with links to their descriptions, visit:

https://en.cppreference.com/w/cpp/algorithm

Most algorithms use iterators to access container elements. Each algorithm has minimum requirements for the kinds of iterators that can be used with it. We’ll see that containers support specific kinds of iterators, some more powerful than others. The iterators a container supports determine whether the container can be used with a specific algorithm. Iterators encapsulate the mechanisms used to traverse containers and access their elements, enabling many algorithms to be applied to containers with significantly different implementations. This also enables you to create new algorithms that can process the elements of multiple container types.

### C++20 Ranges

Chapter 6 introduced C++20’s ranges and views. You saw that a range is a collection of elements you can iterate over. So, arrays and vectors are ranges. You also used views to specify pipelines of operations that manipulate ranges of elements. Any container with iterators representing its beginning and end can be treated as a C++20 range. In this chapter, we’ll use the C++20 standard library algorithm `std::ranges::copy` and the older C++ standard library algorithm `std::copy` to demonstrate how ranges simplify your code. In Chapter 14, we’ll use many more C++20 algorithms from the `std::ranges` namespace to demonstrate additional ranges and views features.

### Custom Templatized Data Structures

Some popular data structures include linked lists, queues, stacks and binary trees:

- Linked lists are collections of data items logically “lined up in a row.” Insertions and removals are made anywhere in a linked list.
- **Stacks** are important in compilers and operating systems. Insertions and removals are made **only** at one end of a stack—its **top**.
- Queues represent waiting lines. Insertions are made at the back (also called the **tail**), and removals are made from the front (also called the **head**).
- Binary trees are nonlinear, hierarchical data structures that facilitate **searching** and **sorting** data and **duplicate elimination**.

Each of these data structures has many other interesting applications. We can carefully weave linked objects together with pointers, but pointer-based code is complex and can be error-prone. The slightest omissions or oversights can lead to serious **memory-access violations** and **memory leaks** with no forewarning from the compiler.

Avoid reinventing the wheel. When possible, use the C++ standard library’s preexisting containers, iterators, and algorithms.² The prepackaged container classes provide the data structures you need for most applications. Using the standard library’s proven containers, iterators and algorithms helps you reduce testing and debugging time. They were conceived and designed for performance and flexibility.

This chapter begins with two special computer science sections on

- **Big O notation** for expressing how hard algorithms have to work based on the number of items they process, and
- hash tables for high-speed storage and retrieval of data in applications with common real-world characteristics.

2. C++ Core Guidelines, “SL.1: Use Libraries Wherever Possible.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rsl-lib.

### 13.2 A Brief Intro to Big O

In this section, we’ll discuss what Big O means and explain the significance of several popular Big O notations, including *O(1)*, *O(n)*, *O(log n)* and *O(n²)*. In Chapter 21, we’ll explain Big O of *O(n log n)*. On today’s desktop computers, which commonly perform billions of operations per second, an algorithm’s efficiency, as expressed by its Big O, translates to whether a program will run almost instantaneously or take seconds, minutes, hours, days, months or even years to complete. Obviously, you’d prefer algorithms that complete quickly, even though the number of items, *n*, they may be processing is large. This is especially true in today’s world of Big Data computing applications. We’ll mention Big O briefly here, use it extensively in Chapter 14 to characterize the efficiency of standard library algorithms and use it in Chapter 21 to characterize the efficiency of various popular searching and sorting algorithms we’ll implement.

### O(1) Algorithms

Suppose an algorithm tests whether the first element of an array is equal to the second. If the array has 10 elements, this algorithm requires one comparison. If the array has 1,000 elements, it still requires one comparison. In fact, the algorithm is independent of the number, *n*, of elements in the array. This algorithm is said to have constant running time, which is represented in Big O notation as *O(1)* and pronounced as “order one.” An algorithm that’s *O(1)* does not necessarily require only one comparison. *O(1)* just means that the number of comparisons is constant—it does not grow as the size of the array increases. An algorithm that tests whether the first element of an array is equal to any of the next three elements is still *O(1)* even though it requires three comparisons.

### O(n) Algorithms

An algorithm that tests whether the first array element is equal to any of the other array elements will require at most *n − 1* comparisons, where *n* is the number of array elements. If the array has 10 elements, this algorithm requires up to nine comparisons. If the array
