
He is the originator of two popular C++ online courses on www.quantnet.com in cooperation with Quantnet LLC and Baruch College (CUNY), NYC. He also trains quant developers around the world. He can be contacted at: dduffy@datasim.nl. The official Datasim site is www.datasimfinancial.com.

## 1.12 THE SOURCE CODE AND GETTING THE SOURCE CODE

The C++ code in this book is based on the C++11 standard (and later versions). The only exception is the code in Chapter 14 where we introduce the Excel Driver library and in Chapter 27 where we discuss interfacing between C++ and Microsoft’s .NET Framework. Furthermore, the code that is presented in each chapter is machine readable and has been tested beforehand. Our development environment is Visual Studio C++ which supports all the C++ functionality that we present in this book. We have not tested the code using other compilers but we would not expect major issues. It is the responsibility of the reader to know how to install the compiler, Boost C++ libraries and Quantlib.

Regarding copyright, legitimate owners of the book are entitled to the source code which can be used for personal use provided you do not remove the copyright notice in the source code

```
(C) Datasim Education BV 2018
```

For further queries concerning training and support, please contact me directly at dduffy@datasim.nl. The corresponding website is www.datasim.nl.

The four other classes in Boost are:

- *Scoped array*: ensures proper deletion of dynamically allocated arrays in a scope.
- *Shared array*: enables shared ownership of arrays. It is similar to the shared pointer class except that it is used with arrays instead of with single objects.
- *Weak pointer*: this is an *observer* of a shared pointer. It does not interfere with the ownership of the object that the shared pointer shares. Its main use is to avoid dangling pointers because a weak pointer cannot hold a dangling pointer. For completeness we note that a valid weak pointer can be promoted to a strong pointer (shared) and hence the lifetime of the original shared pointer might be affected/extended by that promotion.
- *Intrusive pointer*: this is a special kind of smart pointer and is used in code that has already been written with an internal reference counter. You can write your own smart pointer class when you are not happy with the performance of shared pointers or when the software that you are using denotes it.

### 2.2.1 An Introduction to Memory Management

In this section we give a short overview of object lifecycles. In particular, we are interested in *heap-based memory allocation* of objects. Such memory allocation and deallocation in C++ is the responsibility of the developer. But knowing when memory is no longer needed is not easy to determine and this uncertainty can lead to a number of problems:

- *Dangling pointers*: these occur when an object is deleted or deallocated without modifying the value of the pointer. In this case the pointer continues to point to the location of the deallocated memory.
- *Wild pointers*: these are pointers that are used before they are initialised.
- *Memory leak*: in this case the program is unable to release memory that it has acquired. This situation can be caused by a pointer when it goes out of scope. In other words, the dynamically allocated memory is unreachable and lost forever.
- *Double free bugs*: this refers to the case when we try to delete memory that has already been deleted.

In order to resolve (or avoid) these problems we have a number of options open to us. We can allow automatic memory management by using *garbage collection* (GC) that is supported by some languages such as C# and Java. The garbage collector attempts to reclaim memory used by objects that will never be accessed again in an application. Garbage collection is the opposite of *manual memory management*. There are various kinds of garbage collectors, the most common being called *trace garbage collectors*. These first determine which objects are reachable (or potentially reachable) and they then proceed to discard the remaining ‘dead’ objects.

There is also the *reference counting* technique (used in C++) that stores the number of pointers or handles to a dynamically allocated object. When an object is no longer referenced it will be deleted from memory. Reference counting is a form of garbage collection in which each object contains a count of the number of references to it that are held by other objects. Reference counting can entail frequent updates because the reference count needs to be incremented or decremented when an object is referenced or dereferenced.

Some of the advantages of reference counting are:

- Objects are reclaimed as soon as they are no longer referenced and then in an incremental fashion without incurring long waits on collection cycles.
- Reference counting is one of the simplest forms of garbage collection to implement.
- It is a useful technique for the management of non-memory resource objects (such as file and database handles).

Some disadvantages of reference counting are:

- Frequent updates are a source of inefficiency because objects are being continually accessed. Furthermore, each memory-managed object must reserve space for a reference count.
- Some reference-counting algorithms cannot resolve reference cycles (objects that refer directly or indirectly to themselves).

We now discuss the smart pointer library in C++11. We note that classical garbage collection is not implemented in C++. There is a need in C++ for some kind of automatic (or semi-automatic) memory management mechanism and to this end C++ provides template classes to help developers create reliable and robust code. In general, we use smart pointers in the following situations:

- Avoiding the errors that we discussed in this section.
- Creating objects with well-defined lifetimes.
- Shared ownership of resources.
- Resolving a number of exception-unsafe problems when using raw pointers.

## 2.3 USING SMART POINTERS IN CODE

We discuss three classes of smart pointers in C++. In the next sections we focus on the syntax of each class and we give some simple examples to show what they do.

### 2.3.1 Class `std::shared_ptr`

This smart pointer class implements the concept of *shared ownership*. A resource or object (a piece of memory on the heap or a file handle, for example) is shared among a number of shared pointers. Only when the resource is no longer needed is it deleted. This is when the *reference count* becomes zero.

We discuss shared pointers in some detail. First, we show how to create empty shared pointers and shared pointers that are coupled to resources. We also show how a shared pointer gives up ownership of one resource and how it becomes owner of another resource. We can see how many shared pointers *own* a resource by using the member function `use_count()`:

```
#include <memory>

// Handy alias
template <typename T>
    using SP = std::shared_ptr<T>;
using value_type = double;
```

```
// Creating shared pointers with default deleters
SP<value_type> sp1;                          // empty shared ptr
SP<value_type> sp2(nullptr);                // empty shared ptr for
                                            // C++11 nullptr

SP<value_type> sp3(new value_type(148.413));  // ptr owning raw ptr
SP<value_type> sp4(sp3);                    // share ownership with sp3
SP<value_type> sp5(sp4);                    // share ownership with sp4
                                            // and sp3

// The number of shared owners
std::cout << "sp2 shared # " << sp2.use_count() << '\n';
std::cout << "sp3 shared # " << sp3.use_count() << '\n';
std::cout << "sp4 shared # " << sp4.use_count() << '\n';

sp3 = sp2;  // sp3 now shares ownership with sp2;
            // sp3 no longer has ownership of its previous resource
std::cout << "sp3 shared # " << sp3.use_count() << '\n';
std::cout << "sp4 shared # " << sp4.use_count() << '\n';
```

In the above cases the last owner of the resource is responsible for destroying the resource and by default this is achieved by a call of the operator delete. We now show how to create shared pointers in combination with a user-defined deleter. This is a useful option when you wish to execute a command just before destroying a resource, for example notifying clients or printing a message. We can implement a deleter using a function object, lambda function or stored lambda function (which we shall discuss in Chapter 3), in this case as a function object and as a stored lambda function:

```
// Memory deleters
template <typename T>
struct Deleter
{
    void operator() (T* t) const
    {
        std::cout << "delete memory from function object\n";
        delete t;
    }
};

// Creating shared pointers with user-defined deleters

// Deleter as function object
SP<value_type> sp(new value_type(148.413), Deleter<value_type>());

// Deleter as lambda function
SP<value_type> sp2(new value_type(148.413), [] (value_type* p)
    { std::cout << "bye\n";
      delete p; });
```
