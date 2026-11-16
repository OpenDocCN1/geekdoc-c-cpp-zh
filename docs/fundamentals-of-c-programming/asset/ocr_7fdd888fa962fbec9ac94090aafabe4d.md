```
lst1 = lst2; // Syntactic sugar for lst1.operator=(lst2);
```

the this pointer points to lst1 (and lst2 is the parameter named other). The method must return an object reference, not a pointer to the object, so we must dereference it as *this. This is the typical C++ idiom when defining operator= for programmer-defined types.

We could instead define the operator= method to return nothing (that is, declare its return type to be void). Instead we could define the method to return some type of object other than IntList4. If we do so, however, our IntList4 objects will not behave properly with chained assignment (see Section 4.3). To illustrate, suppose lst1, lst2, and lst3 are all properly declared IntList4 objects. If we define the IntList4::operator= method to return void, the following statement:

```
lst1 = lst2;
```

is perfectly acceptable and behaves as intended, but the compiler will not accept the following statement:

```
lst1 = lst2 = lst3;
```

This is because the assignment operator associates right-to-left; the compiler interprets the chained assignment statement above as if we had parentheses placed as shown in the following statement:

```
lst1 = (lst2 = lst3);
```

If our assignment operator returns void, this statement produces a compile-time error because the subexpression (lst2 = lst3) would evaluate to void, and void is a degenerate type that we cannot assign to lst1.

If we use the original definition above of the IntList4::operator= method that returns a reference to the IntList4 object on the left side of the assignment operator (*this), the compiler does not complain, and the chained assignment works flawlessly in the same manner as chained assignment involving the built-in numeric types; that is, after executing the chained assignment statement above, lst1 and lst2 each will contain exact copies of the elements in lst3.

Listing 18.15 (intlist4.cpp) provides the complete implementation of our IntList4 class.

```
Listing 18.15: intlist4.cpp
// intlist4.cpp
#include "intlist4.h"
#include <iostream>
#include <utility> // For std::swap
// Private IntList4 operations
// Node constructor
IntList4::Node::Node(int n): data(n), next(nullptr) {
std::cout << "Creating node " << data
<< " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}
IntList4::Node::~Node() {
std::cout << "Destroying node " << data
<< " (" << reinterpret_cast<uintptr_t>(this) << ")\n";
}
```