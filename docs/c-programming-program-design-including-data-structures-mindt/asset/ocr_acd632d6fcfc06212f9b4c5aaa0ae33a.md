```
Line 31: newWList with partial sum : 1 3 6 10 15 21 28 36
Line 34: newWList with partial multiplication:
              1 2 6 24 120 720 5040 40320
```

The preceding output is self-explanatory. The details are left as an exercise for you.

# QUICK REVIEW

+   1. The three main components of the STL are containers, iterators, and algorithms.
+   2. STL containers are class templates.
+   3. Iterators are used to step through the elements of a container.
+   4. Algorithms are used to manipulate the elements in a container.
+   5. The main categories of containers are sequence containers, associative containers, and container adapters.
+   6. The three predefined sequence containers are vector, deque, and list.
+   7. A vector container stores and manages its objects in a dynamic array.
+   8. Because an array is a random access data structure, elements of a vector can be accessed randomly.
+   9. The name of the class that implements the vector container is vector.
+   10. Item insertion in a vector container is accomplished by using the operations insert and push_back.
+   11. Item deletion in a vector container is accomplished by using the operations pop_back, erase, and clear.
+   12. An iterator to a vector container is declared using the typedef iterator, which is declared as a public member of the class vector.
+   13. Member functions common to all containers are the default constructor, constructors with parameters, the copy constructor, the destructor, empty, size, max_size, swap, begin, end, rbegin, rend, insert, erase, clear, and the relational operator functions.
+   14. The member function begin returns an iterator to the first element into the container.
+   15. The member function end returns an iterator to one past the last element into the container.
+   16. In addition to the member functions listed in item 13, the other member functions common to all sequence containers are insert, push_back, pop_back, erase, clear, and resize.
+   17. The copy algorithm is used to copy the elements in a given range to another place.
+   18. The function copy, using an ostream_iterator, can also be used to output the elements of a container.