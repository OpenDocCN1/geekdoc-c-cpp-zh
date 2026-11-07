# # The Standard Template Library Methods and Functions

The Standard Template Library (STL) aims to provide efficient implementations of common algorithms. It expresses these algorithms in general functions that can be used with any container that satisfies the requirements for the particular algorithm and in methods that can be used with instantiations of particular container classes. This appendix assumes that you have some familiarity with the STL, such as might be gained from reading Chapter 16, “The string Class and the Standard Template Library.” For example, this chapter assumes that you know about iterators and constructors.

# ## The STL and C++11

Just as the changes brought by C++11 to the C++ language are too extensive to cover completely in this book, so are the changes to the STL too extensive to cover completely in this appendix. However, we can summarize many of the additions.

C++11 brings several new elements to the STL. First, it adds several new containers. Second, it adds a few new features to the old containers. Third, it adds a few new template functions to its family of algorithms. All these changes are incorporated into this appendix, but you may find an overview of the first two categories helpful.

# ### New Containers

C++11 adds the following containers: `array`, `forward_list`, `unordered_set`, and the unordered associative containers `unordered_multiset`, `unordered_map`, and `unordered_multimap`.

An `array` container, once declared, is fixed in size and uses static or stack memory rather than dynamically allocated memory. It’s intended as a substitute for the built-in array type; it’s more limited than `vector`, but more efficient.

The `list` container is a bidirectional linked list, with each item, other than the two ends, linked to the item before it and the one after. The `forward_list` is a singly linked