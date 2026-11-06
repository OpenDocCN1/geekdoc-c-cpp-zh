+   J. We use `const` versions of the iterators for traversing read-only containers.

+   K. For input iterators and output iterators, it’s common to save the iterator, then use the saved value later.

+   L. Class templates `array`, `vector` and `deque` are based on built-in arrays.

+   M. Attempting to dereference an iterator positioned outside its container is a compilation error. In particular, the iterator returned by `end` should not be dereferenced or incremented.

+   N. Insertions and deletions in the middle of a `deque` are optimized to minimize the number of elements copied, so it’s more efficient than a `vector` but less efficient than a `list` for this kind of modification.

+   O. Container `set` does *not* allow duplicates.

+   P. Class `stack` (from header `<stack>`) enables insertions into and deletions from the underlying data structure at one end (commonly referred to as a last-in, first-out data structure).

+   Q. Function `empty` is available in all containers except the `deque`.

# 2. 15.5 Fill in the blanks in each of the following statements:

+   A. The three styles of container classes are first-class containers, ______ and near containers.

+   B. Containers are divided into four major categories—sequence containers, ordered associative containers,