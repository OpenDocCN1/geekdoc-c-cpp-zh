A singly-linked list (§31.4.2)
A double-ended queue (§31.2)
A set (§31.4.3)
A set in which a value can occur many times (§31.4.3) An associative array (§31.4.3)
A map in which a key can occur many times (§31.4.3) A map using a hashed lookup (§31.4.3.2)
A multimap using a hashed lookup (§31.4.3.2) A set using a hashed lookup (§31.4.3.2)
A multiset using a hashed lookup (§31.4.3.2)

The unordered containers are optimized for lookup with a key (often a string); in other words, they are implemented using hash tables.

The standard containers are described in §31.4. The containers are defined in namespace std and presented in headers <vector>, <list>, <map>, etc. (§4.1.2, §30.2). In addition, the standard library provides container adaptors queue<T> (§31.5.2), stack<T> (§31.5.1), deque<T> (§31.4), and priority_queue<T> (§31.5.3). The standard library also provides more specialized container-like types, such as a fixed-size array array<T,N> (§34.2.1) and bitset<N> (§34.2.2).

The standard containers and their basic operations are designed to be similar from a notational point of view. Furthermore, the meanings of the operations are equivalent for the various containers. Basic operations apply to every kind of container for which they make sense and can be efficiently implemented. For example:

+   - begin() and end() give iterators to the first and one-beyond-the-last elements, respectively.
+   - push_back() can be used (efficiently) to add elements to the end of a vector, forward_list, list, and other containers.
+   - size() returns the number of elements.

This notational and semantic uniformity enables programmers to provide new container types that can be used in a very similar manner to the standard ones. The range-checked vector, Vector (§2.3.2, §2.4.3.1), is an example of that. The uniformity of container interfaces also allows us to specify algorithms independently of individual container types. However, each has strengths and weaknesses. For example, subscripting and traversing a vector is cheap and easy. On the other hand, vector elements are moved when we insert or remove elements; list has exactly the opposite properties. Please note that a vector is usually more efficient than a list for short sequences of small elements (even for insert() and erase()). I recommend the standard-library vector as the default type for sequences of elements: you need a reason to choose another.

# 4.5 Algorithms

A data structure, such as a list or a vector, is not very useful on its own. To use one, we need operations for basic access such as adding and removing elements (as is provided for list and vector). Furthermore, we rarely just store objects in a container. We sort them, print them, extract subsets, remove elements, search for objects, etc. Consequently, the standard library provides the most common algorithms for containers in addition to providing the most common container types. For example, the following sorts a vector