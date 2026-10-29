# Self-Test Exercises

+   17. Show that a running time \(T(N)=aN+b\) is an \(O(N)\) running time. (Hint: The only issue is the plus. Assume \(N\) is always at least 1.)
+   
+   18. Show that for any two bases \(a\) and \(b\) for logarithms, if \(a\) and \(b\) are both greater than 1, then there is a constant \(c\) such that \(\log_a N \le c(\log_b N)\). Thus, there is no need to specify a base in \(O(\log N)\). That is, \(O(\log_a N)\) and \(O(\log_b N)\) mean the same thing.

# NONMODIFYING SEQUENCE ALGORITHMS

This section describes template functions that operate on containers but do not modify the contents of the container in any way. A good simple and typical example is the generic find function.

The generic find function is similar to the find member function of the set template class but is a different function. The generic find function can be used with any of the STL sequence container classes. Display 19.16 shows a sample use of the generic find function used with the class vector<char>. The function in Display 19.16 would behave exactly the same if we replaced vector<char> by list<char> throughout, or if we replaced vector<char> by any other sequence container class. That is one of the reasons why the functions are called generic: One definition of the find function works for a wide selection of containers.

If the find function does not find the element it is looking for, it returns its second iterator argument, which need not be equal to some end() as it is in Display 19.16. Sample Dialogue 2 in that display shows the situation when find does not find what it is looking for.

Does find work with absolutely any container? No, not quite. To start with, it takes iterators as arguments, and some containers, such as stack, do not have iterators. To use the find function, the container must have iterators, the elements must be stored in a linear sequence so that the ++ operator moves iterators through the container, and the elements must be comparable using ==. In other words, the container must have forward iterators (or some stronger kind of iterators, such as bidirectional iterators).

When presenting generic function templates, we will describe the iterator type parameter by using the name of the required kind of iterator as the type parameter name. So, ForwardIterator should be replaced by a type that is a type for some kind of forward iterator, such as the iterator type in a list, vector, or other container template class. Remember, a bidirectional iterator is also a forward iterator, and a random-access iterator is also a bidirectional iterator. Thus, the type name ForwardIterator can be used with any iterator type that is a bidirectional or random-access iterator type as well as a plain-old forward iterator type. In some cases when we specify ForwardIterator, you