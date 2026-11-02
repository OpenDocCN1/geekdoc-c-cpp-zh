Regardless of whether this is a self-assignment, the member function returns the current object (i.e., *this in line 61) as a constant reference; this enables cascaded Array assignments such as x = y = z, but prevents ones like (x = y) = z because z cannot be assigned to the const Array reference that's returned by (x = y). If self-assignment occurs, and function operator= did not test for this case, operator= would unnecessarily copy the elements of the Array into itself.

> **Software Engineering Observation 18.4**
> A copy constructor, a destructor and an overloaded assignment operator are usually provided as a group for any class that uses dynamically allocated memory. With the addition of move semantics in C++11, other functions should also be provided, as we discuss in Chapter 24 of our book C++ How to Program, 9/e.

> **Common Programming Error 18.5**
> Not providing a copy constructor and overloaded assignment operator for a class when objects of that class contain pointers to dynamically allocated memory is a potential logic error.

# C++11: Move Constructor and Move Assignment Operator

C++11 adds the notions of a move constructor and a move assignment operator. We discuss these new functions in Chapter 24, C++11: Additional Features, of our book C++ How to Program, 9/e.

# C++11: Deleting Unwanted Member Functions from Your Class

Prior to C++11, you could prevent class objects from being copied or assigned by declaring as private the class's copy constructor and overloaded assignment operator. As of C++11, you can simply delete these functions from your class. To do so in class Array, replace the prototypes in lines 15 and 19 of Fig. 18.10 with:

```
Array( const Array & ) = delete;
const Array &operator=( const Array & ) = delete;
```

Though you can delete any member function, it's most commonly used with member functions that the compiler can auto-generate—the default constructor, copy constructor, assignment operator, and in C++11, the move constructor and move assignment operator.

# Overloaded Equality and Inequality Operators

Line 20 of Fig. 18.10 declares the overloaded equality operator (==) for the class. When the compiler sees the expression integers1 == integers2 in line 55 of Fig. 18.9, the compiler invokes member function operator== with the call

```
integers1.operator==( integers2 )
```