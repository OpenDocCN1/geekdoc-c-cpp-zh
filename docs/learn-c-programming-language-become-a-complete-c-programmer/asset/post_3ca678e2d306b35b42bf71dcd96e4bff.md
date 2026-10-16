
# 31

# STL Containers

> It was new. It was singular. It was simple. It must succeed!
> — H. Nelson

## 31.1 Introduction

The STL consists of the iterator, container, algorithm, and function object parts of the standard library. The rest of the STL is presented in Chapter 32 and Chapter 33.

## 31.2 Container Overview

A container holds a sequence of objects. This section summarizes the types of containers and briefly outlines their properties. Operations on containers are summarized in §31.3. Containers can be categorized like this:

- *Sequence containers* provide access to (half-open) sequences of elements.
- *Associative containers* provide associative lookup based on a key.

In addition, the standard library provides types of objects that hold elements while not offering all of the facilities of sequence containers or associative containers:

- *Container adaptors* provide specialized access to underlying containers.
- *Almost containers* are sequences of elements that provide most, but not all, of the facilities of a container.

The STL containers (the sequence and associative containers) are all resource handles with copy and move operations (§3.3.1). All operations on containers provide the basic guarantee (§13.2) to ensure that they interact properly with exception-based error handling.

```
vector<T,A>
list<T,A>
forward_list<T,A> deque<T,A>
```

### Sequence Containers

A contiguously allocated sequence of Ts;
the default choice of container

A doubly-linked list of T; use when you need to insert and delete elements without moving existing elements

A singly-linked list of T; ideal for empty and very short sequences A double-ended queue of T; a cross between a vector and a list; slower than one or the other for most uses

The A template argument is the allocator that the container uses to acquire and release memory (§13.6.1, §34.4). For example:

```
template<typename T, typename A = allocator<T>>
class vector {
```

```
// ...
};
```

A is defaulted to std::allocator<T> (§34.4.1) which uses operator new() and operator delete() when it needs to acquire or release memory for its elements.

These containers are defined in <vector>, <list>, and <deque>. The sequence containers are contiguously allocated (e.g., vector) or linked lists (e.g., forward_list) of elements of their value_type (T in the notation used above). A deque (pronounced “deck”) is a mixture of linked-list and contiguous allocation.

Unless you have a solid reason not to, use a vector. Note that vector provides operations for inserting and erasing (removing) elements, allowing a vector to grow and shrink as needed. For sequences of small elements, a vector can be an excellent representation for a data structure requiring list operations.

When inserting and erasing elements of a vector, elements may be moved. In contrast, elements of a list or an associative container do not move when new elements are inserted or other elements are erased.

A forward_list (a singly-linked list) is basically a list optimized for empty and very short lists. An empty forward_list takes up only one word. There are surprisingly many uses for lists where most are empty (and the rest are very short).

```
map<K,V,C,A> multimap<K,V,C,A> set<K,C,A> multiset<K,C,A>
```

### Ordered Associative Containers (§iso.23.4.2)

C is the type of the comparison; A is the allocator type

An ordered map from K to V; a sequence of (K,V) pairs
An ordered map from K to V; duplicate keys allowed
An ordered set of K
An ordered set of K; duplicate keys allowed

These containers are usually implemented as balanced binary trees (usually red-black trees). The default ordering criterion for a key, K, is std::less<K> (§33.4).
As for sequence containers, the A template argument is the allocator that the container uses to acquire and release memory (§13.6.1, §34.4). The A template argument is defaulted to std::allocator<std::pair<const K,T>> (§31.4.3) for maps and std::allocator<K> for sets.

### Unordered Associative Containers (§iso.23.5.2)

H is the hash function type; E is the equality test; A is the allocator type

```
unordered_map<K,V,H,E,A>
unordered_multimap<K,V,H,E,A>
unordered_set<K,H,E,A>
unordered_multiset<K,H,E,A>
```

An unordered map from K to V

use only if you do a lot of vector arithmetic
A set of N bits with set operations, such as & and |
A specialization of vector<T> with compactly stored bits

