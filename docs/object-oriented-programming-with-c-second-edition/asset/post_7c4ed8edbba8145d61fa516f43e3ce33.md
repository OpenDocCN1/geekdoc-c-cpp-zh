
# Dynamic Memory Management

This version is similar to the previous one with the difference between the empty pair of square brackets appears between the delete keyword and the name of the pointer. C++ knows the exact number of bytes to be returned. It stores the size of the dynamically allocated block in a block of memory that it prefixes the allocated block of memory itself. The set_new_handler() function enables us to set a function of ours as the new handler function.

# Key Terms

- static memory allocation
- static memory deallocation
- dynamic memory allocation
- dynamic memory deallocation
- new operator
- delete operator
- run-time conditions?
- set_new_handler() function
- new handler function

# Exercises

1. What is static memory allocation?
2. When is memory allocated and deallocated in static memory allocation—during compile time, or run time?
3. Under what conditions does static memory allocation become unsuitable?
4. What is dynamic memory allocation? How is it different from static memory allocation?
5. When is memory allocated and deallocated in dynamic memory allocation—during compile time, link time, or run time?
6. Under what conditions does the use of dynamic memory allocation mandatory?
7. What is the syntax of the new operator for
   (a) allocating memory for a single variable?
   (b) allocating memory for an array?
8. Describe how additional blocks of memory can be captured in C++ during run time based on existing run-time conditions?
9. What is the syntax of the delete operator for
   (a) deallocating memory that has been allocated for a single variable?
   (b) deallocating memory that has been allocated for an array?
10. The size of the array, whose memory is to deallocated, is not passed to the delete operator. How does the compiler determine this size?
11. What is memory leak?
12. How can the delete operator be used to prevent a memory leak?
13. What is an out-of-memory condition?
14. What is the new handler? How is the set_new_handler() function used to set our own new handler?

# Constructors and Destructors

We are already aware of the need to include a member function in our class that initializes the data members of its class to desired default values and gets called automatically for each object that has just got created. Constructors fulfill this need and the first portion of this chapter deals with destructors. Various types of constructors are described in the middle portion of this chapter.

There is also the need to include a member function in our class that gets called automatically for each object that is going out of scope. Destructors fulfill this need and the penultimate portion of this chapter deals with destructors.

Along with the class and the access specifiers, constructors and destructors fulfill the requirements needed to created new data type—safe and efficient data types. This is discussed in the last portion of this chapter.

# 4.1 Constructors

The constructor gets called automatically for each object that has just got created. It appears as member function of each class, whether it is defined or not. It has the same name as that of the class. It may or not take parameters. It does not return anything (even void). The prototype of a constructor is:

```
<class name>(parameter list);
```

The need for a function that guarantees initialization of member data of a class was felt in Chapter 2. Constructors fulfill this need. Domain constraints on the values of data members can also be implemented via constructors. For example, the value of data member finches of each object of the class Distance to be between 0.0 and 12.0 at all times during the lifetime of the object. This condition may get violated in case an object has got created. However, introducing a constructor to the class Distance can enforce this condition.

The compiler embeds a call to the constructor for each object when it is created. Suppose a class A has been declared as follows:

```cpp
/*Beginning of A.h*/
class A
{
    int x;
    public:
        void setx(const int x=0);
        int getx();
};
/*End of A.h*/
```

# Constructors and Destructors

Consider the statement that declares an object of a class A in Listing 4.1.

```cpp
/*Beginning of AMain.cpp*/
#include "A.h"
#include <iostream>

void main() {
    A obj1;
}
/*End of AMain.cpp*/
```

# 4.1.1 Zero-argument Constructor

If we do not define any constructor, the compiler provides a default constructor. However, if we define any constructor, the compiler will not provide the default one.

We can define a zero-argument constructor as follows:

```cpp
/*Beginning of A.h*/
class A
{
    int x;
    public:
    A();
    void setx(const int x=0);
    int getx();
};
/*End of A.h*/
```

```cpp
/*Beginning of A.cpp*/
#include "A.h"
#include <iostream>

A::A() {
    x = 0;
    std::cout << "Constructor of class A called" << std::endl;
}
/*End of A.cpp*/
```

When `obj1` is declared in `main()`, the output is:

```
Constructor of class A called
```
