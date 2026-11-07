
```
MyArray destructor
MyArray destructor
MyArray destructor
MyArray destructor
MyArray destructor
```

## Checkpoint

- 1. **(True/False)** When a class contains both a copy constructor and a move constructor, the compiler chooses the move constructor for performance reasons.
  - **Answer:** False. Actually, when a class contains both a copy constructor and a move constructor, the compiler chooses the correct one to use based on the context.
- 2. **(Fill-in)** A(n) ______ reference typically refers to a temporary object or object about to be destroyed. Such objects are called expiring values or ______.
  - **Answer:** *rvalue, xvalues.*
- 3. **(Fill-in)** When the compiler sees that a local object is constructed, returned from a function by value, then used to initialize an object in the caller, the compiler performs the performance optimization called ______.
  - **Answer:** named return value optimization (NRVO).

### 11.6.3 MyArray Class Definition

Now, let’s walk through MyArray’s header (Fig. 11.4). As we refer to each member function in the header, we discuss that function’s implementation in Fig. 11.5. We’ve broken the member-function implementation file into small segments for discussion purposes.

In Fig. 11.4, lines 53–54 declare MyArray’s private data members:

- `m_size` stores its number of elements.
- `m_ptr` is a unique_ptr that manages a dynamically allocated pointer-based int array containing the MyArray object’s elements. When a MyArray goes out of scope, its destructor will call the unique_ptr’s destructor, automatically deleting the dynamically allocated memory.

Throughout this class’s member-function implementations, we use some of C++’s declarative, functional-style programming capabilities discussed in Chapters 6 and 7. We also introduce three additional standard library algorithms—copy, for_each and equal.

```cpp
// Fig. 11.4: MyArray.h
// MyArray class definition with overloaded operators.
#pragma once
#include <initializer_list>
#include <iostream>
#include <memory>

class MyArray final {
    // overloaded stream extraction operator
    friend std::istream& operator>>(std::istream& in, MyArray& a);

    // used by copy assignment operator to implement copy-and-swap idiom
    friend void swap(MyArray& a, MyArray& b) noexcept;

public:
    explicit MyArray(size_t size); // construct a MyArray of size elements

    // construct a MyArray with a brace-initializer list of ints
    explicit MyArray(std::initializer_list<int> list);

    MyArray(const MyArray& original); // copy constructor
    MyArray& operator=(const MyArray& right); // copy assignment operator

    MyArray(MyArray&& original) noexcept; // move constructor
    MyArray& operator=(MyArray&& right) noexcept; // move assignment

    ~MyArray(); // destructor

    size_t size() const noexcept {return m_size;} // return size
    std::string toString() const; // create string representation

    // equality operator
    bool operator==(const MyArray& right) const noexcept;

    // subscript operator for non-const objects returns modifiable lvalue
    int& operator[](size_t index);

    // subscript operator for const objects returns non-modifiable lvalue
    const int& operator[](size_t index) const;

    // convert MyArray to a bool value: true if non-empty; false if empty
    explicit operator bool() const noexcept {return size() != 0;}

    // preincrement every element, then return updated MyArray
    MyArray& operator++();

    // postincrement every element, and return copy of original MyArray
    MyArray operator++(int);

    // add value to every element, then return updated MyArray
    MyArray& operator+=(int value);
private:
    size_t m_size{}; // pointer-based array size
    std::unique_ptr<int[]> m_ptr; // smart pointer to integer array
};

// overloaded operator<< is not a friend—does not access private data
std::ostream& operator<<(std::ostream& out, const MyArray& a);
```

**Fig. 11.4** | MyArray class definition with overloaded operators. (Part 1 of 2.)

**Fig. 11.4** | MyArray class definition with overloaded operators. (Part 2 of 2.)

### 11.6.4 Constructor That Specifies a MyArray’s Size

Line 16 of Fig. 11.4 `explicit MyArray(size_t size); // construct a MyArray of size elements` declares a constructor that specifies the number of MyArray elements. The constructor’s definition (Fig. 11.5, lines 15–19) performs several tasks:

- Line 16 initializes the `m_size` member using the argument `size`.
- Line 17 initializes the `m_ptr` member to a `unique_ptr` returned by the standard library’s `make_unique` function template (see Section 11.5). Here, we use it to create a dynamically allocated int array of size elements. The function `make_unique` value initializes the dynamic memory it allocates, so the int array’s elements are set to 0.
- For pedagogic purposes, line 18 displays that the constructor was called. We do this in all of MyArray’s special member functions and other constructors to give you visual confirmation that the functions are being called.

```cpp
// Fig. 11.5: MyArray.cpp
// MyArray class member- and friend-function definitions.
#include <algorithm>
#include <format>
#include <initializer_list>
#include <iostream>
#include <memory>
#include <span>
#include <sstream>
#include <stdexcept>
#include <utility>
#include "MyArray.h"  // MyArray class definition

// MyArray constructor to create a MyArray of size elements containing 0
MyArray::MyArray(size_t size)
    : m_size{size},
      m_ptr{std::make_unique<int[]>(size)} {
    std::cout << "MyArray(size_t) constructor\n";
}
```

**Fig. 11.5** | MyArray class member- and friend-function definitions.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_675_0.png)

## Checkpoint

- 1. **(True/False)** The function `make_unique` ______ the dynamic memory it allocates.
  - **Answer:** value initializes.

### 11.6.5 Passing a Braced Initializer to a Constructor

In Fig. 6.2, we initialized a `std::array` object with a braced-initializer list, as in

`std::array<int, 5> n{32, 27, 64, 18, 95};`

You can use braced initializers for objects of your own classes by providing a **constructor** with a `std::initializer_list` parameter, as declared in line 19 of Fig. 11.4:

`explicit MyArray(std::initializer_list<int> list);`

The `std::initializer_list` class template is defined in `<initializer_list>`. With this constructor, we can create MyArray objects that initialize their elements as they’re constructed, as in

`MyArray ints{10, 20, 30};`

or

`MyArray ints = {10, 20, 30};`

Each creates a three-element MyArray containing 10, 20 and 30. In a **class that provides an initializer_list constructor**, the class’s other single-argument constructors must be called using parentheses rather than braces. The braced-initialization constructor (lines 22–29 of Fig. 11.5) has one `initializer_list<int>` parameter named `list`. You can determine `list`’s number of elements by calling its **size member function** (line 23).

```cpp
// MyArray constructor that accepts an initializer list
MyArray::MyArray(std::initializer_list<int> list)
    : m_size{list.size()}, m_ptr{std::make_unique<int[]>(list.size())} {
    std::cout << "MyArray(initializer_list) constructor\n";

    // copy list argument's elements into m_ptr's underlying int array
    // m_ptr.get() returns the int array's starting memory location
    std::copy(std::begin(list), std::end(list), m_ptr.get());
}
```

To copy each initializer list value into the new MyArray object, line 28 uses the standard library `copy` algorithm (from header `<algorithm>`) to copy each `initializer_list` element into the new MyArray. The algorithm copies each element in the range specified by its first two arguments—the beginning and end of the `initializer_list`. These elements are copied into the destination specified by `copy`’s third argument. The `unique_ptr`’s **get member function** returns the `int*` that points to the first element of the MyArray’s underlying `int` array.

## Checkpoint

- 1. **(True/False)** In a class that provides an `initializer_list` constructor, the class’s other single-argument constructors must be called using parentheses rather than braces.
  - **Answer:** True.
