
## Dealing with Move Assignments of Objects to Themselves

You might wonder whether you should check for assignments of an object to itself when implementing the move assignment operator. For example, a self move might happen as follows:

```
Customer c{"GNU's Not Unix"};
 c = std::move(c);                     // move assigns c to itself
```

This looks easy to avoid but we might use references and pointers, and in that case, it is not necessarily that obvious that two objects are the same. Consider the following code as a still quite simple example:

```
std::vector<Customer> coll;
 coll.emplace_back("GNU's Not Unix");   // coll has 1 element
 coll[0] = std::move(coll.back());       // move assigns the only element to itself
```

As written, all types in the C++ standard library receive a valid but unspecified state when objects are moved to themselves. This means that by default, you might lose the values of your members and you might even have a more severe problem if your type does not work properly with members that have arbitrary values. In fact, the resulting state might be a problem in the following situations:

- Some values of a moved-from member are a problem
- The values of members depend on each other

The traditional/naive way to protect against self-assignments is to check whether both operands are identical (have the same address). You can also do this when implementing the move assignment operator:

```
Customer& operator= (Customer&& cust) {  // noexcept declaration missing
    std::cout << "MOVEASSIGN " << cust.name << '\n';
    if (this != &cust) {                  // move assignment to myself?
        name = std::move(cust.name);
        values = std::move(cust.values);
    }
    return *this;
}
```

Having a check like this is pretty cheap and would have the benefit that the object keeps its value on a self-move-assignment. However, note that in recursive data structures, it can also be a problem if you (move) assign a child object to a parent object. If we delete the old value of the parent (which owns the child) first before we assign the new value, you might then assign a deleted object. In this case, the objects are not identical, which means that comparing their addresses does not help.

In addition, consider the following from style guides:

- In his book Effective C++ Scott Meyers says that self-assignments are usually not a problem when resource management is encapsulated properly by helper classes (but we did not have move semantics at that time). Furthermore, he points out that otherwise, you also have to ensure that the operator is exception-safe.
- The C++ Core Guidelines categorize this problem as a “one-in-a-million problem” that does not appear to be relevant in practice.²

It seems that in most cases, you can ignore self-move-assignments, which usually means that in your types, you give the same guarantee as the C++ standard library: after move assigning an object to itself, the object is in a valid but unspecified state.

2 See http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-move-self.

## 3.2.5 Using the Special Copy/Move Member Functions

Let us test the class Customer with a small program:

basics/customerimpl.cpp

```
#include "customerimpl.hpp"
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

int main()
{
    std::vector<Customer> coll;
    for (int i=0; i<12; ++i) {
        coll.push_back(Customer{"TestCustomer " + std::to_string(i-5)});
    }

    std::cout << "--- sort():\n";
    std::sort(coll.begin(), coll.end(),
              [] (const Customer& c1, const Customer& c2) {
                  return c1.getName() < c2.getName();
              });
}
```

### Initialization

The first part is the initialization of the vector with 12 customers:

```
std::vector<Customer> coll;
for (int i=0; i<12; ++i) {
    coll.push_back(Customer{"TestCustomer " + std::to_string(i-5)});
}
```

This initialization might have the following output:

```
MOVE TestCustomer -5
MOVE TestCustomer -4
COPY TestCustomer -5
MOVE TestCustomer -3
COPY TestCustomer -5
COPY TestCustomer -4
MOVE TestCustomer -2
MOVE TestCustomer -1
COPY TestCustomer -5
COPY TestCustomer -4
COPY TestCustomer -3
COPY TestCustomer -2
MOVE TestCustomer 0
MOVE TestCustomer 1
MOVE TestCustomer 2
MOVE TestCustomer 3
COPY TestCustomer -5
COPY TestCustomer -4
COPY TestCustomer -3
COPY TestCustomer -2
COPY TestCustomer -1
COPY TestCustomer 0
COPY TestCustomer 1
COPY TestCustomer 2
MOVE TestCustomer 4
MOVE TestCustomer 5
MOVE TestCustomer 6
```

Each time we insert a new object, a temporary object is created and moved into the vector. Therefore, for each element, we have a MOVE.

In addition, we have several copies marked with COPY. These copies are caused by the fact that from time to time, a vector reallocates its internal memory (capacity) so that it is big enough for all elements. In this case, the vector grows from having memory for 1 to having memory for 2, 4, 8, and finally 16 elements. Therefore, we have to copy first 1, then 2, then 4, and then 8 elements already in the vector. Calling coll.reserve(20) before the loop would avoid these copies. However, you might wonder why no move is used here. This has to do with the missing noexcept declarations, which we will discuss in the chapter about move semantics and noexcept.

Note that the exact policy of a vector to grow its capacity is implementation-specific. Thus, the output might differ when implementations grow differently (such as growing by 50% each time).

### Sorting

Next, we sort all elements by name:

```
std::sort(coll.begin(), coll.end(),
    [] (const Customer& c1, const Customer& c2) {
        return c1.getName() < c2.getName();
    });
```

This sorting might have the following output:

```
MOVE TestCustomer -4
MOVEASSIGN TestCustomer -5
MOVEASSIGN TestCustomer -4
MOVE TestCustomer -3
MOVEASSIGN TestCustomer -5
MOVEASSIGN TestCustomer -4
MOVEASSIGN TestCustomer -3
MOVE TestCustomer -2
MOVEASSIGN TestCustomer -5
MOVEASSIGN TestCustomer -4
MOVEASSIGN TestCustomer -3
MOVEASSIGN TestCustomer -2
MOVE TestCustomer -1
MOVEASSIGN TestCustomer -5
MOVEASSIGN TestCustomer -4
MOVEASSIGN TestCustomer -3
MOVEASSIGN TestCustomer -2
MOVEASSIGN TestCustomer -1
MOVE TestCustomer 0
MOVEASSIGN TestCustomer 0
MOVE TestCustomer 1
MOVEASSIGN TestCustomer 1
MOVE TestCustomer 2
MOVEASSIGN TestCustomer 2
MOVE TestCustomer 3
MOVEASSIGN TestCustomer 3
MOVE TestCustomer 4
MOVEASSIGN TestCustomer 4
MOVE TestCustomer 5
MOVEASSIGN TestCustomer 5
MOVE TestCustomer 6
MOVEASSIGN TestCustomer 6
```

As you can see, the whole sorting is only moving around elements; sometimes to create a new temporary object (MOVE), sometimes to assign a value to a different location (MOVEASSIGN).

Again, the output depends on the exact implementation of sort(), which is implementation-specific.

### The Number of Copies We Saved

The output of this program again demonstrates the benefit of move semantics. Before move semantics support, we would only have copies when inserting and sorting elements. However, even in this small program that has a container with 12 elements, move semantics converted 44 expensive element copies into cheap moves. For 10,000 customers we would save more than 150,000 copies. And note that each copy of a Customer means up to 2 memory allocations with the corresponding deallocations later on.

Note again:

- The implementation of std::sort() is implementation-specific, meaning that the number of saved copies might differ slightly.
- The only copies performed are caused by the reallocation of the vector for the memory of the elements. They should also become moves, which will be discussed in the chapter about move semantics and noexcept.

## 3.3 Rules for Special Member Functions

Let us talk about special member functions and in particular, specify exactly when and how the special copy and move member functions are generated.
