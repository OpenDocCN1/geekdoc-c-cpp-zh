# ISO/IEC 14882:2017(E)

# 27 Iterators library

# 27.1 General

This Clause describes components that C++ programs may use to perform iterations over containers (Clause 26), streams (30.7), and stream buffers (30.6).

The following subclauses describe iterator requirements, and components for iterator primitives, defined iterators, and stream iterators, as summarized in Table 92.

| Subclause | Header(s) |
|---|---|
| 27.2 | Requirements |
| 27.4 | Iterator primitives <iterator> |
| 27.5 | Predefined iterators |
| 27.6 | Stream iterators |

# 27.2 Iterator requirements

# 27.1 In general

Iterators are generalizations of pointers that allow a C++ program to work with different data structures (containers) in a uniform manner. To be able to construct algorithms that work correctly and efficiently on different types of data structures, the library formalizes not only the interfaces but also the semantics and complexity assumptions of iterators. An iterator supports the expression *i, a value of some object type T, the value of type*. An iterator has a non-empty set of values that are valid to the iterator; for each type T, the expression *i == j* is valid where i and j are iterators. The expression *i->m* is well-defined supports the expression *corresponding signed integer type X* where each iterator type X is defined, there is a *different type of type X*.

Since iterators are abstraction of pointers, their semantics is a generalization of most of the semantics of pointers in C++. This document ensures that every function that takes iterators works well with regular pointers. This document defines five categories of iterators, according to the operations defined on them: *input iterators, output iterators, forward iterators, bidirectional iterators, and random access iterators*, as shown in Table 93.

Random Access → Bidirectional → Forward → Input Output

Iterators that satisfy the requirements of input iterators can be used whenever an input iterator is specified; Bidirectional iterators also satisfy the requirements of forward iterators and can be used whenever a forward iterator is specified; Random access iterators also satisfy all the requirements of bidirectional iterators and can be used whenever a bidirectional iterator is specified.

Iterators that further satisfy the requirements of output iterators are called *mutable iterators*. Nonmutable iterators are referred to as *constant iterators*.

§ 27.2.1

©ISO/IEC 2017 – All rights reserved 952