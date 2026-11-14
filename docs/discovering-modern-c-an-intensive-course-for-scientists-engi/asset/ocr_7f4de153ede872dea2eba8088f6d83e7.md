RandomAccessIterator: a concept for iterators to which an arbitrary positive or negative offset can be added, i.e., types that additionally provide operator[]. It refines BidirectionalIterator.

Algorithm implementations that only use a simple iterator interface (like that of InputIterator) can be applied to more data structures. Also, data structures that provide a richer iterator interface (e.g., modeling RandomAccessIterator) can be used in more algorithms. .

A clever design choice of all iterator interfaces was that their operations are also provided by pointers. Every pointer models RandomAccessIterator so that all STL algorithms can be applied on old-style arrays via pointers.

# 4.1.2.2 Working with Iterators

All standard container templates provide a rich and consistent set of iterator types. The following very simple example shows a typical use of iterators:

```
using namespace std;
std::list<int> l = {3, 5, 9, 7}; // C++11
for (list<int>::iterator it = l.begin(); it != l.end(); ++it) {
    int i = *it;
}
cout << l << endl;
```

In this first example, we limited ourselves to C++03 features (apart from the list initialization) to demonstrate that the work with iterators is nothing new to C++11. In the remainder of the section, we will use more C++11 features but the principle remains the same.

As illustrated in the code snippet, iterators are typically used in pairs, where one handles the actual iteration and the second one marks the end of the container. The iterators are created by the corresponding container class using the standard methods begin() and end(). The iterator returned by begin() points to the first element whereas end() yields an iterator pointing past the end of elements. The end iterator is only used for comparison since the attempt to access the value fails in most cases. All algorithms in STL are implemented with right-open intervals [b,e) operating on the value referred to by b until b = e. Therefore, intervals of the form [x,x) are regarded as empty.

The member functions begin() and end() preserve the constancy of the container:

+   • If the container object is mutable, then the methods return an iterator type referring to mutable container entries.

+   • For constant containers the methods return const_iterator which accesses the container entries by constant references.

Often iterator is implicitly convertible into const_iterator but you should not count on this. Back to modern C++. We first incorporate type deduction for the iterator:

```
std::list<int> l = {3, 5, 9, 7};
for (auto it = begin(l), e = end(l); it != e; ++it) {
    int i = *it;
    std::cout << l << std::endl;
}
```