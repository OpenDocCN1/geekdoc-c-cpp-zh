
is equal to or larger than X. Provide an algorithm that can determine n in O(log n) comparisons in the worst case. Explain why your algorithm meets the required time bound.

### 3.20

It is possible to change the way that we pick the dividing point in a binary search, and still get a working search routine. However, where we pick the dividing point could affect the performance of the algorithm.

- (a) If we change the dividing point computation in function binary from `i = (l + r)/2` to `i = (l + ((r - l)/3))`, what will the worst-case running time be in asymptotic terms? If the difference is only a constant time factor, how much slower or faster will the modified program be compared to the original version of binary?

- (b) If we change the dividing point computation in function binary from `i = (l + r)/2` to `i = r - 2`, what will the worst-case running time be in asymptotic terms? If the difference is only a constant time factor, how much slower or faster will the modified program be compared to the original version of binary?

### 3.21

Design an algorithm to assemble a jigsaw puzzle. Assume that each piece has four sides, and that each piece’s final orientation is known (top, bottom, etc.). Assume that you have available a function

```
bool compare(Piece a, Piece b, Side ad)
```

that can tell, in constant time, whether piece a connects to piece b on a’s side ad and b’s opposite side bd. The input to your algorithm should consist of an n × m array of random pieces, along with dimensions n and m. The algorithm should put the pieces in their correct positions in the array. Your algorithm should be as efficient as possible in the asymptotic sense. Write a summation for the running time of your algorithm on n pieces, and then derive a closed-form solution for the summation.

### 3.22

Can the average case cost for an algorithm be worse than the worst case cost? Can it be better than the best case cost? Explain why or why not.

### 3.23

Prove that if an algorithm is Θ(f(n)) in the average case, then it is Ω(f(n)) in the worst case.

### 3.24

Prove that if an algorithm is Θ(f(n)) in the average case, then it is O(f(n)) in the best case.

### 3.14 Projects

### 3.1

Imagine that you are trying to store 32 Boolean values, and must access them frequently. Compare the time required to access Boolean values stored alternatively as a single bit field, a character, a short integer, or a long integer. There are two things to be careful of when writing your program. First, be sure that your program does enough variable accesses to make meaningful measurements. A single access takes much less time than a single unit of measurement (typically milliseconds) for all four methods. Second, be sure that your program spends as much time as possible doing variable accesses rather than other things such as calling timing functions or incrementing for loop counters.

### 3.2

Implement sequential search and binary search algorithms on your computer. Run timings for each algorithm on arrays of size n = 10^i for i ranging from 1 to as large a value as your computer’s memory and compiler will allow. For both algorithms, store the values 0 through n − 1 in order in the array, and use a variety of random search values in the range 0 to n − 1 on each size n. Graph the resulting times. When is sequential search faster than binary search for a sorted array?

### 3.3

Implement a program that runs and gives timings for the two Fibonacci sequence functions provided in Exercise 2.11. Graph the resulting running times for as many values of n as your computer can handle.

## PART II

## Fundamental Data Structures

## Lists, Stacks, and Queues

If your program needs to store a few things — numbers, payroll records, or job descriptions for example — the simplest and most effective approach might be to put them in a list. Only when you have to organize and search through a large number of things do more sophisticated data structures usually become necessary. (We will study how to organize and search through medium amounts of data in Chapters 5, 7, and 9, and discuss how to deal with large amounts of data in Chapters 8–10.) Many applications don’t require any form of search, and they do not require that any ordering be placed on the objects being stored. Some applications require processing in a strict chronological order, processing objects in the order that they arrived, or perhaps processing objects in the reverse of the order that they arrived. For all these situations, a simple list structure is appropriate.

This chapter describes representations for lists in general, as well as two important list-like structures called the stack and the queue. Along with presenting these fundamental data structures, the other goals of the chapter are to:

- (1) Give examples of separating a logical representation in the form of an ADT from a physical implementation for a data structure.
- (2) Illustrate the use of asymptotic analysis in the context of some simple operations that you might already be familiar with. In this way you can begin to see how asymptotic analysis works, without the complications that arise when analyzing more sophisticated algorithms and data structures.
- (3) Introduce the concept and use of dictionaries.

We begin by defining an ADT for lists in Section 4.1. Two implementations for the list ADT — the array-based list and the linked list — are covered in detail and their relative merits discussed. Sections 4.2 and 4.3 cover stacks and queues, respectively. Sample implementations for each of these data structures are presented. Section 4.4 presents the Dictionary ADT for storing and retrieving data, which sets a context for implementing search structures such as the Binary Search Tree of Section 5.4.

### 4.1 Lists

We all have an intuitive understanding of what we mean by a "list." Our first step is to define precisely what is meant so that this intuitive understanding can eventually be converted into a concrete data structure and its operations. The most important concept related to lists is that of position. In other words, we perceive that there is a first element in the list, a second element, and so on. We should view a list as embodying the mathematical concepts of a sequence, as defined in Section 2.1.

We define a list to be a finite, ordered sequence of data items known as elements. “Ordered” in this definition means that each element has a position in the list. (We will not use “ordered” in this context to mean that the list elements are sorted by value.) Each list element has a data type. In the simple list implementations discussed in this chapter, all elements of the list have the same data type, although there is no conceptual objection to lists whose elements have differing data types if the application requires it (see Section 12.1). The operations defined as part of the list ADT do not depend on the elemental data type. For example, the list ADT can be used for lists of integers, lists of characters, lists of payroll records, even lists of lists.

A list is said to be empty when it contains no elements. The number of elements currently stored is called the length of the list. The beginning of the list is called the head, the end of the list is called the tail. There might or might not be some relationship between the value of an element and its position in the list. For example, sorted lists have their elements positioned in ascending order of value, while unsorted lists have no particular relationship between element values and positions. This section will consider only unsorted lists. Chapters 7 and 9 treat the problems of how to create and search sorted lists efficiently.

When presenting the contents of a list, we use the same notation as was introduced for sequences in Section 2.1. To be consistent with C++ array indexing, the first position on the list is denoted as 0. Thus, if there are n elements in the list, they are given positions 0 through n − 1 (a0, a1, ..., an−1). The subscript indicates an element’s position within the list. Using this notation, the empty list would appear as ().

Before selecting a list implementation, a program designer should first consider what basic operations the implementation must support. Our common intuition about lists tells us that a list should be able to grow and shrink in size as we insert and remove elements. We should be able to insert and remove elements from anywhere in the list. We should be able to gain access to any element’s value, either to read it or to change it. We must be able to create and clear (or reinitialize) lists. It is also convenient to access the next or previous element from the “current” one.

The next step is to define the ADT for a list object in terms of a set of operations on that object. We will use the C++ notation of an abstract class to formally define