For basic_string, A is the allocator (§34.4) and Tr is the character traits (§36.2.2).

Prefer a container, such as vector, string, or array, over an array when you have a choice. The implicit array-to-pointer conversion and the need to remember the size for a built-in array are major sources of errors (e.g., see §27.2.1).

Prefer the standard strings to other strings and to C-style strings. The pointer semantics of Cstyle strings imply an awkward notation and extra work for the programmer, and they are a major source of errors (such as memory leaks) (§36.3.1).

## 31.2.1 Container Representation

The standard doesn’t prescribe a particular representation for a standard container. Instead, the standard specifies the container interfaces and some complexity requirements. Implementers will choose appropriate and often cleverly optimized implementations to meet the general requirements and common uses. In addition to what is needed to manipulate elements, such a “handle” will hold an allocator (§34.4).

For a vector, the element data structure is most likely an array:
vector: rep elements free space
The vector will hold a pointer to an array of elements, the number of elements, and the capacity (the number of allocated, currently unused slots) or equivalent (§13.6).

A list is most likely represented by a sequence of links pointing to the elements and the number of elements:
list: rep
elements: v v v

A forward_list is most likely represented by a sequence of links pointing to the elements:
forward_list: rep elements: v v v

A map is most likely implemented as a (balanced) tree of nodes pointing to (key,value) pairs:
map: rep
k k k v v v k k
v v

An unordered_map is most likely implemented as a hash table:
unordered_map: repₖ
^ hash table:
k
v kₖ vv

A string might be implemented as outlined in §19.3 and §23.2; that is, for short strings the characters are stored in the string handle itself, and for longer strings the elements are stored contiguously on the free-store (like vector elements). Like vector, a string can grow

into “free space” allocated
to avoid repeated reallocations:
**string**: rep
characters free space
Like a built-in array (§7.3), an **array** is simply a sequence of elements, with no handle:
**array**: elements
This implies that a local **array** does not use any free store (unless it is allocated there) and that an **array** member of a class does not imply any free store operations.

## 31.2.2 Element Requirements

To be an element of a container, an object must be of a type that allows the container implementation to copy or move it, and to swap elements. If a container copies an element using a copy constructor or copy assignment, the result of the copy must be an equivalent object. This roughly means that any test for equality that you can devise on the value of the objects must deem the copy equal to the original. In other words, copying an element must work much like an ordinary copy of an **int**. Similarly, a move constructor and a move assignment must have the conventional definitions and move semantics (§17.5.1). In addition, it must be possible to **swap()** elements with the usual semantics. If a type has copy or move, the standard-library **swap()** will work.

The details of the element requirements are scattered over the standard and quite hard to read (§iso.23.2.3, §iso.23.2.1, §iso.17.6.3.2), but basically a container can hold elements of a type that has conventional copy or move operations. Many basic algorithms, such as **copy()**, **find()**, and **sort()** will work as long as the requirements for being a container element are met as well as the algorithm’s specific requirements (such as elements being ordered; §31.2.2.1).

Some violations of the rules for standard containers can be detected by a compiler, but others cannot and might then cause unexpected behavior. For example, an assignment operation that throws an exception might leave a partially copied element behind. That would be bad design (§13.6.1) and would violate the rules of the standard by not providing the basic guarantee (§13.2). An element in an invalid state could cause serious trouble later.

When copying objects is not reasonable, an alternative is to put pointers to objects into containers instead of the objects themselves. The most obvious example is polymorphic types (§3.2.2, §20.3.2). For example, we use **vector<unique_ptr<Shape>>** or **vector<Shape*>** rather than **vector<Shape>** to preserve polymorphic behavior.

## 31.2.2.1 Comparisons

Associative containers require that their elements can be ordered. So do many operations that can be applied to containers (e.g., **sort()** and **merge()**). By default, the < operator is used to define the order. If < is not suitable, the programmer must provide an alternative (§31.4.3, §33.4). The ordering criterion must define a *strict weak ordering*. Informally, this means that both less-than and equality (if defined) must be transitive. That is, for an
