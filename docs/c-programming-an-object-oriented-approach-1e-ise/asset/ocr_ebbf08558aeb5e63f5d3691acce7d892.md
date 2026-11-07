![](bbox=[0.244, 0.088, 0.833, 0.263])

**Notes:**  
The keys are unique in a set.  
The objects are in a nonlinear relationship with each other.  
The set class uses bidirectional iterators.

**Figure 19.11**  A set

# 19.5.2 Set

The *set* class is defined in the <set> header file. In a *set*, each element in the container stores one template value, which is referred to as the key. The elements are sorted in ascending order, and duplicates are not allowed. Figure 19.11 shows an example of a *set*.

Although the objects in Figure 19.11 appear to be one after another, they are not linearly connected. There is a nonlinear relationship among them. Although the library does not reveal the implementation, they are most likely implemented as a binary search tree.

# Operations

We briefly discuss the operations that we can use with a set.

# **Constructors, Destructor, and Assignment**

We can create a new set using a default constructor (empty set). We can also create a new set using a parameter constructor by copying the elements of another set in which the range is indicated by [first, last). We can also create a set by using a copy constructor or an assignment operator. The following shows how to create a set of integers.

```
set <type> set1                 // Create an empty set
set <type>(pos1, pos2) set2     // Create a set copying elements of another set
set <type>(set2) set3            // Create a set copying all elements of another set
set4 = set3                      // Create a set copying all elements of another set
```

# **Controlling Size**

There are three member functions that we can use to check size, maximum size, and emptiness. They are the same as discussed for sequence containers.

# **Iterators**

The *set* class uses bidirectional (not random-access) iterators because it is normally implemented as a nonlinear linked list. It provides the same eight internal iterators as the sequence containers, in which four are constant and four nonconstant. Both constant and nonconstant iterators have the same syntax.

```
set1.begin()                  // Returns a regular iterator to the first element
set1.end()                    // Returns a regular iterator to the element after the last
set1.rbegin()                 // Returns a reverse iterator to the last element
set1.rend()                   // Returns a reverse iterator to the element before the first
```