
# Chapter 10
# Data structures in C++

## 10.1 Introduction

The previous pointer-like objects presented a variety of abstract data structures (ADTs) that were implemented in C++ and R. This introduction served three purposes:

- it provided an overview of the ADTs that are available in R,
- it gave a general treatment of several important ADTs and their properties and
- it provided illustrations of how one could originate their own code for an ADT of interest.

The present chapter takes a perspective that is similar to our use of the Template Numerical Toolkit for linear algebra in Section 7.6. That is, rather than create code for an ADT from scratch, in most instances it's more advisable to use an existing, third-party ADT implementation. The C++ Standard Template Library (STL) provides a readily available source with support for many of the common ADTs.

The STL includes three basic components: container classes, iterators and algorithms. The phrase class refers to a class that can hold objects from some general class. The container classes in the STL are all ADTs.

Iterators are pointer-like objects that provide the means to explore and access the objects in an ADT. We discussed the concept of iterators in Section 9.5. All the STL implementators that have been tailored to work effectively with the different ADTs.

The STL algorithm is a collection of functions that can be used with containers for purposes that include inserting, finding or removing objects and sorting. Its applications are not restricted to just the STL containers. The algorithm library is implemented in a generic fashion that allows it to work with, e.g., user-defined containers as well as many others. In fact, we have already used the max and min functions from the library in previous chapters.

In subsequent sections we will examine what of the STL is for. The objective is to demonstrate how to use the essential features of the different containers and algorithms while applying them in example settings that illustrate their utility. More detailed discussions can be found in a myriad of books and on-line tutorials. In particular, Josustis (1999) provides a thorough and very readable overview of all three of the STL's components.

## 10.2 Container basics

The standard STL containers are

- the vector and deque array classes,
- the linked list container list and
- map, multimap, set and multiset.

The vector class is an implementation of a dynamic array ADT. The name deque stands for "double-ended queue". Thus, as might be expected, objects can be inserted or removed from either end of this container. The random access deque provides to its contents as well as other features that make it a dynamic array rather than a queue in the usual first-in-first out sense of the term. The list container is a doubly-linked list class. The map container is a dictionary the objects in the container have both a key and a data component. For map the keys must be unique while multimap allows repeated keys. The set containers are simplified versions of map containers where objects have a single member that serves as both the key and data component.

There are certain operations that are provided by all the standard class in the STL. In this section we will discuss several of the "global" methods. Later sections will illustrate their use for specific container types as well as other methods that are container-specific.

To use a particular container, ADName, from the STL one needs the include directive:
`#include <ADName>`

All the containers are equipped with a default constructor, a constructor that takes arguments for the specific ADT, a copy constructor, an assignment operator and a destructor. Thus, for example, the default constructor for ADName would be invoked with a command as:

```
ADName<T> ADObject;
```

Of course, a specific value (i.e., a data type) must be supplied for T to define an ADName object. That choice is the user's decision. This serves the same purpose as our developments in Section 9.5: namely, it makes the ADT container in the sense that it can hold objects from an arbitrary class.

The methods empty and size can be used with any of the STL containers. If ADObject is:

```
ADObject.empty();
```
will return true if ADObject contains no elements and false, otherwise. Similarly,

```
ADObject.size();
```
returns the number of elements in ADObject.

```
ADObject1 = ADObject2
```
will evaluate if the two objects contain the same elements arranged in the order. The <, <=, >= operators will also work in the sense of lexicographical comparison between two containers. For example, the operator compares two containers element-by-element:

- two elements are not equal; the result of applying < to the two containers is then false.
- one of the containers has fewer elements than the other; the one with fewer is viewed as "smaller".
- the two containers are found to be equal in which < returns false.

The common methods that actually modify containers are insert, erase and clear. For an ADT ADObject:

```
ADTObject.insert(iter, object);
```
will insert object into the container at the position specified by the iterator iter.

