approximately 70 algorithms. Most of them use iterators to access container elements. Each algorithm has minimum requirements for the types of iterators that can be used with it. We’ll see that each first-class container supports specific iterator types, some more powerful than others. A container’s supported iterator type determines whether the container can be used with a specific algorithm. Iterators encapsulate the mechanism used to access container elements. This encapsulation enables many of the STL algorithms to be applied to several containers without regard for the underlying container implementation. As long as a container’s iterators support the minimum requirements of the algorithm, then the algorithm can process that container’s elements. This also enables programmers to create new algorithms that can process the elements of multiple container types.

# Software Engineering Observation 20.1

> The STL approach allows general programs to be written so that the code does not depend on the underlying container. Such a programming style is called generic programming.

Data structures like linked lists, queues, stacks and trees carefully weave objects together with pointers. Pointer-based code is complex, and the slightest omission or oversight can lead to serious memory-access violations and memory-leak errors with no compiler complaints. Implementing additional data structures, such as deques, priority queues, sets and maps, requires substantial extra work. In addition, if many programmers on a large project implement similar containers and algorithms for different tasks, the code becomes difficult to modify, maintain and debug. An advantage of the STL is that programmers can reuse the STL containers, iterators and algorithms to implement common data representations and manipulations. This reuse can save substantial development time, money and effort.

# Software Engineering Observation 20.2

> Avoid reinventing the wheel; program with the reusable components of the C++ Standard Library. STL includes many of the most popular data structures as containers and provides various popular algorithms to process data in these containers.

# Error-Prevention Tip 20.1

> When programming pointer-based data structures and algorithms, we must do our own debugging and testing to be sure our data structures, classes and algorithms function properly. It is easy to make errors when manipulating pointers at this low level. Memory leaks and memory-access violations are common in such custom code. For most programmers, and for most of the applications they will need to write, the prepackaged, templated containers of the STL are sufficient. Using the STL helps programmers reduce testing and debugging time. One caution is that, for large projects, template compile time can be significant.

This chapter introduces the STL. It is by no means complete or comprehensive. However, it is a friendly, accessible chapter that should convince you of the value of the STL in software reuse and encourage further study.

# 20.1.1 Introduction to Containers

The STL container types are shown in Fig. 20.1. The containers are divided into three major categories—*sequence containers*, *associative containers* and *container adapters*.