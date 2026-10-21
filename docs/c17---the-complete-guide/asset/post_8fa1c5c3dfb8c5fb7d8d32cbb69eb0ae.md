
According to the one definition rule (ODR), a variable or entity has to be defined in exactly one translation unit—unless the variable or entity is declared to be inline.

Even include guards do not help:

```
#ifndef MYHEADER_HPP
#define MYHEADER_HPP

class MyClass {
    static std::string msg;
    ...
};
std::string MyClass::msg{"OK"};    // Link ERROR if included by multiple CPP files

#endif
```

The problem is not that the header file might be included multiple times; the problem is that two different CPP files include the header so that both define MyClass::msg.

For the same reason, you get a link error if you define an object of your class in a header file:

```
class MyClass {
    ...
};
MyClass myGlobalObject;            // Link ERROR if included by multiple CPP files
```

## Workarounds

For some cases, there are workarounds:

- You can initialize static const data members of integral and enumeration types in a class/struct:

```
class MyClass {
    static const bool trace = false;  // OK, literal type
    ...
};
```

However, this is only allowed for literal types, such as fundamental integral, floating-point, or pointer types, or for classes with only constant expressions to initialize non-static data members and no user-defined or virtual destructor. In addition, you still need a definition in one translation unit once you need the location of the member (e.g., by binding it to a reference).

- You can define an inline function that returns a static local variable:

```
inline std::string& getMsg() {
    static std::string msg{"OK"};
    return msg;
}
```

- You can define a static member function that returns the value:

```
class MyClass {
    static std::string& getMsg() {
        static std::string msg{"OK"};
        return msg;
    }
    ...
};
```

- You can use variable templates (since C++14):

```
template<typename T = std::string>
T myGlobalMsg{"OK"};
```

- You can define a class template for the static member(s):

```
template<typename = void>
class MyClassStatics
{
    static std::string msg;
};

template<typename T>
std::string MyClassStatics<T>::msg{"OK"};
```

and then even derive from it:

```
class MyClass : public MyClassStatics<>
{
    ...
};
```

However, all of these approaches lead to significant overhead, less readability, and/or different ways to use the global variable. In addition, the initialization of a global variable might be postponed until its first use, which disables applications in which we want to initialize objects at program start (such as when using an object to monitor the process).

## 3.2 Using Inline Variables

Now, with inline, you can have a single globally available object by defining it only in a header file, which might be included by multiple CPP files:

```
class MyClass {
    inline static std::string msg{"OK"};  // OK since C++17
    ...
};
```

```
inline MyClass myGlobalObj;  // OK even if included/defined by multiple CPP files
```

Formally, the inline used here has the same semantics as a function declared inline:

- It can be defined in multiple translation units, provided all definitions are identical.
- It must be defined in every translation unit in which it is used.

Both are given by including the definition from the same header file. The resulting behavior of the program is as if there were exactly one variable.

## 3.3 constexpr Now Implies inline for Static Members

For static data members, constexpr implies inline now, such that since C++17, the following declaration defines the static data member n:

```
struct D {
    static constexpr int n = 5; // C++11/C++14: declaration
    // since C++17: definition
};
```

That is, it is the same as:

```
struct D {
    inline static constexpr int n = 5;
};
```

Note that before C++17, you could often have the declaration only without a corresponding definition. Consider the following declaration:

```
struct D {
    static constexpr int n = 5;
};
```

This was enough if no definition of D::n was needed, which was the case if D::n was only passed by value:

```
std::cout << D::n; // OK (ostream::operator<<(int) gets D::n by value)
```

If D::n was passed by reference to a non-inlined function and/or the call was not optimized away, this was invalid. For example:

```
int twice(const int& i);
std::cout << twice(D::n);    // was often an ERROR
```

This code violated the one definition rule (ODR). When built with an optimizing compiler, it might have worked as expected or might have given a link error due to the missing definition. When built without any optimizations, it will almost certainly be rejected due to the missing definition of D::n.¹ Creating a pointer to the static member does even more likely result in a link error due to the missing definition (but it might still work with some compiler modes):

```
const int* p = &D::n;          // was usually an ERROR
```

As a consequence, before C++17, you had to define D::n in exactly one translation unit:

```
constexpr int D::n;            // C++11/C++14: definition
                               // since C++17: redundant declaration (deprecated)
```

Now, when built with C++17, the declaration inside the class is a definition by itself, so all examples above are now valid without the former definition. The former definition is still valid but a deprecated redundant declaration.

## 3.4 Inline Variables and thread_local

By using thread_local you can also make an inline variable unique for each thread:

```
struct ThreadData {
    inline static thread_local std::string name;      // unique name per thread
    ...
};

inline thread_local std::vector<std::string> cache;   // one cache per thread
```

As a complete example, consider the following header file:

`lang/inlinethreadlocal.hpp`

```
#include <string>
#include <iostream>

struct MyData {
    inline static std::string gName = "global";          // unique in program
    inline static thread_local std::string tName = "tls"; // unique per thread
    std::string lName = "local";                          // for each object
    ...
    void print(const std::string& msg) const {
        std::cout << msg << '\n';
        std::cout << "- gName: " << gName << '\n';
        std::cout << "- tName: " << tName << '\n';
        std::cout << "- lName: " << lName << '\n';
    }
};

inline thread_local MyData myThreadData;  // one object per thread
```

You can use it in the translation unit that contains main():

`lang/inlinethreadlocal1.cpp`

```
#include "inlinethreadlocal.hpp"
#include <thread>

void foo();

int main()
{
    myThreadData.print("main() begin:");

    myThreadData.gName = "thread1 name";
    myThreadData.tName = "thread1 name";
    myThreadData.lName = "thread1 name";
    myThreadData.print("main() later:");

    std::thread t(foo);
    t.join();
    myThreadData.print("main() end:");
}
```

You can also use the header file in another translation unit that defines foo(), which is called in a different thread:

`lang/inlinethreadlocal2.cpp`

```
#include "inlinethreadlocal.hpp"

void foo()
{
    myThreadData.print("foo() begin:");

    myThreadData.gName = "thread2 name";
    myThreadData.tName = "thread2 name";
    myThreadData.lName = "thread2 name";
    myThreadData.print("foo() end:");
}
```

The program has the following output:

```
main() begin:
```
