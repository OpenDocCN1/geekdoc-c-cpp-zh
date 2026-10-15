corresponding flight going the other way. Or, if there is, we may want to associate different information with it, such as cost.

Like trees, graphs often are implemented using dynamic links, although they can be implemented using arrays as well.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 13.15 What do trees and graphs have in common?

SR 13.16 Which structure (a tree or a graph) would be a good choice to represent each of the following.

+   a. The directories and files on a computer system.
+   b. Airplane routes.
+   c. An “is a friend of” relationship among a group of people.
+   d. An “is a boss of” relationship in a company.

# 13.5 The Java Collections API

The Java standard class library contains several classes that represent collections of various types. These are often referred to as the Java Collections API (Application Programming Interface).

Most of the names of the classes in this set indicate both the collection type and the underlying implementation. One example is the ArrayList class, which is discussed in some detail in Chapter 5. It represents a list collection, implemented using an underlying array. Similarly, the LinkedList class represents a list collection with a dynamically linked internal implementation.

The Vector class and the Stack class are carried over from earlier Java incarnations, which is why their names aren’t consistent with the newer collection classes.

Several interfaces are used to define the collection operations themselves. These interfaces include List, Set, SortedSet, Map, and SortedMap. A Set is consistent with its normal interpretation as a collection of elements without duplicates. A Map is a group of elements that can be referenced by a key value.

KEY CONCEPT
The Java Collections API defines several collection classes implemented in various ways.

# Generics

As we mentioned in Chapter 5 during the discussion of the ArrayList class, the classes in the Java Collections API are implemented as generic types, meaning