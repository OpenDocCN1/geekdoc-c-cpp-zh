
The general form of reinterpret_cast is:

```
new_type x = reinterpret_cast<new_type> (expr)
the parenthesis is required
```

Here, new_type specifies the target type of the cast, and expr is the expression cast into the new type.

```cpp
// An example that uses reinterpret_cast
#include <iostream>
using namespace std;

int main() {
    size_t x;
    const char *p = "This is a string";

    // cast pointer to long
x = reinterpret_cast<long>(p);
    cout << "integer is:" << x << endl;
    return 0;
}

// output
integer is: 4197988
```

Here, reinterpret_cast casts the pointer into a long integer type. This conversion represents a fundamental change of types and is a typical use of reinterpret_cast. Another example is changing a pointer to one type of object (Apricot*) to a pointer to another type of object (Orange*).

```cpp
Orange* ptrOrange = reinterpret_cast<Orange*>(ptrApricot;
```

Note: reinterpret_cast can cast unrelated pointer types, but can't remove const or volatile qualifiers. We need const_cast for this.

## C++ And Assembler

There are a few highly specialized situations that C++ cannot handle. For example, there is no C++ statement to disable CPU interrupts. C++ provides access to very low level functionality by allowing us to drop into assembly language code at any time from C++ code. This functionality is provided through the asm statement.

With asm we can embed assembly language code directly into a C++ program. This assembly language code is compiled without any modification, and it becomes part of a program's code at the point at which the asm statement occurs.

The general form of the asm keyword is:

```
asm("op-code");
```

op-code is an assembly language instruction that will be embedded into our C++ program. Several compilers also allow the following forms of asm:

```asm
asm op-code;
asm {
  op-code
  op-code
  ...
}
```

Here is an example:

```cpp
#include <iostream>
int main() {
  asm int 5; // generate interrupt 5
  return 0;
}
```

## C++ Linkage Specification

In C++ we can specify how a function is linked into our program. By default, functions are linked as C++ functions. However, by using a linkage specification, you can cause the object code for a function written in a different language to be linked into a C++ program. The general form of a linkage specifier is:

```
extern "language" function declaration;
```

Language denotes the language of the function that is to be linked. All C++ compilers support both C and C++ linkage. Some will well allow linkage to Fortran and Pascal language functions.

Every language has its own conventions about function parameters and the function return value have to be loaded on the stack, and how CPU registers are to be saved when program code calls a function. The extern keyword informs the compiler about this convention.

The following program causes the function myCFunc() to be linked as a C function:

```cpp
#include <iostream>
using namespace std;

extern "C" void myCFunc(int);

int main() {
    myCFunc(5);
    return 0;
}

// Because of the extern statement,
// the following function will be linked as a C function.
void myCFunc(int val) {
    cout << "This links as a C function with value: ";
    cout << val << endl;
}
```

A linkage specification must be declared at the global level; it cannot be placed inside a function.

We can use the following linkage specification to link more than one function at a time:

```
extern "language" {
  function declaration;
  ...
}
```

## Summarizing the Differences Between C and C++

For the most part, Standard C++ is a superset of Standard C, and virtually all C programs are also C++ programs. However, a few differences do exist.

In C++, local variables can be declared anywhere within a block. In C, they must be declared at the start of a block, before any "action" statements occur.

In C, a function declared as follows:

```c
int f();
```

says nothing about the parameters of the function. In C, when there is nothing specified between the parentheses following the function's name, this means that nothing is being stated, one or the other, about any parameters of the function. It might have parameters, or it might not. However, in C++, a function declaration like this means that the function does not have any parameters. In C++, the following two declarations are equivalent:

```cpp
int f();
int f(void);
```

In C++, all functions must have declarations which are typically in header files.

A small but potentially important difference between C and C++ is that in C, a character constant such as 'c' is automatically elevated to an integer. In C++ it is not.

In C, although it is unusual, you can call main from within your program. This is not allowed in C++.

In C, it is not an error to declare a global variable several times, even though this is bad programming practice. In C++, it is an error.

In C, you cannot take the address of a register variable. In C++, this is allowed, however the register keyword is deprecated.

In C, if no type specifier is present in a declaration statement, the type int is assumed. This "default-to-int" rule is not permissible in C++.

## C++ Standard Template Library

The C++ Standard Template Library provides solutions to a variety of common programming problems. The library is composed of three foundational components: containers, iterators and algorithms.

### Containers

Containers are objects that hold other objects. There are several different types of containers. For example, the vector class (container) defines a dynamic array, the deque container implements a double-ended queue, and the list container provides a linear list. These containers are called sequence containers. The STL also implements associative containers, which map keys to values and these enable the retrieval of values from keys.

Each container class defines a set of member functions that may be applied to objects in the container.

### Algorithms

Algorithms act on containers. They provide the means by which we can manipulate the contents of containers. Algorithms can initialize, sort, search and transform the contents of containers.

### Iterators

Iterators are objects that behave like pointers. They give us the ability to traverse through the items in a container in much the same way we can use a pointer to traverse an array. There are five types of iterators:

- **Random Access Iterators**: Store and retrieve values. Elements are accessed randomly.
- **Bidirectional Iterators**: Store and retrieve values. These iterators move forward and backwards.
- **Forward Iterators**: Store and retrieve values. This type of iterator is forward moving only.
- **Input Iterators**: Store but not retrieve values. Forward moving only.
- **Output Iterators**: Retrieves but not store values. Forward moving only.

The STL also supports reverse iterators. Reverse iterators move through a sequence the reverse direction. Thus, if a reverse iterator points to the end of a sequence, incrementing that iterator will cause it to point to one element before the end.

### Other STL Elements

In addition to containers, algorithms, and iterators, the STL also implements several other components such as allocators, predicates, comparison functions, and function objects (functors).

Each container has at least one allocator defined for it. Allocators manage memory allocation for a container. The default allocator is an object of class allocator. We can define our own allocators if needed.

Some of the algorithms and containers use a special type of function called a predicate function. A predicate function returns true or false.

The templates in the header file <functional> help us construct function objects (functors). Function objects can be used in place of function pointers in many places.
