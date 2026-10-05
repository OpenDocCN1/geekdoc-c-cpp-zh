
# Standard Template Library 19

- 19.1 ITERATORS 859
- Iterator Basics 859
- Pitfall: Compiler Problems 864
- Kind of Iterators 865
- Constant and Mutable Iterators 868
- Reverse Iterators 870
- Other Kind of Iterators 871

- 19.2 CONTAINERS 872
- Sequential Containers 872
- Pitfall: Iterators and Removing Elements 877
- Tip: Type Definitions in Containers 878

- The Container Adapters stack and queue 878
- Pitfall: Underlying Containers 879
- The Associative Containers set and map 882
- Efficiency 887

- 19.3 GENERIC ALGORITHMS 889
- Running Times and Big-O Notation 890
- Container Access Running Times 894
- Nonmodifying Sequence Algorithms 895
- Modifying Sequence Algorithms 899
- Set Algorithms 900
- Sorting Algorithms 902

# 19 Standard Template Library

Libraries are not made; they.

AUGUSTINE BIRREL

# Introduction

In Chapter 17 we constructed our versions of the stack and queue data structures. A large collection of standard structures for holding data exists. Because they are so standard, it makes sense to have standard portable implementations of these data structures. Standard Template Library (STL) includes libraries for such data structures. Included in the STL are implementations of the stack, queue, and many other standard data structures. When discussed in the context of the STL, these structures are usually called container classes because they are used to hold collections of data. Chapter 7 presented a view of the STL by describing the vector template class, which is one of the container classes in the STL. Because the STL is very large, we will not be able to give a comprehensive treatment of it here, but we will present enough to get you started using some basic STL container classes as well as some of the other items in the STL.

The STL was developed by Alexander Stepanov and Meng Lee at Hewlett-Packard and based on research by Stepanov, Lee, and David Master. The STL is a collection of libraries written in the C++ language. Although the STL is not part of the core C++ standard, it is so any implementation of C++ that conforms to the C++ standard includes the STL. As a practical matter, you can consider the STL to be part of the C++ language.

As its name suggests, the classes in the STL are template classes. A typical container in the STL has a parameter for the type of data to be stored in the container. The STL container classes make extensive use of iterators. An introduction to the general concept of an iterator was given in Section 17.3 of Chapter 17. Although this chapter does not presuppose that you have read this chapter, most readers will find it helpful to read before this chapter. As defined in the STL, iterators are very general and can be used for more than just cycling through the few container classes we cover. Our discussion of iterators will be specialized to some uses with the container classes discussed in this chapter. This should make the concept more concrete and give you understanding to feel comfortable reading more advanced texts on the STL (there are numerous books dedicated to the STL).

The STL also includes implementations of many important generic algorithms, as searching and sorting. The algorithms are implemented as template functions. After discussing the container classes, we will describe some of these algorithm implementations. The STL differs from other C++ libraries—such as <iostream>, for example—that the classes are generic, which is another way of saying that they are template classes and template functions.

# Iterators 859

If you have not already done so, you should read Section 7.3 of Chapter 7, which covers the vector template class of the STL. Although the current chapter does not use any of the material in Chapter 17, most readers will find reading Chapter 17 before this one will aid his or her comprehension of this chapter by giving sample concrete implementations of some of the abstract ideas intrinsic to the STL. This chapter does not use any of the material in Chapters 12 to 15.

# 19.1 Iterators

To iterate is human, and programmers are human.

ANONYMOUS

If you have not yet done so, you should read Chapter 10 on pointers and arrays and also read Section 7.3 of Chapter 7, which covers vectors. Vectors are one of the container templates in the STL. Iterators are a generalization of pointers. This section shows how to use iterators with vectors. Other container template classes that we introduce in Section 19.2 use iterators in the same way. All that you learn about iterators in this section will apply across a wide range of containers rather than applying solely to vectors. This reflects one of the basic tenets of the STL philosophy: The semantics, naming, and syntax for iterator usage should be (and is) uniform across different types.

# Iterator Basics

An iterator is a generalization of a pointer, and in fact is typically implemented using a pointer, but the abstraction of an iterator is designed to spare you the details of the implementation and give you a uniform interface to iterators that is the same across different classes. Each container class has its own iterator types, like each data type has its pointer type. But just as all pointers behave essentially the same for dynamic variables of their particular type, so too each iterator type behave the same, but each iterator is used with its own container type.

An iterator is not a pointer, but you will not go far if you think of it and as if it were. Like a pointer variable, an iterator variable is located at (meaning, it points to) one entry in the container. You manipulate iterators using the following overloaded operators that operate on iterator objects:

- * Prefix and postfix increment operators (++) for advancing the iterator to the next data item.
- * Prefix and postfix decrement operators (--) for moving the iterator to the previous data item.
- Equal and unequal operators (== and !=) to test whether two iterators point to the same data location.

# CHAPTER 19 Standard Template Library

A dereferencing operator (*) so that if p is an iterator variable, *p gives access to the data located (pointed to by) p. This access may be read or write only, or it may allow reading and changing of the data, depending on the particular container class.

Not all iterators have all of these operators. However, the vector template class is an example of a container whose iterators have all functions that get the iterator process started.

A container class has member functions that get the iterator process started. After all, a new iterator variable is not located (pointing to) any data in the container. Many container classes, including the vector template class, have the following member functions that return iterator objects (iterator values) to point to special data elements in the data structure:

- c.begin() returns an iterator for the container c points to the "first" data item in the container c.
- c.end() returns something that can be used when an iterator has passed the last data item in a container c. The iterator c.end() is completely analogous to NULL used to test whether a pointer has passed the last node in a linked list of the kind discussed in Chapter 17. The iterator c.end() is an iterator that is not located at a data item but is a kind of end marker or sentinel.

For many container classes, these tools allow you to write loops that cycle through all the elements in a container object c, as follows:

```
// p is an iterator variable of the type for the container object c.
for (p = c.begin(); p != c.end(); p++)
    process *p //p is the current data item.
```

That is the big picture. Now we look at the details in the concrete setting of the vector template class.

Display 19.1 illustrates the use of iterators with the vector template class. Keep in mind that each container type in the STL has its own iterator types, although they are all used in the same basic ways. The iterators we want for vector of ints are

```
std::vector<int>::iterator;
```

Another container class is the list template class. Iterators for lists of ints are type

```
std::list<int>::iterator;
```

In the program in Display 19.1, we specialize the type name iterator so it applies to iterators for vectors of ints. The type name iterator that we want in Display 19.1 is defined in the template class vector. Thus, if we specialize the template class vector to ints and want the iterator type for vector<int>, we want the

```
vector<int>::iterator;
```
