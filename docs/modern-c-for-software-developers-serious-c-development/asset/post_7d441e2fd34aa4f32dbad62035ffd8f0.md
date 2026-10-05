
that it can't be deleted or accidentally reused. This is important. Lastly, we set other.m_size to 0.

We have thus replaced an expensive memory allocation and copy operation with a pointer copy. The time complexity for creating the Holder object is constant regardless of the size of the underlying array.

The move assignment operator is similar:

```cpp
Container&operator=(Container& other) {
    if (this == &other) return *this;

    delete[] m_data; // (1)
    m_data = other.m_data; // (2)
    m_size = other.m_size;

    other.m_data = nullptr; // (3)
    other.m_size = 0;

    return *this;
}
```

## Moving lvalue To rvalue

We can move a lvalue to a rvalue by using std::move().move() performs a static cast of a lvalue to a rvalue. Look at the following program:

```cpp
int main() {
    Container h1(100000); // h1 is an lvalue

    // copy constructor h2(Container&) invoked
    Holder h2(h1)
}
```

In this example, the h2 copy constructor and the expensive memory allocation in it is invoked because h1 is a lvalue. But we can avoid this expensive copy by moving h1 to a

```cpp
int main()
{
    Container h1(100000);      // h1 is an lvalue
    // move constructor is invoked because
    // the h2 constructor receives a rvalue

    Holder h2(std::move(h1));
}
```

In this example, the move constructor is invoked. std::move converts a lvalue to a rvalue and in our example, invokes the move constructor.

## Throwing Exceptions

Ideally move constructors and move assignment operators should never throw an exception. The rationale is that we should not allocate memory or call functions in move constructors and move assignment operators. We should only move data and set other objects to null, these are non-throwing operations.

## Modern C++: Smart Pointers (C++11)

A C++ program has five distinct physical memory areas. These are: the Text segment which stores the program code, the Data segment which stores static initialized variables, the Block Started By Segment (BSS) which stores static uninitialized variables, the Stack Segment, and the Heap Segment (you can also refer to the Memory Layout Of C Programs portion in this book).

## The Stack

By default, variables and objects in C++ are stored on the stack:

```cpp
#include <iostream>
#include <string>

void foo(int a) {
    if (a > 0) {
        std::string s = "positive number received: ";
        std::cout << s << a << "\n";
    }
}

int main() {
    foo(5);
}

// output
positive number received: 5
```

In this example, the variables a and s are stored on the stack. The fundamental rule of stack variables is: objects allocated on the stack are automatically destroyed when they go out of scope.

In C++, a scope is defined by a pair of brackets { and } provided that these brackets are not used for variable initialization. Thus:

```cpp
std::vector<int> v = {1, 2, 3}; // this is not a scope
if (v.size() > 0) {
    // this is the beginning of a scope
    // this is the end of a scope
}
```

In C++ there are only three ways a variable can go out of scope:

- encountering a closing bracket }
- encountering a return statement,
- having an exception thrown inside the current scope that is not caught inside the scope

## The Heap

Dynamically allocated objects are stored on the heap. These are objects that are allocated memory by a call to new. new returns a pointer to the allocated memory:

```cpp
float* pi = new float(3.127);
```

Objects that are allocated with new can only be destroyed by manually calling delete:

```cpp
delete pi;
```

Contrary to the objects on the stack, objects allocated on the heap are not destroyed automatically. This offers the advantage of being able to keep these objects around beyond the end of a scope.

There are benefits in having pointers to allocated memory. Objects and functions receive copies of pointers; these copies are very cheap to make. Pointers also allow us to manipulate objects through polymorphism: a pointer to a base class polymorphic object can point to an object of a derived class.

However deleting objects on the heap is not trivial. delete has to be called once and only once to free the memory allocated to a heap-based object. If delete is not called, the memory allocated to the object is not freed, and this memory space is not reusable This is called a memory leak. If on the other hand, the program will have undefined behaviour if delete is called more than once on the same address.

## Types Of Memory Errors

When we are dealing with memory allocation and pointers there are five types of possible errors:

**Memory Leak**: failure to free memory:

```cpp
#include <memory>
void main() {
    int *ptr = new int;
}
```

**Double Free**: Freeing the same piece of memory twice:

```cpp
#include <memory>
void main() {
    int *ptr = new int;
    free(ptr);
    free(ptr);
}
```

**Use After Free**: Using a pointer after the memory to which it has been freed:

```cpp
#include <memory>
void main() {
    int *ptr = new int;
    free(ptr);
    // use ptr here
}
```

The problem with memory management is that objects can have ambiguous semantics. Consider:

```cpp
Container* ptr = nullptr;
```

The problem with memory management is that objects can have ambiguous semantics. Consider:

```cpp
Container* ptr = nullptr;
```

The problem with memory management is that objects can have ambiguous semantics. If the caller deletes the pointer, then the program will have undefined behaviour.

## RAII

Smart pointers are a solution to dangling pointers and UAF errors.

RAII means Resource Allocation Is Initialization. The principle of RAII is simple: we wrap an object around a resource allocated on the heap and the resource is deleted in the object's destructor. The object exists on the stack and is thus destroyed. This is exactly how smart pointers work.

Lets consider a smart pointer class that wraps a raw pointer of T. A smart pointer class for T can be defined as follows:

```cpp
#include <iostream>

template <typename T>
class SmartPointer{
public:
    explicit SmartPointer(T* p) : ptr(p)
    {
        std::cout << "smart constructor called" << std::endl;
    }
    ~SmartPointer()
    {
        delete ptr;
        std::cout << "smart pointer destructor called" << std::endl;
    }
    const T operator*() { return *ptr; }

private:
    T* ptr;
};

int main() {
    // allocate some raw memory
    int *p = new int(5);

    // wrap a smart pointer class around the raw memory
    SmartPointer<int> sp(p);
    std::cout << "value = " << *sp << std::endl;

    // output
smart pointer constructor called
value = 5
smart pointer destructor called
}
```

The main benefit of a smart pointer object is that we can manipulate smart pointers as objects allocated on the stack. The compiler automatically takes care of calling the destructor for a smart pointer because objects allocated on the stack are automatically destroyed when they go out of scope.

If we overload the * and -> operators for a smart pointer class, a smart pointer class can syntactically behave like a raw pointer. The smart pointer can be dereferenced with the * operator or the -> operator, that is to say you can call *sp or sp-> on it. If we
