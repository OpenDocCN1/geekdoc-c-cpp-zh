Finally, we discussed the Collections class’s static methods for obtaining unmodifiable and synchronized views of collections. Chapter 21 demonstrates how to use Java’s generics capabilities to implement your own generic methods and classes.

# Summary

# Section 20.1 Introduction

+   - The Java collections framework (p. 830) provides prebuilt data structures and methods to manipulate them.

# Section 20.2 Collections Overview

+   - A collection is an object that can hold references to other objects.
+   - The classes and interfaces of the collections framework are in package java.util.

# Section 20.3 Type-Wrapper Classes for Primitive Types

+   - Type-wrapper classes (e.g., Integer, Double, Boolean) enable programmers to manipulate primitive-type values as objects (p. 831). Objects of these classes can be used in collections.

# Section 20.4 Autoboxing and Auto-Unboxing

+   - Boxing (p. 832) converts a primitive value to an object of the corresponding type-wrapper class. Unboxing (p. 832) converts a type-wrapper object to the corresponding primitive value.
+   - Java performs boxing conversions and unboxing conversions automatically.

# Section 20.5 Interface Collection and Class Collections

+   - Interfaces Set and List extend Collection (p. 832), which contains operations for adding, clearing, comparing and retaining objects in a collection, and method iterator (p. 836) to obtain a collection’s Iterator (p. 833).
+   - Class Collections (p. 833) provides static methods for manipulating collections.

# Section 20.6 Lists

+   - A List (p. 839) is an ordered Collection that can contain duplicate elements.
+   - Interface List is implemented by classes ArrayList, LinkedList and Vector. ArrayList (p. 833) is a resizable-array implementation. LinkedList (p. 833) is a linkedlist implementation of a List.
+   - Java SE 7 supports type inferencing with the <> notation in statements that declare and create generic type variables and objects.
+   - Iterator method hasNext (p. 836) determines whether a Collection contains another element. Method next returns a reference to the next object in the Collection and advances the Iterator.
+   - Method subList (p. 839) returns a view into a List. Changes made to this view are also made to the List.
+   - Method clear (p. 839) removes elements from a List.
+   - Method toArray (p. 840) returns the contents of a collection as an array.

# Section 20.7 Collections Methods

+   - Algorithms sort (p. 842), binarySearch, reverse (p. 847), shuffle (p. 845), fill (p. 847), copy, addAll (p. 838), frequency and disjoint operate on Lists. Algorithms min and max (p. 848) operate on Collections.