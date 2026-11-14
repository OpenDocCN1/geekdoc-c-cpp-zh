
directly and objects of the class type must be passed as function parameters. Back to our units: to define different ones, we use operator"":

Click here to view code image

```
length operator"" _m(long double l)
{
    return length(l);
}

length operator"" _km(long double l)
{
    return length(1000.0 * l);
}

length operator"" _nm(long double l)
{
    return length(1852.0 * l);
}
```

In addition to the traditional fashion:

```
length len1(13.5);
```

we can also use our literals:

```
length len2(14.2_km),
    len3= 14.2_km;
```

Using auto variables/constants with such literals wouldn't obfuscate our program since the type is clear from the suffix:

```
auto l1= 13.5_m,
    l2= 14.2_km,
    l3= 3 * 12,
    l4= 7.2_nm;
```

We can also use them directly in expressions:

Click here to view code image

```
cout << "2km + 30m = " << 2._km + 30.0_m << endl;
cout << "2.5miles + 3.2nm = " << 2.5_miles + 3.2_nm << endl;
```

which yields:

```
2km + 30m = 2.03km
2.5miles + 3.2nm = 9.94976km
```

## Rule

Start all your suffixes with an underscore.

To reduce conflicts between non-standard software packages, we can import suffix operators from other namespaces selectively, e.g.:

```
using tst::operator"" _nm;
```

Here, we only use nautical miles from namespace `tst`.

The value of a user-defined literal must be `long double` (as demonstrated), `long long unsigned`, or some kind of character or character string literal (`char`, `char16_t`, `const char*`, `const char16_t*`, and so on).

## 2.4 Destructors

A destructor is a function that is called whenever an object is destroyed, for example:

Click here to view code image

```
~complex()
{
    std::cout << "So long and thanks for all the fish.\n";
}
```

Since the destructor is the complementary operation of the constructor, it uses the notation for the complement (~). As opposed to the constructor, there is only one single overload and arguments are not allowed.

### 2.4.1 Implementation Rules

There are two very important rules:

- 1. Never throw an exception out of a destructor! If an exception is thrown in a destructor or in a called function, it must be caught within the destructor. Otherwise our program will probably crash. In C++11 and higher, exceptions from destructors are always treated as a runtime error which aborts the execution (destructors are implicitly declared noexcept, §1.6.2.6). In C++03, the behavior is undefined, but a program abortion is the most likely consequence.

- 2. If a class contains a virtual function, the destructor should be virtual, too. We come back to this in Section 6.1.3.

### 2.4.2 Dealing with Resources Properly

What we do in a destructor is our free choice; we have no limitations from the language. Practically, the main task of a destructor is releasing the resources of an object (memory, file handles, sockets, locks, ...) and cleaning up everything related to the object that is not needed any longer in the program. Because a destructor must not throw exceptions, many programmers are convinced that releasing resources should be the only activity of a destructor.

![](img/5682e787fc967e93d7e33e8bac5f58a0_184_0.png)

In our example, there is nothing to do when a complex number is destroyed and we can omit the destructor. A destructor is needed when the object acquires resources like memory. In such cases, the memory or the other resource must be released in the destructor:

```
class vector
{
public:
  // ...
  ~vector ()
  {
    delete[] data;
  }
  // ...
private:
  unsigned my_size;
  double *data;
};
```

Note that delete already tests whether a pointer is nullptr (0 in C++03). Similarly, files that are opened with old C handles require explicit closing (and this is only one reason for not using them). The unique_ptr-based vector does not need a destructor implementation because the compiler generates one that releases the memory.

### 2.4.2.1 Resource Acquisition Is Initialization

Resource Acquisition Is Initialization (RAII) is a paradigm mainly developed by Bjarne Stroustrup and Andrew Koenig. The idea is tying resources to objects and using the mechanism of object construction and destruction to handle resources automatically in programs. Each time we want to acquire a resource, we do so by creating an object that owns it. Whenever the object goes out of scope, the resource (memory, file, socket, ...) is released automatically, as in our `vector` example above.

Imagine a program that allocates 37,186 memory blocks in 986 program locations. Can we be sure that all the memory blocks are freed? And how much time will we spend to get to this certainty or at least to an acceptable level of confidence? Even with tools like `valgrind` (§B.3), we can only test the absence of memory leaks for a single run but cannot guarantee in general that memory is always released. On the other hand, when all memory blocks are allocated in constructors and freed in destructors, we can be sure that no leaks exist.

### 2.4.2.2 Exceptions

Releasing all resources is even more challenging when exceptions are thrown. Whenever we detect a problem, we have to release all resources acquired so far before we throw the exception. Unfortunately, this is not limited to resources in the current scope but extends to those of surrounding scopes depending on where the exception is caught. This means that changing the error handling needs tedious adaption of the manual resource management. The good news is that this only applies to manually handled resources; resources that are bound to local objects via RAII are automatically released in the respective destructors when we leave a scope with an exception (actually anytime we leave a scope).

### 2.4.2.3 Managed Resources

All the problems mentioned before can be solved by introducing classes that manage the resources. C++ already offers such managers in the standard library. File streams manage the file handles from C. `unique_ptr` and `shared_ptr` handle memory in a leak-free, exception-safe manner.14 Also in our `vector` example, we can benefit from `unique_ptr` by not needing to implement a destructor.

14. Only cyclic references need special treatment.

### 2.4.2.4 Managing Ourselves

The smart pointers show that there can be different treatments of a resource type. However, when none of the existing classes handles a resource in the fashion we want, it is a great occasion to entertain ourselves writing a resource manager tailored to our needs.

When we do so, we should not manage more than one resource in a class. The motivation for this guideline is that exceptions can be thrown in constructors, and it is quite tedious to write the constructor in a way that guarantees that all resources acquired so far are released.

Thus, whenever we write a class that deals with two resources (even of the same type) we should introduce a class that manages one of the resources. Better yet, we should write managers for both resources and separate the resource handling entirely from the scientific content. Even in the case that an exception is thrown in the middle of the constructor, we have no problem with leaking resources since the destructors of their managers are called automatically and will take care of it.

The term “RAII” puts linguistically more weight on the initialization. However, the finalization is even more important technically. It is not mandatory that a resource is acquired in a constructor. This can happen later in the lifetime of an object. Fundamental is that one single object is responsible for the resource and releases it at the end of its lifetime. Therefore, Jon Kalb called RAII an application of the Single Responsibility Principle (SRP).

### C++11 2.4.2.5 Resource Rescue

In this section, we introduce a technique for releasing resources automatically even when we use a software package with manual resource handling. We will demonstrate the technique with the Oracle C++ Call Interface (OCCI) [51] for accessing an Oracle database from a program.
