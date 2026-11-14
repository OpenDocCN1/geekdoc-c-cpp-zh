+   • full: whether stack is full;
+   • empty: whether stack is empty.

Stack over- or underflow must throw an exception.

# 3.11.4 Iterator of a Vector

Add the methods begin() and end() for returning a begin and end iterator to class vector. Add the types iterator and const_iterator to the class as well. Note that pointers are models of the concept of random-access iterators.
Use the STL function sort for ordering vector entries to demonstrate that your iterators work as they should.

# 3.11.5 Odd Iterator

Write an iterator class for odd numbers named odd_iterator. The class must model (realize) the forward_iterator concept (http://www.sgi.com/tech/stl/ForwardIterator.html). That means it must provide the following members:

+   • Default and copy constructor;
+   • operator++ to the next odd element, as pre-increment and post-increment;
+   • operator* as dereference which returns an (odd) int;
+   • operator== and operator!=; and
+   • operator-.

with the obvious semantics. In addition, the class should contain a constructor that accepts an int value. This value will be returned in the dereference operator (as long as the iterator is not incremented). This constructor should throw an exception if the value is even. Likewise the default constructor should initialize the internal value with 1 to provide a legal state.

# 3.11.6 Odd Range

Write a class for a range of odd numbers. The member or free functions begin and end should return an odd_iterator as defined in Exercise 3.11.5.
The following code should print the odd numbers {7, 9, ..., 25}:

```
for (int i : odd_range(7, 27))
std::cout << i << '\n';
```

# 3.11.7 Stack of bool

Specialize your stack implementation from Exercise 3.11.3 for bool. Use an unsigned char for 8 bool as in Section 3.6.1.