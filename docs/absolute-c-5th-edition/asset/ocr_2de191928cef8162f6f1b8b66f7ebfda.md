# Answers to Self-Test Exercises

+   * Container classes with iterators have member functions end() and begin() that return iterator values that you can process all the data in the container as follows:

```
for (p = c.begin( ); p != c.end( ); p++)
    process // *p is the current data item.
```

+   * The main kinds of iterators are: ++ works on the iterator.
  Forward iterators:
  Birectional iterators: -- and work on the iterator.
  Random-access iterators: ++, -- and random access all with the iterator.

+   * With a constant iterator, the dereferencing operator * produces a read-only version of the element. With a mutable iterator p, *p can be assigned a value.

+   * A bidirectional container has reverse iterators that allow your code to cycle through the elements in the container in reverse order.

+   * The main container template classes in the STL are list, which has mutable bidirectional iterators; and the template classes vector and deque, both of which have mutable random-access iterators.

+   * stack and queue are adapter classes, which are built on top of other container classes. A stack is a last-in/first-out container. A queue is a first-in/first-out container.

+   * The set, map, and multimap template classes store their elements in sorted order for efficiency of search algorithms. A set is a collection of elements. A map allows storing and retrieving by key values. The multiset class allows repetitions of entries. The multimap class allows a single key to be associated with multiple data items.

+   * The STL includes template functions to implement generic algorithms with guarantees on their running time.

# Answers to Self-Test Exercises

+   1. v.begin() returns an iterator located at the first element of v.end() returns a value that serves as a sentinel value at the end of all the elements of v.

+   2. *p is the dereferencing operator applied to p. *p is a reference to the element at location p.

+   3. using std::vector<int>;iterator;

```
iterator p;
for (p = v.begin( ); p != v.end( ); p++)
    cout << *p << " ";
```

+   4. D C C

+   5. B C

+   6. Either would work.