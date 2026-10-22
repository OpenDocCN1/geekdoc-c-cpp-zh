+   • Class types with an overloaded operator() (sometimes called functors), including lambdas • Class types with a conversion function yielding a pointer-to-function or reference-to-function Collectively, these types are called function object types, and a value of such a type is a function object. 157

The C++ standard library introduces the slightly broader notion of a callable type, which is either a function object type or a pointer to member. An object of callable type is a callable object, which we refer to as a callable for convenience.

Generic code often benefits from being able to accept any kind of callable, and templates make it possible to do so.

# 11.1.1 Supporting Function Objects

Let’s look how the for_each() algorithm of the standard library is implemented (using our own name “foreach” to avoid name conflicts and for simplicity skipping returning anything): Click here to view code image

basics/foreach.hpp

```
template<typename Iter, typename Callable>
void foreach (Iter current, Iter end, Callable op)
{
while (current != end) { //as long as not reached the end
op(*current); // call passed operator for current element
++current; // and move iterator to next element
}
}
```

The following program demonstrates the use of this template with various function objects: Click here to view code image

basics/foreach.cpp

```
#include <iostream>
#include <vector>
#include "foreach.hpp"

// a function to call:
void func(int i)
{ std::cout << "func() called for: " << i << '\n';
}

// a function object type (for objects that can be used as functions):
```