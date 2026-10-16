# 32

# STL Algorithms

> *Form is liberating.*  
> — Engineer’s proverb

# 32.1 Introduction

This chapter presents the STL algorithms. The STL consists of the iterator, container, algorithm, and function object parts of the standard library. The rest of the STL is presented in Chapter 31 and Chapter 33.

# 32.2 Algorithms

There are about 80 standard algorithms defined in <algorithm>. They operate on *sequences* defined by a pair of iterators (for inputs) or a single iterator (for outputs). When copying, comparing, etc., two sequences, the first is represented by a pair of iterators, [b:e), but the second by just a single iterator, b2, which is considered the start of a sequence holding sufficient elements for the algorithm, for example, as many elements as the first sequence: [b2:b2+(e−b)). Some algorithms, such as sort(), require random-access iterators, whereas many, such as find(), only read their elements in order so that they can make do with a forward iterator. Many algorithms follow the usual convention of returning the end of a sequence to represent “not found” (§4.5). I don’t mention that for each algorithm.

Algorithms, both the standard-library algorithms and the users’ own ones, are important:

+   • Each names a specific operation, documents an interface, and specifies semantics.  
+   • Each can be widely used and known by many programmers.

For correctness, maintainability, and performance, these can be immense advantages compared to “random code” with less well-specified functions and dependencies. If you find yourself writing a piece of code with several loops, local variables that don’t seem to relate to each other, or complicated control structures, consider if the code could be simplified by making a part into a function/algorithm with a descriptive name, a well-defined purpose, a well-defined interface, and welldefined dependencies.

Numerical algorithms in the style of the STL algorithms are presented in §40.6.

# 32.2.1 Sequences

The ideal for a standard-library algorithm is to provide the most general and flexible interface to something that can be implemented optimally. The iterator-based interfaces are a good, but not perfect, approximation to that ideal (§33.1.1). For example, an iterator-based interface does not directly represent the notion of a sequence, leading to the possibility of confusion and difficulties in detecting some range errors: