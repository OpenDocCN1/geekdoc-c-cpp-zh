Here is the output of the program in Listing 16.11:

```
fine fish fashion fate
fine fish fashion fate busy bats
silly singers fine fish fashion fate busy bats
```

The first copy() copies the four strings from s1 into words. This works in part because words is declared to hold four strings, which equals the number of strings being copied. Then the back_insert_iterator inserts the strings from s2 just in front of the end of the words array, expanding the size of words to six elements. Finally, the insert_iterator inserts the two strings from s3 just in front of the first element of words, expanding the size of words to eight elements. If the program attempted to copy s2 and s3 into words by using words.end() and words.begin() as iterators, there would be no room in words for the new data, and the program would probably abort because of memory violations.

If you're feeling overwhelmed by all the iterator varieties, keep in mind that using them will make them familiar. Also keep in mind that these predefined iterators expand the generality of the STL algorithms. Thus, not only can copy() copy information from one container to another, it can copy information from a container to the output stream and from the input stream to a container. And you can also use copy() to insert material into another container. So you wind up with a single function doing the work of many. And because copy() is just one of several STL functions that use an output iterator, these predefined iterators multiply the capabilities of those functions, too.

# Kinds of Containers

The STL has both container concepts and container types. The concepts are general categories with names such as container, sequence container, and associative container. The container types are templates you can use to create specific container objects. The original 11 container types are deque, list, queue, priority_queue, stack, vector, map, multimap, set, multiset, and bitset. (This chapter doesn't discuss bitset, which is a container for dealing with data at the bit level.) C++11 adds forward_list, unordered_map, unordered_multimap, unordered_set, and unordered_multiset, and it moves bitset from the container category into its own separate category. Because the concepts categorize the types, let's start with them.

# Container Concepts

No type corresponds to the basic container concept, but the concept describes elements common to all the container classes. It's sort of a conceptual abstract base class—conceptual because the container classes don't actually use the inheritance mechanism. Or to put it another way, the container concept lays down a set of requirements that all STL container classes must satisfy.

A container is an object that stores other objects, which are all of a single type. The stored objects may be objects in the OOP sense, or they may be values of built-in types. Data stored in a container is owned by the container. That means when a container