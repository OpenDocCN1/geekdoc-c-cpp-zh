```
```
Found value 15
Did not find value 20

After insert, intMultiset contains:
1 7 9 13 15 15 18 22 22 30 85 100

Lower bound of 22: 22
Upper bound of 22: 30

equal_range of 22:
  Lower bound: 22
  Upper bound: 30
```
```

**Fig. 22.19** | Standard Library multiset class template. (Part 3 of 3.)

Line 10 uses a typedef to create a new type name (alias) for a multiset of integers ordered in ascending order, using the function object less< int >. Ascending order is the default for a multiset, so less< int > can be omitted in line 10. This new type (Ins) is then used to instantiate an integer multiset object, intMultiset (line 16).

> **Good Programming Practice 22.1**
> 
> *Use typedefs to make code with long type names (such as multisets) easier to read.*

The output statement in line 19 uses function count (available to all associative containers) to count the number of occurrences of the value 15 currently in the multiset.

Lines 22–23 use one of the three versions of function insert to add the value 15 to the multiset twice. A second version of insert takes an iterator and a value as arguments and begins the search for the insertion point from the iterator position specified. A third version of insert takes two iterators as arguments that specify a range of values to add to the multiset from another container.

Line 31 uses function find (available to all associative containers) to locate the value 15 in the multiset. Function find returns an iterator or a const_iterator pointing to the earliest location at which the value is found. If the value is not found, find returns an iterator or a const_iterator equal to the value returned by a call to end. Line 40 demonstrates this case.

Line 43 uses function insert to insert the elements of array a into the multiset. In line 45, the copy algorithm copies the elements of the multiset to the standard output in ascending order.

Lines 49 and 50 use functions lower_bound and upper_bound (available in all associative containers) to locate the earliest occurrence of the value 22 in the multiset and the element after the last occurrence of the value 22 in the multiset. Both functions return iterators or const_iterators pointing to the appropriate location or the iterator returned by end if the value is not in the multiset.

Line 53 instantiates an instance of class pair called p. Objects of class pair are used to associate pairs of values. In this example, the contents of a pair are two const_iterators for our integer-based multiset. The purpose of p is to store the return value of multiset function equal_range that returns a pair containing the results of both a lower_bound and an upper_bound operation. Type pair contains two public data members called first and second.