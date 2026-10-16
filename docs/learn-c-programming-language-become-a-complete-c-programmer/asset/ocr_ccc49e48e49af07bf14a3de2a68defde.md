(only) and to optimize the process of reading redundant definitions. This strategy treats template functions the same way as inline functions.

An obvious problem with this strategy is that users may accidentally come to depend on declarations included only for the benefit of the definition of **out()**. This danger can be limited by taking approach [2] “include template definitions later,” by using namespaces, by avoiding macros, and generally by reducing the amount of information included. The ideal is to minimize a template definition’s dependency on its environment.

To use the “include template definitions later” approach for our simple **out()** example, we first split **out.h** into two. The declarations go into a **.h** file:

```
```cpp
// file outdecl.h:
template<typename T> void out(const T& t);
```
```

The definitions go into **out.cpp**:

```
```cpp
// file out.cpp:
#include <iostream>

template<typename T> void out(const T& t) {
  std::cerr << t;
}
```
```

A user now **#include**s both:

```
```cpp
// file user3.cpp:
#include “out.h”
// use out()
#include “out.cpp”
```
```

This minimizes the chances of the implementation of the templates having undesirable effects on the user code. Unfortunately, it also increases the chances that something in the user code (say, a macro) will have an undesirable effect on the template definitions.

As ever, non**inline**, non-template functions and **static** members (§16.2.12) must have a unique definition in some compilation unit. This implies that such members are best not used for templates that are otherwise included in many translation units. As shown with **out()**, the definition of a template function may be replicated in different translation units, so beware of contexts that might subtly change the meaning of a definition:

# Section 23.7 Source Code Organization 697

```
```cpp
// file user1.cpp:
#include “out.h” // use out()
```
```

and

```
```cpp
// file user4.cpp:
#define std MyLib
#include “out.c”
// use out()
```
```

This sneaky and error-prone use of a macro changes the definition of **out** so that **user4.cpp**’s definition differs from **user1.cpp**’s. This is an error, but it is an error that an implementation may not catch. This kind of error can be very hard to detect in large