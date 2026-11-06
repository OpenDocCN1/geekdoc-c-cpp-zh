+   - Iterator operator-(), allowing single steps backward;
+   - Type operator-(Iterator const &rhs) const, returning the number of data elements between the current and rhs iterator (returning a negative value if rhs refers to a data element beyond the data element this iterator refers to);
+   - Iterator operator+(int step) const, returning an iterator referring to a data element step data elements beyond the data element this iterator refers to;
+   - Iterator operator-(int step) const, returning an iterator referring to a data element step data elements before the data element this iterator refers to;
+   - bool operator<(Iterator const &rhs) const, returning true if the data element this iterator refers to is located before the data element the rhs iterator refers to.

Each iterator tag assumes that a certain set of operators is available. The `RandomAccessIterator` is the most complex of iterators, as it implies all other iterators.

Note that iterators are always defined over a certain range (`[begin, end)`). Increment and decrement operations may result in undefined behavior of the iterator if the resulting iterator value would refer to a location outside of this range.

Often, iterators only access the elements of the series to which they refer. Internally, an iterator may use an ordinary pointer but it is hardly ever necessary for the iterator to allocate its own memory. Therefore, as the assignment operator and the copy constructor do not have to allocate any memory, their *default implementations* usually suffice. For the same reason iterators usually don't require destructors.

Most classes offering members returning iterators do so by having members construct the required iterators that are thereupon returned as objects by those member functions. As the *caller* of these member functions only has to *use* or sometimes *copy* the returned iterator objects, there is usually no need to provide any publicly available constructor, except for the copy constructor. Therefore these constructors are usually defined as *private* or *protected* members. To allow an outer class to create iterator objects, the iterator class usually declares the outer class as its *friend*.

In the following sections the construction of a `RandomAccessIterator`, the most complex of all iterators, and the construction of a *reverse* `RandomAccessIterator` is discussed. The container class for which a random access iterator must be developed may actually store its data elements in many different ways (e.g., using containers or pointers to pointers). Therefore it is difficult to construct a template iterator class which is suitable for a large variety of container classes.

In the following sections the available `std::iterator` class is used to construct an inner class representing a random access iterator. The reader may follow the approach illustrated there to construct iterator classes for other contexts. An example of such a template iterator class is provided in section 23.8.

The random access iterator developed in the next sections reaches data elements that are only accessible through pointers. The iterator class is designed as an inner class of a class derived from a vector of string pointers.

# ### 21.13.1 Implementing a 'RandomAccessIterator'

In the chapter about containers (chapter 12) it was noted that containers own the information they contain. If they contain objects, then those objects are destroyed once the containers are destroyed. As pointers are not objects their use in containers is discouraged (STL's `unique_ptr` and `shared_ptr` type objects may be used, though). Although discouraged, we might be able to use pointer data types in specific contexts. In the following class `StringPtr`, an ordinary class is derived from the `std::vector` container that uses `std::string *` as its data type:

```
```
#ifndef INCLUDED_STRINGPTR_H_
#define INCLUDED_STRINGPTR_H_
```
```