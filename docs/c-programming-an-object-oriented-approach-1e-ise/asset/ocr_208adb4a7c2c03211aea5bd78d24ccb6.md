```
**Program 13.9**  *File app.cpp (Continued)*

```cpp
#include "smallest.h"
#include <iostream>

int main( )
{
    // Instantiation of an smallest object
    Smallest smallest;
    // Applying the function call operator to objects
    cout << "Smallest so far: " << smallest (5) << endl;
    cout << "Smallest so far: " << smallest (9) << endl;
    cout << "Smallest so far: " << smallest (4) << endl;
    return 0;
}
```

**Run:**

```text
Smallest so far: 5
Smallest so far: 5
Smallest so far: 4
```
```

In Chapter 19 we discuss more about function objects (functor) when we show how C++ uses them in the Standard Template Library (STL).

An interesting point about a function object is that C++ does not limit the number of arguments in a function call. This means that we can overload this operator with more than one argument. One application is to use it to get an element in a class defining a two-dimensional array (or even an array with more dimensions). The first argument can define the index of the first dimension (row), and the second argument can define the index of the second dimensional (column).

# 13.4 OVERLOADING AS A NONMEMBER

When we overload a binary operator as a member function, one of the operands needs to be the host object. This is fine when each operand has a different role in the operation. However, in some operators, such as (a + b) or (a < b), the two operands play the same role and neither of them is related to the result. In these cases, it is better to use a nonmember function. We have two choices: global functions or friend functions.

There is nothing to prevent us from using a global function for overloading binary operators. Although there are many advocates for this strategy, there is one drawback. The definition of the operator function is longer and more complicated because it needs to use the accessor and mutator functions of the class to access data members of the class. We do not develop these types of functions.

C++ allows functions to be declared as friend functions of the class. A **friend function** has no host object, but it is granted friendship so that it can access the private data members and member functions of the class without calling the public member functions. We use friend functions to overload selected operators.