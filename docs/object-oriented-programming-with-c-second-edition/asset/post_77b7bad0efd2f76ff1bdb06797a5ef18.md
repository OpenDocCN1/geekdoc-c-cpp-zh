
# Templates 391

of class
//class_name generated
by
//replacing every
occurrence of T
//by int.

For using the vector template class, the header file
vector needs to be included in the source code.

```cpp
#include<vector>
```

Objects of the pair class represent a pair of values
that may or not be of the same type.

A template class can take more than one template-argument.

For using the template class, the header file
utility needs to be included in the source code.

```cpp
#include<utility>
```

A template class can take a non-type template
argument.

The map is used to create associative containers. Elements of the list are key/value pairs.
The map class does not allow duplicates.

The name of the template argument cannot be used more than once in the template class's list of template
arguments.

For using the map class, the header file map
needs to be included in the source code.

The same name for a template argument can be
used in the list of arguments of two different
template classes.

```cpp
#include<map>
```

Each record in a map class is an object of the pair
class objects.

The name of a template argument cannot be
the same in the declaration and the definition of the
template class.

The set is used to create sequential containers. Elements of the list are single objects. A set stores
a collection of keys in a sorted map. The data
elf serves as the keys to the set. The set contains
in a sorted function and duplicates are
discarded during insertion.

Formal functions of template functions can be
objects of template class.

For using the set template class, the header file
set needs to be included in the source code.

Nested classes can be created for template classes
the same way as they are created for non-template
classes.

```cpp
#include<set>
```

The standard implementation of C++ provides
a large number of useful template
definitions of the class templates, their member
functions, and a global number of associated functions.
The global associated functions implement commonly
widely-used algorithms. This library of class templates and
the helper functions are known as the
Template Library or STL.

The only difference between the map and the multimap class is while that the map class does not
allow duplicate keys (it overrides the old value
associated with a key), the multimap class does allow
duplicate keys.

The list class is used to create sequence
containers. Elements of the list are single objects.
For using the list class, the header file
list needs to be included in the source code.

```cpp
#include<list>
```

The elements of a list occupy a non-contiguous
memory. One of the pointers points at the next
element and the other at the previous element of the list.
This allows both forward and backward traversal.

The difference between a set and a multiset
class is while that the set class does not allow
duplicate keys (it overrides the old key value),
the multiset class does allow duplicate keys.

The vector class is used to create sequence
containers. Elements of the list are single objects.
In a vector, unlike a list, elements are stored in
contiguous blocks (like just an array).

For using the multiset class, the header file
file set needs to be included in the source code.

```cpp
#include<set>
```

# 392 Object-Oriented Programming with C++

# Key Terms

function templates
class templates
STL

- pair class
- map class
- set class
- multimap class
- multiset class
- list class
- vector class

# Exercises

1. What are function templates? What is the need for function templates? How are they created?
2. When and how does the C++ compiler generate an actual definition from its template?
3. How is a template overridden for a specific data type?
4. What are class templates? What is the need for class templates? How are they created?
5. When and how does the C++ compiler generate an actual definition from its template?
6. True or false:
   (a) The compiler generates an actual definition from a function template only once for the type of parameters.
   (b) Function templates cannot be overloaded.
   (c) A template class cannot take a non-type argument.
   (d) The name of a template argument need not be the same in the declaration and definition of the template class.
7. What is the Standard Template Library? Name some of the classes that are available in the STL.
8. Create a template for the bubble sort function.
9. Create a template for the Array class.
10. Write a program that will show the following to the user:
    (a) Insert an integer at the end of the list
    (b) Insert an integer at the beginning of the list
    (c) Insert an integer before a specified integer in the list
    (d) Delete the first integer from the list
    (e) Delete the last integer from the list
    (f) Delete a specified integer from the list
    (g) Display the list of integers
    (h) Save the list of integers
    (i) Quit
    Implement the above menu by using the list class of the STL.
11. Assume the user who has used the program in Exercise 10 to save a list of integers (with plenty of duplicates) in a file. Declare a vector that contains all positions of a given integer in the file. Suppose the contents of the file:
   21
   19
   3254
   937
   19
   19
   423
12. Assume the user who has used the program in Exercise 10 to save a list of integers (with plenty of duplicates) in a file. Declare a vector that contains all positions of a given integer in the file. Suppose the contents of the file:
   21
   19
   3254
   937
   19
   19
   423
13. Assume the user who has used the program in Exercise 10 to save a list of integers (with plenty of duplicates) in a file. Declare a vector that contains all positions of a given integer in the file. Suppose the contents of the file:
   21
   19
   3254
   937
   19
   19
   423
14. Assume the user who has used the program in Exercise 10 to save a list of integers (with plenty of duplicates) in a file. Declare a vector that contains all positions of a given integer in the file. Suppose the contents of the file:
   21
   19
   3254
   937
   19
   19
   423

# 11 Exception Handling

This chapter deals with exception handling. The benefits of exception handling and the needed protocol it establishes between the library and its applications are discussed. The chapter begins with a critical study of the C-style solution to exception handling. It then elucidates the use and mechanism of exception handling (the try-throw-catch mechanism). The need to throw objects, the method of accessing members of thrown objects, and the use of nested exception classes are also discussed. The chapter concludes with a study of the limitations of exception handling.

# 11.1 Introduction

Let us begin by assuming the role of a library programmer. While defining non-member or member functions, we face situations where the function may or not be able to execute further. For example, we write a statement to divide double-type variable with another. Before this statement executes, we want to ensure that the denominator is not zero. We want to prevent the function from executing if denominator is zero. This is only one of the conditions under which we want to prevent the further execution of the function. More conditions exist (the function tries to open an unavailable file or requests more memory than is available). We know well the conditions under which the function should be aborted. However, we cannot decide the appropriate handling strategy. While the library function can easily detect error conditions, it cannot decide upon an appropriate handling strategy.

Now, let us assume the role of the application programmer. While calling a function, we should not be burdened with the task of detecting each error in the parameters that we pass to the functions we call. On the other hand, we can only decide what action be taken whenever a particular error is met by the function being called. While the user of the library function cannot detect error conditions, it can decide upon an appropriate handling strategy.
