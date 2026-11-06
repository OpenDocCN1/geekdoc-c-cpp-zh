When iterators are to be used in the context of generic algorithms they must meet additional requirements. This is caused by the fact that generic algorithms perform checks on the types of the iterators they receive. Simple pointers are usually accepted, but if an iterator-object is used it must be able to specify the kind of iterator it represents.

When deriving a class from the class iterator the type of iterator is defined by the class template's *first* parameter, and the data type to which the iterator refers is defined by the class template's *second* parameter.

The type of iterator that is implemented by the derived class is specified using a so-called *iterator_tag*, provided as the first template argument of the class iterator. For the five basic iterator types, these tags are:

+   - std::input_iterator_tag. This tag defines an InputIterator. Iterators of this type allow reading operations, iterating from the first to the last element of the series to which the iterator refers.
+   
+       The InputIterator dereference operator should be declared as follows:
+   
+           Type const &operator*() const;
+   
+       Except for the standard operators there are no further requirements for InputIterators.
+   
+   - std::output_iterator_tag. This tag defines an OutputIterator. Iterators of this type allow for assignment operations, iterating from the first to the last element of the series to which the iterator refers.
+   
+       The OutputIterator dereference operator should allow assignment to the data its dereference operator refers to. Therefore, the OutputIterator dereference operator should be declared as follows:
+   
+           Type &operator*();
+   
+       Except for the standard operators there are no further requirements for OutputIterators.
+   
+   - std::forward_iterator_tag. This tag defines a ForwardIterator. Iterators of this type allow reading *and* assignment operations, iterating from the first to the last element of the series to which the iterator refers.
+   
+       The ForwardIterator dereference operator should allow assignment to the data its dereference operator refers to. Therefore, the ForwardIterator dereference operator should be declared as follows:
+   
+           Type &operator*();
+   
+       Except for the standard operators there are no further requirements for ForwardIterators.
+   
+   - std::bidirectional_iterator_tag. This tag defines a BidirectionalIterator. Iterators of this type allow reading *and* assignment operations, iterating step by step, possibly in alternating directions, over all elements of the series to which the iterator refers.
+   
+       The ForwardIterator dereference operator should allow assignment to the data its dereference operator refers to and it should allow stepping backward. ForwardIterator should therefore, in addition to the standard operators required for iterators, offer the following operators:
+   
+           Type &operator*();
+           Iterator &operator--();
+   
+   - std::random_access_iterator_tag. This tag defines a RandomAccessIterator. Iterators of this type allow reading *and* assignment operations, iterating, possibly in alternating directions, over all elements of the series to which the iterator refers using any available (random) stepsize. RandomIterator class dereference operators should allow assignment to the data they refer to, and, in addition to the standard operators required for iterators, offer the following operators:
+   
+           – Type &operator*(), allowing assignment to the data the dereference operator refers to;