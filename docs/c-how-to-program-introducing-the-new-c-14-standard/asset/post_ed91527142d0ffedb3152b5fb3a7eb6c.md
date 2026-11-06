
factorization. For example, the output for the number 54 should be

```
The unique prime factorization of 54 is: 2 * 3 * 3 * 3
```

## Recommended Reading

- Gottschling, P. *Discovering Modern C++: An Intensive Course for Scientists, Engineers, and Programmers (C++ In-Depth).* Boston: Addison-Wesley Professional, 2016.
- Horton, I. *Using the C++ Standard Template Libraries.* New York: Springer Science + Business Media, 2015.
- Josuttis, N. *The C++ Standard Library: A Tutorial and Reference (Second edition).* Boston: Addison-Wesley Professional, 2012.
- Karlsson, B. *Beyond the C++ Standard Library: An Introduction to Boost.* Boston: Addison-Wesley Professional, 2005.
- Lippman, S., J. Lajoie, and B. Moo. *C++ Primer (Fifth Edition).* Boston: Addison-Wesley Professional, 2012.
- Meyers, S. *Effective Modern C++: 42 Specific Ways to Improve Your Use of C++11 and C++14.* Sebastopol: O’Reilly, 2015.
- Stroustrup, B. “C++11—the New ISO C++ Standard” [www.stroustrup.com/C++11FAQ.html]. [*Note:* Stroustrup’s FAQ has been merged with Marshall Cline’s to form the C++ FAQ at https://isocpp.org/faq.]
- Stroustrup, B. *The C++ Programming Language, Fourth Edition.* Boston: Addison-Wesley Professional, 2013.
- Wilson, M. *Extended STL, Volume 1: Collections and Iterators.* Boston: Addison-Wesley, 2007.

## Answers to Self-Review Exercises

- 1. **15.1**
    - A. False. The compiler does not warn about these kinds of execution-time errors.
    - B. True.
    - C. False. They are doubly linked lists.
    - D. True.
    - E. True.
    - F. False. It returns a `const_iterator`.
    - G. True.
    - H. False. Disallowing the use of non-`const` member functions.
    - I. False. Using `const_iterator`s where appropriate is another example of the principle of least privilege.
    - J. False. Many algorithms operate on sequences of elements defined by iterators pointing to the first element of the sequence and to one element past the last element.
    - K. True.
    - L. True.
    - M. False. It’s also available for class `deque`.
    - N. False. Insertions and deletions can be made anywhere in a `map`.
    - O. False. Insertions may occur only at the back and deletions may occur only at the front.
- 2. **15.2**
    - A. containers, iterators and algorithms.
    - B. pointers.
    - C. `stack`.
    - D. associative.
    - E. copy.
    - F. `empty`.
    - G. move version of `operator=`.
    - H. `begin`.
    - I. `const` references.
    - J. `list` and `forward_list`.
    - K. `vector`.
    - L. `array`.
    - M. `const_reverse_iterators`.
    - N. predicate.
    - O. the unordered ones do not maintain their keys in sorted order.
    - P. a `multimap` allows duplicate keys with associated values to be stored and a map allows only unique keys with associated values.
    - Q. hold any number of items of various types.
    - R. one-to-one.
    - S. `priority_queue`.
- 3. **15.3**
    - A. `bitset<size> flags;`
    - B. `flags.reset(bitNumber);`
    - C. `flags[bitNumber];`
    - D. `flags.count()`
    - E. `flags.all()`
    - F. `flags != otherFlags`
    - G. `flags <<= n;`

## 16 Standard Library Algorithms

### Objectives

In this chapter you’ll:

- Understand minimum iterator requirements for working with Standard Library algorithms and containers.
- Create anonymous functions using lambda expressions.
- Capture local variables for use in lambda expressions.
- Use containers and iterators with many of the dozens of Standard Library algorithms.
- Use iterators with algorithms to access and manipulate the elements of Standard Library containers.
- Pass lambda expressions, function pointers and function objects into Standard Library algorithms to help them perform their tasks.

### Outline

- 1. **16.1 Introduction**
- 2. **16.2 Minimum Iterator Requirements**
- 3. **16.3 Lambda Expressions**
    - A. **16.3.1 Algorithm** `for_each`
    - B. **16.3.2 Lambda with an Empty Introducer**
    - C. **16.3.3 Lambda with a Nonempty Introducer—Capturing Local Variables**
    - D. **16.3.4 Lambda Return Types**
- 4. **16.4 Algorithms**
    - A. **16.4.1** `fill`, `fill_n`, `generate` and `generate_n`
    - B. **16.4.2** `equal`, `mismatch` and `lexicographical_compare`
    - C. **16.4.3** `remove`, `remove_if`, `remove_copy` and `remove_copy_if`
    - D. **16.4.4** `replace`, `replace_if`, `replace_copy` and `replace_copy_if`
    - E. **16.4.5 Mathematical Algorithms**
    - F. **16.4.6 Basic Searching and Sorting Algorithms**
    - G. **16.4.7** `swap`, `iter_swap` and `swap_ranges`
    - H. **16.4.8** `copy_backward`, `merge`, `unique` and `reverse`
    - I. **16.4.9** `inplace_merge`, `unique_copy` and `reverse_copy`
    - J. **16.4.10 Set Operations**
    - K. **16.4.11** `lower_bound`, `upper_bound` and `equal_range`
    - L. 16.4.12 `min`, `max`, `minmax` and `minmax_element`
- 5. 16.5 Function Objects
- 6. 16.6 Standard Library Algorithm Summary
- 7. 16.7 Wrap-Up

- 1. Summary
- 2. Self-Review Exercises
- 3. Answers to Self-Review Exercises
- 4. Exercises

### 16.1 Introduction

This chapter discusses the Standard Library’s algorithms, focusing on common container manipulations such as *searching*, *sorting* and *comparing elements* or *entire containers*. The Standard Library provides over 90 algorithms—many were added in C++11 and some are new in C++14. For the complete list, see 11 14

> [http://en.cppreference.com/w/cpp/algorithm](http://en.cppreference.com/w/cpp/algorithm)
>
> [http://en.cppreference.com/w/cpp/numeric](http://en.cppreference.com/w/cpp/numeric)

As you’ll see, various algorithms can receive a *function pointer* as an argument—recall that a function’s name is implicitly convertible to a pointer to that function’s code. Such algorithms use the pointer to call the function, typically with one or two container elements as arguments. For most of the examples in this chapter, rather than function pointers we’ll use *lambda expressions*—C++11’s convenient shorthand notation for creating *anonymous functions* (that is, functions that do not have names). Later in the chapter we’ll present the concept of a *function object*, which is similar to a lambda or a function pointer but is implemented as an object of a class that has an overloaded function-call operator (`operator()`). This allows the object’s name to be used like a function name.

### 16.2 Minimum Iterator Requirements

With few exceptions, the *Standard Library* separates algorithms from containers. This makes it much easier to add new algorithms and to use them with multiple containers. An important part of every container is the *type* of iterator it supports (**Fig. 15.7**). This determines which algorithms can be applied to the container. For example, both `vectors` and `arrays` support *random-access iterators* that provide all of the iterator operations shown in **Fig. 15.9**. *All* Standard Library algorithms can operate on `vectors` and those that do not modify a container’s size can also operate on `arrays`. Each Standard Library algorithm that takes iterator arguments requires those iterators to provide a minimum level of functionality. If an algorithm requires a *forward iterator*, for example, that algorithm can operate on any container that supports *forward iterators*, *bidirectional iterators* or *random-access iterators*.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2026_0.png)

### Software Engineering Observation 16.1

*Standard Library algorithms do not depend on the implementation details of the containers on which they operate. As long as a container’s (or built-in array’s) iterators satisfy the requirements of an algorithm, the algorithm can work on the container.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2027_0.png)

### Software Engineering Observation 16.2

*The Standard Library containers are implemented concisely. The algorithms are separated from the containers and operate on elements of the containers only indirectly through iterators. This separation makes it easier to write generic algorithms applicable to a variety of container classes.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2027_1.png)

### Software Engineering Observation 16.3

*Using the “weakest iterator” that yields acceptable performance helps produce maximally reusable components. For example, if an algorithm requires only forward iterators, it can be used with any container that supports forward iterators, bidirectional iterators or random-access*
