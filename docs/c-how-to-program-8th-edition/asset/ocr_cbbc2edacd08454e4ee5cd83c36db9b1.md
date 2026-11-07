Each STL container has associated member functions. A subset of these member functions is defined in *all* STL containers. We illustrate most of this common functionality in our examples of STL containers `vector` (a dynamically resizable array which we introduced in Chapter 7), `list` (a doubly linked list) and `deque` (a double-ended queue, pronounced “deck”).

STL iterators, which have properties similar to those of pointers, are used by programs to manipulate the STL-container elements. Standard arrays also can be manipulated by STL algorithms, using standard pointers as iterators. We’ll see that manipulating containers with iterators is convenient and provides tremendous expressive power when combined with STL algorithms—in some cases, reducing many lines of code to a single statement. There are five categories of iterators, each of which we discuss in Section 22.3 and use throughout this chapter.

STL algorithms are functions that perform such common data manipulations as *searching*, *sorting* and *comparing elements or entire containers*. The STL provides scores of algorithms. Most of them use iterators to access container elements. Each algorithm has minimum requirements for the types of iterators that can be used with it. We’ll see that each first-class container supports specific iterator types, some more powerful than others. A container’s supported iterator type determines whether the container can be used with a specific algorithm. Iterators encapsulate the mechanism used to access container elements. This encapsulation enables many of the STL algorithms to be applied to various containers without regard for the underlying container implementation. As long as a container’s iterators support the minimum requirements of the algorithm, then the algorithm can process that container’s elements. This also enables you to create new algorithms that can process the elements of multiple container types.

> **Software Engineering Observation 22.1**
> 
> *The STL approach allows programs to be written so that the code does not depend on the underlying container. Such a programming style is called generic programming.*

In Chapter 20, we studied data structures. We built linked lists, queues, stacks and trees. We carefully wove linked objects together with pointers. Pointer-based code is complex, and the slightest omission or oversight can lead to serious *memory-access violations* and *memory-leak* errors with no compiler complaints. Implementing additional data structures, such as deques, priority queues, sets and maps, requires substantial extra work. In addition, if many programmers on a large project implement similar containers and algorithms for different tasks, the code becomes difficult to modify, maintain and debug. An advantage of the STL is that you can reuse the STL containers, iterators and algorithms to implement common data structures and manipulations project-wide. This reuse can save substantial development time, money and effort.

> **Software Engineering Observation 22.2**
> 
> *Avoid reinventing the wheel; program with the reusable components of the C++ Standard Library.*

> **Error-Prevention Tip 22.1**
> 
> *The prepackaged, templatized containers of the STL are sufficient for most applications. Using the STL helps you reduce testing and debugging time.*