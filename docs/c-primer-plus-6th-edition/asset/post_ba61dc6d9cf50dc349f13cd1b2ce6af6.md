
# Random Access Iterators

Some algorithms, such as standard sort and binary search, require the ability to jump directly to an arbitrary element of a container. This is termed random access, and it requires a random access iterator. This type of iterator has all the features of a bidirectional iterator, plus adds operations (such as pointer addition) that support random access and relational operators for ordering the elements. Table 16.3 lists the operations a random access iterator has beyond those of a bidirectional iterator. In this table, x represents a random iterator type, τ represents the type pointed to, a and b are iterator values, n is an integer, and r is a random iterator variable or reference.

# Table 16.3 Random Access Iterator Operations

| Expression | Description |
| --- | --- |
| a + n | Points to the nth element after the one points to |
| n + a | Same as a + n |
| a - n | Points to the nth element before the one points to |
| r += n | Equivalent to r = r + n |
| r -= n | Equivalent to r = r - n |
| a [n] | Equivalent to *(a + n) |
| b - a | The value of n such that b == a + n |
| a < b | True if a > 0 |
| a > b | True if b < a |
| a >= b | True if (a < b) |
| a <= b | True if (a > b) |

Expressions such as a + n are valid only if both a and a + n lie within the range of the container (including past-the-end).

# Iterator Hierarchy

You probably noticed that the iterator kind form a hierarchy. A forward iterator has all the capabilities of an input iterator and of an output iterator, plus its own capabilities. A bidirectional iterator has all the capabilities of a forward iterator, plus its own capabilities. And a random access iterator has all the capabilities of a forward iterator, plus its own capabilities. Table 16.4 summarizes the main iterator capabilities. In it, i is an iterator, and n is an integer.

# Table 16.4 Iterator Capabilities

| Iterator Capability | Input | Output | Forward | Bidirectional | Random Access |
| --- | --- | --- | --- | --- | --- |
| Dereferencing read | Yes | No | Yes | Yes | Yes |
| Dereferencing write | No | Yes | Yes | Yes | Yes |
| Fixed and repeatable order | | | | | |
| ++i++ | Yes | Yes | Yes | Yes | Yes |
| --i-- | No | No | No | No | Yes |
| i[n] | No | No | No | No | Yes |
| i + n | No | No | No | No | Yes |
| i - | No | No | No | No | Yes |
| i += n | No | No | No | No | Yes |
| i -= n | No | No | No | No | Yes |

An algorithm written in terms of a particular kind of iterator can use that kind of iterator or any other iterator that has the required capabilities. For a container, say a random access iterator can use an algorithm written for an input iterator.

Why all these different kinds of iterators? The idea is to write an algorithm using the iterator with the fewest requirements possible, allowing it to be used with the largest range of containers. The find() function, using a lowly input iterator, can be used with any container that contains readable values. The sort() function, however, requiring a random access iterator, can be used with just containers that support that kind of iterator.

Note that the iterator kinds are not defined types; rather, they are conceptual characterizations. As mentioned earlier, each container class defines a class scope typedef vector<int>::iterator which has classes of iterators. But the documentation for this class would tell you that vector iterators are random access iterators. In turn, that allows you to use algorithms based on any iterator type because a list<int> class has iterators of list<int>::iterator. The STL implements a doubly linked list, so it uses a bidirectional iterator. Thus, it can't use algorithms based on random access iterators, but it can use algorithms based on demanding iterators.

# Concepts, Refinements, and Models

The STL has several features, such as kinds of iterators, that are not expressible in the C++ language. Although you can design, say, a class that has the properties of a forward iterator, you can't compiler restrict an algorithm to using only that class. The reason is that the forward iterator is a set of requirements, not a type. The requirements could be satisfied by an iterator class you've designed, but they could also be satisfied by an ordinary pointer. An STL algorithm works with any iterator implementation that meets its requirements. STL uses the word concept to describe a set of requirements. Thus, there is an input iterator concept, a forward iterator concept, and so on. By the way, if you need iterators for, say, a container class you're designing, you can look to the STL, which include iterator templates for the standard varieties.

Concepts can have an inheritance-like relationship. For example, a bidirectional iterator inherits the capabilities of a forward iterator. However, you cannot apply the C++ inheritance mechanism to iterators. For example, you might implement a forward iterator as a class and a bidirectional iterator as a regular pointer. In terms of the C++ language, this particular bidirectional iterator, being a built-in type, cannot be derived from a class. Conceptually, it does not inherit. Some STL use the term refinement to indicate this conceptual inheritance. Thus, a bidirectional iterator is a refinement of the forward iterator concept.

A particular implementation of a concept is termed a model. Thus, an ordinary pointer-to-int is a model of the random access iterator. It's also a model of a forward iterator, for it satisfies all the requirements of that concept.

# The Pointer As Iterator

Iterators are generalizations of pointers, and a pointer satisfies all the iterator requirements. Iterators form the interface for STL algorithms, and pointers are iterators, so STL algorithms can use pointers to operate on non-STL containers that are based on pointers. For example, you can use STL algorithms with arrays. Suppose Receipts is an array of double values, and you like to sort in ascending order:

```
const int SIZE = 100;
double Receipts[SIZE];
```

The STL sort () function, recall, takes as arguments an iterator pointing to the first element in a container and an iterator pointing to past-end. Well, &Receipts[0] (or just Receipts) is the address of the first element, and &Receipts[SIZE] (or just Receipts + SIZE) is the address of the last element.
