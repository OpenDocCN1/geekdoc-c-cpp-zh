A unary operator such as ! may be overloaded as a global function with one parameter in two different ways—either with a parameter that is an object (this requires a copy of the object, so the side effects of the function are not applied to the original object), or with a parameter that is a reference to an object (no copy of the original object is made, so all side effects of this function are applied to the original object). If s is a String class object (or a reference to a String class object), then !s is treated as if the call operator! (s) had been written, invoking the global operator! function that is declared as follows:

```
```cpp
bool operator!( const String & );
```
```

# 11.7 Overloading Binary Operators

A binary operator can be overloaded as a non-static member function with one parameter or as a global function with two parameters (one of those parameters must be either a class object or a reference to a class object).

Later in this chapter, we’ll overload < to compare two String objects. When overloading binary operator < as a non-static member function of a String class with one argument, if y and z are String-class objects, then y < z is treated as if y.operator<(z) had been written, invoking the operator< member function declared below

```
```cpp
class String

public:
    bool operator<( const String & ) const;

}; // end class String
```
```

As a global function, binary operator < must take two arguments—one of which must be an object (or a reference to an object) of the class. If y and z are String-class objects or references to String-class objects, then y < z is treated as if the call operator<(y, z) had been written in the program, invoking global-function operator< declared as follows:

```
```cpp
bool operator<( const String &, const String & );
```
```

# 11.8 Dynamic Memory Management

A standard C++ array data structure is fixed in size once it’s created. The size is specified with a constant at compile time. Sometimes it’s useful to determine the size of an array dynamically at execution time and then create the array. C++ enables you to control the allocation and deallocation of memory in a program for objects and for arrays of any built-in or user-defined type. This is known as dynamic memory management and is performed with the operators new and delete.

You can use the new operator to dynamically allocate (i.e., reserve) the exact amount of memory required to hold an object or array at execution time. The object or array is created in the free store (also called the heap)—a region of memory assigned to each program for storing dynamically allocated objects. Once memory is allocated in the free store, you can access it via the pointer that operator new returns. When you no longer need the memory, you can return it to the free store by using the delete operator to deallocate (i.e., release) the memory, which can then be reused by future new operations.