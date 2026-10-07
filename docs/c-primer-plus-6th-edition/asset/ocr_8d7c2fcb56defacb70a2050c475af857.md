```
// below, rx refers to a temporary variable initialized to 21
int k = twice(21);
```

So in the Ueless case, the formal parameter f will be initialized to a temporary object's initialized to the return value of operator+(). Here is an excerpt from the result of using an old compiler compiler with Listing 18.2 and omitting the move constructor:

```
Entering operator+
int constructor called; number of objects: 4
Number of elements: 30 Data address: 01C337C4
temp object:
Leaving operator+()
copy const called; number of objects: 5
Number of elements: 30 Data address: 01C337E8
destructor called; objects left: 4
deleted object:
Number of elements: 30 Data address: 01C337C4
copy const called; number of objects: 5
Number of elements: 30 Data address: 01C337C4
destructor called; objects left: 4
deleted object:
Number of elements: 30 Data address: 01C337E8
```

First, within the Ueless::operator() method, a constructor creates temp, allocating storage for 30 elements at location 01C337C4. Then the copy constructor creates a temporary copy to f will refer, copying the information to location 01C337E8. Next, temp, which uses location 01C337C4, gets deleted. A new object, for is constructed, reusing the free memory at 01C337C4. Then the temporary object, which used location 01C337E8, gets deleted. So three complete objects are constructed, and two of them were destroyed. This is the sort of extra might semantics are meant to eliminate.

As the g++ example shows, an optimizing compiler might eliminate extra copying on its own, but using an rvalue reference lets the programmer dictate move semantics for appropriate.

# Assignment

The same considerations that make move semantics appropriate for constructors make them appropriate for assignment. Here, for example, how you could code the copy assignment and move assignment operators for the Ueless class:

```
Ueless & Ueless::operator=(const Ueless & f) // copy assignment
{
  if (this == &f)
```