```
ADTObject.erase(iter1, iter2);
```
will remove all elements in ADObject starting with iter1 and ending one prior to iter2. The use of:

```
ADTObject.clear();
```
is equivalent in its effect to ADTObject.erase(begin(), end()) (apart from return values) that all elements in the container will be removed and the container will be empty; i.e., ADTObject.empty() will evaluate to true.

In addition to the standard containers, the STL includes container adapters stack, queue and priority_queue. These are adaptations of the standard containers that function like stacks, queues and priority queues. That is, the stack operates under a last-first-out paradigm while the queue removes elements on a first-in-first-out basis, and priority_queue implements a container where objects are withdrawn according to their priority. At any point, any member of stack or queue or priority_queue can be accessed on the top. Thus, the elements of these containers cannot be accessed and, accordingly, iterators are not defined for these classes. The starting point for discussion of container types is the vector container that provided the model of array in Section 9.2.

## 10.3 Vector deque

The deque class is a very flexible data structure that, as its name suggests, possesses similar features to a one-dimensional array. However, as a type of dynamic array it represents a major upgrade of the array concept. In particular, it provides storage flexibility in the sense that the size of a vector object can be expanded adaptively at run-time. This is precisely what is needed when writing to data of unknown size. Although the deque title is an acronym for "double ended queue", the implementation is through a dynamic array structure that allows for random access to its elements. In this sense it is closely related to the vector container than to other STL containers. Accordingly, we will also discuss the deque class briefly at the end of this section.

Access to the vector container class is obtained via the directive
`#include <vector>`

As noted in the previous section, to create a vector container v holding objects of type className you employ the syntax:

```
vector<className> v;
```

So, for example,

```
vector<double> v;
```
would produce something that work just like an ordinary double precision array in that the ith component of v would be accessed using the familiar syntax v[i]. This dereferencing works generally in that regardless of the type that is stored in the vector container, v[i] will always return the object that is stored in its ith slot.

Of particular interest for data analysis purposes is the case

```
vector<double> v;
```
that produces v[i] now corresponds to an “ordinary” array of doubles in its own right. So, for all practical purposes, v is a matrix with row v[i] and its (i, j) entry is accessed with v[i][j]. Note that the space after the first > in the declaration for v is necessary.

The advantage of using vector<double> v in lieu of vector v[] or double** is, in the infrastructure of the STL. For example, when using pointers or arrays, a programmer must, at some point, make a commitment in terms of size of the structure. This is tedious and error-prone. In contrast, class vector provides built-in methods that allow the user to add elements to the structure: either one-by-one or by inserting multiple elements at time.

The specific methods for the vector class that will be of most immediate utility for us are capacity, size, push_back, insert and assign. The function size returns an integer that represents the number of objects that are currently being held in a vector. The capacity method gives the number of slots in a vector. The difference between the value returned by capacity and size is the number of objects that can be added to a vector before more memory must be allocated.

The push_back function adds an additional element to the end of the vector. The code snippet

```
vector<int> v;
int a = 1;
v.push_back(a);
```
creates a new vector object to hold variables of type int and creates a new slot at the end of v that is filled with the value in the variable (a or 1, in this case). To remove the last component from a vector we proceed similarly using the function pop_back.

```
v.pop_back();
```
would undo what we had previously accomplished with push_back.

Insertion of an obj into a vector requires us to use the iterator class that is an internal (i.e., nested) feature of class vector. In general, iterators are obtained via the syntax:

```
vector<className>::iterator iterator;
```

Then, as in Section 10.2, the insert method for class vector takes the form

```
v.insert(iter, obj);
```
where obj is the object to be inserted into the container. The effect of this command is to insert the object in the slot immediately prior to that specified by iter and an iterator that points to the inserted object. Thus, for example:

```
vector<className>::iterator iter = v.insert(v.begin() + 2, obj);
(*iter).methodName();
```
will insert obj in the third slot of v while shifting all the other objects one slot to the right. The iterator returned from insert is used to call a method methodName for the class which
