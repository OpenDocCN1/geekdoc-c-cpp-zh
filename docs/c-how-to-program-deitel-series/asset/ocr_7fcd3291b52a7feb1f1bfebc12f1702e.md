![](bbox=[0.0, 0.126, 0.095, 0.309])

+   - 16.1 Introduction
+   - 16.2 Minimum Iterator Requirements
+   - 16.3 Algorithms
+     - 16.3.1 `fill`, `fill_n`, `generate` and `generate_n`
+     - 16.3.2 `equal`, `mismatch` and `lexicographical_compare`
+     - 16.3.3 `remove`, `remove_if`, `remove_copy` and `remove_copy_if`
+     - 16.3.4 `replace`, `replace_if`, `replace_copy` and `replace_copy_if`
+     - 16.3.5 Mathematical Algorithms
+     - 16.3.6 Basic Searching and Sorting Algorithms
+     - 16.3.7 `swap`, `iter_swap` and `swap_ranges`
+     - 16.3.8 `copy_backward`, `merge`, `unique` and `reverse`
+     - 16.3.9 `inplace_merge`, `unique_copy` and `reverse_copy`
+     - 16.3.10 Set Operations
+     - 16.3.11 `lower_bound`, `upper_bound` and `equal_range`
+     - 16.3.12 Heapsort
+     - 16.3.13 `min`, `max`, `minmax` and `minmax_element`
+   - 16.4 Function Objects
+   - 16.5 Lambda Expressions
+   - 16.6 Standard Library Algorithm Summary
+   - 16.7 Wrap-Up
+   
+   Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# ## 16.1 Introduction

This chapter continues our discussion of the Standard Library’s containers, iterators and algorithms by focusing on algorithms that perform common data manipulations such as *searching*, *sorting* and *comparing elements or entire containers*. The Standard Library provides over 90 algorithms, many of which are new in C++11. The complete list can be found in Sections 25 and 26.7 of the C++ standard document and there are various online references where you can learn about each algorithm, such as en.cppreference.com/w/cpp/algorithm. Most of them use iterators to access container elements. As you’ll see, various algorithms can receive a *function pointer* (a pointer to a function’s code) as an argument. Such algorithms use the pointer to call the function—typically with one or two container elements as arguments. We’ll introduce function pointers in more detail in this chapter. Later in the chapter we’ll present the concept of a *function object*, which is similar to a function pointer but is implemented as an object of a class that has an overloaded function-call operator (`operator()`) so that the object can be used like a function name. Finally, we’ll introduce *lambda expressions*—C++11’s new shorthand mechanism for creating *anonymous function objects* (that is, function objects that do not have names).

# ## 16.2 Minimum Iterator Requirements

With few exceptions, the Standard Library separates algorithms from containers. This makes it much easier to add new algorithms. An important part of every container is the type of iterator it supports (Fig. 15.7). This determines which algorithms can be applied to the container. For example, both vectors and arrays support *random-access iterators* that provide all of the iterator operations shown in Fig. 15.9. All Standard Library algorithms can operate on vectors and the ones that do not modify a container’s size can also operate on arrays. Each Standard Library algorithm that takes iterator arguments requires those iterators to provide a minimal level of functionality. If an algorithm requires a *forward iterator*, for example, that algorithm can operate on any container that supports *forward iterators*, *bidirectional iterators* or *random-access iterators*.