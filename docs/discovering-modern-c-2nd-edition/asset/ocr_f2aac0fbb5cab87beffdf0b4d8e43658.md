![](bbox=[0.23, 0.08, 0.73, 0.33])

# Figure 4-1: Interoperability between STL containers and algorithms

To program m algorithms on n data structures, one needs in classical C and Fortran programming:

m · n implementations.

With iterators we first have to provide the interface for all containers, but then each algorithm only requires one implementation, which reduces the total programming effort to:

m + n implementations!

# 4.1.2.1 Categories

Not all algorithms can be used with every data structure. Which algorithm works on a given data structure (e.g., linear find or binary search) depends on the kind of iterator provided by the container. Iterators can be distinguished by the form of access:

+   InputIterator: an iterator concept for reading the referred entries (only once).

+   OutputIterator: an iterator concept for writing to the referred entries (only once).