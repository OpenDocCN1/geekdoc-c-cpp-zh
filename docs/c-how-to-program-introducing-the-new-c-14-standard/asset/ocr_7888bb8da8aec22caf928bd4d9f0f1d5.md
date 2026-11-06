values. The contents of `p` will be two `const_iterator`s for our `multiset` of `int`s. The `multiset` function `equal_range` returns a `pair` containing the results of calling both `lower_bound` and `upper_bound`. Type `pair` contains two `public` data members called `first` and `second`. Line 49 uses function `equal_range` to determine the `lower_bound` and `upper_bound` of 22 in the `multiset`. Line 52 uses `p.first` and `p.second` to access the `lower_bound` and `upper_bound`. We *dereferenced* the iterators to output the values at the locations returned from `equal_range`. Though we did not do so here, you should always ensure that the iterators returned by `lower_bound`, `upper_bound` and `equal_range` are not equal to the container’s *end* iterator *before* dereferencing the iterators.

# *C++11: Variadic Class Template* `tuple`

C++ also includes class template `tuple`, which is similar to `pair`, but can hold any number of items of various types. As of C++11, class template `tuple` is implemented using *variadic templates*—templates that can receive a *variable* number of arguments. We discuss `tuple` and variadic templates in Chapter 24, C++11 and C++14 Additional Features.

# *C++14: Heterogeneous Lookup*

Prior to C++14, when searching for a key in an associative container, the argument provided to a search function like `find` was required to